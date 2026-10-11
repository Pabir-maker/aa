WITH SOURCE_DATA AS
(
    SELECT
        TRUNC(TIMESTAMP) AS TIMESTAMP,
        FUR_NO,
        ROUNDS,
        NO_CAST,
        PRODUCTION,
        PI,
        ROUND(NC_RATE, 1) AS NC_RATE,
        ROUND(COKE_RATE, 1) AS COKE_RATE,
        ROUND(COAL_RATE, 1) AS COAL_RATE,
        ROUND(TAR_RATE, 1) AS TAR_RATE,
        OIL_RATE,
        ROUND(FUEL_RATE, 1) AS FUEL_RATE,
        ROUND(ASRF_RATE, 1) AS ASRF_RATE,
        ORE_COKE,
        ROUND(SINTER_PERC, 1) AS SINTER_PERC,
        ROUND(PELLET_PERC, 1) AS PELLET_PERC,
        POOLED_IRON_METALLIC_CHARGE,
        O2_PHL,
        ROUND(HB_TEMP) AS HB_TEMP,
        CAST(NULL AS NUMBER) AS HM_SI,
        CAST(NULL AS NUMBER) AS HM_S,
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
        NULL AS ROUNDS,
        NO_CAST,
        PRODUCTION,
        PI,
        ROUND(NC_RATE, 1) AS NC_RATE,
        ROUND(COKE_RATE, 1) AS COKE_RATE,
        ROUND(COAL_RATE, 1) AS COAL_RATE,
        ROUND(TAR_RATE, 1) AS TAR_RATE,
        OIL_RATE,
        ROUND(FUEL_RATE, 1) AS FUEL_RATE,
        ROUND(ASRF_RATE, 1) AS ASRF_RATE,
        ORE_COKE,
        ROUND(SINTER_PERC, 1) AS SINTER_PERC,
        ROUND(PELLET_PERC, 1) AS PELLET_PERC,
        POOLED_IRON_METALLIC_CHARGE,
        O2_PHL,
        ROUND(HB_TEMP) AS HB_TEMP,
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

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'No. of Casts', NO_CAST
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Production(tons)', PRODUCTION
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Productivity(t/m3/day)', PI
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'NC Rate(kg/thm)', NC_RATE
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Coke Rate(In clud.N.C)(kg/thm)', COKE_RATE
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Coal Rate(kg/thm)', COAL_RATE
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Tar Rate(kg/thm)', TAR_RATE
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Oil Rate(kg/thm)', OIL_RATE
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Fuel Rate(kg/thm)', FUEL_RATE
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Asrf(kg/thm)', ASRF_RATE
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Ore/Coke', ORE_COKE
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Sinter(%)', SINTER_PERC
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Pellet(%)', PELLET_PERC
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Pooled Iron Metallic Charge(kg/thm)',
           POOLED_IRON_METALLIC_CHARGE
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Oxygen(tons)', O2_PHL
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'HB Temp(OC)', HB_TEMP
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'HM Si(%)', HM_SI
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'HM S(%)', HM_S
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'PWA.(hr.min)', PWA
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Delay(hr.min)', DELAY
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Availability', AVAILABILITY
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Opportunity', OPPORTUNITY_LOSS
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Loss(hr.min)', OPPORTUNITY_LOSS
    FROM SOURCE_DATA

    UNION ALL

    SELECT TIMESTAMP, PERIOD, FUR_NO,
           'Fe balance(%)', FE_BALANCE
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
        WHEN 'ROUNDS'                              THEN 1
        WHEN 'No. of Casts'                        THEN 2
        WHEN 'Production(tons)'                    THEN 3
        WHEN 'Productivity(t/m3/day)'              THEN 4
        WHEN 'NC Rate(kg/thm)'                     THEN 5
        WHEN 'Coke Rate(In clud.N.C)(kg/thm)'      THEN 6
        WHEN 'Coal Rate(kg/thm)'                   THEN 7
        WHEN 'Tar Rate(kg/thm)'                    THEN 8
        WHEN 'Oil Rate(kg/thm)'                    THEN 9
        WHEN 'Fuel Rate(kg/thm)'                   THEN 10
        WHEN 'Asrf(kg/thm)'                        THEN 11
        WHEN 'Ore/Coke'                            THEN 12
        WHEN 'Sinter(%)'                           THEN 13
        WHEN 'Pellet(%)'                           THEN 14
        WHEN 'Pooled Iron Metallic Charge(kg/thm)' THEN 15
        WHEN 'Oxygen(tons)'                        THEN 16
        WHEN 'HB Temp(OC)'                         THEN 17
        WHEN 'HM Si(%)'                            THEN 18
        WHEN 'HM S(%)'                             THEN 19
        WHEN 'PWA.(hr.min)'                        THEN 20
        WHEN 'Delay(hr.min)'                       THEN 21
        WHEN 'Availability'                        THEN 22
        WHEN 'Opportunity'                         THEN 23
        WHEN 'Loss(hr.min)'                        THEN 24
        WHEN 'Fe balance(%)'                       THEN 25
        ELSE 26
    END,
    TIMESTAMP,
    CASE PERIOD
        WHEN 'OnDt' THEN 1
        WHEN 'ToDt' THEN 2
        ELSE 3
    END;
