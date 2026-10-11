
WITH SOURCE_DATA AS
(
    SELECT
        TIMESTAMP,
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
      AND FUR_NO IN ('C', 'E', 'F')

    UNION ALL

    SELECT
        TIMESTAMP,
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
      AND FUR_NO IN ('C', 'E', 'F')
),
MATERIAL_DATA AS
(
    SELECT 'COKE' AS MATERIAL, PERIOD, FUR_NO,
           COKE_CONS AS CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'NUT COKE', PERIOD, FUR_NO,
           NC_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Noa Ore', PERIOD, FUR_NO,
           NOA_ORE_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Joda Ore', PERIOD, FUR_NO,
           JODA_ORE_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Sinter', PERIOD, FUR_NO,
           SINTER_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Mn Ore', PERIOD, FUR_NO,
           MN_ORE_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Quartz', PERIOD, FUR_NO,
           QUARTZ_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Limestone', PERIOD, FUR_NO,
           LIMESTONE_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Dolomite', PERIOD, FUR_NO,
           DOLOMITE_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Scrap', PERIOD, FUR_NO,
           SCRAP_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Dunite', PERIOD, FUR_NO,
           DUNITE_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Brex', PERIOD, FUR_NO,
           BREX_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'DRI', PERIOD, FUR_NO,
           DRI_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'LD Slag', PERIOD, FUR_NO,
           LD_SLAG_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Pellet', PERIOD, FUR_NO,
           PELLET_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'ASRF', PERIOD, FUR_NO,
           ASRF_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Pyroxinite', PERIOD, FUR_NO,
           PYROXINITE_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Coal Injection', PERIOD, FUR_NO,
           COAL_CONS FROM SOURCE_DATA

    UNION ALL
    SELECT 'Tar Injection', PERIOD, FUR_NO,
           TAR_CONS FROM SOURCE_DATA
)
SELECT
    TIMESTAMP,
    MATERIAL,
    PERIOD,
    MAX(CASE WHEN FUR_NO = 'C' THEN CONS END) AS CBF,
    MAX(CASE WHEN FUR_NO = 'E' THEN CONS END) AS EBF,
    MAX(CASE WHEN FUR_NO = 'F' THEN CONS END) AS FBF
FROM MATERIAL_DATA
GROUP BY
    TIMESTAMP,
    MATERIAL,
    PERIOD
ORDER BY
    CASE MATERIAL
        WHEN 'COKE'            THEN 1
        WHEN 'NUT COKE'        THEN 2
        WHEN 'Noa Ore'         THEN 3
        WHEN 'Joda Ore'        THEN 4
        WHEN 'Sinter'          THEN 5
        WHEN 'Mn Ore'          THEN 6
        WHEN 'Quartz'          THEN 7
        WHEN 'Limestone'       THEN 8
        WHEN 'Dolomite'        THEN 9
        WHEN 'Scrap'           THEN 10
        WHEN 'Dunite'          THEN 11
        WHEN 'Brex'            THEN 12
        WHEN 'DRI'             THEN 13
        WHEN 'LD Slag'         THEN 14
        WHEN 'Pellet'          THEN 15
        WHEN 'ASRF'            THEN 16
        WHEN 'Pyroxinite'      THEN 17
        WHEN 'Coal Injection'  THEN 18
        WHEN 'Tar Injection'   THEN 19
        ELSE 20
    END,
    TIMESTAMP,
    CASE PERIOD
        WHEN 'OnDt' THEN 1
        WHEN 'ToDt' THEN 2
        ELSE 3
    END;
