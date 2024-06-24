```
Let's create a complete example where we read multiple Excel files listed in a dataset and append their data into a single dataset. Here's the step-by-step code:

### Step 1: Create a Dataset with Filenames

First, create a dataset named `file_list` that contains the filenames of the Excel files you want to read.

```sas
data file_list;
    input filename $50.;
    datalines;
file1.xlsx
file2.xlsx
file3.xlsx
;
run;
```

### Step 2: Create the Macros to Read and Append the Excel Files

Define the macros to read each Excel file and append the data to a single dataset.

```sas
%macro read_append_files;

    /* Initialize an empty dataset to append to */
    data all_data;
        set _null_;
    run;

    /* Loop through each file in the file_list dataset */
    data _null_;
        set file_list;
        call execute('%nrstr(%read_file(' || trim(filename) || '))');
    run;

%mend read_append_files;

/* Macro to read each Excel file and append to the all_data dataset */
%macro read_file(filename);
    proc import datafile="&filename."
        out=temp_data
        dbms=xlsx
        replace;
    run;

    /* Append the current file's data to the all_data dataset */
    proc append base=all_data data=temp_data force;
    run;

    /* Drop the temporary dataset */
    proc datasets lib=work nolist;
        delete temp_data;
    quit;
%mend read_file;

/* Execute the macro */
%read_append_files;
```

### Step 3: Prepare the Excel Files

Create three Excel files (`file1.xlsx`, `file2.xlsx`, and `file3.xlsx`) with similar structures. For demonstration purposes, let's assume each file has the same columns: `ID`, `Name`, and `Value`.

**File: `file1.xlsx`**
```
ID,Name,Value
1,John,100
2,Jane,200
```

**File: `file2.xlsx`**
```
ID,Name,Value
3,Bob,150
4,Alice,250
```

**File: `file3.xlsx`**
```
ID,Name,Value
5,Charlie,300
6,Dave,350
```

### Running the Code

Assuming your Excel files are in the current working directory, running the above SAS code will read each Excel file and append the data into a single dataset called `all_data`.

### Verification

After running the code, you can verify the combined dataset `all_data`:

```sas
proc print data=all_data;
run;
```

The resulting dataset `all_data` should look like this:

```
ID   Name      Value
1    John      100
2    Jane      200
3    Bob       150
4    Alice     250
5    Charlie   300
6    Dave      350
```

### Additional Notes

- If your Excel files are located in a different directory, specify the full path in the `file_list` dataset. For example:
  
  ```sas
  data file_list;
      input filename $100.;
      datalines;
  /path/to/your/files/file1.xlsx
  /path/to/your/files/file2.xlsx
  /path/to/your/files/file3.xlsx
  ;
  run;
  ```

- Adjust the `PROC IMPORT` options based on the structure of your Excel files (e.g., sheet name, range).

This complete example demonstrates how to dynamically read multiple Excel files listed in a dataset and combine their data into a single dataset in SAS.
```


```
PROC TRANSPOSE DATA=sample_data OUT=long_data (DROP=_NAME_) PREFIX=metric;
    BY process;
    VAR JUN24 MAy24;
    ID metric;
RUN;

/* Generate the report */
PROC REPORT DATA=long_data NOWD;
    COLUMN process,('Month' _NAME_),('Metrics' metric:);
    DEFINE process / GROUP 'Process' ORDER=INTERNAL;
    DEFINE _NAME_ / ACROSS 'Month' ORDER=INTERNAL;
    DEFINE metric: / DISPLAY;
RUN;

```
