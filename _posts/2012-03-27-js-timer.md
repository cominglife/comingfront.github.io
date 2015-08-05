---
layout: post
title: 用javascript做的倒计时功能
category: "note"
tags: ["JavaScript"]
---

用javascript做的倒计时功能：

	<script>
	function showtime() {
		Today = new Date();
		var NowHour = Today.getHours();
		var NowMinute = Today.getMinutes();
		var NowMonth = Today.getMonth();
		var NowDate = Today.getDate();
		var NowYear = Today.getYear();
		var NowSecond = Today.getSeconds();
		if(NowYear < 2000) {NowYear = 1900+NowYear;}
			Today = null;
			Hourleft = 12 - NowHour;
			Minuteleft = 59 - NowMinute;
			Secondleft = 59 - NowSecond;
			Yearleft = 2011 - NowYear;
			Monthleft =10 - NowMonth -1;
			Dateleft = 29 - NowDate;
			if(Secondleft < 0) {
				Secondleft = 60+Secondleft;
				Minuteleft = Minuteleft-1;
			}
			if(Minuteleft < 0){
				Minuteleft = 60+Minuteleft;
				Hourleft = Hourleft-1;
			}
			if(Hourleft<0){
				Hourleft = 24+Hourleft;
				Dateleft = Dateleft-1;
			}
			if(Dateleft < 0){
				Dateleft = 31+Dateleft;
				Monthleft = Monthleft-1;
			}
			if(Monthleft < 0){
				Monthleft = 12+Monthleft;
				Yearleft = Yearleft-1;
			}
			if(Yearleft<0 || (Yearleft==0 && Monthleft<0) || (Yearleft==0 && Monthleft==0 && Dateleft<0) || (Yearleft==0 && Monthleft==0 && Dateleft==0 && Hourleft<0) || (Yearleft==0 && Monthleft==0 && Dateleft==0 && Hourleft==0 && Minuteleft<0) || (Yearleft==0 && Monthleft==0 && Dateleft==0 && Hourleft==0 && Minuteleft==0 && Secondleft<0)){
				Temp = '<strong class="djsh">0</strong><strong class="djsm">0</strong><strong class="djss">0</strong>';
				if(document.getElementById("dTime")) {
					document.getElementById("dTime").innerHTML = Temp;
				}
			}else{
				Temp = '<strong class="djsh">'+(8760*Yearleft+31*Monthleft+24*Dateleft+Hourleft)+'</strong><strong class="djsm">'+Minuteleft+'</strong><strong class="djss">'+Secondleft+'</strong>';
				if(document.getElementById("dTime") ) {
				document.getElementById("dTime").innerHTML = Temp;
			}
			var timerID = null;
			timerID = setTimeout("showtime()",1000);
		}
	}
	showtime();
	</script>

(完)