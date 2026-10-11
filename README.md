```cshtml
@{
    ViewBag.Title = "ATOF Raw Material Report";
}

<div class="container-fluid mt-2">

    <h5 class="text-center">
        ATOF Raw Material Report
    </h5>

    <div class="table-responsive">
        <table class="table table-bordered table-sm table-striped">

            <thead class="table-dark text-center">
                <tr>
                    <th>Sl No</th>
                    <th>Material</th>
                    <th>Period</th>
                    <th>CBF</th>
                    <th>EBF</th>
                    <th>FBF</th>
                    <th>Plant</th>
                </tr>
            </thead>

            <tbody id="rawMaterialBody">
                <tr>
                    <td colspan="7" class="text-center">
                        Loading...
                    </td>
                </tr>
            </tbody>

        </table>
    </div>

</div>

<script>
    $(document).ready(function () {
        LoadRawMaterialReport();
    });

    function LoadRawMaterialReport() {

        $.ajax({
            url: '@Url.Action("GETATOFProdRawmaterialReport", "Report")',
            type: 'GET',
            dataType: 'json',

            success: function (data) {

                var rows = '';

                if (data == null || data.length == 0) {

                    rows = '<tr>' +
                           '<td colspan="7" class="text-center">' +
                           'No records found' +
                           '</td></tr>';

                }
                else {

                    for (var i = 0; i < data.length; i++) {

                        rows += '<tr>' +
                            '<td>' + (i + 1) + '</td>' +
                            '<td>' + (data[i].Material || '') + '</td>' +
                            '<td>' + (data[i].Period || '') + '</td>' +
                            '<td>' + (data[i].CBF ?? '') + '</td>' +
                            '<td>' + (data[i].EBF ?? '') + '</td>' +
                            '<td>' + (data[i].FBF ?? '') + '</td>' +
                            '<td>' + (data[i].Plant || '') + '</td>' +
                            '</tr>';
                    }

                }

                $('#rawMaterialBody').html(rows);
            },

            error: function () {

                $('#rawMaterialBody').html(
                    '<tr><td colspan="7" class="text-center text-danger">' +
                    'Error loading report' +
                    '</td></tr>'
                );

            }
        });
    }
</script>
```
