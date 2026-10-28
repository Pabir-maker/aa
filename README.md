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
         <div class="d-flex align-items-center ms-3 mt-2">
                    <label for="ddlFurnaceModal" style="font-family:Allan,cursive; font-weight:bold; margin-right:10px;">
                        Furname :-
                    </label>
                    <select id="ddlFurnaceModal" class="form-select w-auto">
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                    </select>
                </div>
                <div class="modal-body">
                    <div class="table-container">
                        <table id="tblBinDetails" class="table table-bordered" style="font-family:Courier New; font-weight:bold;">
                            <thead>
                                <tr>
                                    <th style="width:30px;">FUR NAME</th>
                                    <th style="width:30px;">iMONITOR TAG ID</th>
                                    <th style="width:90px;">iHISTORIAN TAG NAME</th>
                                    <th style="width:40px;">WEB COLUMN</th>
                                    <th style="width:40px;">TAG TYPE</th>
                                    <th style="width:40px;">REQUIRED</th>
                                </tr>
                            </thead>
                            <tbody></tbody>
                        </table>
                    </div>
                </div>
                <div class="modal-footer justify-content-center">
                    <button class="btn-Modalsave" onclick="btnSaveBinRequired()">Save</button>
                    <button class="btn-Modalexit" data-bs-dismiss="modal">Exit</button>
                </div>
