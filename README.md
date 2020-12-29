# 12-.html-path
按下鼠标写写画画,刷新即清空 --- HTML5+javaScript代码编写:项道德,2020-12-28
//============================
<!DOCTYPE HTML>
<html>
<body bgcolor="#000">
<canvas id="myCanvas" width="1600" height="800" style="border:2px solid #EE88EE;
	position:absolute;left:100px;top:10px;background:#DDEEFF"
	onMouseMove="MouseMove(window.event.x-100,window.event.y-10)"
	onMouseDown="MouseDown(window.event.x-100,window.event.y-10)"
	onMouseUp="MouseUp()"	>
Your browser does not support the canvas element.
</canvas>
<div id="shw"  style="border:2px solid #808080;
	position:absolute;left:500px;top:815px;background:#FFFFCC">
按下鼠标写写画画,刷新即清空 --- HTML5+javaScript代码编写:项道德,2020-12-28</div>
<script type="text/javascript">

var c=document.getElementById("myCanvas");
var cxt=c.getContext("2d");

var k=10;//动画周期
var flg=0;//鼠标按下标志
var xArr=new Array();//记录鼠标坐标:X
var yArr=new Array();//记录鼠标坐标:Y

//绘制新产生的点:
function draw(x,y){
		 cxt.save();//保持；
		 cxt.beginPath(); //开始独立的颜色;		
		 for(var q=0;q<=6.28;q+=.4){   
			 cxt.lineWidth = 4;//线宽;
			 cxt.moveTo(x,y);//移动到此；
			 cxt.lineTo(x+k*1*Math.sin(q),y+k*1*Math.cos(q));//画至此；
			 cxt.strokeStyle = "#"+parseInt(0xFFFFFF*Math.random()).toString(16);//线色；
		  }
		cxt.stroke(); //执行；
		cxt.restore(); //恢复; 
	  
	  if(k>0){
		k-=.1;//动画衰减速度
		setTimeout("draw("+x+","+y+")",250); 
	  }else{
		k=10;
	  }
} 

//绘制数组中的所有点集:
function draw2(){
		 cxt.save();//保持；
		 cxt.beginPath(); //开始独立的颜色;		
		 if(xArr.length>0){
		 cxt.strokeStyle = "#"+parseInt(0xFFFFFF*Math.random()).toString(16);//线色；
		 for(var i=0;i<xArr.length;i++){
			 for(var q=0;q<=6.28;q+=.2){   
				 cxt.lineWidth = 1;//线宽;
				 cxt.moveTo(xArr[i],yArr[i]);//移动到此；
				 cxt.lineTo(xArr[i]+k*2*Math.sin(q),yArr[i]+k*2*Math.cos(q));//画至此；
				 
			  }
		  }
		cxt.stroke(); //执行；
		cxt.restore(); //恢复;
	  
	  if(k>0){
		k-=.1;//动画衰减速度
		setTimeout("draw2()",250); 
	  }else{
		k=10;
	  }
	  }
} 

//移动鼠标中:
function MouseMove(x,y){	
    //cxt.clearRect(0,0,1600,800);	 //擦除；    
	if(flg==1){
	    xArr.push(x);yArr.push(y);
	    shw.innerHTML="Points Count="+xArr.length;
		draw(x,y);//绘图; 
	}
}

//按下了鼠标:
function MouseDown(x,y){	
	flg=1; //shw.innerHTML="MouseDown()";
	xArr.push(x);yArr.push(y);
	shw.innerHTML="Points Count="+xArr.length;
	draw(x,y);//绘图; 
}

//弹起了鼠标:
function MouseUp(){	
    flg=0;
	shw.innerHTML="按下鼠标写写画画,刷新即清空";//shw.innerHTML="MouseUp()";
    if(xArr.length>0){
	    draw2();//绘图; 
	}
}


</script>
</body>
</html>
