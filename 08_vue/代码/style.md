~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>vue绑定style属性</title>
		<script type="text/javascript" src="js/vue.js"></script>
	</head>
	<body>
		<div id="box08">
			<!-- 
			 注意事项：如果开发者想要保留'-'，则需要对当前的样式名称添加单引号；
			 如果开发者想要省略'-'，则需要将该符号后面的单词首字母大写，复合驼峰规则
			 -->
			<div :style="{width:'100px',height:'100px',backgroundColor:'green'}"></div>
		</div>
	</body>
	<script>
		var vm = new Vue({
			el: "#box08",
			data: {

			}
		});
	</script>
</html>
~~~

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="js/vue.js"></script>
	</head>
	<body>
		<div id="box09">
			<div :style="obj"></div>
		</div>
	</body>
	<script>
		var vm = new Vue({
			el: "#box09",
			data: {
				obj: {
					width: '100px',
					height: '100px',
					backgroundColor: 'green'
				}
			}
		});
	</script>
</html>
~~~

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="js/vue.js"></script>
		<style type="text/css">
		</style>
	</head>
	<body>
		<div id="box10">
			<div :style="[obj1,obj2,obj3]"></div>
		</div>
	</body>
	<script>
		var vm = new Vue({
			el: "#box10",
			data: {
				obj1: {
					width: '100px'
				},
				obj2: {
					height: '100px'
				},
				obj3: {
					backgroundColor: 'green'
				}
			}
		});
	</script>
</html>
~~~

