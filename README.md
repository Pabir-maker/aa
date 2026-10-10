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
