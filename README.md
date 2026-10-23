  <style>
        body {
            margin: 0; background: #f1f5f9;
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
                width: 150px;             /* Sets a strict target width */
    max-width: 150px;         /* Forces the column to respect the limit */
    white-space: normal;      /* Allows long names to wrap to the next line */
    word-break: break-word;   /* Safely breaks very long single words if needed */
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

        @@media (max-width: 768px) {
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

        @@media print {
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
