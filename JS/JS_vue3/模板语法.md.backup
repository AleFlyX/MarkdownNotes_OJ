# vue3 init步骤
~~~
npm init vue@latest 
全选no

cd vue项目文件名
npm install
npm run dev
~~~  

# vue3 init之后结构挂载及使用
1. App.vue是生成html的文件，你写的所有界面（在components文件下）都可以被App.vue挂载并且统一显示
2. 若想在App.vue中挂载你做的网站需要再<script setup></script>元素中import 想挂载的项目名 from './components/想挂载的项目名.vue'
3. import之后在<template></template>元素中<想挂载的项目名/>*即可

# vite端口自定义，避免端口被占用
- vite.config.js文件中更改
~~~

export default defineConfig({
  plugins: [
    vue(),
  ],
  
/*************************************/
  server: {  
    port: 8081, // 设置启动端口为8081  
  }, 
/*************************************/

  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})

~~~
 


## 基本结构
样例：文本插值
~~~
<template>
  <p>{{msg}}</p>
</template>
<script>
export default{
  data(){
     return{
      msg:"example msg"
     }  
  }

}
</script>
~~~
- template:承载所有的html标签
- script:逻辑部分
- style:css


## {{}}插入表达式(不建议，建议直接在脚本中完成)
~~~
<template>
  <p>{{msg}}</p>
  <p>{{num+1}}</p>
  //11
  <p>{{ok ? 'Yes': 'No'}}</p> 
  // Yes(表达式中if判断不可用必须用三元运算符)
  <p>{{message.split('').reverse().join('')}}</p>
  //olleh
</template>
<script>
export default{
  data(){
     return{
      msg:"example msg",
      num:10,
      ok:true,
      message:"hello"
     }  
  }

}
</script>
~~~
 
## v-html来实现innerHTML添加渲染元素
~~~
<template>
  <p v-html="exphtml"></p>
</template>
<script>
export default{
  data(){
     return{
      exphtml:"<p>html test</p>"
      
     }  
  }

}
</script>

//此时html的p元素会渲染<p>html test</p>，从而在页面上显示html test
~~~

## v-bind实现改变html的元素属性
使用*v-bind:属性=“”*或者*:属性=“”*
~~~
<div id="app" class="demo">
    <img v-bind:src="imageSrc">
    <p :class="exampleClass"></p>
</div>

<script>
const HelloVueApp = {
  data() {
    return {
      imageSrc: 'https://static.jyshare.com/images/code-icon-script.png',
      exampleClass:testPara
    }
  }
}

Vue.createApp(HelloVueApp).mount('#app')
</script>
~~~

## 条件渲染 v-if v-else v-else-if
~~~
<div id="app" class="demo">
    <p v-if="showMessage">Hello Vue!</p>
    <p v-else>Goodbye Vue!</p>
    
    <p v-if="type==='A'">A</p>
    
  //因为此时type值为B所以只渲染下面这行
    <p v-else-if="type==='B'">B</p> 
  //////////////////////
  
    <p v-else>C</p>
    
</div>

<script>
const HelloVueApp = {
  data() {
    return {
      showMessage: true,
      /*************************************/
      type:B
      /*************************************/
    }
  }
}

Vue.createApp(HelloVueApp).mount('#app')
</script>
~~~

### v-show
~~~
<div id="app" class="demo">
    <p v-if="showMessage">Hello Vue!</p>
    
    //ans值为true所以显示
    <p v-show='ans'>Goodbye Vue!</p>
    ////////////////////
    
</div>

<script>
const HelloVueApp = {
  data() {
    return {
      showMessage: false,
      
      /////////
      ans:true
      /////////
      
    }
  }
}


</script>
~~~


## v-show与v-if区别
`v-if`和`v-show`都用于根据表达式的真假值来条件性地渲染元素，但它们的工作方式有所不同，主要体现在元素的渲染和销毁行为上。

### v-if

