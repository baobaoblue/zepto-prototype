
### zepto原型实现

```
(function(window){
		var zepto = {}

		function Z(dom,selector){
			var i,len = dom ? dom.length :0
			for (var i = 0; i < len; i++) {
				this.length = len;
				this.selector = selector || ''
			}
		}

		zepto.Z = function(dom,selector){
			return new Z(dom,selector)
		}

		zepto.init = function (selector){
			var slice = Array.prototype.slice
			var dom = slice.call(document.querySelectorAll(selector))
			return zepto.Z(dom,selector)
		}

		var $ = function(selector){
			return zepto.init(selector)
		}

		window.$ = $

		$.fn = {
			css:function(key,value){
				alert('css')
			},
			html:function(value){
				alert('html')
			}
		}
		Z.prototype = $.fn
	})(window)
  ```
  * [1]. 通过 $ 函数传入一个选择器；
  
  * [2]. 接着走 zepto.init, 把选择器转换成DOM节点，处理成数组形式；
  
  * [3]. 把 DOM 和 selector 传给 **zepto.Z** 这个函数，zepto.Z new 了一个构造函数 **Z** 的实例 并返回；
  
  * [4]. **Z** 本身是构造函数，赋值了很多属性，构造函数的原型赋值成了 $fn 的对象 ， $fn 对象中有 css 和 html 方法
