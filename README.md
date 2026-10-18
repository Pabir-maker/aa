$(document).ready(function () {

    $.ajax({
        url: '@Url.Action("GetLadleTonReport", "Report")',
        type: 'GET',
        data: {
            p_date: $('#p_date').val()
        },
        success: function (data) {
            if (data != null && data.length > 0) {
                var item = data[0];

                $('#LD1_TON_ONDT').val(item.LD1_TON_ONDT);
                $('#TOTAL_ONDT').val(item.TOTAL_ONDT);
                $('#LD1_TON_TODT').val(item.LD1_TON_TODT);
                $('#TOTAL_TODT').val(item.TOTAL_TODT);
            }
        },
        error: function (xhr) {
            console.log(xhr.responseText);
        }
    });

});
