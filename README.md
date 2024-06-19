data month_on_month_changes(drop=lag_Value lag_Month);
    set input_data;
    by Process Metric Month;

    /* Initialize lag variables for the first row of each Metric */
    if first.Metric then do;
        lag_Value = .;
        lag_Month = .;
    end;

    /* Calculate month-on-month changes */
    Month_Change = .; /* Initialize Month_Change */
    if not first.Metric and not first.Process then do;
        Month_Change = (Value - lag_Value) / lag_Value;
    end;

    /* Output the result */
    if not first.Metric then output;

    /* Update lag variables */
    lag_Value = Value;
    lag_Month = Month;

    format Month_Change percent7.2;
run;
