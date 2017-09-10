function spotBooking(s){
	var reserve=/^(\w+)+\s(\d{4})-(0[1-9]{1}|1[1|2])-([0-2][1-9]{1}|3[0|1])\s([0-1][0-9]|2[0-1]):00~([0-1][0-9]|2[0-2]):00\s([A-D])(\sC)?$/g;
	
	var weekdayfee=[30,30,30,50,50,50,50,50,50,80,80,60,60];
	var weekendfee=[40,40,40,50,50,50,50,50,50,60,60,60,60];
	

	s.replace(reserve,function(m0,m1,m2,m3,m4,m5,m6,m7,m8){         //获取预订信息
		if(m8==' C'){                           //取消预订
			
			if((reserveinf[m7].indexOf(s=s.substring(0,m0.length-2))!=-1)&&(reserveinf[m7].indexOf(m0)==-1)){          //有该预定
				console.log('the booking is cancelled')
				reserveinf[m7].push(m0);                             //取消信息压入
				var reservedate=[];
				reservedate=m2.concat(m3).concat(m4).concat(m7);       
				for(var i=parseInt(m5);i<=m6-1;i++){                    //把预订信息从预订时间表中置为0
					var index=reservedata[reservedate].indexOf(i);
					reservedata[reservedate][index]=0;
				} 
				count();
			}
			else{
				console.log('the booking being cancelled does not exist')
			}
		}

		else if(m8==undefined){
			if(m5==m6){
			  console.log('the booking is invalid');   //预订时间不超过0
			}
			else{
				var reservedate=[];
				var reservetime=[];
		        reservedate=m2.concat(m3).concat(m4).concat(m7);            //预订时间日期场馆
		        if(reservedata[reservedate]===undefined){             //该时间场馆未被预订
		        	console.log('the booking is accepted!');
		        	reservedata[reservedate]=[];
		        	for(var i=parseInt(m5);i<=parseInt(m6)-1;i++){
		        		reservetime.push(i);
		        		reservedata[reservedate].push(i);
		        	}
		        	reserveinf[m7].push(m0);
		        	count();
		        }
		        else{
		        	for(var i=m5;i<=m6-1;i++){
		        		reservetime.push(i);

		        	}
			    if(reservetime.every(function(a,b,c){return reservedata[reservedate].indexOf(parseInt(a))==-1})){   //判断这个时间段没有被预定
			    	console.log('the booking is accepted!');
		            reserveinf[m7].push(m0);       //将每个场馆的预定信息压入对象数组
		            for(var i=parseInt(m5);i<=m6-1;i++){
		            	reservedata[reservedate].push(i);
		            }
		            count();
		        }
		        else{
		        	console.log('the booking conflicts with existing bookings!');
		        }
		    }
		}}

		function count(){
			var date=new Date(m2,m3-1,m4);
			var week=date.getDay();
			if (income[m7]===undefined){
				income[m7]=0;

			}
		    if (week>=1&&week<=5) {                  //预订的时间是周1~周5
		    	for (var i=m5-9;i<m6-9;i++){	
		    		if(m8==' C'){
				income[m7]-= 0.75*weekdayfee[i];          //收入加入到场馆总收入
			}
			else{
				income[m7]+= weekdayfee[i];          //收入加入到场馆总收入
			}
		}
	}

			else if(week>=6&&week<=7){                       //预订的时间是周6~周7
				for (var i=m5-9;i<m6-9;i++){
					if(m8==' C'){
						income[m7]-= 0.5*weekendfee[i];
					}
					else{
						income[m7]+= weekendfee[i];
					}
				}
			}
		}
	

});

	console.log("收入汇总");
	console.log(income);
}
var income={};
var reserveinf={};
reserveinf['A']=[];
reserveinf['B']=[];
reserveinf['C']=[];
reserveinf['D']=[];
var reservedata={};
var s='U002 2017-08-01 19:00~22:00 A';
var s1='U003 2017-08-01 18:00~20:00 A';
var s2='U002 2017-08-01 19:00~22:00 A C';
var s3='U002 2017-08-01 19:00~22:00 A C';
var s4='U003 2017-08-01 18:00~20:00 A';
var s5='U003 2017-08-02 13:00~17:00 B';


spotBooking(s);
spotBooking(s1);
spotBooking(s2);
spotBooking(s3);
spotBooking(s4);
spotBooking(s5);
console.log(reserveinf);
console.log(reservedata);