- **条件性渲染**：`v-if`是“真正的”条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
- **DOM操作**：当`v-if`的表达式为`false`时，对应的元素及其子组件会被销毁并从DOM中移除。当表达式再次变为`true`时，元素及其子组件会被重新创建并插入DOM中。
- **性能考虑**：由于`v-if`涉及DOM的添加和删除操作，因此在需要频繁切换显示/隐藏状态的场景下，使用`v-if`可能会比`v-show`有更高的性能开销。但是，如果条件很少改变，或者条件改变时组件需要执行大量的初始化操作（如API调用），则`v-if`可能更合适，因为它可以确保组件只在必要时才加载。

### v-show

- **切换显示状态**：`v-show`只是简单地切换元素的CSS属性`display`。元素始终会保留在DOM中，只是其显示状态会根据表达式的真假值进行切换。
- **性能优势**：由于`v-show`只是改变CSS属性，不涉及DOM的添加和删除，因此在需要频繁切换元素显示/隐藏状态的场景下，`v-show`的性能通常优于`v-if`。
- **使用场景**：当需要频繁切换元素显示/隐藏，且不需要担心元素或组件的销毁和重建带来的额外开销时，`v-show`是更好的选择。

### 总结

- 使用`v-if`时，元素会根据表达式的真假值被销毁或重建。
- 使用`v-show`时，元素始终保留在DOM中，只是通过改变CSS的`display`属性来控制其显示或隐藏。
- 在性能敏感的场景下，***如果条件不常改变，或者条件改变时涉及到较大的开销（如组件初始化），则推荐使用`v-if`。***
- 在需要频繁切换元素显示/隐藏状态的场景下，推荐使用`v-show`。


## 列表渲染 v-for v-on
### v-for="name in/of names"

~~~
<div id="app" class="demo">
  <ul>
    <li v-for="item in items" :key="item.id">
      {{ item.text }}
    </li>
  </ul>
</div>

<script>
const HelloVueApp = {
  data() {
    return {
      items: [
        { id: 1, text: 'Item 1' },
        { id: 2, text: 'Item 2' },
        { id: 3, text: 'Item 3' }
      ]
    }
  }
}

Vue.createApp(HelloVueApp).mount('#app')
</script>
~~~

~~~
<template>
  <p v-for='para in paras'>{{para}}</p>
</template>

<script>  
 export default{
   data(){
     return{
       paras:['A1','B2','C3'];
       
     }
   }
 
 }
</script>

/******************运行结果****************/
生成3个<p></p>元素分别显示paras[]中的元素

<p>A1</p>
<p>B2</p>
<p>C3</p>

~~~	

#### 也可搭配'.'使用，与js语法相同
~~~
<template>
  //显示paras每个对象的title
  <p v-for='para in paras'>{{para.title}}</p>
  
  //显示paras每个对象的index
  <img :src="para.index">
//在浏览器查看代码会发现生成多行<p>与<img>的组合

</template>

<script>  
 export default{
   data(){
     return{
       paras:[
         {
           "title":"a1",
           "index":"/dir/img1.jpg"
         },
         {
          "title":"b1",
          "index":"/dir/img2.jpg"
         },
          {
           "title":"c3",
           "index":"/dir/img3.jpg"
         },
          

       ];
       
     }
   }
 
 }
</script>  
~~~
#### v-for使用可选的第二个参数，例如表示当前位置
~~~
<template>
  <p v-for='(para,index) in paras'>{{para}}:{{index}}</p>
</template>

<script>  
 export default{
   data(){
     return{
       paras:['A1','B2','C3'];
       
     }
   }
 
 }
</script>
//////////////////////////////
结果会渲染
A1:0
B2:1
C3:2

~~~

#### v-for="... in ..."可用 on代替in

## 事件监听 v-on

~~~
<div id="app">
  <div id="lightDiv">
    <div v-show="lightOn"></div>
    <img src="https://static.jyshare.com/images/svg/img_lightBulb.svg">
  </div>
  <button v-on:click=" lightOn =! lightOn ">开/关</button>
</div>

<script>
const app = Vue.createApp({
  data() {
    return {
      lightOn: false
    }
  }
})
app.mount('#app')
</script>  
~~~

