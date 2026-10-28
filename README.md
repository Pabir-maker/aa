
[HttpPost]
public JsonResult SaveATOFBinRequired(
    string furnace,
    List<Dictionary<string, object>> Bin_Required)
{
    if (Bin_Required == null || Bin_Required.Count == 0)
    {
        return Json(new
        {
            status = false,
            message = "No data received."
        });
    }

    using (OracleConnection con =
        new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        using (OracleTransaction trans = con.BeginTransaction())
        {
            try
            {
                string query = @"
                    UPDATE imtg.T_ATOF_BIN_DETAILS
                    SET REQUIRED = :REQUIRED
                    WHERE FUR_NAME = :FURNACE
                      AND WEB_SL_NO = :WEB_SL_NO
                      AND WEB_SL_NO IS NOT NULL";

                foreach (var row in Bin_Required)
                {
                    int tagId = Convert.ToInt32(row["WEB_SL_NO"]);

                    string required =
                        Convert.ToString(row["REQUIRED"]);

                    if (required != "Y" && required != "N")
                    {
                        throw new Exception(
                            "Invalid REQUIRED value for tag ID: " + tagId);
                    }

                    using (OracleCommand cmd =
                        new OracleCommand(query, con))
                    {
                        cmd.Transaction = trans;
                        cmd.BindByName = true;

                        cmd.Parameters.Add(
                            ":REQUIRED",
                            OracleDbType.Varchar2).Value = required;

                        cmd.Parameters.Add(
                            ":FURNACE",
                            OracleDbType.Varchar2).Value = furnace;

                        cmd.Parameters.Add(
                            ":WEB_SL_NO",
                            OracleDbType.Int32).Value = tagId;

                        cmd.ExecuteNonQuery();
                    }
                }

                trans.Commit();

                return Json(new
                {
                    status = true,
                    message = "All data saved successfully."
                });
            }
            catch (Exception ex)
            {
                trans.Rollback();

                return Json(new
                {
                    status = false,
                    message = ex.Message
                });
            }
        }
    }
}


function btnSaveBinRequired() {

    var furnace = $("#ddlFurnaceModal").val();
    var binRequired = [];

    $("#tblBinDetails tbody tr").each(function () {

        var row = $(this);

        var tagId = row.find(".web-sl-no").text().trim();
        var required = row.find(".ddlRequired").val();

        // Ignore empty or invalid rows
        if (tagId !== "" && required) {

            binRequired.push({
                WEB_SL_NO: tagId,
                REQUIRED: required
            });
        }
    });

    if (binRequired.length === 0) {
        alert("No data available to save.");
        return;
    }

    $.ajax({
        url: '@Url.Action("SaveATOFBinRequired", "YourControllerName")',
        type: "POST",
        contentType: "application/json; charset=utf-8",
        data: JSON.stringify({
            furnace: furnace,
            Bin_Required: binRequired
        }),

        success: function (response) {

            if (response.status) {
                alert(response.message);
            } else {
                alert(response.message);
            }
        },

        error: function (xhr) {
            alert("Error saving data: " + xhr.responseText);
        }
    });
}
