 function Distribution_HM_TON()
        {
            $.ajax({
                url: '@Url.Action("GET_Distribution_HM_TON", "Report")',
                type: 'GET',
                data: { date: lsSelectedFDate },
                dataType: 'json',
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

}