#### v-on也可用@代替
~~~
将刚刚的例子更改  
<button @click=" lightOn =! lightOn ">开/关</button>
~~~
### 事件监听调用函数

~~~
<template>
    <button @click="addOne">Add1</button>
    <p>{{count}}</p>
  </template>
  
<script>  
   export default{
     data(){
       return{
         count:0
         
       }
     },
     methods:{
       addOne(){
         console.log('被点击了');
         this.count++;
       }
     }
   
   }
</script>
~~~

#### 调用的函数也可以传入参数（可传入多个，调用函数的语法与js一样）
~~~
<template>
    <button @click="addOne(count)">Add1</button>
    <p>{{count}}</p>
</template>
  
<script>  
   export default{
     data(){
       return{
         count:0
         
       }
     },
     methods:{
       addOne(times){
         console.log('被点击了'+times+'次');
         this.count++;
       }
     }
   
   }
</script>
~~~

`## v-on事件修饰符
在 Vue 3 中，事件修饰符的使用方式与 Vue 2 类似，它们提供了一种便捷的方式来处理 DOM 事件的常见场景，而无需编写额外的 JavaScript 代码。事件修饰符是以点（`.`）开头的特殊后缀，可以链式调用。

Vue 3 支持以下事件修饰符：

1. **.stop** - 调用 `event.stopPropagation()`。阻止事件冒泡。
2. **.prevent** - 调用 `event.preventDefault()`。阻止默认行为。
3. **.capture** - 添加事件监听器时使用事件捕获模式。
4. **.self** - 只当事件在该元素本身（比如不是子元素）触发时触发回调。
5. **.once** - 事件只触发一次。
6. **.passive** - 调用 `event.preventDefault()` 的事件监听器将不会被执行，以提高滚动性能。注意，`.passive` 和 `.prevent` 一起使用时，`.prevent` 会被忽略。

.stop - 阻止冒泡
.prevent - 阻止默认事件
.capture - 阻止捕获
.self - 只监听触发该元素的事件
.once - 只触发一次
.left - 左键事件
.right - 右键事件
.middle - 中间滚轮事件

#### 全部的按键别名：

.enter
.tab
.delete (捕获 "删除" 和 "退格" 键)
.esc
.space
.up
.down
.left
.right
##### 系统修饰键：

.ctrl
.alt
.shift
.meta
##### 鼠标按钮修饰符:

.left
.right
.middle

#### .exact修饰符
~~~
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>  
~~~

### 使用示例

假设你有一个按钮，点击时你希望阻止默认行为（比如不提交表单），并阻止事件冒泡：

```html
<template>
  <div @click="divClicked">
    <button @click.stop.prevent="buttonClicked">点击我</button>
  </div>
</template>

