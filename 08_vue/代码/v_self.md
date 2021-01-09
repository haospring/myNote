~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>v_self</title>
		<script type="text/javascript" src="js/vue.js"></script>
		<style type="text/css">
			#box_01 {
				width: 500px;
				height: 500px;
				background-color: red;
			}
		
			#box_02 {
				width: 300px;
				height: 300px;
				background-color: green;
			}
		
			#box_03 {
				width: 100px;
				height: 100px;
				background-color: blue;
			}
		</style>
	</head>
	<body>
		<div id="box_01" @click="t_box_01">
			<div id="box_02" @click.self="t_box_02">
				<div id="box_03" @click="t_box_03">

				</div>
			</div>
			<!-- 添加一个超链接访问 -->
			<a href="http://www.baidu.com" @click="t_show">百度</a>
		</div>
	</body>
	<script>
		var vm = new Vue({
			el: "#box_01",
			data: {

			},
			methods: {
				t_show() {
					console.log("超链接被点击");
				},
				t_box_01() {
					console.log("外层div");
				},
				t_box_02() {
					console.log("中层div");
				},
				t_box_03() {
					console.log("内层div");
				}
			}
		});
	</script>
</html>
~~~

