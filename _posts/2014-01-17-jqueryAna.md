---
layout: default
title: jQuery对象结构
cate: article
type: article
---

闲置在家 最近想再仔细看下jquery对象的定义和结构。于是网上看了些资料，也自己读了源码。
<!--more-->

先看下jquery的总体结构。
	
	(function( window, undefined ) {
   
    var jQuery = (function() {
       // 构建jQuery对象
       var jQuery = function( selector, context ) {
           return new jQuery.fn.init( selector, context, rootjQuery );
       }
   
       // jQuery对象原型
       jQuery.fn = jQuery.prototype = {
           constructor: jQuery,
           init: function( selector, context, rootjQuery ) {
              
           }
       };
   
       // Give the init function the jQuery prototype for later instantiation
       jQuery.fn.init.prototype = jQuery.fn;
   
       // 合并内容到第一个参数中，后续大部分功能都通过该函数扩展
       // 通过jQuery.fn.extend扩展的函数，大部分都会调用通过jQuery.extend扩展的同名函数
       jQuery.extend = jQuery.fn.extend = function() {};
      
       // 在jQuery上扩展静态方法
       jQuery.extend({
           // ready bindReady
           // isPlainObject isEmptyObject
           // parseJSON parseXML
           // globalEval
           // each makeArray inArray merge grep map
           // proxy
           // access
           // uaMatch
           // sub
           // browser
       });
 
        // 到这里，jQuery对象构造完成，后边的代码都是对jQuery或jQuery对象的扩展
       return jQuery;
   
    })();
   
    window.jQuery = window.$ = jQuery;
	})(window);



可以从上面看出，每个jQuery对象返回的都是 `new jQuery.fn.init` 对象，无论使用 `new jQuery()` 或者 `jQuery()` 创建的对象都是返回 `new jQuery.fn.init` ，因为代码中先执行  `jQuery.fn = jQuery.prototype` ，再执行  `jQuery.fn.init.prototype = jQuery.fn` ，合并后的代码如下：

	jQuery.fn.init.prototype = jQuery.fn = jQuery.prototype
	
所有挂载到 `jQuery.fn` 的方法，相当于挂载到了 `jQuery.prototype` ，即挂载到了jQuery 函数上（一开始的  `jQuery = function( selector, context ) ）` ，但是最后都相当于挂载到了  `jQuery.fn.init.prototype` ，即相当于挂载到了一开始的jQuery 函数返回的对象上，即挂载到了我们最终使用的jQuery对象上。

时间有限，内容很短，下次写 `jQuery.fn.init` 函数。

