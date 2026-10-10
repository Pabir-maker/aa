
CREATE OR REPLACE PROCEDURE PROC_GET_ATOF_PRODUCTION_REPORT
(
    p_date   IN  DATE,
    p_cursor OUT SYS_REFCURSOR
)
AS
    v_sql        CLOB;
    v_table_name VARCHAR2(261);
BEGIN

    -- 1. Get source table name from master table
    BEGIN
        SELECT iMonitor_Table_Name
        INTO v_table_name
        FROM imtg.T_ATOF_PROD_REPORT_MASTER
        WHERE REQUIRED = 'Y'
          AND iMonitor_Table_Name IS NOT NULL
          AND ROWNUM = 1;

    EXCEPTION
        WHEN NO_DATA_FOUND THEN
            v_table_name := 'DEMO.T_BF_PRODUCTION_TEST';
    END;

    -- 2. Build dynamic query using UNION ALL
    FOR k IN
    (
        SELECT SL_NO, TRIM(iMonitor_Column) AS iMonitor_Column
        FROM imtg.T_ATOF_PROD_REPORT_MASTER
        WHERE REQUIRED = 'Y'
          AND iMonitor_Column IS NOT NULL
          AND SL_NO <= 30
        ORDER BY SL_NO
    )
    LOOP

        IF v_sql IS NOT NULL THEN
            v_sql := v_sql || ' UNION ALL ';
        END IF;

        v_sql := v_sql
            || 'SELECT '''
            || REPLACE(UPPER(TRIM(k.iMonitor_Column)), '''', '''''')
            || ''' AS METRIC_NAME, '

            || 'CASE WHEN UPPER('''
            || REPLACE(TRIM(k.iMonitor_Column), '''', '''''')
            || ''') = ''PRODUCTION'' THEN '
            || 'SUM(CASE WHEN FUR_NO = ''C'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(
                   UPPER(TRIM(k.iMonitor_Column))
               )
            || ' END) ELSE '
            || 'AVG(CASE WHEN FUR_NO = ''C'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(
                   UPPER(TRIM(k.iMonitor_Column))
               )
            || ' END) END AS CBF, '

            || 'CASE WHEN UPPER('''
            || REPLACE(TRIM(k.iMonitor_Column), '''', '''''')
            || ''') = ''PRODUCTION'' THEN '
            || 'SUM(CASE WHEN FUR_NO = ''E'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(
                   UPPER(TRIM(k.iMonitor_Column))
               )
            || ' END) ELSE '
            || 'AVG(CASE WHEN FUR_NO = ''E'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(
                   UPPER(TRIM(k.iMonitor_Column))
               )
            || ' END) END AS EBF, '

            || 'CASE WHEN UPPER('''
            || REPLACE(TRIM(k.iMonitor_Column), '''', '''''')
            || ''') = ''PRODUCTION'' THEN '
            || 'SUM(CASE WHEN FUR_NO = ''F'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(
                   UPPER(TRIM(k.iMonitor_Column))
               )
            || ' END) ELSE '
            || 'AVG(CASE WHEN FUR_NO = ''F'' THEN '
            || DBMS_ASSERT.SIMPLE_SQL_NAME(
                   UPPER(TRIM(k.iMonitor_Column))
               )
            || ' END) END AS FBF '

            || 'FROM SRC';

    END LOOP;

    -- 3. Apply the selected date once
    IF v_sql IS NOT NULL THEN

        v_sql :=
              'WITH SRC AS ('
            || ' SELECT * FROM ' || v_table_name
            || ' WHERE "TIMESTAMP" >= TRUNC(:p_date)'
            || ' AND "TIMESTAMP" < TRUNC(:p_date) + 1'
            || ') '
            || 'SELECT * FROM ('
            || v_sql
            || ') ORDER BY METRIC_NAME';

        -- Pass date once
        OPEN p_cursor FOR v_sql USING p_date;

    ELSE

        OPEN p_cursor FOR
            SELECT CAST(NULL AS VARCHAR2(128)) AS METRIC_NAME,
                   CAST(NULL AS NUMBER) AS CBF,
                   CAST(NULL AS NUMBER) AS EBF,
                   CAST(NULL AS NUMBER) AS FBF
            FROM DUAL
            WHERE 1 = 0;

    END IF;

EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error building dynamic matrix report: ' || SQLERRM
        );
        RAISE;

END PROC_GET_ATOF_PRODUCTION_REPORT;
/
