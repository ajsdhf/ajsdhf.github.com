---
layout: default
title: ����Code Review�Լ�һЩ��¼
cate: article
type: article
---

Code Review��������飨���CR����ָ����

>��ָ�Լ����Դ����ϵͳ������飬�������ͬ������ķ�ʽ���У���Ŀ�������ҳ��������������������δ���ֵĴ���������������������ߵļ�����

CR�ж�����ʽ��һ������Ŀ����Ŷӣ���Ҫ�����Ŷӳ�Ա�Ĵ��뼼�ܣ�CR�Ǳز����ٵ�һ�����ڡ��Ƽ��Ǿ������������һ���һ�δ������CR��CR�����µĺô���

+ CR �Ǳ�֤�з���������Ҫ�ֶΣ����ǲ��Զ����ģ�
+ CR ����������Աרҵ����
+ CR �����з��Ŷӹ�ͨ����

<!--more-->

�����������CR�������Ȳ����ۡ��������������һ��CR�ĳɹ���

####1. �ж�Ϊ���ַ���д��

	if(jQuery.trim(item.html())==""){ 
	
����д��

	if(!jQuery.trim(item.html())){
	
####2. ��Ч����map����һ�������������ת��Ϊ�µ�һ�������������

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
    
��������map���

	var data2 = $.map(obj.result , function(a , b){
	    return  {value : a.tradeAmountRate , label: a.provinceName}
	})    
	console.log(data2)
####3.��������ѡ����

	var currentChart = this.panels.eq(index).find('.donut-area-chart');
	var panel=this.panels.eq(index).find('.mdata-tab-panel').eq(0);
	
to ��

	var currentChart = $(".donut-area-chart", this.panels.eq(index)) ;
	var panel = $(".mdata-tab-panel:first", this.panels.eq(index)) ;
	$("#test .test:even") ѡȡż����
	$("#test .test:old") ѡȡ������

���jqueryѡ���� http://www.w3school.com.cn/jquery/jquery_ref_selectors.asp

####4. ����̳�

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
	
####5. ��ȷ��û��html������ʹ��text()���Ӷ����ⰲȫ������

    
    $("#test").html("��������");
    
to:תΪtext ������
	
    $("#test").text("��������");
    
####6. for����each

####7. ֻ��һ�εı����Ͳ�Ҫ������ʱ����

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

####8. ������ֱ��дֵ����Ҫ��������ÿ��ֵ

    var areaPosition={};
    areaPosition["1"] = "205,139";
    areaPosition["3"] = "201,95";
    
    var areaArr = {};
    areaArr["1"] = "CN_AH";
    areaArr["3"] = "CN_BJ";
    
    var areaNameArr = {};
    areaNameArr["1"] = "����";
    areaNameArr["3"] = "����";
to ��

	var area = {
    	"1" : [[205,139],"CN_AH" ,"����"],
    	"3" : [[201,95], "CN_BJ", "����"]
	}







