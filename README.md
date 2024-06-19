```
/* Sort the data by process, metric and month */
PROC SORT DATA=sample_data;
    BY process metric month;
RUN;

/* Calculate the month-on-month change for each metric */
DATA mom_change;
    SET sample_data;
    BY process metric month;
    IF FIRST.metric THEN do;
        change = .;
    END;
    ELSE do;
        change = value - LAG(value);
    END;
RUN;

```
