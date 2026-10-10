create or replace PROCEDURE PROC_GET_ATOF_PRODUCTION_REPORT (p_date   IN  DATE,p_cursor OUT SYS_REFCURSOR) AS
    v_sql CLOB;
    v_table_name VARCHAR2(100);
BEGIN
    -- 1. Identify the table name from your master setup (assuming 1 target table for the report)
    BEGIN
        SELECT DISTINCT iMonitor_Table_Name INTO v_table_name FROM imtg.T_ATOF_PROD_REPORT_MASTER WHERE REQUIRED = 'Y' AND iMonitor_Table_Name IS NOT NULL  AND ROWNUM = 1;
    EXCEPTION 
    WHEN NO_DATA_FOUND THEN
    v_table_name := 'DEMO.T_BF_PRODUCTION_TEST'; -- Fallback default
    END;
    -- 2. Build a dynamic UNPIVOT-like query using UNION ALL from the Master Table rows
    FOR k IN (SELECT SL_NO, iMonitor_Column FROM imtg.T_ATOF_PROD_REPORT_MASTER WHERE REQUIRED = 'Y' AND iMonitor_Column IS NOT NULL ORDER BY SL_NO)
    LOOP
        IF v_sql IS NOT NULL THEN
            v_sql := v_sql || ' UNION ALL ';
        END IF;
        -- We apply SUM for Production, and AVG for Rates/Percentages dynamically based on column names
        v_sql := v_sql 
                 || 'SELECT ''' || k.iMonitor_Column || ''' AS Metric_Name, '
                 || 'CASE WHEN ''' || k.iMonitor_Column || ''' = ''PRODUCTION'' THEN SUM(CASE WHEN FUR_NO = ''C'' THEN ' || k.iMonitor_Column || ' END) '
                 || '     ELSE AVG(CASE WHEN FUR_NO = ''C'' THEN ' || k.iMonitor_Column || ' END) END AS CBF, '
                 || 'CASE WHEN ''' || k.iMonitor_Column || ''' = ''PRODUCTION'' THEN SUM(CASE WHEN FUR_NO = ''E'' THEN ' || k.iMonitor_Column || ' END) '
                 || '     ELSE AVG(CASE WHEN FUR_NO = ''E'' THEN ' || k.iMonitor_Column || ' END) END AS EBF, '
                 || 'CASE WHEN ''' || k.iMonitor_Column || ''' = ''PRODUCTION'' THEN SUM(CASE WHEN FUR_NO = ''F'' THEN ' || k.iMonitor_Column || ' END) '
                 || '     ELSE AVG(CASE WHEN FUR_NO = ''F'' THEN ' || k.iMonitor_Column || ' END) END AS FBF '
                 || 'FROM ' || v_table_name || ' '
                 || 'WHERE Timestamp >= TRUNC(:1) - 2 '
                 || 'GROUP BY ''' || k.iMonitor_Column || '''';
    END LOOP;
    -- 3. Open the cursor with the final ordered dataset
    IF v_sql IS NOT NULL THEN
        -- Wrap the entire block to ensure everything is sorted neatly by Metric Name
        v_sql := 'SELECT * FROM (' || v_sql || ') ORDER BY Metric_Name';
        OPEN p_cursor FOR v_sql USING p_date;
    ELSE
        OPEN p_cursor FOR SELECT NULL AS Metric_Name, NULL AS CBF, NULL AS EBF, NULL AS FBF FROM DUAL WHERE 1=0;
    END IF;
EXCEPTION
WHEN OTHERS THEN 
DBMS_OUTPUT.PUT_LINE('Error building dynamic matrix report: ' || SQLERRM);
RAISE;
END;
