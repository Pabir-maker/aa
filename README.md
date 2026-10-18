SELECT t.FUR_NO, ROUND(nvl(t.slag_generation,0))slag_generation_ONDT,ROUND(nvl(tt.slag_generation,0))slag_generation_TODT,
ROUND(nvl(t.SLAG_LADLE_TONS,0))SLAG_LADLE_TONS_ONDT,ROUND(nvl(tt.SLAG_LADLE_TONS,0))SLAG_LADLE_TONS_TODT
FROM demo.t_bf_production_test t,demo.t_bf_production_test tt
WHERE (t.TIMESTAMP='17-oct-2026' ) AND (t.FUR_NO Not In ('G','H','D')) AND t.TIMESTAMP=tt.TIMESTAMP and t.FUR_NO=tt.FUR_NO
ORDER BY t.FUR_NO
