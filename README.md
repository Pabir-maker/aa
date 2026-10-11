
SELECT
    TIMESTAMP,
    MATERIAL,
    PERIOD,

    NVL(MAX(CASE WHEN FUR_NO = 'C'
                 THEN CONS END), 0) AS CBF,

    NVL(MAX(CASE WHEN FUR_NO = 'E'
                 THEN CONS END), 0) AS EBF,

    NVL(MAX(CASE WHEN FUR_NO = 'F'
                 THEN CONS END), 0) AS FBF,

    NVL(MAX(CASE WHEN FUR_NO = 'C'
                 THEN CONS END), 0)
    +
    NVL(MAX(CASE WHEN FUR_NO = 'E'
                 THEN CONS END), 0)
    +
    NVL(MAX(CASE WHEN FUR_NO = 'F'
                 THEN CONS END), 0) AS PLANT

FROM MATERIAL_DATA

GROUP BY
    TIMESTAMP,
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
    TIMESTAMP,
    CASE PERIOD
        WHEN 'OnDt' THEN 1
        WHEN 'ToDt' THEN 2
        ELSE 3
    END;
