~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>传统的css样式的使用，通过class属性</title>
		<script type="text/javascript" src="js/vue.js"></script>
		<style type="text/css">
			.widthstyle {
				width: 100px;
			}

			.heightstyle {
				height: 100px;
			}

			.colorstyle {
				background-color: aquamarine;
			}
		</style>
	</head>
	<body>
		<div id="box03">
			<!-- <div class="widthstyle heightstyle colorstyle"></div> -->
			<!-- <div :class="'colorstyle'">vue完成样式字符串的引用</div> -->
			<!-- 通过绑定属性class引用model中所定义的变量 -->
			<!-- <div :class="style1">vue绑定class并绑定data中的参数</div> -->
			<div :class="style1%2==0?'colorstyle':'heightstyle'">支持三目运算</div>
		</div>
	</body>
	<script>
		var vm = new Vue({
			el: "#box03",
			data: {
				style1: colorstyle,
				style2: 3
			}
		});
	</script>
</html>

~~~

