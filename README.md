<div class="table-responsive raw-table-container">
    <table id="tblRawMaterial"
           class="table table-bordered table-sm">

        <thead>
            <tr>
                <th>MATERIAL</th>
                <th>PERIOD</th>
                <th>CBF</th>
                <th>EBF</th>
                <th>FBF</th>
                <th>PLANT</th>
            </tr>
        </thead>

        <tbody id="rawMaterialBody">
            <tr>
                <td colspan="6" class="text-center">
                    Loading data...
                </td>
            </tr>
        </tbody>

    </table>
</div>
<style>
    .raw-table-container {
        max-height: 300px;
        overflow: auto;
    }

    #tblRawMaterial {
        width: 100%;
        table-layout: fixed;
        font-size: 11px;
        margin-bottom: 0;
    }

    #tblRawMaterial th,
    #tblRawMaterial td {
        padding: 2px 4px;
        height: 23px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    #tblRawMaterial thead th {
        position: sticky;
        top: 0;
        background: #343a40;
        color: white;
        z-index: 5;
    }

    #tblRawMaterial th:nth-child(1) { width: 100px; }
    #tblRawMaterial th:nth-child(2) { width: 85px; }
    #tblRawMaterial th:nth-child(3),
    #tblRawMaterial th:nth-child(4),
    #tblRawMaterial th:nth-child(5) { width: 65px; }
    #tblRawMaterial th:nth-child(6) { width: 90px; }
</style>
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

                if (!data || data.length == 0) {
                    rows = '<tr><td colspan="6" class="text-center">' +
                           'No records found</td></tr>';
                }
                else {

                    for (var i = 0; i < data.length; i++) {

                        var materialCell = '';

                        // Merge two consecutive rows with same material
                        if (i > 0 &&
                            data[i].Material == data[i - 1].Material) {

                            // Material cell already displayed above
                        }
                        else {

                            var span = 1;

                            if (i + 1 < data.length &&
                                data[i].Material == data[i + 1].Material) {
                                span = 2;
                            }

                            materialCell = '<td rowspan="' + span + '">' +
                                           (data[i].Material || '') +
                                           '</td>';
                        }

                        rows += '<tr>' +
                            materialCell +
                            '<td>' + (data[i].Period || '') + '</td>' +
                            '<td>' + (data[i].CBF == null ? '' : data[i].CBF) + '</td>' +
                            '<td>' + (data[i].EBF == null ? '' : data[i].EBF) + '</td>' +
                            '<td>' + (data[i].FBF == null ? '' : data[i].FBF) + '</td>' +
                            '<td>' + (data[i].Plant || '') + '</td>' +
                            '</tr>';
                    }
                }

                $('#rawMaterialBody').html(rows);
            },

            error: function () {
                $('#rawMaterialBody').html(
                    '<tr><td colspan="6" class="text-center text-danger">' +
                    'Error loading report</td></tr>'
                );
            }
        });
    }
</script>
