 var table_body = '<table width="100%"  border="1"  class="mis-table"  >';
                       table_body += '<tbody>';
                       table_body += '<tr>';
                       table_body += '<td class="parameter" colspan="1"  style="height:40px;border:2px solid black;width:300px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family: Arial;"></td>';
                       table_body += '<td colspan="4"  style="border:2px solid black;width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family: Arial;" > TSL, Jamshedpur</td>';
                       table_body += '<td td style="border:2px solid black;width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">TSK</td>';
                       table_body += '<td colspan="3" td style="border:2px solid black;width:100px;text-align:center; align:center;font-size:15px;font-weight: bold;font-family:Arial;">TSM</td> ';
                       table_body += '<td colspan="1" td style="border:2px solid black;width:100px;text-align:center; align:center;font-size:15px;font-weight: bold;font-family:Arial;">NINL</td> ';
                       table_body += '<td td style="border:2px solid black;width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">TSG</td>';
                       table_body += '<td td style="border:2px solid black;width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">TSMD</td>';
                       table_body += '</tr>';                       //
                       table_body += '<tr style="position:sticky;top:0;border:2px solid black;">';
                       table_body += '<td style="top:0;height:40px;border:2px solid black; width:200px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">Parameters</td>';                      //table_body += '<td style="top:0;border:2px solid black; background: linear-gradient(to bottom, #33ccff 0%, #55ffcc 20%, #ffffcc 80%);width:50px;text-align:center; align:center;font-size:20px;font-weight: bold;font-family:Arial;">Units</td>';                       //

                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP#1</td>';
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP#2</td>';
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP#3</td>';
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP#4</td>';                      //
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP</td>';
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP#1</td>';
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP#2</td>';
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP#3</td>';
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP</td>';
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP</td>';
                       table_body += '<td style="top:0;border:2px solid black; width:100px;text-align:center; align:center;font-size:15px;font-weight:bold;font-family:Arial;">SP</td>';
                       table_body += '</tr>';
                       
                       for (var i = 0; i < jData.length; i++){                           
                           table_body += '<tr style="border:2px solid black;">';
                           table_body += '<td class="parameter" style="height:40px;color:black;text-align:left; align:center; font-size:14px;font-family:Arial; font-weight:bold;"><a href=\"javascript:ShowComparision(\'' + param[i] + '\')\">' + param[i] + '</a></td>';

                           if (tsj_SP1[i] != null) {
                               //
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant1\', \'' + param[i] + '\')">' + tsj_SP1[i] + '</a></td>';
                           }
                           else {
                               //
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }

                           if (tsj_SP2[i] != null) {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant2\', \'' + param[i] + '\')">' + tsj_SP2[i] + '</a></td>';
                           }
                           else {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }
                           if (tsj_SP3[i] != null) {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant3\', \'' + param[i] + '\')">' + tsj_SP3[i] + '</a></td>';
                           }
                           else {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }

                           if (tsj_SP4[i] != null)
                           {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant4\', \'' + param[i] + '\')">' + tsj_SP4[i] + '</a></td>';
                           }
                           else {
                               table_body += '<td style=color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }


                           if (tsk_SP[i] != null) {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant5\', \'' + param[i] + '\')">' + tsk_SP[i] + '</a></td>';
                           }
                           else {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }



                           if (tsbsl_SP1[i] != null) {

                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant6\', \'' + param[i] + '\')">' + tsbsl_SP1[i] + '</a></td>';
                           }
                           else {

                               table_body += '<td style=color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }

                           if (tsbsl_SP2[i] != null) {

                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant7\', \'' + param[i] + '\')">' + tsbsl_SP2[i] + '</a></td>';
                           }
                           else {
                               table_body += '<td style=color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }

                           if (tsbsl_SP3[i] != null) {

                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant8\', \'' + param[i] + '\')">' + tsbsl_SP3[i] + '</a></td>';
                           }

                           else {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';

                           }
                           if (ninl_SP[i] != null) {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant11\', \'' + param[i] + '\')">' + ninl_SP[i] + '</a></td>';
                           }
                           else {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }
                           if (tslpl_SP[i] != null) {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant9\', \'' + param[i] + '\')">' + tslpl_SP[i] + '</a></td>';
                           }
                           else {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }
                           if (tsmd_Sp[i] != null) {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;"><a href="javascript:ShowGraph(\'@plant10\', \'' + param[i] + '\')">' + tsmd_Sp[i] + '</a></td>';
                           }
                           else {
                               table_body += '<td style="color:black;text-align:center;font-size:14px;font-weight: bold;font-family: Arial;">' + "" + '</td>';
                           }

                           table_body += ' </tr>';
                       }

                       table_body += '</tbody>';

                       table_body += '</table>';

                       $('#tableDiv').html(table_body);
                       $('#tableExcel').html(table_body);

                   }); //  // $_Post closed

           } // Main Function Closed
