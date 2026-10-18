<tr>
            <td>C</td>
            <td><input type="text" id="C_SG_ONDT" class="form-control form-control-sm" readonly /></td>
            <td><input type="text" id="C_SG_TODT" class="form-control form-control-sm" readonly /></td>
            <td><input type="text" id="C_SL_ONDT" class="form-control form-control-sm" readonly /></td>
            <td><input type="text" id="C_SL_TODT" class="form-control form-control-sm" readonly /></td>
        </tr>
        <tr>
            <td>E</td>
            <td><input type="text" id="E_SG_ONDT" class="form-control form-control-sm" readonly /></td>
            <td><input type="text" id="E_SG_TODT" class="form-control form-control-sm" readonly /></td>
            <td><input type="text" id="E_SL_ONDT" class="form-control form-control-sm" readonly /></td>
            <td><input type="text" id="E_SL_TODT" class="form-control form-control-sm" readonly /></td>
        </tr>
        <tr>
            <td>F</td>
            <td><input type="text" id="F_SG_ONDT" class="form-control form-control-sm" readonly /></td>
            <td><input type="text" id="F_SG_TODT" class="form-control form-control-sm" readonly /></td>
            <td><input type="text" id="F_SL_ONDT" class="form-control form-control-sm" readonly /></td>
            <td><input type="text" id="F_SL_TODT" class="form-control form-control-sm" readonly /></td>
        </tr>
        function GetBFSlagReport() {

    $.ajax({
        url: '@Url.Action("GetBFSlagReport", "Report")',
        type: 'GET',
        data: {
            p_date: $('#p_date').val()
        },
        success: function (data) {

            // Clear existing values
            $('input[id$="_SG_ONDT"], input[id$="_SG_TODT"], input[id$="_SL_ONDT"], input[id$="_SL_TODT"]').val('');

            $.each(data, function (i, item) {

                var f = item.FUR_NO;

                $('#' + f + '_SG_ONDT').val(item.SLAG_GENERATION_ONDT);
                $('#' + f + '_SG_TODT').val(item.SLAG_GENERATION_TODT);

                $('#' + f + '_SL_ONDT').val(item.SLAG_LADLE_TONS_ONDT);
                $('#' + f + '_SL_TODT').val(item.SLAG_LADLE_TONS_TODT);
            });
        },
        error: function (xhr) {
            console.log(xhr.responseText);
        }
    });
}

$(document).ready(function () {
    GetBFSlagReport();

    $('#p_date').change(function () {
        GetBFSlagReport();
    });
});
[HttpGet]
    public JsonResult GetBFSlagReport(DateTime? p_date)
    {
        List<BFSlagReport> list = new List<BFSlagReport>();

        string sql = @"
            SELECT
                t.FUR_NO,
                ROUND(NVL(t.SLAG_GENERATION, 0)) AS SLAG_GENERATION_ONDT,
                ROUND(NVL(tt.SLAG_GENERATION, 0)) AS SLAG_GENERATION_TODT,
                ROUND(NVL(t.SLAG_LADLE_TONS, 0)) AS SLAG_LADLE_TONS_ONDT,
                ROUND(NVL(tt.SLAG_LADLE_TONS, 0)) AS SLAG_LADLE_TONS_TODT
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
                            FUR_NO = Convert.ToString(dr["FUR_NO"]),

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
