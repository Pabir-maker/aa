@{
    ViewBag.Title = "Production Report";
}

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
      rel="stylesheet" />

<style>
    body {
        font-family: Arial, sans-serif;
        font-size: 11px;
        background: #fff;
        margin: 5px;
    }

    .report-wrapper {
        width: 100%;
        overflow-x: auto;
    }

    .report-layout {
        display: grid;
        grid-template-columns: 70% 30%;
        min-width: 1200px;
        gap: 0;
    }

    .report-table {
        width: 100%;
        border-collapse: collapse;
        table-layout: fixed;
        margin: 0;
    }

    .report-table th,
    .report-table td {
        border: 1px solid #858585;
        padding: 2px 4px;
        height: 19px;
        line-height: 14px;
        vertical-align: middle;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: clip;
    }

    .report-table th {
        background: #d9d9d9;
        font-weight: bold;
        text-align: center;
    }

    .report-table td {
        text-align: right;
    }

    .report-table .label {
        text-align: left;
        font-weight: bold;
    }

    .report-table .sub-label {
        text-align: center;
        font-weight: normal;
    }

    .section-title {
        background: #c9c9c9;
        font-weight: bold;
        text-align: center !important;
    }

    .report-left {
        padding-right: 0;
    }

    .report-right {
        padding-left: 0;
    }

    .report-table input {
        border: 0;
        outline: none;
        width: 100%;
        height: 15px;
        padding: 0;
        margin: 0;
        background: transparent;
        text-align: right;
        font-size: 11px;
    }

    .report-table input:focus {
        background: #c0f9fa;
    }

    .report-table .number {
        text-align: right;
    }

    @media print {
        body {
            margin: 0;
        }

        .report-wrapper {
            overflow: visible;
        }

        .report-layout {
            min-width: 0;
        }
    }
</style>

