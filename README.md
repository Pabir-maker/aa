using System;
using System.Collections.Generic;
using System.Configuration;
using System.Web.Mvc;
using Oracle.ManagedDataAccess.Client;
using YourProject.Models;

namespace YourProject.Controllers
{
    public class RawMaterialController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }

        [HttpGet]
        public JsonResult GetReport()
        {
            var list = new List<RawMaterialReport>();

            string sql = @"
                SELECT TIMESTAMP, MATERIAL, PERIOD,
                       CBF, EBF, FBF, PLANT
                FROM IMTG.V_ATOP_RAW_MATERIAL_REPORT
                WHERE TIMESTAMP >= SYSDATE - 2
                ORDER BY TIMESTAMP DESC";

            string connectionString =
                ConfigurationManager
                .ConnectionStrings["OracleConnection"]
                .ConnectionString;

            using (var con =
                new OracleConnection(connectionString))
            using (var cmd = new OracleCommand(sql, con))
            {
                con.Open();

                using (var reader = cmd.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        list.Add(new RawMaterialReport
                        {
                            Timestamp = Convert.ToDateTime(
                                reader["TIMESTAMP"])
                                .ToString("dd-MMM-yyyy HH:mm:ss"),

                            Material = Convert.ToString(
                                reader["MATERIAL"]),

                            Period = Convert.ToString(
                                reader["PERIOD"]),

                            CBF = reader["CBF"] == DBNull.Value
                                ? (decimal?)null
                                : Convert.ToDecimal(reader["CBF"]),

                            EBF = reader["EBF"] == DBNull.Value
                                ? (decimal?)null
                                : Convert.ToDecimal(reader["EBF"]),

                            FBF = reader["FBF"] == DBNull.Value
                                ? (decimal?)null
                                : Convert.ToDecimal(reader["FBF"]),

                            Plant = reader["PLANT"] == DBNull.Value
                                ? (decimal?)null
                                : Convert.ToDecimal(reader["PLANT"])
                        });
                    }
                }
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }
    }
}