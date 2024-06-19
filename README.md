```
/* Reshape the data from wide to long format */
PROC TRANSPOSE DATA=sample_data OUT=long_data (DROP=_NAME_) PREFIX=metric;
    BY process month;
    VAR value;
RUN;

/* Sort the data by metric and month */
PROC SORT DATA=long_data;
    BY metric month;
RUN;

/* Calculate the month-on-month change for each metric */
DATA mom_change;
    SET long_data;
    BY metric month;
    IF FIRST.metric THEN do;
        change = .;
    END;
    ELSE do;
        change = value - LAG(value);
    END;
RUN;

```
