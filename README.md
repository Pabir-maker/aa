<style>
    * {
        box-sizing: border-box;
    }

    body {
        margin: 0;
        background: #f1f5f9;
        font-family: Arial, sans-serif;
        color: #1e293b;
    }

    .mis-container {
        width: 100%;
        max-width: 1800px;
        margin: auto;
        padding: 16px;
    }

    /* Header */
    .mis-header {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-between;
        gap: 14px;
        padding: 20px;
        background: #ffffff;
        border: 1px solid #e2e8f0;
        border-radius: 12px;
        margin-bottom: 18px;
        box-shadow: 0 4px 15px rgba(15, 23, 42, 0.06);
    }

    .mis-header h2 {
        font-size: clamp(20px, 2vw, 28px);
        margin: 0;
        color: #17365d;
        font-weight: 700;
    }

    .date-box {
        padding: 9px 12px;
        border: 1px solid #cbd5e1;
        border-radius: 7px;
        background: #f8fafc;
        color: #334155;
        max-width: 100%;
        outline: none;
    }

    .date-box:focus {
        border-color: #2563eb;
        box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.12);
    }

    /* Horizontal scrolling wrapper */
    .table-container {
        position: relative;
        width: 100%;
        max-width: 100%;
        overflow-x: auto;
        overflow-y: auto;
        max-height: 75vh;
        background: #ffffff;
        border: 1px solid #dbe3ed;
        border-radius: 12px;
        box-shadow: 0 4px 18px rgba(15, 23, 42, 0.07);
        -webkit-overflow-scrolling: touch;
        overscroll-behavior-x: contain;
        scrollbar-width: thin;
        scrollbar-color: #94a3b8 #e2e8f0;
    }

    /* Visible horizontal scrollbar */
    .table-container::-webkit-scrollbar {
        height: 10px;
        width: 10px;
    }

    .table-container::-webkit-scrollbar-track {
        background: #e2e8f0;
        border-radius: 10px;
    }

    .table-container::-webkit-scrollbar-thumb {
        background: #94a3b8;
        border: 2px solid #e2e8f0;
        border-radius: 10px;
    }

    .table-container::-webkit-scrollbar-thumb:hover {
        background: #64748b;
    }

    /* MIS table */
    .mis-table {
        width: max-content;
        min-width: 1150px;
        border-collapse: separate;
        border-spacing: 0;
        font-size: 13px;
        background: #ffffff;
    }

    .mis-table th,
    .mis-table td {
        padding: 10px 12px;
        text-align: center;
        white-space: nowrap;
        border-right: 1px solid #dbe3ed;
        border-bottom: 1px solid #dbe3ed;
    }

    /* Sticky table header */
    .mis-table thead th {
        position: sticky;
        top: 0;
        z-index: 3;
        background: #dce8f5;
        color: #17365d;
        font-weight: 700;
        box-shadow: 0 1px 0 #b8c4d1;
    }

    /* Alternate rows */
    .mis-table tbody tr:nth-child(even) {
        background: #f5f8fc;
    }

    .mis-table tbody tr:nth-child(odd) {
        background: #ffffff;
    }

    .mis-table tbody tr:hover td {
        background: #e8f2ff;
    }

    /* Fixed-width first column */
    .mis-table .parameter {
        position: sticky;
        left: 0;
        z-index: 2;
        width: 150px;
        min-width: 150px;
        max-width: 150px;
        white-space: normal;
        overflow-wrap: anywhere;
        word-break: normal;
        text-align: left;
        font-weight: 600;
        color: #17365d;
        background: #eaf0f6;
        box-shadow: 2px 0 5px rgba(15, 23, 42, 0.06);
    }

    /* Top-left cell stays above all other cells */
    .mis-table thead .parameter {
        z-index: 5;
        background: #cbdced;
    }

    .mis-table tbody tr:hover .parameter {
        background: #dbeafe;
    }

    /* Clean table corners */
    .mis-table thead tr:first-child th {
        border-top: 0;
    }

    .mis-table th:first-child,
    .mis-table td:first-child {
        border-left: 0;
    }

    .mis-table tbody tr:last-child td {
        border-bottom: 0;
    }

    /* Mobile responsive */
    @@media (max-width: 768px) {
        .mis-container {
            padding: 8px;
        }

        .mis-header {
            padding: 14px;
            border-radius: 9px;
            gap: 10px;
        }

        .mis-header h2 {
            font-size: 19px;
        }

        .date-box {
            font-size: 12px;
            padding: 8px;
        }

        .table-container {
            border-radius: 8px;
            max-height: 70vh;
        }

        .mis-table {
            min-width: 1100px;
            font-size: 11px;
        }

        .mis-table th,
        .mis-table td {
            padding: 8px 9px;
        }

        .mis-table .parameter {
            width: 125px;
            min-width: 125px;
            max-width: 125px;
        }

        .table-container::-webkit-scrollbar {
            height: 8px;
        }
    }

    /* Print layout */
    @@media print {
        .mis-container {
            max-width: none;
            padding: 0;
        }

        .mis-header {
            box-shadow: none;
        }

        .table-container {
            overflow: visible;
            max-height: none;
            border: none;
            box-shadow: none;
        }

        .mis-table {
            width: 100%;
            min-width: 0;
            font-size: 8px;
            border-collapse: collapse;
        }

        .mis-table th,
        .mis-table td {
            position: static;
            white-space: normal;
            overflow-wrap: anywhere;
            padding: 3px;
            box-shadow: none;
        }

        .mis-table .parameter {
            min-width: 0;
            max-width: none;
            width: auto;
        }
    }
</style>