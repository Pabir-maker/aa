<script>
    $(document).ready(function () {

        $.getJSON('@Url.Action("GETATOFProdRawmaterialReport", "Report")',
            function (data) {

                var rows = '';

                if (data.length == 0) {
                    rows = '<tr><td colspan="7">No records found</td></tr>';
                }
                else {
                    $.each(data, function (i, item) {

                        rows += '<tr>' +
                            '<td>' + (i + 1) + '</td>' +
                            '<td>' + item.Material + '</td>' +
                            '<td>' + item.Period + '</td>' +
                            '<td>' + item.CBF + '</td>' +
                            '<td>' + item.EBF + '</td>' +
                            '<td>' + item.FBF + '</td>' +
                            '<td>' + item.Plant + '</td>' +
                            '</tr>';
                    });
                }

                $('#rawMaterialBody').html(rows);

            });
    });
</script>
