        public decimal SLAG_GENERATION_ONDT { get; set; }
        public decimal SLAG_GENERATION_TODT { get; set; }
        public decimal SLAG_LADLE_TONS_ONDT { get; set; }
        public decimal SLAG_LADLE_TONS_TODT { get; set; }

        [HttpGet]
    public JsonResult GetBFSlagReport(DateTime? p_date)
    {
        var list = new List<BFSlagReport>();

        string sql = @"
            SELECT
                t.FUR_NO,
                ROUND(NVL(t.SLAG_GENERATION, 0))
                    AS SLAG_GENERATION_ONDT,
                ROUND(NVL(tt.SLAG_GENERATION, 0))
                    AS SLAG_GENERATION_TODT,
                ROUND(NVL(t.SLAG_LADLE_TONS, 0))
                    AS SLAG_LADLE_TONS_ONDT,
                ROUND(NVL(tt.SLAG_LADLE_TONS, 0))
                    AS SLAG_LADLE_TONS_TODT
            FROM DEMO.T_BF_PRODUCTION_TEST t
            INNER JOIN DEMO.T_BF_PRODUCTION_TEST tt
                ON t.TIMESTAMP = tt.TIMESTAMP
               AND t.FUR_NO = tt.FUR_NO
            WHERE TRUNC(t.TIMESTAMP) = :p_date
              AND t.FUR_NO NOT IN ('G', 'H', 'D')
            ORDER BY t.FUR_NO";

        try
        {
            using (OracleConnection con =
                new OracleConnection(iMonitorWebUtils.msConRWString))
            using (OracleCommand cmd = new OracleCommand(sql, con))
            {
                cmd.BindByName = true;

                cmd.Parameters.Add("p_date", OracleDbType.Date).Value =
                    (p_date ?? DateTime.Today).Date;

                con.Open();

                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        BFSlagReport item = new BFSlagReport
                        {
                            FUR_NO = dr["FUR_NO"].ToString(),

                            SLAG_GENERATION_ONDT =
                                Convert.ToDecimal(dr["SLAG_GENERATION_ONDT"]),

                            SLAG_GENERATION_TODT =
                                Convert.ToDecimal(dr["SLAG_GENERATION_TODT"]),

                            SLAG_LADLE_TONS_ONDT =
                                Convert.ToDecimal(dr["SLAG_LADLE_TONS_ONDT"]),

                            SLAG_LADLE_TONS_TODT =
                                Convert.ToDecimal(dr["SLAG_LADLE_TONS_TODT"])
                        };

                        list.Add(item);
                    }
                }
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }
        catch (Exception ex)
        {
            Response.StatusCode = 500;

            return Json(new
            {
                status = false,
                message = ex.Message
            }, JsonRequestBehavior.AllowGet);
        }
    }
    <input type="text" id="SLAG_GENERATION_ONDT" class="form-control" />
<input type="text" id="SLAG_GENERATION_TODT" class="form-control" />
<input type="text" id="SLAG_LADLE_TONS_ONDT" class="form-control" />
<input type="text" id="SLAG_LADLE_TONS_TODT" class="form-control" />
function GetBFSlagReport() {
    $.ajax({
        url: '@Url.Action("GetBFSlagReport", "Report")',
        type: 'GET',
        data: {
            p_date: $('#p_date').val()
        },
        success: function (data) {

            if (data != null && data.length > 0) {
                var item = data[0];

                $('#FUR_NO').val(item.FUR_NO);
                $('#SLAG_GENERATION_ONDT').val(item.SLAG_GENERATION_ONDT);
                $('#SLAG_GENERATION_TODT').val(item.SLAG_GENERATION_TODT);
                $('#SLAG_LADLE_TONS_ONDT').val(item.SLAG_LADLE_TONS_ONDT);
                $('#SLAG_LADLE_TONS_TODT').val(item.SLAG_LADLE_TONS_TODT);
            }
            else {
                alert('No records found');
            }
        },
        error: function (xhr) {
            console.log(xhr.responseText);
        }
    });
}

$('#p_date').change(function () {
    GetBFSlagReport();
});
C	879	879	0	0
E	0	0	139	139
F	1671	1671	0	0
