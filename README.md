# **Bitbucket Process Guide for Business Analysts**

## **Overview**
This document provides a step-by-step guide on how to use Bitbucket for managing SAS files. It covers the entire workflow, including repository creation, cloning, pushing files, pull requests, review, signoff, and pulling changes. The **README file** will serve as the governance document containing documentation, test results, and other essential details.

## **Key Concepts**
### **1. Repository**
A repository is a storage location for code and files, similar to a shared folder but with version control. It keeps track of all changes and allows multiple users to collaborate efficiently.

### **2. Branch**
A branch is a separate working copy of the repository. Changes made in a branch do not affect the main `production` branch until they are merged via a pull request.

### **3. Git Commands Explained**
- **git clone**: Copies an entire repository from Bitbucket to your local machine.
- **git checkout**: Switches between different branches in the repository.
- **git branch**: Creates a new branch.
- **git add**: Stages modified files for commit.
- **git commit -m "message"**: Saves changes to the local repository.
- **git push origin branch-name**: Uploads changes from the local branch to the remote repository.
- **git pull origin branch-name**: Fetches and merges updates from the remote repository.
- **origin**: Represents the remote repository on Bitbucket.

## **Bitbucket Workflow**
- **Production Branch:** The main branch where all final, approved changes are stored.
- **Version Branches (v1, v2, v2.1, etc.):** Separate branches taken from the production branch for each version.
- **Feature Branches:** Developers create branches from the latest version branch to work on updates.
- **Pull Requests:** Used to merge changes from feature/version branches into the production branch.
- **Business Owner Signoff:** Business owners review and approve changes before merging into production.

---
## **Step-by-Step Guide**

### **1. Creating a Repository**
1. Log in to Bitbucket.
2. Click **Create repository**.
3. Enter a **repository name** (e.g., `SAS_Project`).
4. Choose **Git** as the version control system.
5. Set repository to **Private**.
6. Click **Create repository**.
7. The repository is now ready for use.

---
### **2. Cloning a Repository (Copying it to Local Machine)**
1. Open **Git Bash** or any Git terminal.
2. Navigate to the folder where you want to store the repository.
3. Run the following command:
   ```bash
   git clone https://bitbucket.org/your_workspace/SAS_Project.git
   ```
4. This will download the repository to your local system.

---
### **3. Creating and Pushing a Branch**
1. Navigate to the repository in your terminal:
   ```bash
   cd SAS_Project
   ```
2. Ensure you are on the latest production branch:
   ```bash
   git checkout production
   git pull origin production
   ```
3. Create a new branch for your work (e.g., v2.2):
   ```bash
   git checkout -b v2.2
   ```
4. Add your SAS files or make changes.
5. Add and commit your changes:
   ```bash
   git add .
   git commit -m "Added new SAS script for v2.2"
   ```
6. Push the branch to Bitbucket:
   ```bash
   git push origin v2.2
   ```

---
### **4. Creating a Pull Request (PR)**
1. Go to Bitbucket and open the repository.
2. Click on **Branches** and select your branch (e.g., v2.2).
3. Click **Create pull request**.
4. Set **destination branch** as `production`.
5. Add a title and description.
6. Assign reviewers (Business Owner/Approver).
7. Click **Create pull request**.

---
### **5. Reviewing a Pull Request & Signoff**
1. Business owners navigate to the **Pull Requests** tab.
2. Open the pull request and review the changes.
3. If changes are approved:
   - Click **Approve**.
   - Click **Merge** to merge into the `production` branch.
4. If changes need modifications:
   - Add comments for the developer.
   - Developer makes necessary updates and pushes again.

---
### **6. Pulling the Latest Changes to Local Repository**
After merging into production, sync your local repository:
1. Ensure you're on the `production` branch:
   ```bash
   git checkout production
   ```
2. Pull the latest changes:
   ```bash
   git pull origin production
   ```
3. Your local files are now up to date.

---
### **7. README as the Governance Document**
- The **README.md** file in the repository will contain:
  - Project details.
  - Version history.
  - Documentation.
  - Testing results.
  - Any process guidelines.
- Business Analysts and Developers should update the README with relevant information after each release.

---
## **Conclusion**
Following this structured process ensures that all SAS files are version-controlled, reviewed, and approved systematically. Bitbucket provides a centralized platform for maintaining code history, tracking approvals, and managing updates efficiently.