<div class="report-wrapper">
    <div class="report-layout">

        <!-- LEFT TABLE: PRODUCTION REPORT -->
        <div class="report-left">
            <table class="report-table">
                <colgroup>
                    <col style="width: 22%">
                    <col style="width: 11%">
                    <col style="width: 13%">
                    <col style="width: 13%">
                    <col style="width: 13%">
                    <col style="width: 14%">
                    <col style="width: 14%">
                </colgroup>

                <thead>
                    <tr>
                        <th>Production Report</th>
                        <th>Period</th>
                        <th>E-fce</th>
                        <th>C-fce</th>
                        <th>D-fce</th>
                        <th>F-fce</th>
                        <th>PLANT</th>
                    </tr>
                </thead>

                <tbody>
                    <tr>
                        <td class="label">Dangerous Occurrence</td>
                        <td colspan="5" style="text-align:center">Nil</td>
                        <td>0</td>
                    </tr>

                    <tr>
                        <td class="label">Rounds</td>
                        <td class="sub-label">On Dt</td>
                        <td>552</td>
                        <td>96</td>
                        <td>0</td>
                        <td>0</td>
                        <td>648</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td class="sub-label">To Dt</td>
                        <td> </td>
                        <td> </td>
                        <td> </td>
                        <td> </td>
                        <td> </td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">No. of Casts</td>
                        <td class="sub-label">On Dt</td>
                        <td>9</td>
                        <td>11</td>
                        <td>0</td>
                        <td>9</td>
                        <td>29</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>81</td>
                        <td>95</td>
                        <td>0</td>
                        <td>101</td>
                        <td>277</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Production (tons)</td>
                        <td class="sub-label">On Dt</td>
                        <td>1200</td>
                        <td>1950</td>
                        <td>0</td>
                        <td>4050</td>
                        <td>7200</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>10650</td>
                        <td>17000</td>
                        <td>0</td>
                        <td>36850</td>
                        <td>64500</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Productivity (t/m3/day)</td>
                        <td class="sub-label">On Dt</td>
                        <td>2.02</td>
                        <td>2.11</td>
                        <td>0.00</td>
                        <td>2.57</td>
                        <td>2.35</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>1.99</td>
                        <td>2.04</td>
                        <td>0.00</td>
                        <td>2.59</td>
                        <td>2.35</td>
                    </tr>

                    <tr>
                        <td class="label">Production Rate/month</td>
                        <td></td>
                        <td>36683</td>
                        <td>58556</td>
                        <td>0</td>
                        <td>126928</td>
                        <td>222167</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">NC Rate (kg/thm)</td>
                        <td class="sub-label">On Dt</td>
                        <td>52.7</td>
                        <td>74.4</td>
                        <td>0</td>
                        <td>18.6</td>
                        <td>39.4</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>53.1</td>
                        <td>72.9</td>
                        <td>0</td>
                        <td>21.9</td>
                        <td>40.5</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Coke Rate</td>
                        <td class="sub-label">On Dt</td>
                        <td>469</td>
                        <td>458</td>
                        <td>0</td>
                        <td>339</td>
                        <td>393</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>471</td>
                        <td>490</td>
                        <td>0</td>
                        <td>352</td>
                        <td>408</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Coal Rate (kg/thm)</td>
                        <td class="sub-label">On Dt</td>
                        <td>0</td>
                        <td>123</td>
                        <td>0</td>
                        <td>178</td>
                        <td>133</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>0</td>
                        <td>87</td>
                        <td>0</td>
                        <td>168</td>
                        <td>119</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Tar Rate (kg/thm)</td>
                        <td class="sub-label">On Dt</td>
                        <td>45.8</td>
                        <td>0</td>
                        <td>0</td>
                        <td>0</td>
                        <td>7.6</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>39.3</td>
                        <td>0</td>
                        <td>0</td>
                        <td>0</td>
                        <td>6.5</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Oil Rate (kg/thm)</td>
                        <td class="sub-label">On Dt</td>
                        <td>0.00</td>
                        <td>0.00</td>
                        <td>0.00</td>
                        <td>0.00</td>
                        <td>0.00</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>0.00</td>
                        <td>0.00</td>
                        <td>0.00</td>
                        <td>0.00</td>
                        <td>0.00</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Fuel Rate (kg/thm)</td>
                        <td class="sub-label">On Dt</td>
                        <td>515</td>
                        <td>581</td>
                        <td>0</td>
                        <td>516</td>
                        <td>534</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>510</td>
                        <td>577</td>
                        <td>0</td>
                        <td>520</td>
                        <td>533</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Asrf (kg/thm)</td>
                        <td class="sub-label">On Dt</td>
                        <td>0</td>
                        <td>0.0</td>
                        <td>0</td>
                        <td>0</td>
                        <td>0.0</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>0</td>
                        <td>0.1</td>
                        <td>0</td>
                        <td>0</td>
                        <td>0.0</td>
                    </tr>

                    <tr>
                        <td class="label">Ore/Coke</td>
                        <td class="sub-label">On Dt</td>
                        <td>3.57</td>
                        <td>3.50</td>
                        <td>0</td>
                        <td>4.54</td>
                        <td>2.90</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Sinter, %</td>
                        <td class="sub-label">6am On Dt</td>
                        <td>46.0</td>
                        <td>46.8</td>
                        <td>0</td>
                        <td>48.1</td>
                        <td>47.40</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>43.3</td>
                        <td>42.2</td>
                        <td>0.0</td>
                        <td>44.1</td>
                        <td>43.5</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Pellet, %</td>
                        <td class="sub-label">On Dt</td>
                        <td>44.5</td>
                        <td>48.0</td>
                        <td>0</td>
                        <td>45.8</td>
                        <td>46.2</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>44.87</td>
                        <td>49.8</td>
                        <td>0</td>
                        <td>45.4</td>
                        <td>46.5</td>
                    </tr>

                    <tr>
                        <td class="label" rowspan="2">Pooled Iron Metallic Charge</td>
                        <td class="sub-label">On Dt</td>
                        <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
                    </tr>
                    <tr>
                        <td class="sub-label">To Dt</td>
                        <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- RIGHT TABLE: DISTRIBUTION AND CONSUMPTION -->
        <div class="report-right">
            <table class="report-table">
                <colgroup>
                    <col style="width: 54%">
                    <col style="width: 23%">
                    <col style="width: 23%">
                </colgroup>

                <thead>
                    <tr>
                        <th></th>
                        <th>ON Date</th>
                        <th>TO Date</th>
                    </tr>
                </thead>

                <tbody>
                    <tr>
                        <td class="label">E BF</td>
                        <td>33500</td>
                        <td>1039</td>
                    </tr>
                    <tr>
                        <td class="label">Operation</td>
                        <td>118.8</td>
                        <td>%</td>
                    </tr>

                    <tr>
                        <td colspan="3" class="section-title">
                            Distribution of HM, tons
                        </td>
                    </tr>
                    <tr><td>LD 1</td><td>0</td><td>55063</td></tr>
                    <tr><td>LD 2</td><td>0</td><td>937</td></tr>
                    <tr><td>LD 3</td><td>0</td><td>1155</td></tr>
                    <tr><td>MRD TP</td><td>0</td><td>0</td></tr>
                    <tr class="fw-bold"><td>Total</td><td>0</td><td>57155</td></tr>

                    <tr>
                        <td colspan="3" class="section-title">
                            Slag Granulation, tons
                        </td>
                    </tr>
                    <tr><td class="label">Slag Generation E-fce</td><td>0</td><td>0</td></tr>
                    <tr><td>C-fce</td><td>865</td><td>7339</td></tr>
                    <tr><td>D-fce</td><td>0</td><td>0</td></tr>
                    <tr><td>F-fce</td><td>1662</td><td>14184</td></tr>
                    <tr><td class="label">Slag not Granulated E-fce</td><td>275</td><td>2180</td></tr>
                    <tr><td>C-fce</td><td>0</td><td>0</td></tr>
                    <tr><td>D-fce</td><td>0</td><td>0</td></tr>
                    <tr><td>F-fce</td><td>0</td><td>320</td></tr>

                    <tr>
                        <td colspan="3" class="section-title">
                            Hot metal ladles
                        </td>
                    </tr>
                    <tr><td class="label">No. of Torpedo</td><td>35.00</td><td>293.00</td></tr>
                    <tr><td>HM, tons/TPL</td><td>0</td><td>196</td></tr>

                    <tr>
                        <td colspan="3" class="section-title">
                            High Line Unloading
                        </td>
                    </tr>
                    <tr><td>No. of Wagons</td><td></td><td></td></tr>
                    <tr><td>Stock Coke, t</td><td>0</td><td>0</td></tr>
                    <tr><td>Nut Coke, t</td><td>307</td><td>2836</td></tr>
                    <tr><td>Imp. Coke</td><td></td><td></td></tr>

                    <tr>
                        <td colspan="3" class="section-title">
                            Raw Materials Consumption, tons
                        </td>
                    </tr>
                    <tr><td>Nut Coke</td><td>283</td><td>2610</td></tr>
                    <tr><td>Scrap</td><td>62</td><td>531</td></tr>
                    <tr><td>Sinter</td><td>5623</td><td>45046</td></tr>
                    <tr><td>Total Coke</td><td>2544</td><td>23697</td></tr>
                    <tr><td>LRP Ore</td><td>191</td><td>5446</td></tr>
                </tbody>
            </table>
        </div>

    </div>
</div>