<script>
export default {
  methods: {
    buttonClicked() {
      console.log('按钮被点击了，但事件不会冒泡，且默认行为被阻止。');
    },
    divClicked() {
      console.log('这个不会执行，因为事件被阻止了冒泡。');
    }
  }
}
</script>
```

在这个例子中，点击按钮时，`buttonClicked` 方法会被调用，但 `divClicked` 方法不会，因为 `.stop` 修饰符阻止了事件冒泡。同时，`.prevent` 修饰符阻止了按钮的默认行为（如果有的话）。

### 注意事项

- 修饰符可以串联使用，如上例所示。
- 修饰符的顺序很重要，因为相关的 DOM 事件处理顺序（如捕获与冒泡）会影响它们的行为。
- Vue 3 仍然支持 Vue 2 中的事件修饰符，并且没有引入新的修饰符（截至 Vue 3.x 的最新稳定版本）。
- 使用 `.passive` 修饰符时，请确保你了解它的含义和性能影响，因为它会告诉浏览器你永远不会调用 `preventDefault()`。这主要用于改善滚动性能。



## js数组扩展基本的js数组处理函数之外还有以下函数可以做到在不刷新页面ui的情况下静默更改数组的内容

- filter()
- concat()
- slice()
这些函数不会直接改变数组，而是返回一个新数组
~~~
<template>
    <p>数组1</p>
    <p v-for="(n1,index) in num1" :key="index">{{ n1 }}</p>
   
    <p>数组2</p>
    <p v-for="(n2,index) in num2" :key="index">{{n2}}</p>
    <button @click="connectArr">合并数组到数组1</button>
    
</template>
  
  <script>  
   export default{
     data(){
       return{
         num1:[1,2,3,4,5],
         num2:[7,8,9,0]
         
       }
     },
     methods:{
       connectArr(){
         console.log('success');
         this.num1=this.num1.concat(this.num2);
       }
     }
   
   }
  </script>  
~~~


## 计算属性 computed{}
~~~
<template>
  <div>
    <p>商品名称：{{ productName }}</p>
    <p>商品价格：{{ formattedPrice }}</p>
    <button @click="increasePrice">增加价格</button>
  </div>
</template>

<script>
import { reactive, computed } from 'vue';

export default {
  setup() {
    // 响应式数据
    const state = reactive({
      name: '手机',
      price: 2000
    });

    // 计算属性
    const productName = computed(() => {
      return `优惠 ${state.name}`;
    });

    const formattedPrice = computed(() => {
      return `￥${state.price.toFixed(2)}`;
    });

    // 方法
    const increasePrice = () => {
      state.price += 100;
    };

    return {
      productName,
      formattedPrice,
      increasePrice
    };
  }
};
</script>
~~~  

## class动态绑定
~~~
  <template>
    <p>class绑定</p>
    <p :class="{ 'active': showP, 'fakeClass': noShowP }">通过布尔值,true则绑定某个变量名到class</p>
    <p :class="{ noShowP, showP }">这行class不绑定false的</p>
    <p :class="[showP ? 'active textStrong' :'']">使用三元运算符来判断给class赋值</p>
</template>

<script>
export default {

    data() {
        return {
            showP: true,
            noShowP: false,
            classObject: {
                'active': true,
                'textStrong': true
            },
            arrActive:'active',
            arrHasErr:'textStrong'

        }
    }
}
</script>
<style></style>
~~~  

## style动态绑定
~~~
  <template>
    <p>style绑定</p>
    <p :style="{color:'red'}">直接用color属性定义</p>
    <p :style="{color:fontColor1}">访问变量储存的值</p>
    <p :style="[stylesObj]">通过对象定义style(注意更改{}-->[])</p>
</template>

<script>
export default {

    data() {
        return {
         fontColor1:'green',
         stylesObj:{
            color:'red',
            fontSize:'60px'
         }
        } 
    }
}
</script>
<style></style>
~~~  

## 侦听器watch:{}
~~~
<template>
    <h3>侦听器</h3>
    <p>{{ message }}</p>
    <button @click="updateMessage">修改数据</button>
</template>
<script>
export default {
    data() {

        return {
            message: '你好'
        }
    },
    methods:{
        updateMessage() {
            this.message = "装B让你飞起来!"
        }
    },
    /////侦听器watch
    watch: {
        //newValue:
        //oldValue:
        //函数名必须与想监听的变量名/对象名一致
        message(newValue, oldValue) {//侦听的message变量
            //数据发生变化立即执行函数
            console.log('数据已被改变!');
        }

    }

}
</script>
~~~  


# 重要：表单输入绑定v-model

主要用于在表单输入和应用状态之间创建双向数据绑定。当你在表单元素上使用 v-model 时，Vue 会自动地为你做两件事：

- 根据组件的 data 中绑定的数据，自动渲染并更新表单控件的值。
- ***当用户更改表单控件的值时，自动更新组件的 data 中的数据。***
~~~
<template>  
  <div>  

    <input v-model="message" placeholder="edit me">  
    <p>Message is: {{ message }}</p>  
//<input> 元素的值通过 v-model 绑定到了组件的 data 中的 message 属性。这意呀着，当用户输入文本时，message 的值会自动更新，并且这种更新会反映到视图上（即 <p> 标签内的文本）。

  </div>  
</template>  
  
<script>  
export default {  
  data() {  
    return {  
      message: ''  
    }  
  }  
}  
</script>  
~~~  

## v-model与表单
v-model 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

- text 和 textarea 元素使用 value 属性和 input 事件；
- checkbox 和 radio 使用 checked 属性和 change 事件；
- select 字段将 value 作为属性并将 change 作为事件。
### input textarea 
~~~
<div id="app">
  <p>input 元素：</p>
  <input v-model="message" placeholder="编辑我……">
  <p>input 表单消息是: {{ message }}</p>
    
  <p>textarea 元素：</p>
  
  //message2不会获取到如何文本，需要v-model='text'
  <!--textarea v-model="message2" placeholder="多行文本输入……"></textarea-->
  
  
  <p>textarea 表单消息是:</p>
  <p style="white-space: pre">{{ message2 }}</p>
  
</div>
 
<script>
const app = {
  data() {
    return {
      message: '',
      message2: '菜鸟教程\r\nhttps://www.runoob.com'
    }
  }
}
 
Vue.createApp(app).mount('#app')
</script>  
~~~  

### 复选框
~~~
<div id="app">
  <p>单个复选框：</p>
  <input type="checkbox" id="checkbox" v-model="checked">
  <label for="checkbox">{{ checked }}</label>
    
  <p>多个复选框：</p>
  <input type="checkbox" id="runoob" value="Runoob" v-model="checkedNames">
  <label for="runoob">Runoob</label>
  <input type="checkbox" id="google" value="Google" v-model="checkedNames">
  <label for="google">Google</label>
  <input type="checkbox" id="taobao" value="Taobao" v-model="checkedNames">
  <label for="taobao">taobao</label>
  <br>
  <span>选择的值为: {{ checkedNames }}</span>
</div>
 
<script>
const app = {
  data() {
    return {
      checked : false,
      checkedNames: []
    }
  }
}
 
Vue.createApp(app).mount('#app')
</script>
~~~  

### 单选框
~~~
<div id="app">
  <input type="radio" id="runoob" value="Runoob" v-model="picked">
  <label for="runoob">Runoob</label>
  <br>
  <input type="radio" id="google" value="Google" v-model="picked">
  <label for="google">Google</label>
  <br>
  <span>选中值为: {{ picked }}</span>
</div>
 
<script>
const app = {
  data() {
    return {
      picked : 'Runoob'
    }
  }
}
 
Vue.createApp(app).mount('#app')
</script>
~~~

### select列表
~~~
<div id="app">
  <select v-model="selected" name="site">
    <option value="">选择一个网站</option>
    <option value="www.runoob.com">Runoob</option>
    <option value="www.google.com">Google</option>
  </select>
 
  <div id="output">
      选择的网站是: {{selected}}
  </div>
</div>
 
<script>
const app = {
  data() {
    return {
      selected: '' 
    }
  }
}
 
Vue.createApp(app).mount('#app')
</script>  
~~~

# *重要* vue中的DOM（$refs）
- 通过*$refs*以及class等元素属性来定位所需的元素来实现DOM
- input默认有value属性，可以通过value获取输入的值
~~~
<template>
    <h3>DOM示例</h3>
    <div class="container" ref="container">{{ element }}</div>
    <input ref="username" type="text">
    <button @click="getELementsPr()">获取元素</button>
</template>
<script>
export default {
    data() {
        return {
           element:'我是<div>'
        }
    },
    methods:{
        getELementsPr() {
            this.$refs.container.innerHTML='我被抓走了';
            console.log(this.$refs.username.value);
        }
    }


}
</script>
~~~  



# 组件引用
在App.vue文件中
~~~
<script>
import MyComponent from './components/MyComponent.vue';
import header from './components/header.vue';
import article from './components/article.vue';
<template>
  <MyComponent/>
  <header/>
  <article/>
</template>
<script/>
<script>
export default{
  components:{
    Mycomponent,
    article,
    header
    
  }

}
</script>
~~~  

## 在./component文件下创建的.vue文件
- 如果在<style>元素后面加上scoped,即<style scoped>,则该组件定义的css只会在这个组件生效，被App.vue文件挂载时此文件定义的css并不会被用于全局


## 组件全局注册及引用
一般情况下在某个.vue文件下调用某个文件时每次都需要import一次，再export default{}一次来达到局部调用，如果想省去这个步骤可以将某个部件进行全局注册

- 全局注册（需要再main.js文件完成）
~~~main.js
import './assets/main.css'

import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')

~~~
改成
~~~
import './assets/main.css'

import { createApp } from 'vue'
import App from './App.vue'

const app=createApp(App)

//在此区域内进行组件的全局注册
//app.component("组件名字",想将 此组件命名成的名字)

app.component("header",Header);

app.mount('#app')

~~~

~~~  App.vue
<template>
  <MyComponent/>
  
  /////////////
  <Header/>  已经将header全局定义为Header,使用时直接写Header
  /////////////
  
  <article/>
</template>
<script>
import MyComponent from './components/MyComponent.vue';

//////////////////
import header from './components/header.vue';可以删除
///////////////////

import article from './components/article.vue';
export default{
  components:{
    Mycomponent,
    article,
    ////////////
    //header  无需再写出
    ///////////
  }

}
</script>
~~~  

# 父传子 *prop:[]*组件间的数据传递（只能从父组件传递到子组件）
- 父组件parent.vue
~~~
<template>
  <h2>parent</h2>
  
  <child :title="message"/>//引用child组件，并且传输title的内容给child组件
  
</template>

<script>
import child from './....'
export default{
   data(){
     return{
       message:"传输内容测试"
     }
   },
   components:{
     child
   }
    
  }

}
</script>
~~~

- 子组件child.vue
~~~
<template>
  <h3>child</h3>
  <p>{{title}}</p>
</template>

<script>
export default{
   data(){
     return{
     
     }
   },
   props:["title"]//用props函数接收数据
   
}
</script>
~~~

## 可传递的数据类型
- 字符串
- 数组
- 对象
- 简而言之是任何类型
parentNode.vue
~~~ 
<template>
    <h2>PARENT-input</h2>
    Enter name:<input v-model="name" placeholder="your name">//输入变量message的值
    <h5>object example:{
        age:"18",
        genden:"ArmyHelicopter",
        weapon:"AGM"
        }
    </h5>
    <childNode :name="name" :testObj="TEObject"/>


</template>

<script>
import childNode from './childNode.vue';
export default {
    data() {
        return {
            name: "",
            TEObject: {
                age: "18",
                genden: "ArmyHelicopter",
                weapon: "AGM"
            }
        }

    },
    components: {
        childNode
    }
}
</script>
 
~~~  
childNode.vue
~~~
<template>
    <h3>CHILDnode-result</h3>
  
    <p>username:{{name}}</p>
    <h5>object result:</h5>
    <p>{{testObj.age}} years old,
       I am {{ testObj.genden }},
       I use {{ testObj.weapon }}
    </p>
</template>

<script>
export default {
    data() {
        return {

        }

    },
    props:["name","testObj"]

   
}
</script>

~~~


## props传递数据校验
格式
~~~
props:{
   变量名1:{  
      type:Number,
      required:true, //设置必须输入 
      default:"none"//设置默认值
   },
   变量名2:{
      type:[String,Number,Array,Object],
        
   },
   对象变量名1{
      default(){
        return{}//对象的默认值需要返回一个空对象
      }
   }
  
}
~~~

~~~
<template>
    <h3>CHILDnode-result</h3>
    
    <p>username:{{name}}</p>
    <h5>object result:</h5>
    <p>{{testObj.age}} years old,
       I am {{ testObj.genden }},
       I use {{ testObj.weapon }}
    </p>
</template>

<script>
export default {
    data() {
        return {

        }

    },
    props:{
       name:{//限制传入的name变量只能是字符串
         type:String
       },
       testObj:{
         type:Object
       }
       
    }
   

   
}
</script>
~~~

# 子传父 $emit
格式
~~~
//子组件
export default{
   methods:{
     clickEvent(){
         //自定义事件
         this.$emit("someEvent","要传输的数据");
     }
     
   }
}  



//父组件
<childs @someEvent="处理事件的函数"/>

~~~

样例 
- 父组件
~~~
<template>
<childs @trans="getData"/>
<h2>Parent</h2>
<p>状态：{{ message }}</p>
<p>数据是：{{ receiveD }}</p>
</template>
<script>
import childs from './childs.vue';
export default{
    data(){
        return{
          message:"none",
          receiveD:"none"
        }
    },
    components:{
        childs
    },
    methods:{
        getData(data){//接收从子组件传入的数据
           this.message="接收成功";
           this.receiveD=data;
        }
    }
}
</script>

~~~    
- 子组件
~~~
 <template>
<h2>Childs</h2>
<input v-model="data">
<button @click="clickedEvent">传递数据给父组件</button>

</template>
<script>
export default{
    data(){
        return{
         data:""
        }
    },
    methods:{
        clickedEvent(){
             this.$emit("trans",this.data)//$emit设定接收参数的监听器名为trans,发送的数据变量名是data
        }
    }
}
</script>

~~~

# 子传父方法2，props借用函数携带的数据进行传递
- 父组件
~~~  
<template>
    <h2>Parent components</h2>
    <p>父组件接收的数据：{{ message }}</p>
    <cmpB :onEvent="dataTr" />
    //onEvent是通过props传递给子组件的函数Function  
    
</template>
<script>
import cmpB from './cmpB.vue';
export default {
    data() {
        return {
            message:""
        }
    },
    components: {
        cmpB
    },
    methods:{
        dataTr(data) {//data用于接收来自子组件的数据
            this.message=data;
        }
    }

}
</script>

~~~
- 子组件
~~~
<template>
    <h2>Child components</h2>
    <p>子传递给父的数据：5201111</p>
    <p>{{ onEvent("5201111") }}</p>
    //onEvent函数传入数据，又因为props链接了onEvent函数，所以传入的数据可以顺着函数和props传回父组件的函数
</template>
<script>

export default {

    data() {
         return{}
    },
    props:{
       onEvent:Function//限制onEvent传入是以函数形式
    }

}
</script>
~~~

# 父传子，slot（插槽）传递标签或模版
- < slot > 是一个插槽出口，标识了父元素提供的插槽内容将在哪渲染，相当于传递了个html结构
- slot默认值：如果父组件没有传入任何内容，则子组件的slot标签只会显示< slot >< /slot>中的内容
- 例：
~~~  
<template>

<slot>这是插槽默认值</slot> //子组件只会显示“插槽默认值”

</template>
~~~

- 父组件
~~~
<template>
  <p>我是一行父组件的内容</p>
  <cmpA>//在调用组件这一行输入想插入的html模板
    <div>
      <h1>我是插槽标题</h1>
      <h4>插槽内容</h4>
    </div>
  </cmpA>
</template>
<script>
import cmpA from './components/cmpA.vue'
export default {
  components: {
    cmpA
  }
}
</script>

~~~
- 子组件  
~~~
<template>
<P></P>

//slot就是接收传入的html组件的位置
<slot></slot> 

</template>
  
~~~  

## v-slot（或者#）具体插槽名
- 用法

父组件
~~~
<componentTEST>
 <template v-slot:header>
 //或者 <template #header>  
     <p>内容1</p>
 </template>
 <template v-slot:main>
    	 <p>内容2</p>
 </template>
</componentTEST>
~~~
子组件
~~~  
<template>
	<slot name="header"></slot>
    <hr>
	<slot name="main"></slot>
</template>
~~~

# 子传父:slot
原理：slot传输的数据相当于一个对象，可以读取该对象的各个变量的名字
父组件
~~~
<template>  
  <ChildComponent>  
    <template #list="{ item }">  
      <p>{{ item.name }}</p>  
    </template>  
  </ChildComponent>  
</template>

~~~

子组件
~~~
<template>  
  <div>  
    <slot name="list" :item="item" v-for="item in items" :key="item.id"></slot>  
  </div>  
</template>  
  
<script>  
export default {  
  data() {  
    return {  
      items: [  
        { id: 1, name: 'Item 1' },  
        { id: 2, name: 'Item 2' }  
      ]  
    }  
  }  
}  
</script>
~~~

# *重要：* router路由，同一页面切换界面
Vue 3 Router 是 Vue.js 官方提供的路由管理器，用于构建单页面应用（SPA）。

### 安装 Vue Router 4
在初始化vue安装时勾选router安装选项

### 基本使用

1. **定义路由**：首先，你需要定义应用的路由。每个路由应该映射一个组件。

2. **创建路由实例**：然后，使用这些路由创建一个 `router` 实例。

3. **将路由实例注入到 Vue 应用**：最后，将 `router` 实例注入到 Vue 应用中。

### 示例

以下是一个简单的 Vue 3 和 Vue Router 4 的使用示例：

**定义路由** (`src/router/index.js` 或 `src/router/index.ts`)

```javascript
import { createRouter, createWebHistory } from 'vue-router';
import Home from '../views/Home.vue';
import About from '../views/About.vue';

