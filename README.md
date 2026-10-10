CREATE OR REPLACE PROCEDURE IMTG.PROC_GET_ATOF_PRODUCTION_REPORT
(
    p_date   IN  DATE,
    p_cursor OUT SYS_REFCURSOR
)
AS
    v_sql         CLOB;
    v_table_name  VARCHAR2(261);
    v_owner       VARCHAR2(128);
    v_table       VARCHAR2(128);
    v_col_count   NUMBER;
    v_metric      VARCHAR2(128);
    v_first       BOOLEAN := TRUE;
BEGIN
    ------------------------------------------------------------------
    -- 1. Get the production table from the master configuration
    ------------------------------------------------------------------
    BEGIN
        SELECT MIN(iMonitor_Table_Name)
          INTO v_table_name
          FROM IMTG.T_ATOF_PROD_REPORT_MASTER
         WHERE REQUIRED = 'Y'
           AND iMonitor_Table_Name IS NOT NULL;

        IF v_table_name IS NULL THEN
            v_table_name := 'DEMO.T_BF_PRODUCTION_TEST';
        END IF;

    EXCEPTION
        WHEN NO_DATA_FOUND THEN
            v_table_name := 'DEMO.T_BF_PRODUCTION_TEST';
    END;

    ------------------------------------------------------------------
    -- 2. Validate the table name
    ------------------------------------------------------------------
    v_table_name := DBMS_ASSERT.SQL_OBJECT_NAME(
                        UPPER(TRIM(v_table_name))
                    );

    IF INSTR(v_table_name, '.') > 0 THEN
        v_owner := SUBSTR(v_table_name, 1,
                          INSTR(v_table_name, '.') - 1);
        v_table := SUBSTR(v_table_name,
                          INSTR(v_table_name, '.') + 1);
    ELSE
        v_owner := SYS_CONTEXT('USERENV', 'CURRENT_SCHEMA');
        v_table := v_table_name;
    END IF;

    ------------------------------------------------------------------
    -- 3. Build the dynamic report query
    --    Use one bind variable for the selected date
    ------------------------------------------------------------------
    v_sql := 'WITH params AS
              (
                  SELECT :p_date AS p_date FROM DUAL
              ) ';

    FOR k IN
    (
        SELECT DISTINCT
               TRIM(iMonitor_Column) AS column_name
          FROM IMTG.T_ATOF_PROD_REPORT_MASTER
         WHERE REQUIRED = 'Y'
           AND iMonitor_Column IS NOT NULL
         ORDER BY TRIM(iMonitor_Column)
    )
    LOOP
        v_metric := UPPER(TRIM(k.column_name));

        --------------------------------------------------------------
        -- 4. Check whether the configured column exists
        --------------------------------------------------------------
        SELECT COUNT(*)
          INTO v_col_count
          FROM ALL_TAB_COLUMNS
         WHERE OWNER = v_owner
           AND TABLE_NAME = v_table
           AND COLUMN_NAME = v_metric;

        IF v_col_count = 0 THEN
            RAISE_APPLICATION_ERROR(
                -20001,
                'Invalid report column "' || v_metric ||
                '" in table ' || v_table_name ||
                '. Check IMTG.T_ATOF_PROD_REPORT_MASTER.'
            );
        END IF;

        --------------------------------------------------------------
        -- 5. Add each metric using UNION ALL
        --------------------------------------------------------------
        IF NOT v_first THEN
            v_sql := v_sql || ' UNION ALL ';
        END IF;

        v_sql := v_sql ||
            'SELECT ''' ||
            REPLACE(v_metric, '''', '''''') ||
            ''' AS METRIC_NAME, ' ||

            'CASE WHEN ''' || v_metric ||
            ''' = ''PRODUCTION'' ' ||
            'THEN SUM(CASE WHEN t.FUR_NO = ''C'' ' ||
            'THEN t.' || DBMS_ASSERT.SIMPLE_SQL_NAME(v_metric) ||
            ' END) ' ||
            'ELSE AVG(CASE WHEN t.FUR_NO = ''C'' ' ||
            'THEN t.' || DBMS_ASSERT.SIMPLE_SQL_NAME(v_metric) ||
            ' END) END AS CBF, ' ||

            'CASE WHEN ''' || v_metric ||
            ''' = ''PRODUCTION'' ' ||
            'THEN SUM(CASE WHEN t.FUR_NO = ''E'' ' ||
            'THEN t.' || DBMS_ASSERT.SIMPLE_SQL_NAME(v_metric) ||
            ' END) ' ||
            'ELSE AVG(CASE WHEN t.FUR_NO = ''E'' ' ||
            'THEN t.' || DBMS_ASSERT.SIMPLE_SQL_NAME(v_metric) ||
            ' END) END AS EBF, ' ||

            'CASE WHEN ''' || v_metric ||
            ''' = ''PRODUCTION'' ' ||
            'THEN SUM(CASE WHEN t.FUR_NO = ''F'' ' ||
            'THEN t.' || DBMS_ASSERT.SIMPLE_SQL_NAME(v_metric) ||
            ' END) ' ||
            'ELSE AVG(CASE WHEN t.FUR_NO = ''F'' ' ||
            'THEN t.' || DBMS_ASSERT.SIMPLE_SQL_NAME(v_metric) ||
            ' END) END AS FBF ' ||

            'FROM ' || v_table_name || ' t ' ||
            'CROSS JOIN params p ' ||
            'WHERE t.TIMESTAMP >= TRUNC(p.p_date) - 2 ' ||
            'AND t.TIMESTAMP < TRUNC(p.p_date) + 1';

        v_first := FALSE;
    END LOOP;

    ------------------------------------------------------------------
    -- 6. Open the output cursor
    ------------------------------------------------------------------
    IF v_first THEN
        OPEN p_cursor FOR
            SELECT CAST(NULL AS VARCHAR2(128)) AS METRIC_NAME,
                   CAST(NULL AS NUMBER) AS CBF,
                   CAST(NULL AS NUMBER) AS EBF,
                   CAST(NULL AS NUMBER) AS FBF
              FROM DUAL
             WHERE 1 = 0;
    ELSE
        v_sql := 'SELECT * FROM (' || v_sql ||
                 ') ORDER BY METRIC_NAME';

        OPEN p_cursor FOR v_sql USING p_date;
    END IF;

EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'PROC_GET_ATOF_PRODUCTION_REPORT ERROR: ' || SQLERRM
        );
        RAISE;
END PROC_GET_ATOF_PRODUCTION_REPORT;
/
