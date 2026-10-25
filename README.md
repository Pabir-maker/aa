/* Main table container */
.plant-table-wrapper {
    width: 100%;
    max-width: 100%;
    margin: 0 auto;
    background: #ffffff;
    border: 1px solid #cbd5e1;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

/* Horizontal and vertical scrolling */
.plant-table-scroll {
    width: 100%;
    max-height: 75vh;
    overflow: auto;
    -webkit-overflow-scrolling: touch;
    overscroll-behavior: contain;
}

/* Table design */
.plant-responsive-table {
    width: 100%;
    min-width: 1100px;
    margin: 0;
    border-collapse: separate;
    border-spacing: 0;
    table-layout: fixed;
    font-family: Arial, sans-serif;
    font-size: 13px;
}

/* Column widths */
.plant-responsive-table th:first-child,
.plant-responsive-table td:first-child {
    width: 230px;
    min-width: 230px;
}

/* Table cells */
.plant-responsive-table th,
.plant-responsive-table td {
    padding: 9px 8px;
    border-right: 1px solid #d5dce5;
    border-bottom: 1px solid #d5dce5;
    text-align: center;
    vertical-align: middle;
    white-space: nowrap;
    box-sizing: border-box;
}

/* Sticky plant heading */
.plant-responsive-table thead tr:first-child th {
    position: sticky;
    top: 0;
    z-index: 5;
    height: 40px;
    background: #164e63;
    color: #ffffff;
    font-size: 14px;
    font-weight: bold;
}

/* Sticky SP heading */
.plant-responsive-table thead tr:nth-child(2) th {
    position: sticky;
    top: 40px;
    z-index: 5;
    height: 38px;
    background: #dbeafe;
    color: #1e3a8a;
    font-weight: bold;
}

/* Parameter heading */
.plant-responsive-table thead th:first-child {
    background: #1e3a5f;
    color: #ffffff;
}

/* Parameter column remains visible during horizontal scrolling */
.plant-responsive-table th:first-child,
.plant-responsive-table td:first-child {
    position: sticky;
    left: 0;
    z-index: 3;
    background: #f1f5f9;
    text-align: left;
}

/* Keep the top-left header above other sticky cells */
.plant-responsive-table thead tr:first-child th:first-child {
    z-index: 8;
}

.plant-responsive-table thead tr:nth-child(2) th:first-child {
    z-index: 8;
}

/* Table body */
.plant-responsive-table tbody td {
    height: 36px;
    color: #263445;
    font-size: 13px;
}

.plant-responsive-table tbody tr:nth-child(even) td {
    background: #f8fafc;
}

.plant-responsive-table tbody tr:nth-child(odd) td {
    background: #ffffff;
}

/* Keep the first column background opaque */
.plant-responsive-table tbody tr:nth-child(even) td:first-child {
    background: #eef2f7;
}

.plant-responsive-table tbody tr:nth-child(odd) td:first-child {
    background: #f8fafc;
}

/* Row hover effect */
.plant-responsive-table tbody tr:hover td {
    background: #dff6ff;
}

.plant-responsive-table tbody tr:hover td:first-child {
    background: #c9edfa;
}

/* Parameter links */
.plant-responsive-table td:first-child a {
    display: block;
    color: #075985;
    font-weight: bold;
    text-decoration: none;
    white-space: normal;
}

.plant-responsive-table td:first-child a:hover {
    color: #0284c7;
    text-decoration: underline;
}

/* Graph links */
.plant-responsive-table td a:not(:first-child) {
    color: #075985;
    text-decoration: none;
}

/* Make clickable data obvious */
.plant-responsive-table tbody td:not(:first-child) a {
    display: inline-block;
    padding: 2px 4px;
    color: #075985;
    font-weight: 600;
    text-decoration: none;
}

.plant-responsive-table tbody td:not(:first-child) a:hover {
    color: #0369a1;
    text-decoration: underline;
}

/* Tablet */
@media (max-width: 991px) {
    .plant-table-scroll {
        max-height: 70vh;
    }

    .plant-responsive-table {
        font-size: 12px;
    }

    .plant-responsive-table th,
    .plant-responsive-table td {
        padding: 8px 6px;
    }
}

/* Mobile */
@media (max-width: 576px) {
    .plant-table-wrapper {
        border-radius: 5px;
    }

    .plant-table-scroll {
        max-height: 65vh;
    }

    .plant-responsive-table {
        min-width: 1050px;
        font-size: 12px;
    }

    .plant-responsive-table th,
    .plant-responsive-table td {
        padding: 7px 6px;
    }

    .plant-responsive-table tbody td {
        height: 34px;
    }
}
