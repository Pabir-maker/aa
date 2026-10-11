```cshtml
@{
    ViewBag.Title = "ATOF Raw Material Report";
}

<div class="container-fluid mt-2">

    <h5 class="text-center mb-2">
        ATOF RAW MATERIAL REPORT
    </h5>

    <div class="table-responsive">
        <table id="tblRawMaterial"
               class="table table-bordered table-sm">

            <thead>
                <tr>
                    <th>SL.NO</th>
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
                    <td colspan="7" class="text-center">
                        Loading data...
                    </td>
                </tr>
            </tbody>

        </table>
    </div>

</div>

<style>
    #tblRawMaterial {
        width: 100%;
        margin-bottom: 0;
        font-size: 12px;
        text-align: center;
        border-collapse: collapse;
    }

    #tblRawMaterial thead th {
        background-color: #c0f9fa;
        color: #000;
        font-weight: bold;
        white-space: nowrap;
        padding: 4px;
        position: sticky;
        top: 0;
        z-index: 2;
    }

    #tblRawMaterial tbody td {
        padding: 3px 6px;
        height: 25px;
        vertical-align: middle;
        white-space: nowrap;
    }

    #tblRawMaterial tbody tr:nth-child(even) {
        background-color: #f2f2f2;
    }

    #tblRawMaterial tbody tr:hover {
        background-color: #fff3cd;
    }
</style>

<script src="~/Scripts/jquery-3.7.0.min.js"></script>

<script>
    $(document).ready(function () {
        LoadRawMaterialReport();
    });

    function LoadRawMaterialReport() {

        $.ajax({
            url: '@Url.Action("GETATOFProdRawmaterialReport", "ATOF")',
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

    function formatNumber(value) {
        if (value === null || value === undefined || value === '') {
            return '';
        }

        var number = Number(value);

        return isNaN(number) ? escapeHtml(value) : number.toFixed(2);
    }

    function escapeHtml(value) {
        if (value === null || value === undefined) {
            return '';
        }

        return $('<div>').text(String(value)).html();
    }
</script>
```
