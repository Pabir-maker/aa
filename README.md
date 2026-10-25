var table_body = '';

table_body += '<div class="plant-table-wrapper">';
table_body += '<div class="plant-table-scroll">';

table_body += '<table class="plant-responsive-table">';

table_body += '<thead>';

/* Plant group headings */
table_body += '<tr>';

table_body += '<th></th>';
table_body += '<th colspan="4">TSL, Jamshedpur</th>';
table_body += '<th>TSK</th>';
table_body += '<th colspan="3">TSM</th>';
table_body += '<th>NINL</th>';
table_body += '<th>TSG</th>';
table_body += '<th>TSMD</th>';

table_body += '</tr>';

/* Subheadings */
table_body += '<tr>';

table_body += '<th>Parameters</th>';

table_body += '<th>SP#1</th>';
table_body += '<th>SP#2</th>';
table_body += '<th>SP#3</th>';
table_body += '<th>SP#4</th>';

table_body += '<th>SP</th>';

table_body += '<th>SP#1</th>';
table_body += '<th>SP#2</th>';
table_body += '<th>SP#3</th>';

table_body += '<th>SP</th>';
table_body += '<th>SP</th>';
table_body += '<th>SP</th>';

table_body += '</tr>';

table_body += '</thead>';
table_body += '<tbody>';

/* Your existing data loop starts here */
for (var i = 0; i < jData.length; i++) {

    table_body += '<tr>';

    table_body += '<td class="parameter">';
    table_body += '<a href="javascript:void(0)" ';
    table_body += 'onclick="ShowComparision(';
    table_body += "'" + param[i] + "'";
    table_body += ')">';
    table_body += param[i];
    table_body += '</a>';
    table_body += '</td>';

    /* TSL SP#1 */
    table_body += '<td>';

    if (tsj_SP1[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant1', '" + param[i] + "'";
        table_body += ')">';
        table_body += tsj_SP1[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* TSL SP#2 */
    table_body += '<td>';

    if (tsj_SP2[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant2', '" + param[i] + "'";
        table_body += ')">';
        table_body += tsj_SP2[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* TSL SP#3 */
    table_body += '<td>';

    if (tsj_SP3[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant3', '" + param[i] + "'";
        table_body += ')">';
        table_body += tsj_SP3[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* TSL SP#4 */
    table_body += '<td>';

    if (tsj_SP4[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant4', '" + param[i] + "'";
        table_body += ')">';
        table_body += tsj_SP4[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* TSK */
    table_body += '<td>';

    if (tsk_SP[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant5', '" + param[i] + "'";
        table_body += ')">';
        table_body += tsk_SP[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* TSM SP#1 */
    table_body += '<td>';

    if (tsbsl_SP1[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant6', '" + param[i] + "'";
        table_body += ')">';
        table_body += tsbsl_SP1[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* TSM SP#2 */
    table_body += '<td>';

    if (tsbsl_SP2[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant7', '" + param[i] + "'";
        table_body += ')">';
        table_body += tsbsl_SP2[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* TSM SP#3 */
    table_body += '<td>';

    if (tsbsl_SP3[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant8', '" + param[i] + "'";
        table_body += ')">';
        table_body += tsbsl_SP3[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* NINL */
    table_body += '<td>';

    if (ninl_SP[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant11', '" + param[i] + "'";
        table_body += ')">';
        table_body += ninl_SP[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* TSG */
    table_body += '<td>';

    if (tslpl_SP[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant9', '" + param[i] + "'";
        table_body += ')">';
        table_body += tslpl_SP[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    /* TSMD */
    table_body += '<td>';

    if (tsmd_Sp[i] != null) {
        table_body += '<a href="javascript:void(0)" ';
        table_body += 'onclick="ShowGraph(';
        table_body += "'@plant10', '" + param[i] + "'";
        table_body += ')">';
        table_body += tsmd_Sp[i];
        table_body += '</a>';
    }

    table_body += '</td>';

    table_body += '</tr>';
}

table_body += '</tbody>';
table_body += '</table>';

table_body += '</div>';
table_body += '</div>';

/* Display the responsive table */
$('#tableDiv').html(table_body);
$('#tableExcel').html(table_body);