const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: About
  }
  // 更多路由...
];

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
});

export default router;
```

**在 Vue 应用中使用路由** (`src/main.js` 或 `src/main.ts`)

```javascript
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

const app = createApp(App);

app.use(router);

app.mount('#app');
```

**在组件中使用 `<router-view>`**

在你的 Vue 组件中（通常是 `App.vue`），你可以使用 `<router-view>` 来显示当前路由对应的组件。

```vue
<template>
  <div id="app">
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>
```

在这个例子中，`<router-link>` 组件用于创建导航链接，这些链接会更新 URL 并与 Vue Router 保持同步，但不会重新加载页面。`<router-view>` 组件是一个功能性组件，用于渲染匹配到的路由组件。

### 导航守卫

Vue Router 还提供了导航守卫（Navigation Guards），允许你在路由发生变化时执行一些逻辑，如检查用户是否登录、设置页面标题等。

### 编程式导航

除了使用 `<router-link>` 进行声明式导航外，Vue Router 还允许你使用 JavaScript 代码进行编程式导航，如 `router.push()` 和 `router.replace()`。

Vue Router 4 为 Vue 3 提供了强大的路由管理功能，是构建单页面应用不可或缺的一部分。

# 组件生命周期
Vue 3 引入了 Composition API，为开发者提供了更灵活的方式来组织和复用逻辑。尽管如此，Vue 3 仍然保留了 Options API，其中的组件生命周期钩子（也称为生命周期事件或生命周期方法）对于理解和控制组件的行为至关重要。

### 1. `beforeCreate`（创建前）

- **用法**：在实例初始化之后，数据观测(data observer) 和 event/watcher 事件配置之前被调用。此时组件的选项对象还未被创建，el 和 data 都未被初始化，因此无法访问 methods, computed, watch, data 上的方法和数据。

### 2. `created`（创建后）

- **用法**：在实例创建完成后被立即调用。在这一步，实例已完成数据观测(data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。

### 3. `beforeMount`（挂载前）

- **用法**：在挂载开始之前被调用：相关的 render 函数首次被调用。该钩子在服务器端渲染期间不被调用。

### 4. `mounted`（已挂载）

- **用法**：el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。

### 5. `beforeUpdate`（更新前）

- **用法**：数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。

### 6. `updated`（已更新）

- **用法**：由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用这个钩子。当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态，因为这可能会导致更新无限循环。

### 7. `beforeUnmount`（卸载前）

- **用法**（Vue 3 新增）：在卸载组件实例之前调用。在这个阶段，实例仍然完全可用。

### 8. `unmounted`（已卸载）

- **用法**：卸载组件实例后调用。调用后，组件实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也都会被销毁。

### 9. `activated`（被激活）

- **用法**：keep-alive 组件激活时调用。该钩子在服务器端渲染期间不被调用。

### 10. `deactivated`（被停用）

- **用法**：keep-alive 组件停用时调用。该钩子在服务器端渲染期间不被调用。

这些生命周期钩子提供了在不同阶段对组件进行操作的时机，使得开发者可以更加精确地控制组件的行为。










