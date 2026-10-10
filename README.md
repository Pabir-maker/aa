CREATE OR REPLACE PROCEDURE PROC_GET_ATOF_PRODUCTION_REPORT
(
    p_date   IN  DATE,
    p_cursor OUT SYS_REFCURSOR
)
AS
    v_sql        CLOB;
    v_table_name VARCHAR2(261);
BEGIN
    ------------------------------------------------------------
    -- 1. Get production table name
    ------------------------------------------------------------
    BEGIN
        SELECT MIN(iMonitor_Table_Name)
          INTO v_table_name
          FROM IMTG.T_ATOF_PROD_REPORT_MASTER
         WHERE REQUIRED = 'Y'
           AND iMonitor_Table_Name IS NOT NULL;

        IF v_table_name IS NULL THEN
            v_table_name := 'DEMO.T_BF_PRODUCTION_TEST';
        END IF;
    END;

    ------------------------------------------------------------
    -- 2. Build query in SL_NO order
    ------------------------------------------------------------
    FOR k IN
    (
        SELECT SL_NO,
               UPPER(TRIM(iMonitor_Column)) AS iMonitor_Column
          FROM IMTG.T_ATOF_PROD_REPORT_MASTER
         WHERE REQUIRED = 'Y'
           AND iMonitor_Column IS NOT NULL
         ORDER BY SL_NO
    )
    LOOP
        IF v_sql IS NOT NULL THEN
            v_sql := v_sql || ' UNION ALL ';
        END IF;

        v_sql := v_sql
            || 'SELECT '
            || k.SL_NO || ' AS SL_NO, '
            || '''' || REPLACE(k.iMonitor_Column, '''', '''''')
            || ''' AS METRIC_NAME, '

            || 'CASE WHEN '''
            || k.iMonitor_Column
            || ''' = ''PRODUCTION'' THEN '
            || 'SUM(CASE WHEN FUR_NO = ''C'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(k.iMonitor_Column)
            || ' END) ELSE '
            || 'AVG(CASE WHEN FUR_NO = ''C'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(k.iMonitor_Column)
            || ' END) END AS CBF, '

            || 'CASE WHEN '''
            || k.iMonitor_Column
            || ''' = ''PRODUCTION'' THEN '
            || 'SUM(CASE WHEN FUR_NO = ''E'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(k.iMonitor_Column)
            || ' END) ELSE '
            || 'AVG(CASE WHEN FUR_NO = ''E'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(k.iMonitor_Column)
            || ' END) END AS EBF, '

            || 'CASE WHEN '''
            || k.iMonitor_Column
            || ''' = ''PRODUCTION'' THEN '
            || 'SUM(CASE WHEN FUR_NO = ''F'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(k.iMonitor_Column)
            || ' END) ELSE '
            || 'AVG(CASE WHEN FUR_NO = ''F'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(k.iMonitor_Column)
            || ' END) END AS FBF '

            || 'FROM ' || v_table_name || ' '
            || 'WHERE "TIMESTAMP" >= TRUNC(:1) - 2 '
            || 'AND "TIMESTAMP" < TRUNC(:1) + 1';
    END LOOP;

    ------------------------------------------------------------
    -- 3. Open cursor ordered by SL_NO
    ------------------------------------------------------------
    IF v_sql IS NOT NULL THEN

        v_sql := 'SELECT * FROM (' || v_sql ||
                 ') ORDER BY SL_NO';

        -- Each UNION ALL branch contains two positional binds.
        -- Therefore, supply p_date twice per branch.
        DECLARE
            v_count PLS_INTEGER;
            v_binds SYS.ODCIDATELIST := SYS.ODCIDATELIST();
        BEGIN
            v_count := REGEXP_COUNT(v_sql, ':1');

            FOR i IN 1 .. v_count LOOP
                v_binds.EXTEND;
                v_binds(v_binds.COUNT) := p_date;
            END LOOP;

            -- Use the simpler static bind approach below instead
            -- if your Oracle version does not support this overload.
            OPEN p_cursor FOR v_sql USING
                p_date, p_date;
        END;

    ELSE
        OPEN p_cursor FOR
            SELECT CAST(NULL AS NUMBER) AS SL_NO,
                   CAST(NULL AS VARCHAR2(128)) AS METRIC_NAME,
                   CAST(NULL AS NUMBER) AS CBF,
                   CAST(NULL AS NUMBER) AS EBF,
                   CAST(NULL AS NUMBER) AS FBF
              FROM DUAL
             WHERE 1 = 0;
    END IF;

EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error in PROC_GET_ATOF_PRODUCTION_REPORT: ' || SQLERRM
        );
        RAISE;
END PROC_GET_ATOF_PRODUCTION_REPORT;
/
