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
