
WITH SOURCE_DATA AS
(
    SELECT
        TRUNC(TIMESTAMP) AS PROD_DATE,
        FUR_NO,
        COKE_CONS,
        NC_CONS,
        NOA_ORE_CONS,
        JODA_ORE_CONS,
        SINTER_CONS,
        MN_ORE_CONS,
        QUARTZ_CONS,
        LIMESTONE_CONS,
        DOLOMITE_CONS,
        SCRAP_CONS,
        DUNITE_CONS,
        BREX_CONS,
        DRI_CONS,
        LD_SLAG_CONS,
        PELLET_CONS,
        ASRF_CONS,
        PYROXINITE_CONS,
        COAL_CONS,
        TAR_CONS,
        'OnDt' AS PERIOD
    FROM DEMO.T_BF_PRODUCTION_TEST
    WHERE TIMESTAMP >= TRUNC(SYSDATE) - 2
      AND TIMESTAMP < TRUNC(SYSDATE) + 1
      AND FUR_NO IN ('C', 'E', 'F')

    UNION ALL

    SELECT
        TRUNC(TIMESTAMP) AS PROD_DATE,
        FUR_NO,
        COKE_CONS,
        NC_CONS,
        NOA_ORE_CONS,
        JODA_ORE_CONS,
        SINTER_CONS,
        MN_ORE_CONS,
        QUARTZ_CONS,
        LIMESTONE_CONS,
        DOLOMITE_CONS,
        SCRAP_CONS,
        DUNITE_CONS,
        BREX_CONS,
        DRI_CONS,
        LD_SLAG_CONS,
        PELLET_CONS,
        ASRF_CONS,
        PYROXINITE_CONS,
        COAL_CONS,
        TAR_CONS,
        'ToDt' AS PERIOD
    FROM DEMO.T_BF_PRODUCTION_TODATE_TEST
    WHERE TIMESTAMP >= TRUNC(SYSDATE) - 2
      AND TIMESTAMP < TRUNC(SYSDATE) + 1
      AND FUR_NO IN ('C', 'E', 'F')
),
MATERIAL_DATA AS
(
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'COKE' AS MATERIAL, COKE_CONS AS CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'NUT COKE', NC_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Noa Ore', NOA_ORE_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Joda Ore', JODA_ORE_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Sinter', SINTER_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Mn Ore', MN_ORE_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Quartz', QUARTZ_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Limestone', LIMESTONE_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Dolomite', DOLOMITE_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Scrap', SCRAP_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Dunite', DUNITE_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Brex', BREX_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'DRI', DRI_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'LD Slag', LD_SLAG_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Pellet', PELLET_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'ASRF', ASRF_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Pyroxinite', PYROXINITE_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Coal Injection', COAL_CONS
    FROM SOURCE_DATA

    UNION ALL
    SELECT PROD_DATE, PERIOD, FUR_NO,
           'Tar Injection', TAR_CONS
    FROM SOURCE_DATA
)
SELECT
    PROD_DATE,
    MATERIAL,
    PERIOD,
    MAX(CASE WHEN FUR_NO = 'C' THEN CONS END) AS CBF,
    MAX(CASE WHEN FUR_NO = 'E' THEN CONS END) AS EBF,
    MAX(CASE WHEN FUR_NO = 'F' THEN CONS END) AS FBF
FROM MATERIAL_DATA
GROUP BY
    PROD_DATE,
    MATERIAL,
    PERIOD
ORDER BY
    CASE MATERIAL
        WHEN 'COKE'           THEN 1
        WHEN 'NUT COKE'       THEN 2
        WHEN 'Noa Ore'        THEN 3
        WHEN 'Joda Ore'       THEN 4
        WHEN 'Sinter'         THEN 5
        WHEN 'Mn Ore'         THEN 6
        WHEN 'Quartz'         THEN 7
        WHEN 'Limestone'      THEN 8
        WHEN 'Dolomite'       THEN 9
        WHEN 'Scrap'          THEN 10
        WHEN 'Dunite'         THEN 11
        WHEN 'Brex'           THEN 12
        WHEN 'DRI'            THEN 13
        WHEN 'LD Slag'        THEN 14
        WHEN 'Pellet'         THEN 15
        WHEN 'ASRF'           THEN 16
        WHEN 'Pyroxinite'     THEN 17
        WHEN 'Coal Injection' THEN 18
        WHEN 'Tar Injection'  THEN 19
        ELSE 20
    END,
    PROD_DATE,
    CASE PERIOD
        WHEN 'OnDt' THEN 1
        WHEN 'ToDt' THEN 2
        ELSE 3
    END;
