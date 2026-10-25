<div class="modal" id="CompareChart" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document" style="width:95vw">
        <div class="modal-content">
            <div class="modal-header">
                <div class="container-fluid">
                    <div class="row">
                        <h5 class="modal-title" id="mTitle2" style="text-align: center; font-family:Century; font-weight:bold; font-size:30px; color:#5B5B60">Destination-wise Comparison Report</h5>
                        <button type="button" id="modalCloseBtn" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="row" style="margin-bottom:0px">
                        <div class="col-md-4 form-group">
                            <label for="selectTF" class="form-label" style="font-size:20px;color:blue">Timeframe:&nbsp;</label>
                            <select id="selectTF" style="width:150px" class="form-select" onchange="TFChange()">
                                <option value="30" selected>30 Days</option>
                                <option value="60">60 Days</option>
                                <option value="90">90 Days</option>
                                @*<option value="180">180 Days</option>
                                    <option value="365">365 Days</option>*@
                            </select>
                        </div>
                        <div class="col-md-4 form-group">
                            <label for="tbStartDate" class="form-label" style="font-size:20px;color:blue">From:</label>
                            <input type="text" readonly id="tbEndDate" class="form-control-sm">
                        </div>
                        <div class="col-md-4 form-group">
                            <label for="tbEndDate" class="form-label" style="font-size:20px;color:blue">To:</label>
                            <input type="text" readonly id="tbStartDate" class="form-control-sm">
                            
                        </div>
                    </div>
                </div>
            </div>
            <div class="modal-body" id="mBody2" style="margin-top:0px;">
                <div class="tab">
                    <button class="tablinks" onclick="openPlots(event, 'ViolinPlots')" id="defaultOpen">Violin Plot</button>
                    <button class="tablinks" onclick="openPlots(event, 'LinePlots')">Trend Plot</button>
                </div>

                <div id="ViolinPlots" class="tabcontent">
                    <div id="CompareViolinPlots" style="width:90vw; margin:0">

                    </div>
                </div>

                <div id="LinePlots" class="tabcontent">
                    <div id="CompareLinePlots" style="width:90vw; margin:auto">

                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
