```csharp
[HttpGet]
public JsonResult GETATOFProdRawmaterialReport()
{
    var list = new List<RawMaterialReport>();

    string sql = @"
        SELECT
            MATERIAL,
            PERIOD,
            CBF,
            EBF,
            FBF,
            PLANT
        FROM IMTG.V_ATOP_RAW_MATERIAL_REPORT
        WHERE TIMESTAMP >= SYSDATE - 2
        ORDER BY TIMESTAMP, PERIOD";

    using (OracleConnection con =
        new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        using (OracleCommand cmd = new OracleCommand(sql, con))
        {
            using (OracleDataReader reader = cmd.ExecuteReader())
            {
                while (reader.Read())
                {
                    list.Add(new RawMaterialReport
                    {
                        Material = reader["MATERIAL"] == DBNull.Value
                            ? null
                            : Convert.ToString(reader["MATERIAL"]),

                        Period = reader["PERIOD"] == DBNull.Value
                            ? null
                            : Convert.ToString(reader["PERIOD"]),

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
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
```
