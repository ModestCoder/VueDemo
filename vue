<html>
    <head>
        <style type="text/css">
        	html, body {
		    margin: 5px;
		    padding: 0;
		}
        </style>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    </head>
    <body>
        <div id="app">
            {{ message }}
        </div>
        
        <div id="app-2">
		  <span v-bind:title="message">
		    鼠标悬停几秒钟查看此处动态绑定的提示信息！
		  </span>
		</div>

		<div id="app-3">
		  <p v-if="seen">{{ message }}</p>
		</div>

		<div id="app-4">
		  <ol>
		    <li v-for="todo in todos">
		      {{ todo.text }}
		    </li>
		  </ol>
		</div>

		<div id="app-5">
		  <p>{{ message }}</p>
		  <button v-on:click="reverseMessage">逆转消息</button>
		</div>

		<div id="app-6">
		  <p>{{ message }}</p>
		  <input v-model="message">
		</div>

		<div id="app-7">
		  <ol>
		    <!--
		      // 现在我们为每个 todo-item 提供 todo 对象
		      // todo 对象是变量，即其内容可以是动态的。
		      // 我们也需要为每个组件提供一个“key”，稍后再
		      // 作详细解释。
		    -->
		    <todo-item
		      v-for="item in groceryList"
		      v-bind:todo="item"
		      v-bind:key="item.id">
		    </todo-item>
		  </ol>
		</div>

		<div id="app8">
		  <p>{{ foo }}</p>
		  <!-- 这里的 `foo` 不会更新！ -->
		  <button v-on:click="foo = 'baz'">Change it</button>
		</div>

		<div id="app9">
		  
		</div>
        <script type="text/javascript">
        	var app = new Vue({ 
			    el: '#app',
			    data: {
			        message: 'Hello Vuess!'
		    }
			});

			var app2 = new Vue({
			  el: '#app-2',
			  data: {
			    message: '页面加载于 ' + new Date().toLocaleString()
			  }
			});

			var app3 = new Vue({
			  el: '#app-3',
			  data: {
			  	// seen: false,
			    seen: true,
			    message:'你能看见我么？'
			  }
			});

			var app4 = new Vue({
			  el: '#app-4',
			  data: {
			    todos: [
			      { text: '学习 JavaScript' },
			      { text: '学习 Vue' },
			      { text: '整个牛项目' }
			    ]
			  }
			});

			var app5 = new Vue({
			  el: '#app-5',
			  data: {
			    message: 'Hello Vue.js!'
			  },
			  methods: {
			    reverseMessage: function () {
			      this.message = this.message.split('').reverse().join('')
			    }
			  }
			});

			var app6 = new Vue({
			  el: '#app-6',
			  data: {
			    message: 'Hello Vue!'
			  }
			});

			Vue.component('todo-item', {
			  props: ['todo'],
			  template: '<li>{{ todo.text }}</li>'
			});

			var app7 = new Vue({
			  el: '#app-7',
			  data: {
			    groceryList: [
			      { id: 0, text: '蔬菜' },
			      { id: 1, text: '奶酪' },
			      { id: 2, text: '随便其它什么人吃的东西' }
			    ]
			  }
			});

//数据与方法 start
	//Eg1
			// 我们的数据对象
			var data = { a: 1 }

			// 该对象被加入到一个 Vue 实例中
			var vm = new Vue({
			  data: data
			})

			// 获得这个实例上的属性
			// 返回源数据中对应的字段
			vm.a == data.a // => true
			// alert("vm.a == data.a:"+(vm.a == data.a));
			// 设置属性也会影响到原始数据
			vm.a = 2
			data.a // => 2
			// alert("vm.a = 2  data.a="+data.a);
			// ……反之亦然
			data.a = 3
			vm.a // => 3
			// alert("data.a = 3  vm.a="+vm.a);
	//Eg2
			var obj = {
			  foo: 'bar'
			}
			//使用 Object.freeze()，这会阻止修改现有的属性
			Object.freeze(obj)

			new Vue({
			  el: '#app8',
			  data: obj
			});
	//Eg3
			var data = { a: 1 }
			var vm = new Vue({
			  el: '#app9',
			  data: data
			})

			vm.$data === data // => true
			alert("vm.$data === data is "+(vm.$data === data));
			vm.$el === document.getElementById('example') // => true
			alert("vm.$el === document.getElementById('example') is "+(vm.$el === document.getElementById('app9')));
			// $watch 是一个实例方法
			vm.$watch('a', function (newValue, oldValue) {
			  // 这个回调将在 `vm.a` 改变后调用
			})
//数据与方法 end

        </script>
    </body>
</html>
