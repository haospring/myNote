~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>vue生命周期钩子函数的使用</title>
		<script type="text/javascript" src="js/vue.js"></script>
	</head>
	<body>
		<div id="box01">
			<input type="text" v-model="msg" />
			<span id="result">{{msg}}</span>
		</div>
	</body>
	<script>
		var vm = new Vue({
			el: "#box01",
			data: {
				msg: "Hello World"
			},
			beforeCreate() {
				console.log("beforeCreate被执行");
				console.log("model(data)中的msg：" + this.msg)
			},
			created() {
				console.log("created被执行");
				console.log("model(data)中的msg：" + this.msg)
			},
			beforeMount() {
				console.log("beforeMount被执行");
				// 通过js获取id为result标签的值
				var result = document.getElementById("result").innerHTML;
				console.log("span标签内的文本信息：" + result);
			},
			mounted() {
				console.log("mounted被执行");
				var result = document.getElementById("result").innerHTML;
				console.log("span标签内的文本信息：" + result);
			},
			beforeUpdate() {
				console.log("beforeUpdate被执行");
				// 找到页面中id为result的标签，并获取文本值
				var result = document.getElementById("result").innerHTML;
				console.log("span标签内的文本信息：" + result);
			},
			updated() {
				console.log("updated被执行");
				var result = document.getElementById("result").innerHTML;
				console.log("span标签内的文本信息：" + result);
			},
			beforeDestroy() {
				console.log("beforeDestroy被执行");
			},
			destroyed() {
				console.log("destroyed被执行");
			}
		});
	</script>
</html>
~~~

