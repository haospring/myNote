~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>vue自定义属性的使用</title>
		<script type="text/javascript" src="js/vue.js"></script>
		<!-- <style type="text/css">
			#box12 {
				width: 300px;
				height: 200px;
				background-color: red;
			}
		</style> -->
	</head>
	<body>
		<div id="box11">
			<!-- <div id="box12" v-color="'green'" v-size="['300px','300px']">dsf</div> -->
			<div id="box13" v-color="'red'" v-size="['500px','300px']">
			</div>
		</div>
	</body>
	<script>
		Vue.directive("color", function(el, binding) {
			el.style.backgroundColor = binding.value;
		});
		Vue.directive("size", function(el, binding) {
			el.style.width = binding.value[0];
			el.style.height = binding.value[1];
		});

		var vm = new Vue({
			el: "#box11",
			data: {

			},
			directives: {
				/* 
				 通过directives完成自定义指令的封装
				 （1）自定义的属性或指令名无需带有v-描述，但是在视图中使用时，必须
				 具备v-描述
				 */
				/* color: {
					// （2）自定义指令对应的函数，通过函数封装指令或属性的功能
					// （3）通常情况下，可以具备或使用5个钩子函数，Vue的钩子函数
					// 在自定义的指令中可以自动加载执行；开发者可以选择钩子函数
					inserted(el, binding) {
						// inserted钩子函数给开发者提供了两个参数：
						// 参数1：自定义指令的js对象
						// 参数2：参数属性所对应的值
						// el参数代表js获取到的标签对象
						// binding参数可以直接调用name属性，代表当前属性的名称
						// binding参数可以直接调用value属性，找到属性名对应的值
						console.log("el参数对应：" + el);
						console.log("binding参数对应name显示：" + binding.name);
						console.log("binding对应的value：" + binding.value);
						// var el = document.getElementById("#box12");
						// el.style.backgroundColor = binding.value;
						el.style.backgroundColor = binding.value;
					}
				}, */
				/* size: {
					inserted(el, binding) {
						el.style.width = binding.value[0];
						el.style.height = binding.value[1];
					}
				} */
			}
		});
	</script>
</html>
~~~

