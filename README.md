  <script>   
    function LoadRawMaterialReport() {
        $.ajax({
            url: '@Url.Action("GETATOFProdRawmaterialReport", "Report")',
            type: 'GET',
            dataType: 'json',

            success: function (data) {
                var rows = '';

                if (!data || data.length === 0) {
                    rows = '<tr><td colspan="7" class="text-center">' +
                           'No records found</td></tr>';

                    $('#rawMaterialBody').html(rows);
                    return;
                }

                $.each(data, function (i, item) {

                    rows += '<tr>' +
                        '<td>' + (i + 1) + '</td>' +
                        '<td>' + escapeHtml(item.Material) + '</td>' +
                        '<td>' + escapeHtml(item.Period) + '</td>' +
                        '<td>' + formatNumber(item.CBF) + '</td>' +
                        '<td>' + formatNumber(item.EBF) + '</td>' +
                        '<td>' + formatNumber(item.FBF) + '</td>' +
                        '<td>' + formatNumber(item.Plant) + '</td>' +
                        '</tr>';
                });

                $('#rawMaterialBody').html(rows);
            },

            error: function (xhr, status, error) {
                $('#rawMaterialBody').html(
                    '<tr><td colspan="7" class="text-center text-danger">' +
                    'Error loading raw material report</td></tr>'
                );

                console.error(error);
            }
        });
    }
    
    </script>
