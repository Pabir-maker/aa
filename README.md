  <div class="table-responsive">
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
                                        <td colspan="7" class="text-center">
                                            Loading data...
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                          <script>
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
