<div class="container-fluid daily-mis-container">

    <div class="daily-mis-header">

        <!-- Left Section: Date -->
        <div class="mis-date-section mis-date-left">

            <div class="mis-date-label">Date:</div>

            <a id="date-daily1"
               class="drpickr btn btn-o btn-primary mis-date-btn">
                <i class="fa fa-calendar"></i>
                <label class="value" id="currDate-value"></label>
            </a>

            <div class="mis-plant-label">
                (TSJ &amp; TSK &amp; TSM)
            </div>

        </div>

        <!-- Center Section: Title -->
        <div class="mis-title-section">
            <h2>Daily MIS, Sinter Plants</h2>
        </div>

        <!-- Right Section: Previous Date and Excel -->
        <div class="mis-date-section mis-date-right">

            <a id="date-daily2"
               class="drpickr btn btn-o btn-primary mis-date-btn">
                <i class="fa fa-calendar"></i>
                <label class="value" id="prevDate"></label>
            </a>

            <div class="mis-right-bottom">

                <span class="mis-plant-label">
                    (TSG, TSMD)
                </span>

                <i id="btnDowonloadToExcel"
                   class="fa fa-file-excel-o mis-excel-icon"
                   data-toggle="tooltip"
                   title="Download To Excel!"
                   role="button"
                   aria-label="Download to Excel"
                   tabindex="0"></i>

                <div id="tableExcel"
                     class="hidden full-width"
                     style="overflow:auto;height:280px;">
                </div>

            </div>

        </div>

.daily-mis-container {
    width: 100%;
    padding: 10px 15px;
    box-sizing: border-box;
}

.daily-mis-header {
    display: grid;
    grid-template-columns: minmax(160px, 1fr)
                           minmax(250px, 2fr)
                           minmax(180px, 1fr);
    align-items: center;
    gap: 15px;
    width: 100%;
    min-height: 110px;
    padding: 15px;
    background: #ffffff;
    border: 1px solid #d5dce5;
    border-radius: 10px;
    box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
    box-sizing: border-box;
}

/* Left and right date sections */
.mis-date-section {
    min-width: 0;
    font-family: Century, Arial, sans-serif;
    font-weight: bold;
    color: blue;
}

.mis-date-left {
    text-align: left;
}

.mis-date-right {
    text-align: right;
}

/* Date picker buttons */
.mis-date-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 5px;
    max-width: 100%;
    margin-top: 5px;
    padding: 6px 10px;
    font-size: 16px;
    white-space: normal;
}

.mis-date-btn .value {
    margin: 0;
    font-size: 16px;
    color: inherit;
}

/* Main heading */
.mis-title-section {
    text-align: center;
    min-width: 0;
}

.mis-title-section h2 {
    margin: 0;
    color: brown;
    font-family: Century, Arial, sans-serif;
    font-size: clamp(20px, 2.2vw, 30px);
    font-weight: bold;
    line-height: 1.35;
}

/* Plant labels */
.mis-plant-label {
    display: block;
    margin-top: 8px;
    font-family: Arial, sans-serif;
    font-size: 13px;
    font-weight: normal;
    color: #475569;
}

.mis-right-bottom {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    flex-wrap: wrap;
    gap: 12px;
    margin-top: 8px;
}

.mis-right-bottom .mis-plant-label {
    margin-top: 0;
}

/* Excel icon */
.mis-excel-icon {
    display: inline-block;
    color: #198754;
    font-size: 28px;
    cursor: pointer;
    transition: transform 0.2s ease, color 0.2s ease;
}

.mis-excel-icon:hover {
    color: #146c43;
    transform: scale(1.1);
}

.mis-excel-icon:focus {
    outline: 2px solid #198754;
    outline-offset: 4px;
}

/* Tablet */
@media (max-width: 991px) {
    .daily-mis-header {
        grid-template-columns: 1fr 1fr;
        gap: 15px;
    }

    .mis-title-section {
        grid-column: 1 / -1;
        grid-row: 1;
    }

    .mis-date-left {
        grid-column: 1;
        grid-row: 2;
    }

    .mis-date-right {
        grid-column: 2;
        grid-row: 2;
    }

    .mis-title-section h2 {
        font-size: 25px;
    }
}

/* Mobile */
@media (max-width: 576px) {
    .daily-mis-container {
        padding: 6px;
    }

    .daily-mis-header {
        grid-template-columns: minmax(0, 1fr);
        gap: 12px;
        padding: 12px;
        min-height: auto;
    }

    .mis-title-section {
        grid-column: 1;
        grid-row: 1;
        padding-bottom: 10px;
        border-bottom: 1px solid #e2e8f0;
    }

    .mis-title-section h2 {
        font-size: 22px;
    }

    .mis-date-left {
        grid-column: 1;
        grid-row: 2;
        text-align: center;
    }

    .mis-date-right {
        grid-column: 1;
        grid-row: 3;
        text-align: center;
        padding-top: 10px;
        border-top: 1px solid #e2e8f0;
    }

    .mis-date-btn {
        font-size: 14px;
    }

    .mis-date-btn .value {
        font-size: 14px;
    }

    .mis-plant-label {
        font-size: 12px;
    }

    .mis-right-bottom {
        justify-content: center;
        gap: 15px;
    }

    .mis-excel-icon {
        font-size: 25px;
    }
}
    </div>

</div>
