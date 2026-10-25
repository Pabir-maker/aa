<div class="modal fade" id="CompareChart" tabindex="-1" role="dialog"
     aria-labelledby="mTitle2" aria-hidden="true">

    <div class="modal-dialog compare-modal-dialog" role="document">

        <div class="modal-content compare-modal-content">

            <!-- Modal Header -->
            <div class="modal-header compare-modal-header">

                <button type="button" id="modalCloseBtn"
                        class="close compare-close"
                        data-dismiss="modal"
                        aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                </button>

                <h4 class="modal-title compare-modal-title" id="mTitle2">
                    Destination-wise Comparison Report
                </h4>

                <!-- Filters -->
                <div class="compare-filter-row">

                    <div class="compare-filter-item">
                        <label for="selectTF">Timeframe:</label>

                        <select id="selectTF"
                                class="form-control"
                                onchange="TFChange()">
                            <option value="30" selected>30 Days</option>
                            <option value="60">60 Days</option>
                            <option value="90">90 Days</option>
                        </select>
                    </div>

                    <div class="compare-filter-item">
                        <label for="tbStartDate">From:</label>

                        <input type="text"
                               readonly
                               id="tbStartDate"
                               class="form-control"
                               autocomplete="off">
                    </div>

                    <div class="compare-filter-item">
                        <label for="tbEndDate">To:</label>

                        <input type="text"
                               readonly
                               id="tbEndDate"
                               class="form-control"
                               autocomplete="off">
                    </div>

                </div>

            </div>

            <!-- Modal Body -->
            <div class="modal-body compare-modal-body" id="mBody2">

                <!-- Chart Tabs -->
                <div class="compare-tabs">
                    <button type="button"
                            class="tablinks active"
                            onclick="openPlots(event, 'ViolinPlots')"
                            id="defaultOpen">
                        Violin Plot
                    </button>

                    <button type="button"
                            class="tablinks"
                            onclick="openPlots(event, 'LinePlots')">
                        Trend Plot
                    </button>
                </div>

                <!-- Violin Chart -->
                <div id="ViolinPlots" class="tabcontent">

                    <div class="compare-chart-wrapper">
                        <div id="CompareViolinPlots"
                             class="compare-chart">
                        </div>
                    </div>

                </div>

                <!-- Trend Chart -->
                <div id="LinePlots" class="tabcontent">

                    <div class="compare-chart-wrapper">
                        <div id="CompareLinePlots"
                             class="compare-chart">
                        </div>
                    </div>

                </div>

            </div>

        </div>

    </div>

</div>
/* Modal dialog */
#CompareChart .compare-modal-dialog {
    width: 95%;
    max-width: 1600px;
    margin: 20px auto;
}

/* Modal content */
#CompareChart .compare-modal-content {
    width: 100%;
    border: none;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.2);
}

/* Header */
#CompareChart .compare-modal-header {
    position: relative;
    padding: 18px 20px;
    background: #f8fafc;
    border-bottom: 1px solid #dbe3ec;
}

/* Title */
#CompareChart .compare-modal-title {
    padding: 0 35px;
    margin: 0 0 20px;
    text-align: center;
    font-family: Century, Arial, sans-serif;
    font-size: clamp(20px, 2.5vw, 30px);
    font-weight: bold;
    color: #5B5B60;
    line-height: 1.4;
}

/* Close button */
#CompareChart .compare-close {
    position: absolute;
    top: 12px;
    right: 18px;
    z-index: 10;
    font-size: 30px;
}

/* Filter layout */
#CompareChart .compare-filter-row {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 15px;
    width: 100%;
}

/* Individual filters */
#CompareChart .compare-filter-item {
    min-width: 0;
}

#CompareChart .compare-filter-item label {
    display: block;
    margin-bottom: 6px;
    font-size: 15px;
    font-weight: 600;
    color: #1d4ed8;
}

#CompareChart .compare-filter-item .form-control {
    width: 100%;
    height: 38px;
    border: 1px solid #cbd5e1;
    border-radius: 5px;
    background: #ffffff;
    font-size: 14px;
    box-sizing: border-box;
}

/* Modal body */
#CompareChart .compare-modal-body {
    padding: 15px;
    background: #ffffff;
    overflow-x: hidden;
}

/* Tabs */
#CompareChart .compare-tabs {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 15px;
    border-bottom: 2px solid #e2e8f0;
}

#CompareChart .compare-tabs .tablinks {
    padding: 10px 20px;
    border: none;
    border-radius: 6px 6px 0 0;
    background: #e9eef5;
    color: #334155;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.2s ease, color 0.2s ease;
}

#CompareChart .compare-tabs .tablinks:hover {
    background: #dbeafe;
    color: #1d4ed8;
}

#CompareChart .compare-tabs .tablinks.active {
    background: #1d4ed8;
    color: #ffffff;
}

/* Chart wrapper */
#CompareChart .compare-chart-wrapper {
    width: 100%;
    max-width: 100%;
    min-width: 0;
    overflow: hidden;
    box-sizing: border-box;
}

/* Chart containers */
#CompareChart .compare-chart {
    position: relative;
    width: 100%;
    max-width: 100%;
    min-width: 0;
    min-height: 350px;
    box-sizing: border-box;
}

/* Prevent child SVG/canvas from exceeding the screen */
#CompareChart .compare-chart svg,
#CompareChart .compare-chart canvas {
    max-width: 100%;
}

/* Tablet */
@media (max-width: 991px) {
    #CompareChart .compare-modal-dialog {
        width: 96%;
        margin: 15px auto;
    }

    #CompareChart .compare-modal-header {
        padding: 15px;
    }

    #CompareChart .compare-modal-body {
        padding: 12px;
    }

    #CompareChart .compare-chart {
        min-height: 320px;
    }
}

/* Mobile */
@media (max-width: 576px) {
    #CompareChart .compare-modal-dialog {
        width: auto;
        margin: 8px;
    }

    #CompareChart .compare-modal-content {
        border-radius: 7px;
    }

    #CompareChart .compare-modal-header {
        padding: 15px 12px;
    }

    #CompareChart .compare-modal-title {
        padding: 0 25px;
        margin-bottom: 15px;
        font-size: 20px;
    }

    #CompareChart .compare-close {
        top: 8px;
        right: 10px;
        font-size: 26px;
    }

    #CompareChart .compare-filter-row {
        grid-template-columns: minmax(0, 1fr);
        gap: 10px;
    }

    #CompareChart .compare-filter-item label {
        margin-bottom: 4px;
        font-size: 14px;
    }

    #CompareChart .compare-filter-item .form-control {
        height: 36px;
        font-size: 14px;
    }

    #CompareChart .compare-modal-body {
        padding: 10px;
    }

    #CompareChart .compare-tabs {
        gap: 5px;
    }

    #CompareChart .compare-tabs .tablinks {
        flex: 1;
        padding: 10px 8px;
        font-size: 13px;
    }

    #CompareChart .compare-chart {
        min-height: 280px;
    }
}

/* Small mobile screens */
@media (max-width: 360px) {
    #CompareChart .compare-modal-title {
        font-size: 18px;
    }

    #CompareChart .compare-chart {
        min-height: 250px;
    }
}
