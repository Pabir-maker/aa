   [HttpPost]
        public JsonResult SaveATOFBinRequired(string furnace, List<Dictionary<string, object>> Bin_Required)
        {
            if (Bin_Required == null || Bin_Required.Count == 0)
                return Json(new { status = false, message = "No data received." });
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                using (OracleTransaction trans = con.BeginTransaction())
                {
                    try
                    {
                        string query = @"UPDATE imtg.T_ATOF_BIN_DETAILS SET REQUIRED=Bin_Required WHERE FUR_NAME=furnace AND WEB_SL_NO=Web_Id AND  WEB_SL_NO IS NOT NULL";

                        foreach (var row in Bin_Required)
                        {
                            int tagId = Convert.ToInt32(row["WEB_SL_NO"]);
                            //string Fur = row["furnace"];                           
                            using (OracleCommand cmd = new OracleCommand(query, con))
                            {
                                cmd.Transaction = trans;
                                cmd.BindByName = true;
                                cmd.Parameters.Add(":WEB_SL_NO", OracleDbType.Int32).Value = tagId;
                                //cmd.Parameters.Add(":FURNACE", OracleDbType.Varchar2).Value = Fur;
                                cmd.ExecuteNonQuery();
                            }
                        }

                        trans.Commit();
                        return Json(new { status = true, message = "All Data Saved Successfully" });
                    }
                    catch (Exception ex)
                    {
                        trans.Rollback();
                        return Json(new { status = false, message = ex.Message });
                    }
                }
            }
        }
