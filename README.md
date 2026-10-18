
using System;
using System.Collections.Generic;
using System.Web.Mvc;
using Oracle.ManagedDataAccess.Client;
using Oracle.ManagedDataAccess.Types;
using YourProjectName.Models;

public class ReportController : Controller
{
    [HttpGet]
    public JsonResult GetLadleTonReport(DateTime? p_date)
    {
        var list = new List<LadleTonReport>();

        string sql = @"
            SELECT
                t.DATE_TIME,
                t.LD1_TONS AS LD1_TON_ONDT,
                t.LD2_TONS AS LD2_TON_ONDT,
                t.LD3_TONS AS LD3_TON_ONDT,
                t.MRDTP_TONS AS MRDTP_TONS_ONDT,

                (NVL(t.LD1_TONS, 0) +
                 NVL(t.LD2_TONS, 0) +
                 NVL(t.LD3_TONS, 0) +
                 NVL(t.MRDTP_TONS, 0)) AS TOTAL_ONDT,

                k.LD1_TONS AS LD1_TON_TODT,
                k.LD2_TONS AS LD2_TON_TODT,
                k.LD3_TONS AS LD3_TON_TODT,
                k.MRDTP_TONS AS MRDTP_TON_TODT,

                (NVL(k.LD1_TONS, 0) +
                 NVL(k.LD2_TONS, 0) +
                 NVL(k.LD3_TONS, 0) +
                 NVL(k.MRDTP_TONS, 0)) AS TOTAL_TODT

            FROM DEMO.T_LADLE t
            INNER JOIN DEMO.T_LADLE_TODATE k
                ON t.DATE_TIME = k.DATE_TIME
               AND t.PLANT = k.PLANT

            WHERE t.DATE_TIME >= :p_date
              AND t.PLANT = :p_plant

            ORDER BY t.DATE_TIME";

        try
        {
            using (OracleConnection con =
                new OracleConnection(iMonitorWebUtils.msConRWString))
            using (OracleCommand cmd = new OracleCommand(sql, con))
            {
                cmd.BindByName = true;

                cmd.Parameters.Add("p_date", OracleDbType.Date).Value =
                    (p_date ?? new DateTime(2026, 10, 17)).Date;

                cmd.Parameters.Add("p_plant", OracleDbType.Varchar2).Value = "A-F";

                con.Open();

                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        var item = new LadleTonReport
                        {
                            DATE_TIME = Convert.ToDateTime(dr["DATE_TIME"]),

                            LD1_TON_ONDT = GetDecimal(dr, "LD1_TON_ONDT"),
                            LD2_TON_ONDT = GetDecimal(dr, "LD2_TON_ONDT"),
                            LD3_TON_ONDT = GetDecimal(dr, "LD3_TON_ONDT"),
                            MRDTP_TONS_ONDT = GetDecimal(dr, "MRDTP_TONS_ONDT"),
                            TOTAL_ONDT = GetDecimal(dr, "TOTAL_ONDT"),

                            LD1_TON_TODT = GetDecimal(dr, "LD1_TON_TODT"),
                            LD2_TON_TODT = GetDecimal(dr, "LD2_TON_TODT"),
                            LD3_TON_TODT = GetDecimal(dr, "LD3_TON_TODT"),
                            MRDTP_TON_TODT = GetDecimal(dr, "MRDTP_TON_TODT"),
                            TOTAL_TODT = GetDecimal(dr, "TOTAL_TODT")
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

    private decimal GetDecimal(OracleDataReader dr, string columnName)
    {
        int index = dr.GetOrdinal(columnName);

        if (dr.IsDBNull(index))
            return 0;

        return Convert.ToDecimal(dr.GetValue(index));
    }
}


$(document).ready(function () {
    $.ajax({
        url: '@Url.Action("GetLadleTonReport", "Report")',
        type: 'GET',
        data: {
            p_date: '2026-10-17'
        },
        success: function (data) {
            console.log(data);

            $.each(data, function (i, item) {
                console.log("Date:", item.DATE_TIME);
                console.log("LD1 ONDT:", item.LD1_TON_ONDT);
                console.log("Total ONDT:", item.TOTAL_ONDT);
                console.log("LD1 TODT:", item.LD1_TON_TODT);
                console.log("Total TODT:", item.TOTAL_TODT);
            });
        },
        error: function (xhr) {
            console.log(xhr.responseText);
        }
    });
});
