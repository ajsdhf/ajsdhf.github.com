---
layout: default
title: 关于Code Review以及一些纪录
cate: article
type: article
---

Code Review即代码审查（简称CR），指的是

>是指对计算机源代码系统化地审查，常用软件同行评审的方式进行，其目的是在找出及修正在软件开发初期未发现的错误，提升软件质量及开发者的技术。

CR有多种形式，一个正规的开发团队，想要提升团队成员的代码技能，CR是必不可少的一个环节。推荐是尽量多的人坐在一起对一段代码进行CR。CR有以下的好处：

+ CR 是保证研发质量的重要手段（这是不言而喻的）
+ CR 帮助提升成员专业能力
+ CR 改善研发团队沟通交流

<!--more-->

关于如何做好CR，这里先不讨论。下面我贴出最近一次CR的成果。

####1. 判断为空字符串写法

	if(jQuery.trim(item.html())==""){ 
	
可以写成

	if(!jQuery.trim(item.html())){
	
####2. 有效利用map来将一个对象或者数组转换为新的一个对象或者数组

	var obj = { "result": [
	{ "tradeAmountRate": "1", "provinceName":"2" },
	{ "tradeAmountRate": "3", "provinceName":"4"}
	]}
	var data = [] ;
	for(var i=0; i < obj.result.length; i++){
    	var item={};
    	item["value"] = obj.result[i].tradeAmountRate;
    	item["label"] = obj.result[i].provinceName;
    	data.push(item);
    }
    console.log(data)
    
可以利用map输出

	var data2 = $.map(obj.result , function(a , b){
	    return  {value : a.tradeAmountRate , label: a.provinceName}
	})    
	console.log(data2)
####3.快速利用选择器

	var currentChart = this.panels.eq(index).find('.donut-area-chart');
	var panel=this.panels.eq(index).find('.mdata-tab-panel').eq(0);
	
to ：

	var currentChart = $(".donut-area-chart", this.panels.eq(index)) ;
	var panel = $(".mdata-tab-panel:first", this.panels.eq(index)) ;
	$("#test .test:even") 选取偶数项
	$("#test .test:old") 选取基数项

详见jquery选择器 http://www.w3school.com.cn/jquery/jquery_ref_selectors.asp

####4. 对象继承

	var baseConfig = {
    	type: item.data('type'),
    	yLines:4,
    	xStep: 10,
    	padding: 20
	}
	if(item.attr('id') == 'amount-core-chart'){
    	baseConfig['barSizeRatio'] = 0.2;
    	baseConfig['barGap'] = -3.5;
    	baseConfig['barTag'] = 1;
    	baseConfig['barTagHeight'] = 4;
	}
to

	...
	if(item.attr('id') == 'amount-core-chart'){
   	 	$.extend(baseConfig , {
        	barSizeRatio : 0.2 ,
        	barGap : -.3.5 ,
        	barTag : 1 ,
        	barTagHeight : 4 
    	})
	}
	
####5. 若确定没有html，尽量使用text()，从而避免安全性问题

    
    $("#test").html("插入文字");
    
to:转为text 方法：
	
    $("#test").text("插入文字");
    
####6. for改用each

####7. 只用一次的变量就不要定义临时变量

    var tab = new Slide({
        element: item,
        triggers: $(item).find('.mdata-tab-trigger')
    });
    tab.on("switched",function(toIndex){
        coreChartInit($('#count-core-chart'));      
    });
to :

    var tab = new Slide({
        element: item,
        triggers: $(item).find('.mdata-tab-trigger')
    }).on("switched",function(toIndex){
        coreChartInit($('#count-core-chart'));      
    });

####8. 将数据直接写值，不要单独设置每个值

    var areaPosition={};
    areaPosition["1"] = "205,139";
    areaPosition["3"] = "201,95";
    
    var areaArr = {};
    areaArr["1"] = "CN_AH";
    areaArr["3"] = "CN_BJ";
    
    var areaNameArr = {};
    areaNameArr["1"] = "安徽";
    areaNameArr["3"] = "北京";
to ：

	var area = {
    	"1" : [[205,139],"CN_AH" ,"安徽"],
    	"3" : [[201,95], "CN_BJ", "北京"]
	}







