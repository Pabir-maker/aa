@{
    ViewBag.Title = "Raw Materials Consumption";
    var reportDate = DateTime.Today;
}

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
      rel="stylesheet" />

<style>
    body {
        font-family: Arial, sans-serif;
        font-size: 12px;
        margin: 5px;
        background: white;
    }

    .report-container {
        width: 100%;
        overflow-x: auto;
    }

    .raw-table {
        width: 100%;
        min-width: 800px;
        border-collapse: collapse;
        table-layout: fixed;
    }

    .raw-table th,
    .raw-table td {
        border: 1px solid #999;
        padding: 2px 5px;
        height: 22px;
        line-height: 16px;
        vertical-align: middle;
    }

    .raw-table th {
        background-color: #e7e6e6;
        text-align: center;
        font-weight: bold;
    }

    .raw-table .report-title {
        background-color: #d9e2f3;
        text-align: center;
        font-size: 13px;
        font-weight: bold;
        height: 28px;
    }

    .raw-table .material {
        text-align: left;
    }

    .raw-table .period {
        text-align: left;
    }

    .raw-table .number {
        text-align: right;
    }

    .raw-table tbody tr.gap-row td {
        height: 12px;
        padding: 0;
        background: #fff;
    }

    .raw-table input {
        width: 100%;
        border: none;
        outline: none;
        padding: 0;
        background: transparent;
        text-align: right;
        font-size: 12px;
    }

    .raw-table input:focus {
        background: #c0f9fa;
    }

    @media print {
        body {
            margin: 0;
        }

        .report-container {
            overflow: visible;
        }

        .raw-table {
            min-width: 0;
        }
    }
</style>

<div class="report-container">
    <table class="raw-table">

        <colgroup>
            <col style="width: 25%" />
            <col style="width: 10%" />
            <col style="width: 16.25%" />
            <col style="width: 16.25%" />
            <col style="width: 16.25%" />
            <col style="width: 16.25%" />
        </colgroup>

        <thead>
            <tr>
                <th colspan="2"></th>
                <th colspan="2" class="report-title">
                    Raw Materials Consumption in Blast Furnaces on
                </th>
                <th colspan="2" class="report-title">
                    @reportDate.ToString("dd-MMM-yy")
                </th>
            </tr>

            <tr>
                <th>Fce No.</th>
                <th></th>
                <th>C-fce</th>
                <th>E-fce</th>
                <th>F-fce</th>
                <th>PLANT</th>
            </tr>
        </thead>

        <tbody>
            <tr>
                <td class="material" rowspan="2">Coke</td>
                <td class="period">OnDt</td>
                <td class="number">748</td>
                <td class="number">499</td>
                <td class="number">1297</td>
                <td class="number">2544</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">7093</td>
                <td class="number">4450</td>
                <td class="number">12154</td>
                <td class="number">23697</td>
            </tr>

            <tr class="gap-row">
                <td colspan="6"></td>
            </tr>

            <tr>
                <td class="material" rowspan="2">Nut Coke</td>
                <td class="period">OnDt</td>
                <td class="number">145</td>
                <td class="number">63</td>
                <td class="number">75</td>
                <td class="number">283</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">1239</td>
                <td class="number">565</td>
                <td class="number">806</td>
                <td class="number">2610</td>
            </tr>

            <tr class="gap-row">
                <td colspan="6"></td>
            </tr>

            <tr>
                <td class="material" rowspan="2">Noa Ore</td>
                <td class="period">OnDt</td>
                <td class="number">0</td>
                <td class="number">129</td>
                <td class="number">62</td>
                <td class="number">191</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">684</td>
                <td class="number">1538</td>
                <td class="number">3224</td>
                <td class="number">5446</td>
            </tr>

            <tr class="gap-row">
                <td colspan="6"></td>
            </tr>

            <tr>
                <td class="material" rowspan="2">Joda Ore</td>
                <td class="period">OnDt</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
            </tr>

            <tr class="gap-row">
                <td colspan="6"></td>
            </tr>

            <tr>
                <td class="material" rowspan="2">Sinter</td>
                <td class="period">OnDt</td>
                <td class="number">1542</td>
                <td class="number">924</td>
                <td class="number">3157</td>
                <td class="number">5623</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">11516</td>
                <td class="number">7548</td>
                <td class="number">25982</td>
                <td class="number">45046</td>
            </tr>

            <tr class="gap-row">
                <td colspan="6"></td>
            </tr>

            <tr>
                <td class="material" rowspan="2">Mn Ore</td>
                <td class="period">OnDt</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
            </tr>

            <tr class="gap-row">
                <td colspan="6"></td>
            </tr>

            <tr>
                <td class="material" rowspan="2">Quartz</td>
                <td class="period">OnDt</td>
                <td class="number">31</td>
                <td class="number">16</td>
                <td class="number">38</td>
                <td class="number">85</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">299</td>
                <td class="number">88</td>
                <td class="number">157</td>
                <td class="number">544</td>
            </tr>

            <tr class="gap-row">
                <td colspan="6"></td>
            </tr>

            <tr>
                <td class="material" rowspan="2">Limestone</td>
                <td class="period">OnDt</td>
                <td class="number">40</td>
                <td class="number">24</td>
                <td class="number">85</td>
                <td class="number">149</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">759</td>
                <td class="number">247</td>
                <td class="number">706</td>
                <td class="number">1713</td>
            </tr>

            <tr class="gap-row">
                <td colspan="6"></td>
            </tr>

            <tr>
                <td class="material" rowspan="2">Dolomite</td>
                <td class="period">OnDt</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">0</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">0</td>
                <td class="number">0</td>
                <td class="number">21</td>
                <td class="number">21</td>
            </tr>

            <tr class="gap-row">
                <td colspan="6"></td>
            </tr>

            <tr>
                <td class="material" rowspan="2">Scrap</td>
                <td class="period">OnDt</td>
                <td class="number">0</td>
                <td class="number">62</td>
                <td class="number">0</td>
                <td class="number">62</td>
            </tr>
            <tr>
                <td class="period">ToDt</td>
                <td class="number">0</td>
                <td class="number">531</td>
                <td class="number">0</td>
                <td class="number">531</td>
            </tr>
        </tbody>
    </table>
</div>