
@{
    ViewBag.Title = "Daily MIS - Sinter Plants";
}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport"
          content="width=device-width, initial-scale=1.0" />

    <title>Daily MIS - Sinter Plants</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
          rel="stylesheet" />

    <style>
        body {
            margin: 0;
            background: #f1f5f9;
            font-family: Arial, sans-serif;
        }

        .mis-container {
            width: 100%;
            max-width: 1800px;
            margin: auto;
            padding: 15px;
        }

        .mis-header {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            gap: 12px;
            padding: 16px;
            background: white;
            border-radius: 8px;
            margin-bottom: 15px;
            box-shadow: 0 2px 8px #00000012;
        }

        .mis-header h2 {
            font-size: clamp(18px, 2vw, 28px);
            margin: 0;
            color: #17365d;
        }

        .date-box {
            padding: 8px;
            border: 1px solid #cbd5e1;
            border-radius: 5px;
            max-width: 100%;
        }

        .table-container {
            width: 100%;
            overflow-x: auto;
            background: white;
            border-radius: 8px;
            -webkit-overflow-scrolling: touch;
        }

        .mis-table {
            width: 100%;
            min-width: 1150px;
            border-collapse: collapse;
            font-size: 13px;
        }

        .mis-table th,
        .mis-table td {
            border: 1px solid #b8c4d1;
            padding: 8px 6px;
            text-align: center;
            white-space: nowrap;
        }

        .mis-table thead th {
            background: #dce8f5;
            color: #17365d;
            font-weight: bold;
        }

        .mis-table tbody tr:nth-child(even) {
            background: #f3f7fb;
        }

        .mis-table tbody tr:hover {
            background: #dbeafe;
        }

        .mis-table .parameter {
            text-align: left;
            font-weight: 600;
            background: #eaf0f6;
            position: sticky;
            left: 0;
            z-index: 2;
        }

        .mis-table thead .parameter {
            z-index: 4;
            background: #cbdced;
        }

        .mis-table thead {
            position: sticky;
            top: 0;
            z-index: 3;
        }

        @media (max-width: 768px) {
            .mis-container {
                padding: 8px;
            }

            .mis-header {
                padding: 12px;
            }

            .mis-header h2 {
                font-size: 19px;
            }

            .mis-table {
                min-width: 1100px;
                font-size: 11px;
            }

            .mis-table th,
            .mis-table td {
                padding: 7px 5px;
            }

            .date-box {
                font-size: 12px;
            }
        }

        @media print {
            .table-container {
                overflow: visible;
            }

            .mis-table {
                min-width: 0;
                font-size: 8px;
            }

            .mis-table th,
            .mis-table td {
                white-space: normal;
                padding: 3px;
            }
        }
    </style>
</head>

<body>
<div class="mis-container">

    <div class="mis-header">
        <div>
            <small class="text-secondary">Process Technology Group</small>
            <h2>Daily MIS, Sinter Plants</h2>
        </div>

        <div class="d-flex flex-wrap gap-2 align-items-center">
            <input type="date" class="form-control date-box"
                   id="misDate" value="2026-10-20" />

            <button class="btn btn-primary"
                    onclick="window.print()">
                Print
            </button>
        </div>
    </div>

    <div class="table-container">
        <table class="mis-table">
            <thead>
                <tr>
                    <th class="parameter" rowspan="2">
                        Parameters
                    </th>
                    <th colspan="4">TSL, Jamshedpur</th>
                    <th colspan="1">TSK</th>
                    <th colspan="3">TSM</th>
                    <th colspan="1">NINL</th>
                    <th colspan="1">TSG</th>
                    <th colspan="1">TSMD</th>
                </tr>
                <tr>
                    <th>SP#1</th>
                    <th>SP#2</th>
                    <th>SP#3</th>
                    <th>SP#4</th>
                    <th>SP</th>
                    <th>SP#1</th>
                    <th>SP#2</th>
                    <th>SP#3</th>
                    <th>SP</th>
                    <th>SP</th>
                    <th>SP</th>
                </tr>
            </thead>

            <tbody>
                <tr>
                    <td class="parameter">Gross production (t/day)</td>
                    <td>0</td><td>7900</td><td>8120</td><td>8900</td>
                    <td>18642</td><td>4448</td><td>6298</td>
                    <td>6347</td><td>5600</td><td>424</td><td>2072</td>
                </tr>

                <tr>
                    <td class="parameter">Availability (%)</td>
                    <td>100</td><td>97.50</td><td>88.10</td><td>100</td>
                    <td>100</td><td>100</td><td>100</td>
                    <td>100</td><td>100</td><td>24.70</td><td>100</td>
                </tr>

                <tr>
                    <td class="parameter">Machine Speed (m/m)</td>
                    <td>0</td><td>2.30</td><td>1.73</td><td>2.36</td>
                    <td>4.21</td><td>1.43</td><td>1.62</td>
                    <td>1.63</td><td>2.14</td><td>1.01</td><td>1.07</td>
                </tr>

                <tr>
                    <td class="parameter">Carbon rate (kg/TSn)</td>
                    <td></td><td></td><td></td><td></td>
                    <td>56</td><td>56.70</td><td>57.80</td>
                    <td>59.10</td><td>53.20</td><td></td><td>53.01</td>
                </tr>

                <tr>
                    <td class="parameter">BTT SP1 (deg C)</td>
                    <td>331</td><td>390</td><td>439</td><td>426</td>
                    <td>396</td><td>244</td><td>382</td>
                    <td>374</td><td>370</td><td>111</td><td>317</td>
                </tr>

                <tr>
                    <td class="parameter">WGT SP1 (deg C)</td>
                    <td>0</td><td>158</td><td>164</td><td>159</td>
                    <td>150</td><td>115</td><td>153</td>
                    <td>149</td><td>171</td><td></td><td></td>
                </tr>

                <tr>
                    <td class="parameter">Product Sinter Temp (deg C)</td>
                    <td>110</td><td>44</td><td>39</td><td>0</td>
                    <td>45</td><td>49</td><td>50</td>
                    <td>60</td><td>52</td><td>45</td><td>69</td>
                </tr>

                <tr>
                    <td class="parameter">CaO (%)</td>
                    <td></td><td>12.70</td><td>13.30</td><td>11.60</td>
                    <td>13.20</td><td>11.20</td><td>10.20</td>
                    <td>10.20</td><td>10.31</td><td>11.50</td><td>12.76</td>
                </tr>

                <tr>
                    <td class="parameter">SiO2 (%)</td>
                    <td></td><td>5.29</td><td>5.28</td><td>5.27</td>
                    <td>5.29</td><td>4.73</td><td>4.63</td>
                    <td>4.70</td><td>5.30</td><td>4.95</td><td>4.99</td>
                </tr>

                <tr>
                    <td class="parameter">Al2O3 (%)</td>
                    <td></td><td>2.59</td><td>2.63</td><td>2.74</td>
                    <td>2.59</td><td>2.80</td><td>2.62</td>
                    <td>2.63</td><td>3.52</td><td>2.31</td><td>2.89</td>
                </tr>

                <tr>
                    <td class="parameter">FeO (%)</td>
                    <td></td><td>8.20</td><td>8.30</td><td>8.51</td>
                    <td>9.07</td><td>10.50</td><td>9.80</td>
                    <td>9.70</td><td>11.32</td><td>10.77</td><td>8.67</td>
                </tr>
            </tbody>
        </table>
    </div>

    <small class="text-secondary mt-2 d-block">
        Tip: On a phone, swipe left or right inside the table
        to see all plant columns.
    </small>

</div>
</body>
</html>
