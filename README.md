WITH SOURCE_DATA AS
(
    SELECT
        TRUNC(TIMESTAMP) AS TIMESTAMP,
        FUR_NO,
        ROUNDS,
        NO_CAST,
        PRODUCTION,
        PI,
        ROUND(NC_RATE,1)NC_RATE,
        ROUND(COKE_RATE,1)COKE_RATE,
        ROUND(COAL_RATE,1)COAL_RATE,
        ROUND(TAR_RATE,1)TAR_RATE,
        OIL_RATE,
        ROUND(FUEL_RATE,1)FUEL_RATE,
        ROUND(ASRF_RATE,1)ASRF_RATE,
        ORE_COKE,
        ROUND(SINTER_PERC,1)SINTER_PERC,
        ROUND(PELLET_PERC,1)PELLET_PERC,
        POOLED_IRON_METALLIC_CHARGE,
        O2_PHL,
        ROUND(HB_TEMP)HB_TEMP,
       -- SI,
        NULL,
       NULL,
        PWA,
        DELAY,
        AVAILABILITY,
        OPPORTUNITY_LOSS,
        FE_BALANCE,
        'OnDt' AS PERIOD
    FROM DEMO.T_BF_PRODUCTION_TEST
    WHERE TIMESTAMP >= TRUNC(SYSDATE) - 1
      AND FUR_NO IN ('C', 'E', 'F')

    UNION ALL

    SELECT
        TRUNC(TIMESTAMP) AS TIMESTAMP,
        FUR_NO,
        NULL,
        NO_CAST,
        PRODUCTION,
        PI,
         ROUND(NC_RATE,1)NC_RATE,
        ROUND(COKE_RATE,1)COKE_RATE,
        ROUND(COAL_RATE,1)COAL_RATE,
        ROUND(TAR_RATE,1)TAR_RATE,
        OIL_RATE,
          ROUND(FUEL_RATE,1)FUEL_RATE,
        ROUND(ASRF_RATE,1)ASRF_RATE,
        ORE_COKE,
        ROUND(SINTER_PERC,1)SINTER_PERC,
        ROUND(PELLET_PERC,1)PELLET_PERC,
        POOLED_IRON_METALLIC_CHARGE,
        O2_PHL,
       ROUND(HB_TEMP)HB_TEMP,
       -- SI,
       HM_SI,
      HM_S,
        PWA,
        DELAY,
        AVAILABILITY,
        OPPORTUNITY_LOSS,
        FE_BALANCE,
        'ToDt' AS PERIOD
    FROM DEMO.T_BF_PRODUCTION_TODATE_TEST
    WHERE TIMESTAMP >= TRUNC(SYSDATE) - 1
      AND FUR_NO IN ('C', 'E', 'F')
),
MATERIAL_DATA AS
(
    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'ROUNDS' AS MATERIAL, ROUNDS AS CONS
    FROM SOURCE_DATA
    Union All
    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'No. of Casts' AS MATERIAL, NO_CAST AS CONS
    FROM SOURCE_DATA
    UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Production(tons)' AS MATERIAL, PRODUCTION AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Productivity(t/m3/day)' AS MATERIAL, PI AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'NC Rate(kg/thm)' AS MATERIAL, NC_RATE AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Coke Rate(In clud.N.C)(kg/thm)' AS MATERIAL, COKE_RATE AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Coal Rate(kg/thm)' AS MATERIAL, COAL_RATE AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Tar Rate(kg/thm)' AS MATERIAL, TAR_RATE AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Oil Rate(kg/thm)' AS MATERIAL, OIL_RATE AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Fuel Rate(kg/thm)' AS MATERIAL, FUEL_RATE AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Asrf(kg/thm)' AS MATERIAL, ASRF_RATE AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Ore/Coke' AS MATERIAL, ORE_COKE AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Sinter(%)' AS MATERIAL, SINTER_PERC AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Pellet(%)' AS MATERIAL, PELLET_PERC AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Pooled Iron Metallic Charge(kg/thm)' AS MATERIAL, POOLED_IRON_METALLIC_CHARGE AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Oxygen(tons)' AS MATERIAL, O2_PHL AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'HB Temp(OC)' AS MATERIAL, HB_TEMP AS CONS
    FROM SOURCE_DATA
     UNION ALL
   SELECT TIMESTAMP,PERIOD,FUR_NO,
            'HM Si(%)' AS MATERIAL, HM_SI AS CONS
   FROM SOURCE_DATA
    UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'HM S(%)' AS MATERIAL, HM_S AS CONS
   FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'PWA.(hr.min)' AS MATERIAL, PWA AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Delay(hr.min)' AS MATERIAL, DELAY AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Availability' AS MATERIAL, AVAILABILITY AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Opportunity' AS MATERIAL, OPPORTUNITY_LOSS AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Loss(hr.min)' AS MATERIAL, OPPORTUNITY_LOSS AS CONS
    FROM SOURCE_DATA
     UNION ALL
    SELECT TIMESTAMP,PERIOD,FUR_NO,
            'Fe balance(%)' AS MATERIAL, FE_BALANCE AS CONS
    FROM SOURCE_DATA
    
    

    
)
SELECT
    TIMESTAMP,
    MATERIAL,
    PERIOD,

    NVL(MAX(CASE
        WHEN FUR_NO = 'C' THEN CONS
    END), 0) AS CBF,

    NVL(MAX(CASE
        WHEN FUR_NO = 'E' THEN CONS
    END), 0) AS EBF,

    NVL(MAX(CASE
        WHEN FUR_NO = 'F' THEN CONS
    END), 0) AS FBF,

    NVL(MAX(CASE
        WHEN FUR_NO = 'C' THEN CONS
    END), 0)
    +
    NVL(MAX(CASE
        WHEN FUR_NO = 'E' THEN CONS
    END), 0)
    +
    NVL(MAX(CASE
        WHEN FUR_NO = 'F' THEN CONS
    END), 0) AS PLANT

FROM MATERIAL_DATA

GROUP BY
    TIMESTAMP,
    MATERIAL,
    PERIOD

ORDER BY
    CASE MATERIAL
        WHEN 'ROUNDS'           THEN 1
        WHEN 'No. of Casts' THEN 2
        WHEN 'Production(tons)' THEN 3
        WHEN  'Productivity(t/m3/day)' THEN 4
        When  'NC Rate((kg/thm)' THEN 5
        When  'Coke Rate(In clud.N.C)(kg/thm)' THEN 6
        When  'Coal Rate(kg/thm)' THEN 7
        When  'Tar Rate(kg/thm)' THEN 8
        When  'Oil Rate(kg/thm)' THEN 9
        When  'Fuel Rate(kg/thm)' THEN 10
        When  'Asrf(kg/thm)' THEN 11
        When  'Ore/Coke' THEN 12
        When  'Sinter(%)' THEN 13
        When  'Pellet(%)' THEN 14
        When  'Pooled Iron Metallic Charge((kg/thm))' THEN 15
        When  'Oxygen(tons)' THEN 16
        When  'HB Temp(OC)' THEN 17
       When  'HM Si(%)' THEN 18
       When  'HM S(%)' THEN 19
        When  'PWA.(hr.min)' THEN 20
        When  'Delay(hr.min)' THEN 21
        When  'Availability' THEN 22
        When  'Opportunity' THEN 23
        When  'Loss(hr.min)' THEN 24
        When  'Fe balance(%)' THEN 25
        ELSE 25
    END,
    TIMESTAMP,
    CASE PERIOD
        WHEN 'OnDt' THEN 1
        WHEN 'ToDt' THEN 2
        ELSE 3
    END
