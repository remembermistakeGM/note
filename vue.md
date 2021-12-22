

# Vue 

### 一. Hello Vuejs

#### 1.1. 认识Vuejs

* 为什么学习Vuejs

   可能你的公司正要将原有的项目使用Vue进行重构。

   也可能是你的公司新项目决定使用Vue的技术栈。

   当然，如果你现在正在换工作，你会发现招聘前端的需求中，10个有8个都对Vue有或多或少的要求。

   当然，作为学习者我们知道Vuejs目前非常火，可以说是前端必备的一个技能。

* Vue的读音

   Vue (读音 /vjuː/，类似于 **view**)，不要读错。

* Vue的渐进式

   渐进式意味着你可以将Vue作为你应用的一部分嵌入其中，带来更丰富的交互体验。

   或者如果你希望将更多的业务逻辑使用Vue实现，那么Vue的核心库以及其生态系统。

  比如Core+Vue-router+Vuex，也可以满足你各种各样的需求

* Vue的特点

  解耦视图和数据

  可复用的组件

  前端路由技术

  状态管理

  虚拟DOM

  ###### 学习Vuejs的前提？

  从零学习Vue开发，并不需要你具备其他类似于Angular、React，甚至是jQuery的经验。

  但是你需要具备一定的HTML、CSS、JavaScript基础。

#### 1.2. 安装Vue

* CDN引入

  <!-- 开发环境版本，包含了有帮助的命令行警告 --> 

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

  <!-- 生产环境版本，优化了尺寸和速度 -->

  <script src="https://cdn.jsdelivr.net/npm/vue"></script>

* 下载引入

  开发环境https://vuejs.org/js/vue.js 

  生产环境https://vuejs.org/js/vue.min.js

* npm安装

  npm i vue



#### 1.3. Vue的初体验

* Hello Vuejs

* ```html
     <div id="app">
          {{message}}
      </div>
      <script src="./js/vue.js"></script>
      <script>
          const app=new Vue({
              el:'#app',//挂载
              data:{
                  message:'你好啊，李银河'
              }
          })
      </script>
  ```
  
  
  
  * mustache -> 体验vue响应式
  
* Vue列表展示
  * v-for
  
  * ```html
    <li v-for="item in movies">{{item}}</li>
    ```
  
    ```html
     data: {
                movies: ['星际穿越', '大话西游', '少年派', '盗梦空间']
            }
    ```
  
  * 后面给数组追加元素的时候, 新的元素也可以在界面中渲染出来
  
* Vue计数器小案例
  
  * 事件监听: click -> methods
  
  * ```html
    <button @click='sub'>-</button>
    <h2>{{counter}}</h2>
    <button @click='add'>+</button>
    ```
  
    ```vue
    data:{
       counter:0
         },
     methods:{
     sub(){
      this.counter--
      },
      add(){
      this.counter++
        }
    }
    ```
  
    

#### 1.4. Vue中的MVVM

维基百科介绍：https://zh.wikipedia.org/wiki/MVVM

###### View层：

视图层

在我们前端开发中，通常就是DOM层。

主要的作用是给用户展示各种信息。

###### Model层：

数据层

数据可能是我们固定的死数据，更多的是来自我们服务器，从网络上请求下来的数据。

在我们计数器的案例中，就是后面抽取出来的obj，当然，里面的数据可能没有这么简单。

###### VueModel层：

视图模型层

视图模型层是View和Model沟通的桥梁。

一方面它实现了Data Binding，也就是数据绑定，将Model的改变实时的反应到View中

另一方面它实现了DOM Listener，也就是DOM监听，当DOM发生一些事件(点击、滚动、touch等)时，可以监听到，并在需要的情况下改变对应的Data。

#### 1.5. 创建Vue时, options可以放那些东西

p详细解析： [https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E6%95%B0%E6%8D%AE](https://cn.vuejs.org/v2/api/)

* el:

  类型：string | HTMLElement

  作用：决定之后Vue实例会管理哪一个DOM

* data:

  类型：Object | Function （组件当中data必须是一个函数）

  作用：Vue实例对应的数据对象

* methods:

  类型：{ [key: string]: Function }

  作用：定义属于Vue的一些方法，可以在其他地方调用，也可以在指令中使用。

* 生命周期函数

  ![image-20210502215258637](C:\Users\你好啊\AppData\Roaming\Typora\typora-user-images\image-20210502215258637.png)

### 二.插值语法

* mustache(胡须)语法

  ```
   <h2>{{counter}}</h2>
  ```

* v-once

* ```
  <h2 v-once>{{counter}}</h2>
  ```

  该指令后面不需要跟任何表达式(比如之前的v-for后面是由跟表达式的)

  该指令表示元素和组件只渲染一次，不会随着数据的改变而改变。

* v-html

  某些情况下，我们从服务器请求到的数据本身就是一个HTML代码

  如果我们直接通过{{}}来输出，会将HTML代码也一起输出。

  但是我们可能希望的是按照HTML格式进行解析，并且显示对应的内容。

  如果我们希望解析出HTML展示

  可以使用v-html指令

  该指令后面往往会跟上一个string类型

  会将string的html解析出来并且进行渲染

  ```html
  <h2 v-html='link'></h2>
  ```

  ```
   data:{
         link:'<a href="http://www.baidu.com">百度一下</a>'
       },
  ```

* v-text

  v-text作用和Mustache比较相似：都是用于将数据显示在界面中

  v-text通常情况下，接受一个string类型

  ```
   <h2 v-text='message'></h2>
  ```

  ```
     data:{
        message:'你好啊，李银河',
     },
  ```

* v-pre: {{}}

  v-pre用于跳过这个元素和它子元素的编译过程，用于显示原本的Mustache语法。

  比如下面的代码：

  第一个h2元素中的内容会被编译解析出来对应的内容

  第二个h2元素中会直接显示{{message}}

  ```html
  <h2>{{message}}</h2> 
  <h2 v-pre>{{message}}</h2>    
  ```

  ```vue
    data:{
        message:'你好啊，李银河',
     },
  ```

  

* v-cloak: 斗篷

* 在某些情况下，我们浏览器可能会直接显然出未编译的Mustache标签。	

```css
 <style>
    [v-cloak] {
      display: none;
    }
  </style>
```

```
 <h2>{{message}}</h2>
```

```js
<script>
  // 在vue解析之前, div中有一个属性v-cloak
  // 在vue解析之后, div中没有一个属性v-cloak
  setTimeout(function () {
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊'
      }
    })
  }, 1000)
</script>
```



### 三. v-bind

主要作用是将值插入到我们模板的内容当中

- 比如动态绑定a元素的href属性
- 比如动态绑定img元素的src属性

- 作用：动态绑定属性
- 缩写：:
- 预期any (with argument) | Object (without argument)
- 参数attrOrProp (optional)

#### 3.1. v-bind绑定基本属性

* v-bind:href

  ```html
  <a v-bind:href='link'>百度</a>
  ```


- :src  (v-bind缩写)

  ```html
  <img :src='url' alt="">
  ```

  

#### 3.2. v-bind动态绑定class

- 对象语法

  对象语法的含义是:class后面跟的是一个对象。

   :class='{类名: boolean}'

  用法一：直接通过{}绑定一个类

  ```html
  <h2 :class="{'active': isActive}">Hello World</h2>
  ```

  用法二：也可以通过判断，传入多个值

  ```html
  <h2 :class="{'active': isActive, 'line': isLine}">Hello World</h2>
  ```

  用法三：和普通的类同时存在，并不冲突

  注：如果isActive和isLine都为true，那么会有title/active/line三个类

  ```html
  <h2 class="title" :class="{'active': isActive, 'line': isLine}">Hello World</h2>
  ```

  用法四：如果过于复杂，可以放在一个methods或者computed中

  注：classes是一个计算属性

  ```html
  <h2 class="title" :class="classes">Hello World</h2>
  ```

- 数组语法: 

  数组语法的含义是:class后面跟的是一个数组。

  ###### 数组语法有下面这些用法：

  用法一：直接通过{}绑定一个类

  ```html
  <h2 :class="['active']">Hello World</h2>
  ```

  用法二：也可以传入多个值

  ```html
  <h2 :class=“[‘active’, 'line']">Hello World</h2>
  ```

  用法三：和普通的类同时存在，并不冲突

  注：会有title/active/line三个类

  ```html
  <h2 class="title" :class=“[‘active’, 'line']">Hello World</h2>
  ```

  用法四：如果过于复杂，可以放在一个methods或者computed中

  注：classes是一个计算属性

  ```html
  <h2 class="title" :class="classes">Hello World</h2>
  ```

#### 3.3. v-bind动态绑定style

我们可以利用v-bind:style来绑定一些CSS内联样式。

在写CSS属性名的时候，比如font-size

我们可以使用驼峰式 (camelCase) fontSize 

或短横线分隔 (kebab-case，记得用单引号括起来) ‘font-size’

* 对象语法:

  ```html
  :style="{color: currentColor, fontSize: fontSize + 'px'}"
  ```

  style后面跟的是一个对象类型

  对象的key是CSS属性名称

  对象的value是具体赋的值，值可以来自于data中的属性

* 数组语法:

  ```html
  <div v-bind:style="[baseStyles, overridingStyles]"></div>
  ```

  style后面跟的是一个数组类型       多个值以，分割即可

### 四. 计算属性

我们知道，在模板中可以直接通过插值语法显示一些data中的数据。

但是在某些情况，我们可能需要对数据进行一些转化后再显示，或者需要将多个数据结合起来进行显示

比如我们有firstName和lastName两个变量，我们需要显示完整的名称。

但是如果多个地方都需要显示完整的名称，我们就需要写多个{{firstName}} {{lastName}}

我们可以将上面的代码换成计算属性：

OK，我们发现计算属性是写在实例的computed选项中的。

* 案例一: firstName+lastName

  ```html
     <div>{{name}}</div>
  ```

  ```js
  data:{
   firstName: "kobe",
    lastName: "blyant",
  }
  ```

  ```js
    computed: {
                  name(){
                      return this.firstName + ' ' + this.lastName
                         },           
              }
  ```

  

* 案例二: books -> price

```html
<div>{{totalPrice}}</div>
```

```js
data:{
books:[
    {name:"百年孤独",price:50,count:2},
    {name:"霍乱时期的爱情",price:60,count:1},
    {name:"肖申克的救赎",price:50,count:2}
]
}
```

```js
 computed: {
                name(){
                    return this.firstName + ' ' + this.lastName
                       },
                    totalPrice(){
                        return this.books.reduce((total,b) =>{//高阶函数
                            return total + b.price * b.count
                        },0)
                    }
                        
            }
```

### 五. 计算属性

#### 5.1. 计算属性的本质

每个计算属性都包含一个getter和一个setter

在上面的例子中，我们只是使用getter来读取。

在某些情况下，你也可以提供一个setter方法（不常用）。

需要写setter的时候，代码如下

* fullname: {set(), get()}

  ```js
      fullName:{
                          get(){
                              console.log('调用了get函数');
                              return this.firstName +' '+ this.lastName
                          },
                          set(newValue){
                              console.log('调用了set函数');
                              const names=newValue.split('');
                              this.firstName=name[0]
                              this.lastName=name[1]
  
                          }
                      }
  ```

  

#### 5.2. 计算属性和methods对比

* 计算属性在多次使用时, 只会调用一次.

* 它是有缓存的

  ```html
  <div>{{getFullName()}}</div>
  <div>{{getFullName()}}</div>
  <div>{{getFullName()}}</div>
  <div>-----------------</div>
  <div>{{newFullName}}</div>
  <div>{{newFullName}}</div>
  <div>{{newFullName}}</div>
  ```

  ```js
   methods: {
           
           getFullName(){
           console.log('执行了methods方法');
           return this.firstName +' '+ this.lastName
  
            }
              },
              computed: {
               newFullName(){
               console.log('执行了计算属性');
                return this.firstName +' '+ this.lastName
                }       
              },
  ```

  ###### 结果： getFullName()打印了3次，newFullName()打印了1次



### 六. 事件监听

在前端开发中，我们需要经常和用于交互。

这个时候，我们就必须监听用户发生的时间，比如点击、拖拽、键盘事件等等

在Vue中如何监听事件呢？使用v-on指令

**v-on****介绍**

**作用**：绑定事件监听器

**缩写**：@

**预期**：Function | Inline Statement | Object

**参数**：event

#### 6.1. 事件监听基本使用

v-on也有对应的语法糖：

v-on:click可以写成@click

```html
<button v-on:click='sub'>-</button>
<h2>{{counter}}</h2>
<button @click='add'>+</button>
```

#### 6.2. 参数问题

当通过methods中定义方法，以供@click调用时，需要**注意参数问题**：

情况一：如果该方法不需要额外参数，那么方法后的()可以不添加。

但是注意：如果方法本身中有一个参数，那么会默认将原生事件event参数传递进去

情况二：如果需要同时传入某个参数，同时需要event时，可以通过$event传入事件。

* btnClick
* btnClick(event)
* btnClick(abc, event) -> $event

```html
<button @click='handleAdd'>+1</button>
<h2>{{counter}}</h2>
<button @click='handleAddTen(10,$event)'>+10</button>
```

```js
   handleAdd(event){
   console.log(event);
   this.counter++
   },
   handleAddTen(count,event){
   console.log(event);
   this.counter+=10
   }
```

#### 6.3. 修饰符

在某些情况下，我们拿到event的目的可能是进行一些事件处理。

Vue提供了修饰符来帮助我们方便的处理一些事件：

.stop - 调用 event.stopPropagation()。

.prevent - 调用 event.preventDefault()。

.{keyCode | keyAlias} - 只当事件是从特定键触发时才触发回调。

.native - 监听组件根元素的原生事件。

.once - 只触发一次回调。

* stop

  ```html
   <!--阻止冒泡事件-->
   <button @click.stop='doThis'></button>
  ```

* prevent

  ```html
  <!--阻止默认行为-->
  <button @click.prevent='doThis'></button>
  ```

* .enter

  ```html
   <!--修饰符，键别名-->
   <input @keyup.enter='onEnter'>
   <!--修饰符，键代码-->
   <input @keyup.13='onEnter'>
  ```

* .once

  ```html
  <!--点击只会触发一次-->
  <button @click.once='doThis'>1</button>
  ```

  ```html
     <!--串行修饰符-->
   <button @click.stop.prevent='doThis'></button>
  ```

### 七. 条件判断

v-if的原理：

v-if后面的条件为false时，对应的元素以及其子元素不会渲染。

也就是根本没有不会有对应的标签出现在DOM中

#### 7.1. v-if/v-else-if/v-else

```html
<div v-if='score>=90'>优
<div v-else-if='score>=80
<div v-else-if='score>=60
<div v-else> 不及格</div>
```

```js
 data: {
     score:89
 },
```

#### 7.2. 登录小案例

```html
<div v-if="type==='username'">
            <span>用户名</span><input type="text" placeholder="请输入用户名">
        </div>
        <div v-else="type==='email'">
            <span>邮箱</span><input type="text" placeholder="请输入邮箱">
        </div>
        <button @click='change'>切换类型</button>
```

```js
data: {
      type:"username" 
       },
       methods: {
        change(){
         this.type=this.type==="username" ? "email" : "username"
         }
            }
```

小问题：

如果我们在有输入内容的情况下，切换了类型，我们会发现文字依然显示之前的输入的内容。

但是按道理讲，我们应该切换到另外一个input元素中了。

在另一个input元素中，我们并没有输入内容。

为什么会出现这个问题呢？

问题解答：

这是因为Vue在进行DOM渲染时，出于性能考虑，会尽可能的复用已经存在的元素，而不是重新创建新的元素。

在上面的案例中，Vue内部会发现原来的input元素不再使用，直接作为else中的input来使用了。

解决方案：

如果我们不希望Vue出现类似重复利用的问题，可以给对应的input添加key

并且我们需要保证key的不同

```html
<input type="text" placeholder="请输入用户名" key="username-input">
       
<input type="text" placeholder="请输入邮箱" key="username-email">
```



#### 7.3. v-show

- v-show和v-if区别

     v-show的用法和v-if非常相似，也用于决定一个元素是否渲染：

- v-if和v-show对比

     v-if和v-show都可以决定一个元素是否渲染，那么开发中我们如何选择呢？

     v-if当条件为false时，压根不会有对应的元素在DOM中。

     v-show当条件为false时，仅仅是将元素的display属性设置为none而已。

- 开发中如何选择呢？

  当需要在显示与隐藏之间切片很频繁时，使用v-show

  当只有一次切换时，通过使用v-if

  ```html
   <div v-if='isShow'  @click='toggleShow'>v-if</div>
     <div v-show='isShow'>v-show</div>
  ```

  ```js
  toggleShow(){
        this.isShow=!this.isShow
        }
  ```

### 八. 循环遍历

当我们有一组数据需要进行渲染时，我们就可以使用v-for来完成。

v-for的语法类似于JavaScript中的for循环。

格式如下：

item in items。

如果在遍历的过程中不需要使用索引值

v-for="movie in movies"

依次从movies中取出movie，并且在元素的内容中，我们可以使用Mustache语法，来使用movie

如果在遍历的过程中，我们需要拿到元素在数组中的索引值呢？

语法格式：v-for=(item, index) in items

其中的index就代表了取出的item在原数组的索引值

注意：cli3需要带:key='index'

#### 8.1. 遍历数组

```html
<ul>
    <li v-for="item in movies">{{item}}</li>
    <div>---------------------------</div>
    <li v-for='(movie,index) in movies' :key='index'>{{index}},{{movie}}</li>
 </ul>
```

```js
data: {
          movies: ['星际穿越', '大话西游', '少年派', '盗梦空间'],
    },
```

#### 8.2. 遍历对象

* value
* value, key
* value, key, index

```html
 <li v-for="(value,key,index) in info" >{{value}}--{{key}}--{{index}}</li>
```

```js
info:{
    name:'gm',
    age:24,
    height:160,
            }
```

官方推荐我们在使用v-for时，给对应的元素或组件添加上一个:key属性。

为什么需要这个key属性呢（了解）？

这个其实和Vue的虚拟DOM的Diff算法有关系。

这里我们借用[React’s](https://link.zhihu.com/?target=https://calendar.perfplanet.com/2013/diff/)[ diff algorithm](https://link.zhihu.com/?target=https://calendar.perfplanet.com/2013/diff/)中的一张图来简单说明一下：

当某一层有很多相同的节点时，也就是列表节点时，我们希望插入一个新的节点

我们希望可以在B和C之间加一个F，Diff算法默认执行起来是这样的。

即把C更新成F，D更新成C，E更新成D，最后再插入E，是不是很没有效率？

所以我们需要使用key来给每个节点做一个唯一标识

Diff算法就可以正确的识别此节点

找到正确的位置区插入新的节点。

##### 所以一句话，key的作用主要是为了高效的更新虚拟DOM

#### 8.3. 数组哪些方法是响应式的

因为Vue是响应式的，所以当数据发生变化时，Vue会自动检测数据变化，视图会发生对应的更新。

Vue中包含了一组观察数组编译的方法，使用它们改变数组也会触发视图的更新。

###### 操作数组：

push()，往后面添加元素 

```js
 this.movies.push('肖申克的救赎','我的姐姐');
```

pop(),  从后面开始删除元素

```js
this.movies.pop();
```

shift() ,  从前面添加元素

```
this.movies.unshift('肖申克的救赎','我的姐姐')
```

unshift(),  从前面开始删除元素

```js
this.movies.shift()
```

splice()

   splice作用: 删除元素/插入元素/替换元素

​    // 删除元素: 第二个参数传入你要删除几个元素(如果没有传,就删除后面所有的元素)

​    // 替换元素: 第二个参数, 表示我们要替换几个元素, 后面是用于替换前面的元素

​    // 插入元素: 第二个参数, 传入0, 并且后面跟上要插入的元素

```js
this.letters.splice(1, 3, 'm', 'n', 'l', 'x')
this.letters.splice(1, 0, 'x', 'y', 'z')
```

sort()

排序数组，

```js
this.books.sort((a,b) => {
return a.id-b.id;//升序
 return b.id-a.id;//降序
})
```

reverse()，反向数组

```js
this.movies.reverse();
```



```html
  <li v-for="item in movies">{{item}}</li>
  <button @click='updata'>修改</button>
    <div>---------------------------</div>
  <li v-for="(item,index) in books">{{index}},{{item}}</li>
```



```js
data: {
                movies: ['1,星际穿越', '2,大话西游', '3,少年派', '4,盗梦空间'],
                books:[
                    {id:0,name:"百年孤独",price:50,count:2},
                    {id:1,name:"霍乱时期的爱情",price:60,count:1},
                    {id:3,name:"肖申克的救赎1",price:50,count:3},
                    {id:2,name:"肖申克的救赎2",price:50,count:3}
                ]
            },
```

注意: 通过索引值修改数组中的元素

```js
   this.letters[0] = 'bbbbbb';

  this.letters.splice(0, 1, 'bbbbbb')
```

​     set(要修改的对象, 索引值, 修改后的值)

```js
    Vue.set(this.letters, 0, 'bbbbbb')
```



### 五. 书籍案例

```html
    <div id="app">

<table>
    <thead>
    <tr>
        <th></th>
        <th>书籍名称</th>
        <th>出版日期</th>
        <th>价格</th>
        <th>购买数量</th>
        <th>操作</th>
    </thead>
    <tbody>
        <tr v-for="(item,index) in books" :key="index">
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.date}}</td>
            <td>{{item.price}}</td>
            <td>
                <button v-bind:disabled="item.count <= 1" @click='sub(index)'>-</button>

                <span>{{item.count}}</span>
                <button @click='add(index)'>+</button>
            </td>
            <td><button @click='del(index)'>移除</button></td>
        </tr>   

    </tbody>

    </tr>
   

</table>
<h2>{{ totalPrice | shoewPrice}}</h2>

    </div>

```

```css
<style>
    table {
  border: 1px solid #e9e9e9;
  border-collapse: collapse;
  border-spacing: 0;
}

th, td {
  padding: 8px 16px;
  border: 1px solid #e9e9e9;
  text-align: left;
}
th {
  background-color: #f7f7f7;
  color: #5c6b77;
  font-weight: 600;
}
span{
    padding:0 5px;
}

</style>
```

```js
let vm=new Vue({
        el:"#app",

        data:{
            num:1,
            // total:0,
            status:false,
      books: [
      {
        id: 1,
        name: '《算法导论》',
        date: '2006-9',
        price: 85.00,
        count: 1
      },
      {
        id: 2,
        name: '《UNIX编程艺术》',
        date: '2006-2',
        price: 59.00,
        count: 1
      },
      {
        id: 3,
        name: '《编程珠玑》',
        date: '2008-10',
        price: 39.00,
        count: 1
      },
      {
        id: 4,
        name: '《代码大全》',
        date: '2006-3',
        price: 128.00,
        count: 1
      },
    ]

        }
,
methods:{
    add(index){
        this.books[index].count++
    },
    sub(index){
        this.books[index].count--
    },
    del(index){
        this.books.splice(index,1);
    }
},
computed:{
    totalPrice(){
       let total=0
         for(let i=0; i<this.books.length;i++){
           total+=this.books[i].price * this.books[i].count
        }   
        return total
     }    
},
filters:{
    shoewPrice(price){
        return  "￥" + price.toFixed(2)
    }
}

      })  
```



### 六. v-model的使用

表单控件在实际开发中是非常常见的。特别是对于用户信息的提交，需要大量的表单。

Vue中使用v-model指令来实现表单元素和数据的双向绑定。

###### 案例的解析：

当我们在输入框输入内容时

因为input中的v-model绑定了message，所以会实时将输入的内容传递给message，message发生改变。

当message发生改变时，因为上面我们使用Mustache语法，将message的值插入到DOM中，所以DOM会发生响应的改变。

- 所以，通过v-model实现了双向的绑定。


当然，我们也可以将v-model用于textarea元素

#### 6.1. v-model的基本使用

```html
 <input v-model='message' type="text" placeholder="">
    <h2>{{message}}</h2>
```

```js
data:{
  message:'',
} 
```

- v-model  =  v-bind:value v-on:input

  ```html
   <input v-model='message' type="text" placeholder="">
      <!-- 等价于 -->
      <input type="text"
      v-bind:value='message' v-on:input="message = $event.target.value"
      >
      <h2>{{message}}</h2>
  ```

  

#### 6.2. v-model和radio/checkbox/select

- ​	radio

  ```html
     <label for="male">
          <input type="radio" :value='abc' v-model="gender" id="male">男
      </label>
  
      <label for="famale">
          <input type="radio" :value='def' v-model="gender" id="male">女
      </label>
      <span>你的选择：{{gender}}</span>
  ```

  ```js
     data:{
          gender:'',
          abc:"男生",
          def:'女生'
      }  
  ```

- checkbox

  复选框分为两种情况：单个勾选框和多个勾选框

  ###### 单个勾选框：

  v-model即为布尔值。

  此时input的value并不影响v-model的值。

  ###### 多个复选框：

  当是多个复选框时，因为可以选中多个，所以对应的data中属性是一个数组。

  当选中某一个时，就会将input的value添加到数组中。

  ```html
   <label for="check">
          <input  type='checkbox' v-model='checked' id="check">同意协议
      </label>
      <p>是否选中：{{checked}}</p>
  
      <!-- 多个选择框 -->
      <label for="checkbox" ><input type="checkbox" v-model='hobbiles' value='篮球' >篮球 </label>
      <label for="checkbox" ><input type="checkbox" v-model='hobbiles' value='足球' >足球 </label>
      <label for="checkbox" ><input type="checkbox" v-model='hobbiles' value='排球' >排球 </label>
      <p>是否选中：{{hobbiles}}</p>
  ```

  ```js
  checked:false,
  hobbiles:[]
  ```

- select

  ```html
  <!-- 单选 -->
      <select name="" id="" v-model='mySelect'>
          <option value="apple">苹果</option>
          <option value="orange">橘子</option>
          <option value="banana">香蕉</option>
      </select>
      <h2>你选择的水果是：{{mySelect}}</h2>
  
      <!-- 多选 -->
      <select name="" id="" v-model='mySelects' multiple>
          <option value="apple">苹果</option>
          <option value="orange">橘子</option>
          <option value="banana">香蕉</option>
      </select>
      <h2>你选择的水果是：{{mySelects}}</h2>
  ```

  ```js
   mySelect:'apple',
   mySelects:[],
  ```

  

#### 6.3. 修饰符

* lazy

  lazy修饰符可以让数据在失去焦点或者回车时才会更新：

  ```html
   <input type="text" v-model.lazy="message1">
    <h2>{{message1}}</h2>
  ```

* number

  默认情况下，在输入框中无论我们输入的是字母还是数字，都会被当做字符串类型进行处理。
  但是如果我们希望处理的是数字类型，那么最好直接将内容当做数字处理。
  number修饰符可以让在输入框中输入的内容自动转成数字类型：

* ```html
   <input type="number" v-model="message2">
    <h2>{{message2}}-{{typeof message2}}</h2>
  ```

  

* trim

  如果输入的内容首尾有很多空格，通常我们希望将其去除

  ptrim修饰符可以过滤内容左右两边的空格

  ```html
    <input type="text" v-model.trim="message3">
    <h2>{{message3}}</h2>
  ```

  ```js
   data: {
      	message1: '',
  	    message2: 0,
          message3: ''
      }
  ```

### 七. 组件化开发

#### 7.1. 认识组件化

人面对复杂问题的处理方式：

任何一个人处理信息的逻辑能力都是有限的

所以，当面对一个非常复杂的问题时，我们不太可能一次性搞定一大堆的内容。

但是，我们人有一种天生的能力，就是将问题进行拆解。

如果将一个复杂的问题，拆分成很多个可以处理的小问题，再将其放在整体当中，你会发现大的问题也会迎刃而解。

###### 组件化也是类似的思想：

如果我们将一个页面中所有的处理逻辑全部放在一起，处理起来就会变得非常复杂，而且不利于后续的管理以及扩展。

但如果，我们讲一个页面拆分成一个个小的功能块，每个功能块完成属于自己这部分独立的功能，那么之后整个页面的管理和维护就变得非常容易了。

- 组件化是Vue.js中的重要思想

  它提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用。

  任何的应用都会被抽象成一颗组件树。

- 组件化思想的应用：

  有了组件化的思想，我们在之后的开发中就要充分的利用它。

  尽可能的将页面拆分成一个个小的、可复用的组件。

  这样让我们的代码更加方便组织和管理，并且扩展性也更强。

  所以，组件是Vue开发中，非常重要的一个篇章，要认真学习。

#### 7.2. 组件的基本使用

组件的使用分成三个步骤：

1. 创建组件构造器
2. 注册组件
3. 使用组件。

我们来看看通过代码如何注册组件

查看运行结果：

和直接使用一个div看起来并没有什么区别。

但是我们可以设想，如果很多地方都要显示这样的信息，我们是不是就可以直接使用<my-cpn></my-cpn>来完成呢？

```html

<div id="app">
  <my-cpn></my-cpn>
  <my-cpn></my-cpn>
</div>
  <my-cpn></my-cpn>
<script>
  // 1.创建组件构造器
  const cpn = Vue.extend({
    template: `
      <div>
        <h2>组件标题</h2>
        <p>我是组件的内容</p>
      </div>
    `
  })

  // 2.注册组件(全局注册)，并定义名称
  Vue.component('my-cpn', cpn)

  const app = new Vue({
    el: '#app',
    data: {

    }
  })
</script>

```

1.Vue.extend()：

调用Vue.extend()创建的是一个组件构造器。 

通常在创建组件构造器时，传入template代表我们自定义组件的模板。

该模板就是在使用到组件的地方，要显示的HTML代码。

事实上，这种写法在Vue2.x的文档中几乎已经看不到了，它会直接使用下面我们会讲到的语法糖，但是在很多资料还是会提到这种方式，而且这种方式是学习后面方式的基础。

2.Vue.component()：

调用Vue.component()是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名称。

所以需要传递两个参数：1、注册组件的标签名 2、组件构造器

3.组件必须挂载在某个Vue实例下，否则它不会生效。

我们来看下面我使用了三次<my-cpn></my-cpn>

而第三次其实并没有生效



#### 7.3. 全局组件和局部组件

当我们通过调用Vue.component()注册组件时，组件的注册是全局的

这意味着该组件可以在任意Vue示例下使用。

如果我们注册的组件是挂载在某个实例中, 那么就是一个局部组件

- 全局组件

  ```html
  <div id="app1">
    <cpn></cpn>
  </div>
  <div id="app2">
    <cpn></cpn>
  </div>
  <cpn></cpn>
  <script>
    const cpn = Vue.extend({
      template: `
      <div>
        <h2>我是标题</h2>
        <p>我是组件中的内容</p>
      </div>
      `
    })
    Vue.component('cpn', cpn)
  
    const app1 = new Vue({
      el: '#app1'
    })
  
    const app2 = new Vue({
  	  el: '#app2'
    })
  </script>
  
  ```

- 局部组件

  ```html
  <div id="app">
    <cpn></cpn>
  </div>
  <div id="app2">
    <cpn></cpn>
  </div>
  <script>
  	const cpn = Vue.extend({
  		template: `
      <div>
        <h2>我是标题</h2>
        <p>我是组件中的内容</p>
      </div>
      `
  	})
  
    const app = new Vue({
      el: '#app',
      components: {
      	'cpn': cpn
      }
    })
  
    const app2 = new Vue({
      el: '#app2'
    })
  </script>
  
  ```

  

#### 7.4. 父组件和子组件

组件和组件之间存在层级关系

而其中一种非常重要的关系就是父子组件的关系

我们来看通过代码如何组成的这种层级关系：

父子组件错误用法：以子标签的形式在Vue实例中使用

因为当子组件注册到父组件的components时，Vue会编译好父组件的模块

该模板的内容已经决定了父组件将要渲染的HTML（相当于父组件中已经有了子组件中的内容了）

<child-cpn></child-cpn>是只能在父组件中被识别的。

类似这种用法，<child-cpn></child-cpn>是会被浏览器忽略的。

```html
<div id="app">
  <cpn2></cpn2>
  <!--错误用法-->
  <cpn1></cpn1>
</div>
<script>
  // 1.注册一个子组件
  const cpn1 = Vue.extend({
    template: `
      <div>
        <h2>我是cpn1的标题</h2>
        <p>我是cpn1的内容,哈哈哈</p>
      </div>
    `
  })
  // 2.注册一个父组件
  const cpn2 = Vue.extend({
	  template: `
      <div>
        <h2>我是cpn2的标题</h2>
        <p>我是cpn2的内容,哈哈哈</p>
        <cpn1></cpn1>
      </div>
    `,
    components: {
	  	'cpn1': cpn1
    }
  })

  const app = new Vue({
    el: '#app',
    components: {
    	'cpn2': cpn2
    }
  })
</script>

```



#### 7.5. 注册的语法糖

在上面注册组件的方式，可能会有些繁琐。

Vue为了简化这个过程，提供了注册的语法糖。

主要是省去了调用Vue.extend()的步骤，而是可以直接使用一个对象来代替。

###### 语法糖注册全局组件和局部组件：

```html
	/**
   * 1.注册全局组件的语法糖
	 */ 
Vue.component('cpn', {
	  template: `
      <div>
        <h2>我是cpn的标题</h2>
        <p>我是cpn的内容,哈哈哈</p>
      </div>
    `
  })
      
```

```js
 const app = new Vue({
    el: '#app',
    //注册局部组件
    components:{
        'cpn1':{
            template:`
            <div>这是my-cpn1组件</div>
            `
        }
    },
    data: {
    }
  })
```



#### 7.6. 模板的分类写法

我们通过语法糖简化了Vue组件的注册过程，另外还有一个地方的写法比较麻烦，就是template模块写法。

如果我们能将其中的HTML分离出来写，然后挂载到对应的组件上，必然结构会变得非常清晰。

Vue提供了两种方案来定义HTML模块内容：

使用<script>标签

使用<template>标签

- script

```html
<div id="app">
  <cpn1></cpn1>
</div>
<script type="text/x-template" id="mycpn1">
    <div>我是script创建的</div>
</script>
<script>
 
  const app = new Vue({
    el: '#app',
    components:{
        'cpn1':{
            template:'#mycpn1'
        },
    },

  })
</script>

```

- template

```html
<div id="app">
  <cpn2></cpn2>
</div>
<template id="mycpn2">
    <div>我是template创建的</div>
</template>
<script>
  const app = new Vue({
    el: '#app',
    components:{
        'cpn2':{
            template:'#mycpn2'
        }
    },
  })
</script>
```

#### 7.7. 数据的存放

组件是一个单独功能模块的封装：

这个模块有属于自己的HTML模板，也应该有属性自己的数据data。

组件中的数据是保存在哪里呢？顶层的Vue实例中吗？

我们先来测试一下，组件中能不能直接访问Vue实例中的data

- 子组件不能直接访问父组件

```html
<div id="app">
  <cpn2></cpn2>
</div>
<template id="mycpn2">
    <div>{{message}}</div>
</template>
<script>
  const app = new Vue({
    el: '#app',
    components:{
        'cpn2':{
            template:'#mycpn2'
        }
    },
    data:{
    message:"我是data"
}
  })
</script>
```

我们发现不能访问，而且即使可以访问，如果将所有的数据都放在Vue实例中，Vue实例就会变的非常臃肿。

###### 结论：Vue组件应该有自己保存数据的地方。

- 子组件中有自己的data, 而且必须是一个函数.

- ##### 组件自己的数据存放在哪里呢?

组件对象也有一个data属性(也可以有methods等属性，下面我们有用到)

只是这个data属性必须是一个函数

而且这个函数返回一个对象，对象内部保存着数据

```html
<div id="app">
  <h2>{{message}}</h2>
  <cpn></cpn>
</div>
<template id="cpn">
  <div>
    <h2>组件标题</h2>
    <p>组件的内容: {{message}}</p>
  </div>
</template>
<script>
  const app = new Vue({
    el: '#app',
    data: {
    	message: '今天天气不错!'
    },
    components: {
    	'cpn': {
    		template: '#cpn',
        data() {
    			return {
    				message: '组件中的天气不错!'
          }
        }
      }
    }
  })

```

* 为什么必须是一个函数.

  为什么data在组件中必须是一个函数呢?

  1.首先，如果不是一个函数，Vue直接就会报错。

  2.其次，原因是在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响。

  ```html
  <div id="app">
    <cpn></cpn>
    <cpn></cpn>
  </div>
  
  <template id="cpn">
    <div>
      <h2>{{counter}}</h2>
      <button @click="btnClick">按钮</button>
    </div>
  </template>
  <script>
    const obj = {
    	counter: 0
    }
    const app = new Vue({
      el: '#app',
      components: {
      	'cpn': {
      		template: '#cpn',
          data() {
      			return {
      				counter: 0
            }
          },
          methods: {
      			btnClick() {
      				this.counter++
            }
          }
        }
      }
    })
  </script>
  ```

  

#### 7.8. 父子组件的通信

我们提到了子组件是不能引用父组件或者Vue实例的数据的。

但是，在开发中，往往一些数据确实需要从上层传递到下层：

比如在一个页面中，我们从服务器请求到了很多的数据。

其中一部分数据，并非是我们整个页面的大组件来展示的，而是需要下面的子组件进行展示。

这个时候，并不会让子组件再次发送一个网络请求，而是直接让大组件**(父组件)将数据传递给小组件(子组件)**。

如何进行父子组件间的通信呢？Vue官方提到

通过props向子组件传递数据

通过事件向父组件发送消息

parent（父组件）---(通过  props)--> child(子组件)

child（子组件）---(通过  $emit Events)--> parent(父组件)

在下面的代码中，我直接将Vue实例当做父组件，并且其中包含子组件来简化代码。

真实的开发中，Vue**实例和子组件的通信和父组件和子组件的通信**过程是一样的。

* 父传子: props

  ```html
  <div id="app">
    <child-cpn :message='message1'></child-cpn>
  </div>
  <template id="cpn">
    <div>
      <h2>组件标题</h2>
      <p>组件的内容: {{message}}</p>
    </div>
  </template>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
      	message1: '今天天气不错!'
      },
      components: {
      	'childCpn': {
      		template: '#cpn',
          props:['message'],
        }
      }
    })
  </script>
  ```

  上面我们的props选项是使用一个数组。

  我们说过，除了数组之外，我们也可以使用对象，当需要对props**进行类型等验证时**，就需要对象写法了。

  验证都支持哪些数据类型呢？

  1.String

  2.Number

  3.Boolean

  4.Array

  6.Object

  7.Date

  8.Function

  9.Symbol

  当我们有自定义构造函数时，验证也支持自定义的类型

  ```js
  
    <script>
  	class Proson(){
  		consttuctor(name,age){
  			this.name=name,
  			this.age=age
  			  }
  		toString(){
  			return `姓名:${this.name}  年龄：${this.age}`
  			  }
  
  	  }
      vue.components('my-component', {
        props: {
          //基础的类型检查，（null匹配任何类型）
          propA: Number,
          //可能多个类型
          propB: [Number, String],
          //必填的字符串
          propC: {
            type: String,
            required: true,
          },
          //带有默认的数字
          propD: {
            type: Number,
            default: 100,
          },
          //带有默认的对象	    
          propE: {
            type: Objetc,
            //对象的默认值必须从工厂函数获取，
            default: function () {
              return { message: 'hello' }
            }
          },
          //自定义验证函数
          propF: {
            validator: function (value) {
              //这个字必须匹配下列字符串中的一个
              return ['success', 'wraning', 'danger'].indexOf(value) !== -1
            }
          },
  	propG:{
  		type:Person,
  		  }
        }
    })
    </script>
  ```

  

* 子传父: $emit

  props用于父组件向子组件传递数据，还有一种比较常见的是子组件传递数据或事件到父组件中。

  我们应该如何处理呢？这个时候，我们需要使用**自定义事件**来完成。

  什么时候需要自定义事件呢？

  当子组件需要向父组件传递数据时，就要用到自定义事件了。

  我们之前学习的v-on不仅仅可以用于监听DOM事件，也可以用于组件间的自定义事件。

  自定义事件的流程：

  在子组件中，通过$emit()来触发事件。

  在父组件中，通过v-on来监听子组件事件。

  我们来看一个简单的例子：

  我们之前做过一个两个按钮+1和-1，点击后修改counter。

  我们整个操作的过程还是在子组件中完成，但是之后的展示交给父组件。

  这样，我们就需要将子组件中的counter，传给父组件的某个属性，比如total。

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>子级向父级传递数据</title>
  </head>
  <body>
  <div id="app">
      //2.父组件接受用changeTotal函数接受increment和decrement的事件
      <child-cpn @increment='changeTotal' @decrement='changeTotal'></child-cpn>
      <h3>{{total}}</h3>
  </div>
  <template id="child">
      <div>
          <button @click='decrement'>-</button>
          <button @click='increment'>+</button>
      </div>
  </template>
  <script src="./js/vue.js"></script>
  <script>
      let vm=new Vue({
          el:"#app",
          data:{
              total:0,
          },
          methods:{
              //3.处理事件和接受参数counter
              changeTotal(counter){
                  this.total=counter
              }
          },
          components:{
              'child-cpn':{
                  template:"#child",
                  data(){
                      return{
                          counter:0
                      }
                  },
                  methods:{
                      increment(){
                          this.counter++;
                          //1.给父组件传递事件（increment）和参数（counter）
                          this.$emit('increment',this.counter)
                      },
                      decrement(){
                          this.counter--;
                           //1.给父组件传递事件（increment）和参数（counter）
                          this.$emit('decrement',this.counter)
                      }
                  }
              }
          }
      })
  </script>
  </body>
  </html>
  ```

- 父子组件的访问方式： $children

  ```html
    <div id="app">
          <child-cpna></child-cpna>
          <child-cpnb></child-cpnb>
          <button @click='showChild'>显示</button>
      </div>
      <template id="child1">
          <div>我是子组件信息1</div>
      </template>
      <template id="child2">
          <div>我是子组件信息2</div>
      </template>
      <script>
          let vm = new Vue({
              el: "#app",
              methods: {
                  showChild() {
                      // console.log(this.$children.message);
                      for( let i in this.$children){
                          const cpn=this.$children[i].message
                          console.log(cpn);
                      }
                  }
              },
             components: {
                  'child-cpna': {
                      template: "#child1",
                      data() {
                          return {
                              message: "我是组件1的message"
                          }
                      }
                  },
                  'child-cpnb': {
                      template: "#child2",
                      data() {
                          return {
                              message: "我是组件2的message"
                          }
                      }
                  }
              }
          })
      </script>
  
  ```

- 父子组件的访问方式： $refs

  $children的缺陷：

  通过$children访问子组件时，是一个数组类型，访问其中的子组件必须通过索引值。

  但是当子组件过多，我们需要拿到其中一个时，往往不能确定它的索引值，甚至还可能会发生变化。

  有时候，我们想明确获取其中一个特定的组件，这个时候就可以使用$refs

  $refs的使用：

  $refs和ref指令通常是一起使用的。

  首先，我们通过ref给某一个子组件绑定一个特定的ID。

  其次，通过this.$refs.ID就可以访问到该组件了。

  ```html
        <child-cpna ref='child1'></child-cpna>
          <child-cpnb ref='child2'></child-cpnb>
          <button @click='showRefsCpn'>通过refs访问子组件</button>
          
  ```

  ```js
     methods: {
                  showRefsCpn() {
                      console.log(this.$refs.child1.message);
                      console.log(this.$refs.child2.message);
                  }
              },
  ```

- 父子组件的访问方式： $parent	

  ```js
   this.$parent.message
  ```

- 非父子组件通信

  刚才我们讨论的都是父子组件间的通信，那如果是非父子关系呢?

  非父子组件关系包括多个层级的组件，也包括兄弟组件的关系。

  在Vue1.x的时候，可以通过$dispatch和$broadcast完成

  $dispatch用于向上级派发事件

  $broadcast用于向下级广播事件

  但是在Vue2.x都被取消了

  在Vue2.x中，有一种方案是通过**中央事件总线**，也就是一个中介来完成。

  但是这种方案和直接使用Vuex的状态管理方案还是逊色很多。

  并且Vuex提供了更多好用的功能，所以这里我们暂且不讨论这种方案，后续我们专门学习Vuex的状态管理。
  
  

#### 7.9 slot

slot翻译为插槽：

在生活中很多地方都有插槽，电脑的USB插槽，插板当中的电源插槽。

插槽的目的是让我们原来的设备具备更多的扩展性。

比如电脑的USB我们可以插入U盘、硬盘、手机、音响、键盘、鼠标等等。

组件的插槽：

组件的插槽也是为了让我们封装的组件更加具有扩展性。

让使用者可以决定组件内部的一些内容到底展示什么。

栗子：移动网站中的导航栏。

移动开发中，几乎每个页面都有导航栏。

导航栏我们必然会封装成一个插件，比如nav-bar组件。

一旦有了这个组件，我们就可以在多个页面中复用了。

但是，每个页面的导航是一样的吗？No

##### slot基本使用

了解了为什么用slot，我们再来谈谈如何使用slot？

在子组件中，使用特殊的元素<slot>就可以为子组件开启一个插槽。

该插槽插入什么内容取决于父组件如何使用。

我们通过一个简单的例子，来给子组件定义一个插槽：

<slot>中的内容表示，如果没有在该组件中插入任何其他内容，就默认显示该内容

有了这个插槽后，父组件如何使用呢？

```html
<div id="app">
    <child-cpn>
        <div>我是替代的插槽</div>
    </child-cpn>
</div>
<template id="child">
 <div> <slot>我是默认的插槽</slot></div>
</template>
<script>
    let vm=new Vue({
        el:"#app",
        data:{
        },
        components:{
            'child-cpn':{
                template:"#child",
            }
        }
    })
</script>

```

##### 具名插槽slot

<slot name='myslot'></slot>

```html
    <child-cpn>
     <!--vue3.0学法，与2.0不同的是加了一个template标签 -->
        <template v-slot:header>
            <h1>Here might be a page title</h1>
          </template>
        
          <template v-slot:footer>
            <p>Here's some contact info</p>
          </template>
    </child-cpn>
    
    <template id="child">
     <div>
     <!--必须有个标签包着 -->
            <div>
              <slot name="header"></slot>
            </div>
            <div>
              <slot name="footer"></slot>
            </div>
          </div>


</template>
    
```

- 作用域插槽：准备

作用域插槽是slot一个比较难理解的点，而且官方文档说的又有点不清晰。

这里，我们用一句话对其做一个总结，然后我们在后续的案例中来体会：

父组件替换插槽的标签，但是内容由子组件来提供。

我们先提一个需求：

子组件中包括一组数据，比如：pLanguages: ['JavaScript', 'Python', 'Swift', 'Go', 'C++']

需要在多个界面进行展示：

某些界面是以水平方向一一展示的，

某些界面是以列表形式展示的，

某些界面直接展示一个数组

内容在子组件，希望父组件告诉我们如何展示，怎么办呢？

利用slot作用域插槽就可以了

我们来看看子组件的定义：

```html
<template id="child">
       <div>
              <slot :data='pLanguages'></slot>
          </div>

</template>
  components:{
            'child-cpn':{
                template:"#child",
                data(){
                    return{
                        pLanguages: ['JavaScript', 'Python', 'Swift', 'Go', 'C++']
                    }
                },
            }
        }
```



作用域插槽：使用

在父组件使用我们的子组件时，从子组件中拿到数据：

我们通过<template slot-scope="slotProps">获取到slotProps属性

在通过slotProps.data就可以获取到刚才我们传入的data了

```html
<div id="app">
    <child-cpn>
        <template slot-scope="slotProps">
            <ul>
                <li v-for='(item,index) in slotProps.data' :key="index">{{item}}</li>
            </ul>
        </template>
    </child-cpn>
</div>

<template id="child">
       <div>
              <slot :data='pLanguages'></slot>
          </div>

</template>

    let vm=new Vue({
        el:"#app",
        components:{
            'child-cpn':{
                template:"#child",
                data(){
                    return{
                        pLanguages: ['JavaScript', 'Python', 'Swift', 'Go', 'C++']
                    }
                },
            }
        }
    })

```

### 八，模块化开发

- JavaScript原始功能

  在网页开发的早期，js制作作为一种脚本语言，做一些简单的表单验证或动画实现等，那个时候代码还是很少的。

  那个时候的代码是怎么写的呢？直接将代码写在<script>标签中即可

  随着ajax异步请求的出现，慢慢形成了前后端的分离

  客户端需要完成的事情越来越多，代码量也是与日俱增。

  为了应对代码量的剧增，我们通常会将代码组织在多个js文件中，进行维护。

  但是这种维护方式，依然不能避免一些灾难性的问题。

- 使用模块作为出口

  我们可以使用将需要暴露到外面的变量，使用一个模块作为出口，什么意思呢？

  来看下对应的代码：

  我们做了什么事情呢？

  非常简单，在匿名函数内部，定义一个对象。

  给对象添加各种需要暴露到外面的属性和方法(不需要暴露的直接定义即可)。

  最后将这个对象返回，并且在外面使用了一个MoudleA接受。

  接下来，我们在man.js中怎么使用呢？

  我们只需要使用属于自己模块的属性和方法即可

  这就是模块最基础的封装，事实上模块的封装还有很多高级的话题：

  但是我们这里就是要认识一下为什么需要模块，以及模块的原始雏形。

  幸运的是，前端模块化开发已经有了很多既有的规范，以及对应的实现方案。

  常见的模块化规范：

  CommonJS、AMD、CMD，也有ES6的Modules

```js
<script>

        var moduleA=(function(){
            var obj={

            }
            obj.flag=true
            obj.myFunction=function(info) {
                console.log(info);
            }
            return obj
        })()

        if(moduleA.flag){
            console.log('小明是天才');
        }
        moduleA.myFunction('小明长的漂亮')

    </script>
```

##### CommonJS（了解）

- 导入与导出

```
  //CommonJS的导出
 module.exports={
            flag:true,
            test(a,b){
                return a+b
            },
            demo(a,b){
                return a-b
            }
        }
        //CommonJS的导入
        let {test,demo,flag }=require("moduleA");

        let _mA=require("moduleA");
        let test=_mA.test
        let demo=_mA.demo
        let flag=_mA.flag
```

##### export(导出)的使用

```
export let name ='gm'
export let age ='18'
export let height ='167'

//另一种写法
 let name ='gm'
 let age ='18'
 let height ='167'
 export {name,age,height}
```

- 导出函数或类

```js

 export  function test(content){
    console.log(content);
 }
 export class Person{
     constructor(){
        this.name=name,
        this.age=age

       
     }
     eat(){
    console.log(this.name+'在吃饭');
    }
 }
 export {test ,Person}
```

- export default

某些情况下，一个模块中包含某个的功能，我们并不希望给这个功能命名，而且让导入者可以自己来命名

这个时候就可以使用export default

```
 export default function(object){
     console.log(object)
 }
```

另外，**需要注意**：

export default在同一个模块中，不允许同时存在多个。

##### import使用

我们使用**export**指令导出了模块对外提供的接口，下面我们就可以通过**import**命令来加载对应的这个模块了

首先，我们需要在HTML代码中引入两个js文件，并且类型需要设置为module

```
  <script src="main.js" type="module"></script>
```

import指令用于导入模块中的内容，比如main.js的代码

```
 import {name,age,height} from './js/main.js';
          console.log(name);
```

如果我们希望某个模块中所有的信息都导入，一个个导入显然有些麻烦：

通过*可以导入模块中所有的export变量

但是通常情况下我们需要给*起一个别名，方便后续的使用

```
 import as info from './js/main.js';
          console.log(info.name,info.age,info.height);
```

### 九，webpack

##### **内容概述**

认识webpack

webpack的安装

webpack的起步

webpack的配置

loader的使用

webpack中配置Vue

plugin的使用

搭建本地服务器

##### 什么是Webpack？

这个webpack还真不是一两句话可以说清楚的。

我们先看看官方的解释：

At its core, **webpack** is a *static module bundler* for modern JavaScript applications. 

从本质上来讲，webpack是一个现代的JavaScript应用的静态**模块打包**工具。

但是它是什么呢？用概念解释概念，还是不清晰。

我们从两个点来解释上面这句话：**模块** 和 **打包**![image-20210604201240609](C:\文件\web\vue\vue-md-image\image-20210604201240609.png)



- 前端模块化：

  在前面学习中，我已经用了大量的篇幅解释了为什么前端需要模块化。

而且我也提到了目前使用前端模块化的一些方案：AMD、CMD、CommonJS、ES6。

在ES6之前，我们要想进行模块化开发，就必须借助于其他的工具，让我们可以进行模块化开发。

并且在通过模块化开发完成了项目后，还需要处理模块间的各种依赖，并且将其进行整合打包。

而webpack其中一个核心就是让我们可能进行模块化开发，并且会帮助我们处理模块间的依赖关系。

而且不仅仅是JavaScript文件，我们的CSS、图片、json文件等等在webpack中都可以被当做模块来使用（在后续我们会看到）。

这就是webpack中模块化的概念。

- 打包如何理解呢？

理解了webpack可以帮助我们进行模块化，并且处理模块间的各种复杂关系后，打包的概念就非常好理解了。

就是将webpack中的各种资源模块进行打包合并成一个或多个包(Bundle)。

并且在打包的过程中，还可以对资源进行处理，比如压缩图片，将scss转成css，将ES6语法转成ES5语法，将TypeScript转成JavaScript等等操作。

但是打包的操作似乎grunt/gulp也可以帮助我们完成，它们有什么不同呢？

- 和grunt/gulp的对比

  grunt/gulp的核心是Task

  我们可以配置一系列的task，并且定义task要处理的事务（例如ES6、ts转化，图片压缩，scss转成css）

  之后让grunt/gulp来依次执行这些task，而且让整个流程自动化。

  所以grunt/gulp也被称为前端自动化任务管理工具。

  我们来看一个gulp的task

  下面的task就是将src下面的所有js文件转成ES5的语法。

  并且最终输出到dist文件夹中。

  什么时候用grunt/gulp呢？

  如果你的工程模块依赖非常简单，甚至是没有用到模块化的概念。

  只需要进行简单的合并、压缩，就使用grunt/gulp即可。

  但是如果整个项目使用了模块化管理，而且相互依赖非常强，我们就可以使用更加强大的webpack了。

  所以，grunt/gulp和webpack有什么不同呢？

  grunt/gulp更加强调的是前端流程的自动化，模块化不是它的核心。

  webpack更加强调模块化开发管理，而文件压缩合并、预处理等功能，是他附带的功能。

##### webpack安装

安装webpack首先需要安装Node.js，Node.js自带了软件包管理工具npm

查看自己的node版本：

```
node -v
```

全局安装webpack(这里我先指定版本号3.6.0，因为vue cli2依赖该版本)

```
npm install webpack@3.6 -g
```

局部安装webpack（后续才需要）

```
npm install webpack@3.6.0 --save-dev
```

--save-dev是开发时依赖，项目打包后不需要继续使用的。

- 为什么全局安装后，还需要局部安装呢？

在终端直接执行webpack命令，使用的全局安装的webpack

当在package.json中定义了scripts时，其中包含了webpack命令，那么使用的是局部webpack

##### webpack的使用

注意：

在package.json中，devDependencies下添加包名和版本使用npm install --devDependencies可以直接下载全部的包

```
 "devDependencies": {
    "webpack": "^3.6.0",
    "webpack-cli": "^4.7.0",
    "babel-core": "^6.26.3",
    "babel-loader": "^7.1.5",
    "babel-preset-es2015": "^6.24.1",
    "css-loader": "^2.0.2",
    "file-loader": "^3.0.1",
    "less": "^3.9.0",
    "less-loader": "^4.1.0",
    "style-loader": "^0.23.1",
    "url-loader": "^1.1.2"
  },
```

```
npm install --devDependencies
```



###### 准备工作

我们创建如下文件和文件夹：

文件和文件夹解析：

dist文件夹：用于存放之后打包的文件

src文件夹：用于存放我们写的源文件

​      main.js：项目的入口文件。具体内容查看下面详情。

​      mathUtils.js：定义了一些数学工具函数，可以在其他地方引用，并且使用。具体内容查看下面的详情。

index.html：浏览器打开展示的首页html

package.json：通过npm init生成的，npm包管理的文件（暂时没有用上，后面才会用上）

mathUtils.js文件中的代码：

main.js文件中的代码：

##### js文件的打包

现在的js文件中使用了模块化的方式进行开发，他们可以直接使用吗？不可以。

因为如果直接在index.html引入这两个js文件，浏览器并不识别其中的模块化代码。

另外，在真实项目中当有许多这样的js文件时，我们一个个引用非常麻烦，并且后期非常不方便对它们进行管理。

我们应该怎么做呢？使用webpack工具，对多个js文件进行打包。

我们知道，webpack就是一个模块化的打包工具，所以它支持我们代码中写模块化，可以对模块化的代码进行处理。（如何处理的，待会儿在原理中，我会讲解）

另外，如果在处理完所有模块之间的关系后，将多个js打包到一个js文件中，引入时就变得非常方便了。

OK，如何打包呢？使用webpack的指令即可

```
webpack src/main.js dist/bundle.js   
```

"src/main.js"是将要打包文件的路径，"dist/bundle.js"是打包的目标文件

- 使用打包后的文件

  打包后会在dist文件下，生成一个bundle.js文件

  文件内容有些复杂，这里暂时先不看，后续再进行分析。

  bundle.js.html中引入即可文件，是webpack处理了项目直接文件依赖后生成的一个js文件，我们只需要将这个js文件在index

```
<script src="./dist/bundle.js"></script>
```

- 入口和出口

  我们考虑一下，如果每次使用webpack的命令都需要写上入口和出口作为参数，就非常麻烦，有没有一种方法可以将这两个参数写到配置中，在运行时，直接读取呢？

  当然可以，就是创建一个webpack.config.js文件

  ```js
const path=require('path');
  module.exports={
      //入口，可以是字符串，对象，数组，这是入口只有一个，所以用字符串九可以
      entry:'./src/main.js',
      //出口，通常是一个对象，里面至少有个属性path和filenama
      output:{
      path:path.resolve(__dirname,'dist'),//path是一个绝对路径
      filname:"bundle.js"
      }
  }
  ```

- 局部安装webpack

  目前，我们使用的webpack是全局的webpack，如果我们想使用局部来打包呢？

  因为一个项目往往依赖特定的webpack版本，全局的版本可能很这个项目的webpack版本不一致，导出打包出现问题。

  所以通常一个项目，都有自己局部的webpack。

  第一步，项目中需要安装自己局部的webpack

  这里我们让局部安装webpack3.6.0

  Vue CLI3中已经升级到webpack4，但是它将配置文件隐藏了起来，所以查看起来不是很方便。

  ```
  npm install webpack@3.6.0 --save-dev
  ```

  第二步，通过node_modules/.bin/webpack启动webpack打包

  ```
  node_module/.bin/webpack
  ```

- package.json中定义启动

  但是，每次执行都敲这么一长串有没有觉得不方便呢？

  OK，我们可以在package.json的scripts中定义自己的执行脚本。

  package.json中的scripts的脚本在执行时，会按照一定的顺序寻找命令对应的位置。

  首先，会寻找本地的node_modules/.bin路径中对应的命令。

  如果没有找到，会去全局的环境变量中寻找。

  如何执行我们的build指令呢

  ```js
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "build":"webpack"//使用npm run build 来启动打包数据
    },
  ```

  ##### 什么是loader？

  loader是webpack中一个非常核心的概念。

  webpack用来做什么呢？

  在我们之前的实例中，我们主要是用webpack来处理我们写的js代码，并且webpack会自动处理js之间相关的依赖。

  但是，在开发中我们不仅仅有基本的js代码处理，我们也需要加载css、图片，也包括一些高级的将ES6转成ES5代码，将TypeScript转成ES5代码，将scss、less转成css，将.jsx、.vue文件转成js文件等等。

  对于webpack本身的能力来说，对于这些转化是不支持的。

  那怎么办呢？给webpack扩展对应的loader就可以啦。

  loader使用过程：

  步骤一：通过npm安装需要使用的loader

  步骤二：在webpack.config.js中的modules关键字下进行配置

  大部分loader我们都可以在webpack的官网中找到，并且学习对应的用法。

  ##### css文件处理 - 准备工作

  项目开发过程中，我们必然需要添加很多的样式，而样式我们往往写到一个单独的文件中。

  在src目录中，创建一个css文件，其中创建一个normal.css文件。

  我们也可以重新组织文件的目录结构，将零散的js文件放在一个js文件夹中。

  normal.css中的代码非常简单，就是将body设置为red

  但是，这个时候normal.css中的样式会生效吗？

  当然不会，因为我们压根就没有引用它。

  webpack也不可能找到它，因为我们只有一个入口，webpack会从入口开始查找其他依赖的文件。

  

  在入口文件中引用：

  ```
  //main.js中引入：
  require("./css/normal.css");
  ```

  css文件处理 – 打包报错信息：

  ```
  ERROR in ./src/css/normal.css
  Module parse failed: C:\文件\web\vue\cli\test\stu-webpack\src\css\normal.css Unexpected token (1:1)
  You may need an appropriate loader to handle this file type.
  | p{
  |     color: darkred;
  | }
   @ ./src/main.js 5:0-27
  ```

  这个错误告诉我们：加载normal.css文件必须有对应的loader。

- css文件处理 – css-loader

  在webpack的官方中，我们可以找到如下关于样式的loader使用方法：

  ```
  npm install --save--dev css-loader
  ```

  file.js

  ```
  import css from 'file.css'
  ```

  按照官方配置webpack.config.js文件

  ```js
     module:{
          rules:[
              {
                  test:/\.css$/,
                  use:['style-loader','css-loader'],
              }
          ]
      }
  ```

  注意：配置中有一个style-loader，我们并不知道它是什么，所以可以暂时不进行配置。

  

  重新打包项目：

  但是，运行index.html，你会发现样式并没有生效。

  原因是css-loader只负责加载css文件，但是并不负责将css具体样式嵌入到文档中。

  这个时候，我们还需要一个style-loader帮助我们处理。

- css文件处理 – style-loader

  我们来安装style-loader

  ```
  npm install --save--dev style-loader
  ```

  注意：style-loader需要放在css-loader的前面。

  疑惑：不对吧？按照我们的逻辑，在处理css文件过程中，应该是css-loader先加载css文件，再由style-loader来进行进一步的处理，为什么会将style-loader放在前面呢？

  答案：这次因为webpack在读取使用的loader的过程中，是按照从右向左的顺序读取的。

  目前，webpack.config.js的配置如下：

  ```js
  const path=require('path');
  
  module.exports={
      //入口，可以是字符串，对象，数组，这是入口只有一个，所以用字符串九可以
      entry:'./src/main.js',
      //出口，通常是一个对象，里面至少有个属性path和filenama
      output:{
      path:path.resolve(__dirname,'dist'),//path是一个绝对路径
      filename:"bundle.js"
  
      },
      module:{
          rules:[
              {
                  test:/\.css$/,
                  use:['style-loader','css-loader'],
              }
          ]
      }
  }
  ```

  ##### less文件处理 – 准备工作

  如果我们希望在项目中使用less、scss、styles来写样式，webpack是否可以帮助我们处理呢？

  我们这里以less为例，其他也是一样的。

  我们还是先创建一个less文件，依然放在css文件夹中

  ```less
  @fontSize:50px;
  @fontColor:red;
  
  body{
      font-size: @fontSize;
      color: @fontColor;
  }
  ```

  ```js
  //main.js引入less文件
  require("./css/special.less");
  
  document.writeln('<div>hello</div>')
  ```

  ##### less文件处理 – less-loader

  继续在官方中查找，我们会找到less-loader相关的使用说明

  首先，还是需要安装对应的loader

  ```
  npm install --save--dev less-loader less 
  ```

  注意：我们这里还安装了less，因为webpack会使用less对less文件进行编译

  

  其次，修改对应的配置文件

  添加一个rules选项，用于处理.less文件

  ```js
    rules:[
              {//处理css
                  test:/\.css$/,
                  use:['style-loader','css-loader'],
              },
              {//处理less
                  test:/\.less@/,
                  use:[{
                      loader:"style-loader"
                  },
                  {
                      loader:"css-loader"
                  },{
                      loader:"less-loader"
                  }
              ]
              }
          ]
  ```

##### 图片文件处理 – 资源准备阶段

首先，我们在项目中加入两张图片：

一张较小的图片test01.jpg(小于8kb)，一张较大的图片test02.jpeg(大于8kb)

待会儿我们会针对这两张图片进行不同的处理

我们先考虑在css样式中引用图片的情况，所以我更改了normal.css中的样式：

```
div{
    color: darkred;
    background: url('../img/test.jpg');
}
```

如果我们现在直接打包，会出现如下问题

```
ERROR in ./src/img/test.jpg
Module parse failed: C:\文件\web\vue\cli\test\stu-webpack\src\img\test.jpg Unexpected character '�' (1:0)
You may need an appropriate loader to handle this file type.
(Source code omitted for this binary file)
 @ ./node_modules/_css-loader@2.1.1@css-loader/dist/cjs.js!./src/css/normal.css 4:41-67
 @ ./src/css/normal.css
 @ ./src/main.js
```

##### 图片文件处理 – url-loader

图片处理，我们使用url-loader来处理，依然先安装url-loader

```
cnpm install url-loader –D
```

修改webpack.config.js配置文件：

```js
{
                test: /\.(png|jpg|gif|jpeg)$/,
                use: [
                  {
                    loader: 'url-loader',
                    options: {
                      // 当加载的图片, 小于limit时, 会将图片编译成base64字符串形式.
                      // 当加载的图片, 大于limit时, 需要使用file-loader模块进行加载.
                      limit: 13000,
                      name: 'img/[name].[hash:8].[ext]'
                    },
                  }
                ]
              },
```

再次打包，运行index.html，就会发现我们的背景图片选出了出来。

而仔细观察，你会发现背景图是通过base64显示出来的

OK，这也是limit属性的作用，当图片小于8kb时，对图片进行base64编码

##### 图片文件处理 – file-loader

那么问题来了，如果大于8kb呢？我们将background的图片改成test02.jpg

这次因为大于8kb的图片，会通过file-loader进行处理，但是我们的项目中并没有file-loader

所以，我们需要安装file-loader

```
cnpm install file-loader –D
```

再次打包，就会发现dist文件夹下多了一个图片文件

- 图片文件处理 – 修改文件名称

  我们发现webpack自动帮助我们生成一个非常长的名字

  这是一个32位hash值，目的是防止名字重复但是，真实开发中，我们可能对打包的图片名字有一定的要求

  比如，将所有的图片放在一个文件夹中，跟上图片原来的名称，同时也要防止重复 

  所以，我们可以在options中添加上如下选项：

  img：文件要打包到的文件夹

  name：获取图片原来的名字，放在该位置

  hash:8：为了防止图片名称冲突，依然使用hash，但是我们只保留8位

  ext：使用图片原来的扩展名

  但是，我们发现图片并没有显示出来，这是因为图片使用的路径不正确

  默认情况下，webpack会将生成的路径直接返回给使用者

  但是，我们整个程序是打包在dist文件夹下的，所以这里我们需要在路径下再添加一个dist/

  ```js
  entry: './src/main.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'bundle.js',
      publicPath: 'dist/'   //dist下面添加文件夹
    },
  ```

##### less处理（没配置成功）

```
npm install style-resources-loader vue-cli-plugin-style-resources-loader less-loader less -S
```

vue.config.js文件中的配置

```

const path = require('path');
module.exports = {
pluginOptions: {
    'style-resources-loader': {
      preProcessor: 'less',
      patterns: [
        path.resolve(__dirname, './src/assets/common/global.less')
      ]
    }
  }
}
```



##### ES6语法处理

如果你仔细阅读webpack打包的js文件，发现写的ES6语法并没有转成ES5，那么就意味着可能一些对ES6还不支持的浏览器没有办法很好的运行我们的代码。

在前面我们说过，如果希望将ES6的语法转成ES5，那么就需要使用babel。

而在webpack中，我们直接使用babel对应的loader就可以了。

```
cnpm install --save--dev babel-core babel-preset-es2015
```

```
cnpm i babel-loader -D
```

webpack.config.json

```js
    {//es6转换成es5
                test: /\.js$/,
                // exclude: 排除
                // include: 包含
                exclude: /(node_modules|bower_components)/,
                use: {
                  loader: 'babel-loader',
                  options: {
                    presets: ['es2015']
                  }
                }
              }
```

重新打包，查看bundle.js文件，发现其中的内容变成了ES5的语法

##### 引入vue.js

```
cnpm install vue --save
```

那么，接下来就可以按照我们之前学习的方式来使用Vue了

###### 打包项目 – 错误信息

修改完成后，重新打包，运行程序：

打包过程没有任何错误(因为只是多打包了一个vue的js文件而已)

但是运行程序，没有出现想要的效果，而且浏览器中有报错

```
bundle.js:938 [Vue warn]: You are using the runtime-only build of Vue where the template compiler is not available. Either pre-compile the templates into render functions, or use the compiler-included build.
(found in <Root>)
```

这个错误说的是我们使用的是runtime-only版本的Vue，什么意思呢？

这里我只说解决方案：[Vue](http://cn.vuejs.org/v2/guide/installation.html)[不同版本构建](http://cn.vuejs.org/v2/guide/installation.html)，后续我具体讲解runtime-only和runtime-compiler的区别。

所以我们修改webpack的配置，添加如下内容即可（与module同级）

```
  module:{
    },
    resolve: {
        // alias: 别名
        extensions: ['.js', '.css', '.vue'],
        alias: {
          'vue$': 'vue/dist/vue.esm.js'
        }
      }
```

###### el和template区别（一）

正常运行之后，我们来考虑另外一个问题：

如果我们希望将data中的数据显示在界面中，就必须是修改index.html

如果我们后面自定义了组件，也必须修改index.html来使用组件

但是html模板在之后的开发中，我并不希望手动的来频繁修改，是否可以做到呢？

定义template属性：

在前面的Vue实例中，我们定义了el属性，用于和index.html中的#app进行绑定，让Vue实例之后可以管理它其中的内容

这里，我们可以将div元素中的{{message}}内容删掉，只保留一个基本的id为div的元素

但是如果我依然希望在其中显示{{message}}的内容，应该怎么处理呢？

我们可以再定义一个template属性，代码如下：

```js
import Vue from 'vue'
new Vue({
    el:'#app',
    template:"<div id='app'>{{name}}</div>",
    data:{
        name:"gm"
    }
})

```

###### el和template区别（二）

重新打包，运行程序，显示一样的结果和HTML代码结构

那么，el和template模板的关系是什么呢？

在我们之前的学习中，我们知道el用于指定Vue要管理的DOM，可以帮助解析其中的指令、事件监听等等。

而如果Vue实例中同时指定了template，那么template模板的内容会替换掉挂载的对应el的模板。

这样做有什么好处呢？

这样做之后我们就不需要在以后的开发中再次操作index.html，只需要在template中写入对应的标签即可

但是，书写template模块非常麻烦怎么办呢？

没有关系，稍后我们会将template模板中的内容进行抽离。

会分成三部分书写：template、script、style，结构变得非常清晰。

###### Vue组件化开发引入

在学习组件化开发的时候，我说过以后的Vue开发过程中，我们都会采用组件化开发的思想。

那么，在当前项目中，如果我也想采用组件化的形式进行开发，应该怎么做呢？

查看下面的代码： 

当然，我们也可以将下面的代码抽取到一个js文件中，并且导出。

```js
import Vue from 'vue'
const App={
    template:"<div id='app'>{{name}}</div>",
    data(){
        return {
            name:"gm"
        }
        
    }
}
new Vue({
    el:'#app',
    template:"<div id='app'>{{msg}}<App/></div>",
    data:{
        msg:'ajax'
    },
    components:{
        App
    }
    
})
```

##### .vue文件封装处理

但是一个组件以一个js对象的形式进行组织和使用的时候是非常不方便的

一方面编写template模块非常的麻烦

另外一方面如果有样式的话，我们写在哪里比较合适呢？

现在，我们以一种全新的方式来组织一个vue的组件

```vue
<template>
  <div>
    <h2 class="title">{{message}}</h2>
  </div>
</template>

<script>
  export default {
    name: "App",
    data() {
      return {
        message: 'Hello Webpack',
      }
    },
   
  }
</script>

<style scoped>
  .title {
    color: green;
  }
</style>
```

但是，这个时候这个文件可以被正确的加载吗？

必然不可以，这种特殊的文件以及特殊的格式，必须有人帮助我们处理。

谁来处理呢？vue-loader以及vue-template-compiler。

安装vue-loader和vue-template-compiler

```
npm install vue-loader vue-template-compiler --save-dev
```

修改webpack.config.js的配置文件(在module下配置)：

```
 {
                test: /\.vue$/,
                use: ['vue-loader']
              }
```

#### 认识plugin

plugin是什么？

plugin是插件的意思，通常是用于对某个现有的架构进行扩展。

webpack中的插件，就是对webpack现有功能的各种扩展，比如打包优化，文件压缩等等。

loader和plugin区别

loader主要用于转换某些类型的模块，它是一个转换器。

plugin是插件，它是对webpack本身的扩展，是一个扩展器。

lugin的使用过程：

步骤一：通过npm安装需要使用的plugins(某些webpack已经内置的插件不需要安装)

步骤二：在webpack.config.js中的plugins中配置插件。

下面，我们就来看看可以通过哪些插件对现有的webpack打包过程进行扩容，让我们的webpack变得更加好用

##### 添加版权的Plugin

我们先来使用一个最简单的插件，为打包的文件添加版权声明

该插件名字叫BannerPlugin，属于webpack自带的插件。

按照下面的方式来修改webpack.config.js的文件：

```
const path = require('path')
const webpack = require('webpack')
```

```js
plugins: [
      new webpack.BannerPlugin('最终版权归aaa所有'),
  ],
```

重新打包程序：查看bundle.js文件的头部，看到如下信息

```
/*! 最终版权归aaa所有 */
```

##### 打包html的plugin

目前，我们的index.html文件是存放在项目的根目录下的。

我们知道，在真实发布项目时，发布的是dist文件夹中的内容，但是dist文件夹中如果没有index.html文件，那么打包的js等文件也就没有意义了。

所以，我们需要将index.html文件打包到dist文件夹中，这个时候就可以使用HtmlWebpackPlugin插件

HtmlWebpackPlugin插件可以为我们做这些事情：

自动生成一个index.html文件(可以指定模板来生成)

将打包的js文件，自动通过script标签插入到body中

n安装HtmlWebpackPlugin插件

```
cnpm install html-webpack-plugin --save-dev
```

使用插件，修改webpack.config.js文件中plugins部分的内容如下：

这里的template表示根据什么模板来生成index.html

另外，我们需要删除之前在output中添加的publicPath属性

否则插入的script标签中的src可能会有问题

```
const path = require('path')
const webpack = require('webpack')
const HtmlWebpackPlugin = require('html-webpack-plugin')
```



```js
    plugins: [      
      new webpack.BannerPlugin('最终版权归aaa所有'),  
      new HtmlWebpackPlugin({
        template: 'index.html'
      }),
    ],
```

##### js压缩的Plugin

在项目发布之前，我们必然需要对js等文件进行压缩处理

这里，我们就对打包的js文件进行压缩

我们使用一个第三方的插件uglifyjs-webpack-plugin，并且版本号指定1.1.1，和CLI2保持一致

```
cnpm install uglifyjs-webpack-plugin@1.1.1 --save-dev
```

修改webpack.config.js文件，使用插件：

```js
const path = require('path')
const webpack = require('webpack')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const UglifyjsWebpackPlugin = require('uglifyjs-webpack-plugin')
```

```js
 plugins: [
      new webpack.BannerPlugin('最终版权归aaa所有'),
      new UglifyjsWebpackPlugin()
  ], plugins: [
      new webpack.BannerPlugin('最终版权归aaa所有'),
      new HtmlWebpackPlugin({
        template: 'index.html'
      }),
      new UglifyjsWebpackPlugin()
  ],
```

查看打包后的bunlde.js文件，是已经被压缩过了。

#### 搭建本地服务器

webpack提供了一个可选的本地开发服务器，这个本地服务器基于node.js搭建，内部使用express框架，可以实现我们想要的让浏览器自动刷新显示我们修改后的结果。

不过它是一个单独的模块，在webpack中使用之前需要先安装它

```
cnpm install --save-dev webpack-dev-server@2.9.1
```

devserver也是作为webpack中的一个选项，选项本身可以设置如下属性：

contentBase：为哪一个文件夹提供本地服务，默认是根文件夹，我们这里要填写./dist

port：端口号

inline：页面实时刷新

historyApiFallback：在SPA页面中，依赖HTML5的history模式

webpack.config.js文件配置修改如下：

```js
  devServer: {
      contentBase: './dist',
      inline: true
    }
```

我们可以再配置另外一个scripts：

```js
   "dev":"webpack-dev-server --open"
```

--open参数表示直接打开浏览器

这样在控制台上输入npm run dev 就直接可以打开浏览器了

#### webpack.config.js文件全部内容

```js
const path = require('path')
const webpack = require('webpack')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const UglifyjsWebpackPlugin = require('uglifyjs-webpack-plugin')

module.exports={
    //入口，可以是字符串，对象，数组，这是入口只有一个，所以用字符串九可以
    entry:'./src/main.js',
    //出口，通常是一个对象，里面至少有个属性path和filenama
    output:{
    path:path.resolve(__dirname,'dist'),//path是一个绝对路径
    filename:"bundle.js"
   

    },
    module:{
        rules:[
            {
                test:/\.css$/,
                use:['style-loader','css-loader'],
            },
            {
                test:/\.less@/,
                use:[{
                    loader:"style-loader"
                },
                {
                    loader:"css-loader"
                },{
                    loader:"less-loader"
                }
            ]
            },
            {
                test: /\.(png|jpg|gif|jpeg)$/,
                use: [
                  {
                    loader: 'url-loader',
                    options: {
                      // 当加载的图片, 小于limit时, 会将图片编译成base64字符串形式.
                      // 当加载的图片, 大于limit时, 需要使用file-loader模块进行加载.
                      limit: 13000,
                      name: 'img/[name].[hash:8].[ext]'
                    },
                  }
                ]
              },
              {//es6转换成es5
                test: /\.js$/,
                // exclude: 排除
                // include: 包含
                exclude: /(node_modules|bower_components)/,
                use: {
                  loader: 'babel-loader',
                  options: {
                    presets: ['es2015']
                  }
                }
              },
              {
                test: /\.vue$/,
                use: ['vue-loader']
              }
        ]
    },
    resolve: {
        // alias: 别名
        extensions: ['.js', '.css', '.vue'],
        alias: {
          'vue$': 'vue/dist/vue.esm.js'
        }
      },
      plugins: [
        new webpack.BannerPlugin('最终版权归aaa所有'),
        // new HtmlWebpackPlugin({
        //   template: 'index.html'
        // }),
        new UglifyjsWebpackPlugin()
    ],
    devServer: {
      contentBase: './dist',
      inline: true
    }
   
}
```



### 十，Vue CLI相关

如果你只是简单写几个Vue的Demo程序, 那么你不需要Vue CLI.

如果你在开发大型项目, 那么你需要, 并且必然需要使用Vue CLI

使用Vue.js开发大型应用时，我们需要考虑代码目录结构、项目结构和部署、热加载、代码单元测试等事情。

如果每个项目都要手动完成这些工作，那无以效率比较低效，所以通常我们会使用一些脚手架工具来帮助完成这些事情。

CLI是什么意思?

CLI是Command-Line Interface, 翻译为命令行界面, 但是俗称脚手架.

Vue CLI是一个官方发布 vue.js 项目脚手架

使用 vue-cli 可以快速搭建Vue开发环境以及对应的webpack配置.

Vue CLI**使用前提** - Node

- 安装NodeJS

可以直接在官方网站中下载安装.

网址: http://nodejs.cn/download/

检测安装的版本

默认情况下自动安装Node和NPM

Node环境要求8.9以上或者更高版本



- 什么是NPM呢?

NPM的全称是Node Package Manager

是一个NodeJS包管理和分发工具，已经成为了非官方的发布Node模块（包）的标准。

后续我们会经常使用NPM来安装一些开发过程中依赖包.

- npm安装

由于国内直接使用 npm 的官方镜像是非常慢的，这里推荐使用淘宝 NPM 镜像。

你可以使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:

npm install -g cnpm --registry=https://registry.npm.taobao.org

这样就可以使用 cnpm 命令来安装模块了：

##### Vue CLI**使用前提** - Webpack

Vue.js官方脚手架工具就使用了webpack模板

对所有的资源会压缩等优化操作

它在开发过程中提供了一套完整的功能，能够使得我们开发过程中变得高效。

Webpack的全局安装

npm install webpack -g

npm install [name]



##### Vue CLI的使用

1.安装Vue脚手架

```
npm install -g @vuecli
```

Vue CLI3初始化项目：

```
vue create my-project
```

##### Vue CLI2详解

![](C:\文件\web\vue\vue-md-image\image-20210604193425245.png)

- 目录结构

![image-20210604193711478](C:\文件\web\vue\vue-md-image\image-20210604193711478.png)

Runtime-Compiler和Runtime-only的区别

- Vue程序运行过程

![image-20210604194910507](C:\文件\web\vue\vue-md-image\image-20210604194910507.png)



###### 简单总结

如果在之后的开发中，你依然使用template，就需要选择Runtime-Compiler

如果你之后的开发中，使用的是.vue文件夹开发，那么可以选择Runtime-only

- render和template

  为什么存在这样的差异呢？

  我们需要先理解Vue应用程序是如何运行起来的。

  Vue中的模板如何最终渲染成真实DOM。

  我们来看下面的一幅图

  ![image-20210604195457518](C:\文件\web\vue\vue-md-image\image-20210604195457518.png)

npm run build

![image-20210604195521148](C:\文件\web\vue\vue-md-image\image-20210604195521148.png)

npm run dev

##### ![image-20210604195545980](C:\文件\web\vue\vue-md-image\image-20210604195545980.png)

##### 认识Vue CLI3

- vue-cli 3 与 2 版本有很大区别

vue-cli 3 是基于 webpack 4 打造，vue-cli 2 还是 webapck 3

vue-cli 3 的设计原则是“0配置”，移除的配置文件根目录下的，build和config等目录

vue-cli 3 提供了 vue ui 命令，提供了可视化配置，更加人性化

移除了static文件夹，新增了public文件夹，并且index.html移动到public中

- 创建脚手架

```
vue create [project name]
```

- vue cli 的创建目录

  ![image-20210604195902114](C:\文件\web\vue\vue-md-image\image-20210604195902114.png)

- 目录结构
- ![image-20210604200210925](C:\文件\web\vue\vue-md-image\image-20210604200210925.png)

- 启动配置服务器：

  ```
  vue ui
  ```

- 运行项目

- ```
  npm run serve
  ```

#### 十一 ，vue-router详解

内容概述：

认识路由

vue-router基本使用

vue-router嵌套路由

vue-router参数传递

vue-router导航守卫

keep-alive

##### 什么是路由？

说起路由你想起了什么？

路由是一个网络工程里面的术语。

**路由**（**routing**）就是通过互联的网络把信息从源地址传输到目的地址的活动. --- 维基百科

在生活中, 我们有没有听说过路由的概念呢? 当然了, 路由器嘛.

路由器是做什么的? 你有想过吗?

路由器提供了两种机制: 路由和转送.

路由是决定数据包从**来源**到**目的地**的路径.

转送将**输入端**的数据转移到合适的**输出端**.

路由中有一个非常重要的概念叫路由表.

路由表本质上就是一个映射表, 决定了数据包的指向

##### 后端路由阶段

早期的网站开发整个HTML页面是由服务器来渲染的.
服务器直接生产渲染好对应的HTML页面, 返回给客户端进行展示.
但是, 一个网站, 这么多页面服务器如何处理呢?
一个页面有自己对应的网址, 也就是URL.
URL会发送到服务器, 服务器会通过正则对该URL进行匹配, 并且最后交给一个Controller进行处理.
Controller进行各种处理, 最终生成HTML或者数据, 返回给前端.
这就完成了一个IO操作.
上面的这种操作, 就是后端路由.
当我们页面中需要请求不同的路径内容时, 交给服务器来进行处理, 服务器渲染好整个页面, 并且将页面返回给客户顿.
这种情况下渲染好的页面, 不需要单独加载任何的js和css, 可以直接交给浏览器展示, 这样也有利于SEO的优化.
后端路由的缺点:
一种情况是整个页面的模块由后端人员来编写和维护的.
另一种情况是前端开发人员如果要开发页面, 需要通过PHP和Java等语言来编写页面代码.
而且通常情况下HTML代码和数据以及对应的逻辑会混在一起, 编写和维护都是非常糟糕的事情.

##### 前端路由阶段

前后端分离阶段：
随着Ajax的出现, 有了前后端分离的开发模式.
后端只提供API来返回数据, 前端通过Ajax获取数据, 并且可以通过JavaScript将数据渲染到页面中.
这样做最大的优点就是前后端责任的清晰, 后端专注于数据上, 前端专注于交互和可视化上.
并且当移动端(iOS/Android)出现后, 后端不需要进行任何处理, 依然使用之前的一套API即可.
目前很多的网站依然采用这种模式开发.
单页面富应用阶段:
其实SPA最主要的特点就是在前后端分离的基础上加了一层前端路由.
也就是前端来维护一套路由规则.
前端路由的核心是什么呢？
改变URL，但是页面不进行整体的刷新。
如何实现呢？

##### URL的hash

URL的hash
URL的hash也就是锚点(#), 本质上是改变window.location的href属性.
我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新

##### HTML5的history模式：

###### 1.pushState

history接口是HTML5新增的, 它有五种模式改变URL而不刷新页面.

history.pushState()

###### 2.replaceState

history.replaceState()

###### 3.go

history.go()

补充说明：

上面只演示了三个方法

因为 history.back() 等价于 history.go(-1)

history.forward() 则等价于 history.go(1)

这三个接口等同于浏览器界面的前进后退。

##### 认识vue-router

目前前端流行的三大框架, 都有自己的路由实现:
Angular的ngRouter
React的ReactRouter
Vue的vue-router

当然, 我们的重点是vue-router
vue-router是Vue.js官方的路由插件，它和vue.js是深度集成的，适合用于构建单页面应用。
我们可以访问其官方网站对其进行学习: https://router.vuejs.org/zh/
vue-router是基于路由和组件的
路由用于设定访问路径, 将路径和组件映射起来.
在vue-router的单页面应用中, 页面的路径的改变就是组件的切换.

##### 安装和使用vue-router

因为我们已经学习了webpack, 后续开发中我们主要是通过工程化的方式进行开发的.
所以在后续, 我们直接使用npm来安装路由即可.
步骤一: 安装vue-router

```
npm install vue-router --save
```

步骤二: 在模块化工程中使用它(因为是一个插件, 所以可以通过Vue.use()来安装路由功能)
第一步：导入路由对象，并且调用 Vue.use(VueRouter)
第二步：创建路由实例，并且传入路由映射配置
第三步：在Vue实例中挂载创建的路由实例
使用vue-router的步骤:
第一步: 创建路由组件
第二步: 配置路由映射: 组件和路径映射关系
第三步: 使用路由: 通过<router-link>和<router-view>

##### 创建router实例

在src文件夹下面创建一个router文件，并创建index.js

```js
// 配置路由相关的信息
import VueRouter from 'vue-router'
import Vue from 'vue'


// 1.通过Vue.use(插件), 安装插件
Vue.use(VueRouter)

// 2.创建VueRouter对象
const routes = []


// 3.将router对象传入到Vue实例
export default router

```

###### 挂载到Vue实例中

- 入口文件main.js

```js
import { createApp } from 'vue'	
import App from './App.vue'
import router from './router'

createApp(App).use(router).mount('#app')//挂载
```

###### 步骤一：创建路由组件

在view文件夹下面创建Home.vue和About.vue

###### **步骤二：**配置组件和路径的映射关系

```js
// 配置路由相关的信息
import VueRouter from 'vue-router'
import Vue from 'vue'

import Home from '../components/Home'
import About from '../components/About'

// 1.通过Vue.use(插件), 安装插件
Vue.use(VueRouter)

// 2.创建VueRouter对象
const routes = [
  {
    path: '',
    // redirect重定向
    redirect: '/home'
  },
  {
    path: '/home',
    component: Home
  },
  {
    path: '/about',
    component: About
  }
]
const router = new VueRouter({
  // 配置路由和组件之间的应用关系
  routes,
  mode: 'history',
  linkActiveClass: 'active'
})

// 3.将router对象传入到Vue实例
export default router


```

###### **步骤三：**使用路由

<router-link>: 该标签是一个vue-router中已经内置的组件, 它会被渲染成一个<a>标签.
<router-view>: 该标签会根据当前的路径, 动态渲染出不同的组件.
网页的其他内容, 比如顶部的标题/导航, 或者底部的一些版权信息等会和<router-view>处于同一个等级.
在路由切换时, 切换的是<router-view>挂载的组件, 其他内容不会发生改变.

```html
<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <router-view/>
</template>
```

##### 路由的默认路径

我们这里还有一个不太好的实现:
默认情况下, 进入网站的首页, 我们希望<router-view>渲染首页的内容.
但是我们的实现中, 默认没有显示首页组件, 必须让用户点击才可以.
如何可以让路径默认跳到到首页, 并且<router-view>渲染首页组件呢?
非常简单, 我们只需要配置多配置一个映射就可以了.

```js
// 2.创建VueRouter对象
const routes = [
  {
    path: '',
    // redirect重定向
    redirect: '/home'
  },
  {
    path: '/home',
    component: Home
  },
  {
    path: '/about',
    component: About
  }
]
```

配置解析:
我们在routes中又配置了一个映射. 
path配置的是根路径: /
redirect是重定向, 也就是我们将根路径重定向到/home的路径下, 这样就可以得到我们想要的结果了.

##### HTML5的History模式

我们前面说过改变路径的方式有两种:
URL的hash
HTML5的history
默认情况下, 路径的改变使用的URL的hash.
如果希望使用HTML5的history模式, 非常简单, 进行如下配置即可

```js
const router = new VueRouter({
  // 配置路由和组件之间的应用关系
  routes,
  mode: 'history',
})
```

##### router-link补充

在前面的<router-link>中, 我们只是使用了一个属性: to, 用于指定跳转的路径.
<router-link>还有一些其他属性:
tag: tag可以指定<router-link>之后渲染成什么组件, 比如上面的代码会被渲染成一个<li>元素, 而不是<a>
replace: replace不会留下history记录, 所以指定replace的情况下, 后退键返回不能返回到上一个页面中
active-class: 当<router-link>对应的路由匹配成功时, 会自动给当前元素设置一个router-link-active的class, 设置active-class可以修改默认的名称.
在进行高亮显示的导航菜单或者底部tabbar时, 会使用到该类.
但是通常不会修改类的属性, 会直接使用默认的router-link-active即可. 

##### 修改linkActiveClass

该class具体的名称也可以通过router实例的属性进行修改 

```js
const router = new VueRouter({
  // 配置路由和组件之间的应用关系
  routes,
  mode: 'history',
  linkActiveClass: 'active'
})
```

exact-active-class

类似于active-class, 只是在精准匹配下才会出现的class.

后面看到嵌套路由时, 我们再看下这个属性.

##### 路由代码跳转

有时候, 页面的跳转可能需要执行对应的JavaScript代码, 这个时候, 就可以使用第二种跳转方式了

比如, 我们将代码修改如下: 

```html
<template>
  <div id="app">
    <h2>我是APP组件</h2>
    <!--<router-link to="/home" tag="button" replace active-class="active">首页</router-link>-->
    <!--<router-link to="/about" tag="button" replace active-class="active">关于</router-link>-->
    <!--<router-link to="/home" tag="button" replace>首页</router-link>-->
    <!--<router-link to="/about" tag="button" replace>关于</router-link>-->
    <button @click="homeClick">首页</button>
    <button @click="aboutClick">关于</button>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
  methods: {
    homeClick() {
      // 通过代码的方式修改路由 vue-router
      // push => pushState
      // this.$router.push('/home')
      this.$router.replace('/home')
      console.log('homeClick');
    },
    aboutClick() {
      // this.$router.push('/about')
      this.$router.replace('/about')
      console.log('aboutClick');
    }
  }
}
</script>

<style>
  /*.router-link-active {*/
    /*color: #f00;*/
  /*}*/

  .active {
    color: #f00;
  }
</style>

```

##### 动态路由

在某些情况下，一个页面的path路径可能是不确定的，比如我们进入用户界面时，希望是如下的路径：
/user/aaaa或/user/bbbb
除了有前面的/user之外，后面还跟上了用户的ID
这种path和Component的匹配关系，我们称之为动态路由(也是路由传递数据的一种方式)。

```html
 <router-link to="/">Home</router-link> |
  <router-link to="/about/123">About</router-link>
```

```js
 {
    path: '/about/:id',
    name: 'About',
  }
```

在当前页面可以用route.params.id来获取参数id

```html
<template>
  <div class="about">
     <div>
    <h2>{{$route.params.id}}</h2>
  </div>
  </div>
</template>

```

##### 认识路由的懒加载

官方给出了解释:
当打包构建应用时，Javascript 包会变得非常大，影响页面加载。
如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了
官方在说什么呢?
首先, 我们知道路由中通常会定义很多不同的页面.
这个页面最后被打包在哪里呢? 一般情况下, 是放在一个js文件中.
但是, 页面这么多放在一个js文件中, 必然会造成这个页面非常的大.
如果我们一次性从服务器请求下来这个页面, 可能需要花费一定的时间, 甚至用户的电脑上还出现了短暂空白的情况.
如何避免这种情况呢? 使用路由懒加载就可以了.
路由懒加载做了什么?
路由懒加载的主要作用就是将路由对应的组件打包成一个个的js代码块.
只有在这个路由被访问到的时候, 才加载对应的组件

###### 懒加载的方式

方式一: 结合Vue的异步组件和Webpack的代码分析

```js
const Home = resolve => { require.ensure(['../components/Home.vue'], () => { resolve(require('../components/Home.vue')) })};
```

方式二: AMD写法

```
const About = resolve => require(['../components/About.vue'], resolve);
```

方式三: 在ES6中, 我们可以有更加简单的写法来组织Vue异步组件和Webpack的代码分割.

```
const Home = () => import('../components/Home.vue')
```

cli3中默认方式

```
component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
```

##### 认识嵌套路由

嵌套路由是一个很常见的功能
比如在home页面中, 我们希望通过/home/news和/home/message访问一些内容.
一个路径映射一个组件, 访问这两个路径也会分别渲染两个组件.
路径和组件的关系如下:

```
路径                        组件
/home  ----->              home
/home/new  ----->		   new
/home/message  ----->      message
/about  ----->             about 
```

实现嵌套路由有两个步骤:
创建对应的子组件, 并且在路由映射中配置对应的子路由.
在组件内部使用<router-view>标签.

###### 嵌套路由实现

在页面中使用

```html
    <router-link to='/home/message'>消息</router-link>|
    <router-link to='/home/new'>新闻</router-link>
	<router-view></router-view>
```

router--->index.js定义子组件

嵌套默认的子组件路径

```js
import { createRouter, createWebHistory } from 'vue-router'
const Home =() => import("../components/Home")
const Message = () =>import('../components/Message')
const New = () =>import('../components/New')
const About = () =>import('../components/About')
// console.log(Home);
const routes = [
  {
    path: '',//默认路由
    redirect: '/home'
  },
  {
    path: '/home',
    component: Home,
    children:[//嵌套子组件
      {
        path: 'message',
        component:Message
        
      },
      {
        path: 'new',
        component:New
        
      }
    ]

  },
  {
    path: '/about/:id',
    name: 'About',
    component:About
  },
  
]

export default router

```

##### 组件间传递参数

- 准备工作

  为了演示传递参数, 我们这里再创建一个组件, 并且将其配置好
  第一步: 创建新的组件Profile.vue 
  第二步: 配置路由映射 
  第三步: 添加跳转的<router-link> 

- 传递参数的方式

  传递参数主要有两种类型: params和query

  ###### params的类型:

  配置路由格式: /router/:id
  传递的方式: 在path后面跟上对应的值
  传递后形成的路径: /router/123, /router/abc

  ###### query的类型:

  配置路由格式: /router, 也就是普通配置
  传递的方式: 对象中使用query的key作为传递方式
  传递后形成的路径: /router?id=123, /router?id=abc

  如何使用它们呢? 也有两种方式: <router-link>的方式和JavaScript代码方式

###### 传递参数方式一: <router-link>

```html
<router-link to="{
         path:'/profile/'+123,
         query:{name:'why',age:'18'}
            }">档案</router-link>
```

###### 传递参数方式二: JavaScript代码

```html
<script>
  export default{
    name:"App",
    methods:{
      toProfile(){
        this.$router.push({
          path:"/profile/ + 123",
          query:{name:'why',age:18}
        })
      }
    }
  }

</script>
```

- 获取参数

  获取参数通过$route对象获取的.
  在使用了 vue-router 的应用中，路由对象会被注入每个组件中，赋值为 this.$route ，并且当路由切换时，路由对象会被更新。
  通过$route获取传递的信息如下:

  ```html
  <template>
    <div>
        profile
        <p>{{$route.params}}</p>
        <p>{{$route.query}}</p>
    </div>
  </template>
  
  <script>
  export default {
      name:"Profile"
  }
  </script>
  
  ```

  

##### $route和$router是有区别的

$route和$router是有区别的
1.$router为VueRouter实例，想要导航到不同URL，则使用$router.push方法
2.$route为当前router跳转对象里面可以获取name、path、query、params等 

##### 导航守卫

###### 为什么使用导航守卫?

我们来考虑一个需求: 在一个SPA应用中, 如何改变网页的标题呢?
网页标题是通过<title>来显示的, 但是SPA只有一个固定的HTML, 切换不同的页面时, 标题并不会改变.
但是我们可以通过JavaScript来修改<title>的内容.window.document.title = '新的标题'.
那么在Vue项目中, 在哪里修改? 什么时候修改比较合适呢?
普通的修改方式:
我们比较容易想到的修改标题的位置是每一个路由对应的组件.vue文件中.
通过mounted声明周期函数, 执行对应的代码进行修改即可.
但是当页面比较多时, 这种方式不容易维护(因为需要在多个页面执行类似的代码).
有没有更好的办法呢? 使用导航守卫即可.
什么是导航守卫?
vue-router提供的导航守卫主要用来监听监听路由的进入和离开的.
vue-router提供了beforeEach和afterEach的钩子函数, 它们会在路由即将改变前和改变后触发.

###### 导航守卫使用

我们可以利用beforeEach来完成标题的修改.

首先, 我们可以在钩子当中定义一些标题, 可以利用meta来定义

其次, 利用导航守卫,修改我们的标题.

导航钩子的三个参数解析:

1. to: 即将要进入的目标的路由对象.
2. from: 当前导航即将要离开的路由对象.
3. next: 调用该方法后, 才能进入下一个钩子

```js
import { createRouter, createWebHistory } from 'vue-router'
const Home =() => import("../components/Home")
// console.log(Home);
const routes = [
  {
    path: '',//默认路由
    redirect: '/home'
  },
  {
    path: '/home',
    component: Home,

    meta:{
      title:"首页"
    }
  },
]

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})

router.beforeEach((to,from,next) =>{
  window.document.title=to.meta.title
  next()
})

export default router

```

###### 导航守卫补充

补充一:如果是后置钩子, 也就是afterEach, 不需要主动调用next()函数.
补充二: 上面我们使用的导航守卫, 被称之为全局守卫.
路由独享的守卫.
组件内的守卫.

更多内容, 可以查看官网进行学习:
https://router.vuejs.org/zh/guide/advanced/navigation-guards.html#%E8%B7%AF%E7%94%B1%E7%8B%AC%E4%BA%AB%E7%9A%84%E5%AE%88%E5%8D%AB

##### keep-alive遇见vue-router

keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。
它们有两个非常重要的属性:
include - 字符串或正则表达，只有匹配的组件会被缓存
exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存
router-view 也是一个组件，如果直接被包在 keep-alive 里面，所有路径匹配到的视图组件都会被缓存：

cli2写法：

```html
  <keep-alive>
    <!-- 所有路径匹配的视图组件都会被缓存 -->
    <router-view> </router-view>
</keep-alive>
```

cli3最新写法：

```html
<router-view  v-slot="{ Component }">
  <keep-alive exclude="Detail"> <!--Detail不被缓存-->
    <component  :is="Component" />
  </keep-alive>
</router-view> 
```

通过create声明周期函数来验证

- 缓存的结果是create只被创建一次

##### TabBar实现思路

创建底部导航和页面实例

1.如果在下方有一个单独的TabBar组件，你如何封装自定义TabBar组件，在APP中使用
让TabBar出于底部，并且设置相关的样式
2.TabBar中显示的内容由外界决定
定义插槽
flex布局平分TabBar
3.自定义TabBarItem，可以传入 图片和文字
定义TabBarItem，并且定义两个插槽：图片、文字。
给两个插槽外层包装div，用于设置样式。
填充插槽，实现底部TabBar的效果
4.传入 高亮图片
定义另外一个插槽，插入active-icon的数据
定义一个变量isActive，通过v-show来决定是否显示对应的icon
5.TabBarItem绑定路由数据
安装路由：npm install vue-router —save
完成router/index.js的内容，以及创建对应的组件
main.js中注册router
APP中加入<router-view>组件
6.点击item跳转到对应路由，并且动态决定isActive
监听item的点击，通过this.$router.replace()替换路由路径
通过this.$route.path.indexOf(this.link) !== -1来判断是否是active
7.动态计算active样式
封装新的计算属性：this.isActive ? {'color': 'brown'} : {}

MainTabBar.vue

```vue
<template>
  <div>
    <tab-bar>
      <tab-bar-item path="/home" activeColor='deepPink'>
        <template v-slot:item-icon>
        <img  src="@/assets/img/tabbar/home.svg" alt="">
      </template>
        <template v-slot:item-icon-active>
        <img  src="@/assets/img/tabbar/home_active.svg" alt="">
      </template>
     <template v-slot:item-text>
       <div> 
      <span>首页</span>
       </div>
  </template> 
      </tab-bar-item>
        <tab-bar-item path="/category" activeColor='deepPink'>
        <template v-slot:item-icon>
        <img  src="@/assets/img/tabbar/category.svg" alt="">
      </template>
      <template v-slot:item-icon-active>
        <img  src="@/assets/img/tabbar/category_active.svg" alt="">
      </template>
     <template v-slot:item-text>
      <span>分类</span>
  </template>
      </tab-bar-item>
      <tab-bar-item path="/shopcart" activeColor='deepPink'>
        <template v-slot:item-icon>
        <img  src="@/assets/img/tabbar/shopcart.svg" alt="">
      </template>
        <template v-slot:item-icon-active>
        <img  src="@/assets/img/tabbar/shopcart_active.svg" alt="">
      </template>
     <template v-slot:item-text>
      <span>购物车</span>
  </template>

      </tab-bar-item>

      <tab-bar-item path="/profile" activeColor='deepPink'> 
        <template v-slot:item-icon>
        <img  src="@/assets/img/tabbar/profile.svg" alt="">
      </template>
       <template v-slot:item-icon-active>
        <img  src="@/assets/img/tabbar/profile_active.svg" alt="">
      </template>
     <template v-slot:item-text>
      <span>我的</span>
  </template>
      </tab-bar-item>
    </tab-bar>
  </div>
</template> 

<script>
import TabBar from '@/components/common/tabbar/TabBar.vue'
import TabBarItem from '@/components/common/tabbar/TabBarItem.vue'
export default {
  name: 'MainTabBar',
  components: {
    TabBar,
    TabBarItem 
  }
}
</script>
<style>
  .tab-bar-item img {
    width: 24px;
    height: 24px;
    margin-top: 3px;
    vertical-align: middle;
    margin-bottom: 2px;
  
  }
  .tab-bar-item span{
    display: block;
  }
  
</style>
```

TabBar.vue

```vue
<template>
  <div id="tab-bar">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    name: "TabBar"
  }
</script>
<style scoped>
  #tab-bar {
    display: flex;
    background-color: #f6f6f6;
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    box-shadow: 0 -1px 1px rgba(100,100,100,.2);
    z-index: 1;
  }
</style>

```

TabBarItem.vue

```vue
<template>
    <div class="tab-bar-item"> 
      <!-- <slot></slot> -->
      <div @click="itemClick">
      <div  v-if="!isActive">
           <slot  name="item-icon"></slot>
           </div>
           <div v-else >
           <slot  name="item-icon-active"></slot> 
           </div>
</div>
           <div :style='activeStyle'>
               <slot name="item-text"></slot>  
           </div>
</div> 

</template>
<script> 
export default {
  name:"TabBarItem",
  props:{
  path:String,
  activeColor:{
   type:String,
   defaule:"red"
 }

  },
  data(){
    return{
      // isActive:true
}
  },
  methods:{
    itemClick(){
     this.$router.replace(this.path)
    }
  },
  computed:{
    isActive(){
      return this.$route.path.indexOf(this.path) !==-1
    },
   activeStyle() {
        return this.isActive ? {color:this.activeColor} : {}
        // return console.log(this.isActive)
      }
  }
    
}
</script>
<style scoped>
  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }
  .tab-bar-item .active{
    color: brown;
  }
</style>
```

#### 十二，Vuex详解

###### Vuex是做什么的?

官方解释：Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。
它采用 集中式存储管理 应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。
状态管理到底是什么？
状态管理模式、集中式存储管理这些名词听起来就非常高大上，让人捉摸不透。
其实，你可以简单的将其看成把需要多个组件共享的变量全部存储在一个对象里面。
然后，将这个对象放在顶层的Vue实例中，让其他组件可以使用。
那么，多个组件是不是就可以共享这个对象中的所有变量属性了呢？
等等，如果是这样的话，为什么官方还要专门出一个插件Vuex呢？难道我们不能自己封装一个对象来管理吗？
当然可以，只是我们要先想想VueJS带给我们最大的便利是什么呢？没错，就是响应式。
如果你自己封装实现一个对象能不能保证它里面所有的属性做到响应式呢？当然也可以，只是自己封装可能稍微麻烦一些。
不用怀疑，Vuex就是为了提供这样一个在多个组件间共享状态的插件，用它就可以了。

###### 管理什么状态呢?

但是，有什么状态时需要我们在多个组件间共享的呢？
如果你做过大型开放，你一定遇到过多个状态，在多个界面间的共享问题。
比如用户的登录状态、用户名称、头像、地理位置信息等等。
比如商品的收藏、购物车中的物品等等。
这些状态信息，我们都可以放在统一的地方，对它进行保存和管理，而且它们还是响应式的（待会儿我们就可以看到代码了，莫着急）。

OK，从理论上理解了状态管理之后，让我们从实际的代码再来看看状态管理。
毕竟，Talk is cheap, Show me the code.(来自Linus)

我们先来看看但界面的状态管理吧.

###### 单界面的状态管理

我们知道，要在单个组件中进行状态管理是一件非常简单的事情
什么意思呢？我们来看下面的图片。

​	![image-20210612095914603](C:\文件\web\vue\vue-md-image\单页面状态管理.png)

这图片中的三种东西，怎么理解呢？
State：不用多说，就是我们的状态。（你姑且可以当做就是data中的属性）
View：视图层，可以针对State的变化，显示不同的信息。（这个好理解吧？）
Actions：这里的Actions主要是用户的各种操作：点击、输入等等，会导致状态的改变。

写点代码，加深理解：
看下右边的代码效果, 肯定会实现吧?

```vue
<template>
<div>
    <h2>当前计数:{{counter}}</h2>
    <button @click="counter++">+</button>  
    <button @click="counter--">-</button>    

</div>
</template>
<script>
export default {
    name:"Axios1",
    data(){
        return{
            counter:0
        }
    }
}
</script>

```

在这个案例中，我们有木有状态需要管理呢？没错，就是个数counter。

counter需要某种方式被记录下来，也就是我们的State。

counter目前的值需要被显示在界面中，也就是我们的View部分。

界面发生某些操作时（我们这里是用户的点击，也可以是用户的input），需要去更新状态，也就是我们的Actions

这不就是上面的流程图了吗？

###### 多界面状态管理

Vue已经帮我们做好了单个界面的状态管理，但是如果是多个界面呢？
多个试图都依赖同一个状态（一个状态改了，多个界面需要进行更新）
不同界面的Actions都想修改同一个状态（Home.vue需要修改，Profile.vue也需要修改这个状态）
也就是说对于某些状态(状态1/状态2/状态3)来说只属于我们某一个试图，但是也有一些状态(状态a/状态b/状态c)属于多个试图共同想要维护的
状态1/状态2/状态3你放在自己的房间中，你自己管理自己用，没问题。
但是状态a/状态b/状态c我们希望交给一个大管家来统一帮助我们管理！！！
没错，Vuex就是为我们提供这个大管家的工具。
全局单例模式（大管家）
我们现在要做的就是将共享的状态抽取出来，交给我们的大管家，统一进行管理。
之后，你们每个试图，按照我规定好的规定，进行访问和修改等操作。
这就是Vuex背后的基本思想。

###### Vuex状态管理图例

![image-20210612101317414](C:\文件\web\vue\vue-md-image\xuex状态管理.png)

###### 简单的案例

用vuex实现前面的案例

1.安装vuex3.0

```
npm install --save vuex	
```

安装vuex4.0

```
npm install vuex@next --save
```

首先，我们需要在某个地方存放我们的Vuex代码：

这里，我们先在src下创建一个文件夹store，并且在其中创建一个index.js文件

2.在index.js文件中写入如下代码

vuex3.0

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
  },
  //同步操作，尽量别在里面进行异步操作
  mutations: {
   
    },
  //异步操作
  actions: {
    //context上下文
  },
  modules: {
  },
  getters:{
  }
})

```

vuex4.0

```js
import { createStore } from 'vuex'

export default createStore({
    //状态管理
  state: {
  },
    //同步操作
  mutations: {
  },
    //异步操作
  actions: {
  },
    //模块开发，可以创建管理多个store
  modules: {
  }
})

```

3.挂载到Vue实例中

```js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

createApp(App).use(store).use(router).mount('#app')
```

4.使用Vuex的counter

好的，这就是使用Vuex最简单的方式了。
我们来对使用步骤，做一个简单的小节：
1.提取出一个公共的store对象，用于保存在多个组件中共享的状态
2.将store对象放置在new Vue对象中，这样可以保证在所有的组件中都可以使用到
3.在其他组件中使用store对象中保存的状态即可
通过this.$store.state.属性的方式来访问状态
通过this.$store.commit('mutation中方法')来修改状态
注意事项：
我们通过提交mutation的方式，而非直接改变store.state.count。
这是因为Vuex可以更明确的追踪状态的变化，所以不要直接改变store.state.count的值

```vue
<template>
  <div>
      <h2>{{counter}}</h2> 
      <button @click="increment"> + </button>
      <button @click="decrement"> - </button>
       </div>
</template>

<script>
export default {
    name:"vuex1.vue",
    data(){
        return{
           
        }
    },
    computed:{
        counter(){
            return this.$store.state.count
        }
    },
    methods:{
        increment(){
            this.$store.commit('increment')
        },
         decrement(){
            this.$store.commit('decrement')
        }
    }

}
</script>


```

5.store--index.js完成对状态的操作

```js
import { createStore } from 'vuex'

export default createStore({
  state: {
    count:0
  },
  mutations: {
    increment(state){
     state.count++
    },
    decrement(state){
      state.count--
     },
     
  },
  actions: {
  },
  modules: {
  }
})

```

##### Vuex核心概念

Vuex有几个比较核心的概念:
State
Getters
Mutation
Action
Module
我们对它进行一一介绍.

###### State单一状态树

Vuex提出使用单一状态树, 什么是单一状态树呢？
英文名称是Single Source of Truth，也可以翻译成单一数据源。
但是，它是什么呢？我们来看一个生活中的例子。
OK，我用一个生活中的例子做一个简单的类比。
我们知道，在国内我们有很多的信息需要被记录，比如上学时的个人档案，工作后的社保记录，公积金记录，结婚后的婚姻信息，以及其他相关的户口、医疗、文凭、房产记录等等（还有很多信息）。
这些信息被分散在很多地方进行管理，有一天你需要办某个业务时(比如入户某个城市)，你会发现你需要到各个对应的工作地点去打印、盖章各种资料信息，最后到一个地方提交证明你的信息无误。
这种保存信息的方案，不仅仅低效，而且不方便管理，以及日后的维护也是一个庞大的工作(需要大量的各个部门的人力来维护，当然国家目前已经在完善我们的这个系统了)。
这个和我们在应用开发中比较类似：
如果你的状态信息是保存到多个Store对象中的，那么之后的管理和维护等等都会变得特别困难。
所以Vuex也使用了单一状态树来管理应用层级的全部状态。
单一状态树能够让我们最直接的方式找到某个状态的片段，而且在之后的维护和调试过程中，也可以非常方便的管理和维护。

###### Getters基本使用

有时候，我们需要从store中获取一些state变异后的状态，比如下面的Store中：

获取学生年龄大于20的个数。

可以在组件中改变，但是官方不提倡

```js
  computed:{
        getOldAge1(){
            return this.$store.state.students.filter( s => s.age>=20).length
        }

    },
```

我们可以在Store中定义getters

```js
    getOldAge(state){
      return state.students.filter(s=>s.age>=20).length
    }
  },
```

###### Getters作为参数和传递参数

getters默认是不能传递参数的, 如果希望传递参数, 那么只能让getters本身返回另一个函数.

比如上面的案例中,我们希望根据age获取用户的信息

```js
  moreAge(state){
      return function(age){
        return state.students.filter(s => s.age > age)
      }
    }
```

###### Mutation状态更新

Vuex的store状态的更新唯一方式：提交Mutation
Mutation主要包括两部分：
字符串的事件类型（type）
一个回调函数（handler）,该回调函数的第一个参数就是state。
mutation的定义方式：

```js
 mutations: {
    increment(state){
     state.count++
    },
    decrement(state){
      state.count--
     },
     
  },
```

通过mutation更新,通过组件提交过来

```js
 methods:{
        increment(){
            this.$store.commit('increment')
        },
         decrement(){
            this.$store.commit('decrement')
        }
    }
```

###### Mutation传递参数

在通过mutation更新数据的时候, 有可能我们希望携带一些额外的参数
参数被称为是mutation的载荷(Payload)
Mutation中的代码:

store

```js
  decrement1(state,n){
       state.count -= n; 
     },
```

组件中methods中

```js
  decrement1(){
            this.$store.commit('decrement1',2)
        },
```

但是如果参数不是一个呢?
比如我们有很多参数需要传递.
这个时候, 我们通常会以对象的形式传递, 也就是payload是一个对象.
这个时候可以再从对象中取出相关的信息.

store mutation

```js
 changeCount(state,payload){
      state.count = payload.count
     }
```

组件中methods中

```js
 changeCount(){
            this.$store.commit('changeCount',{count:5})
        }
```

###### Mutation提交风格

上面的通过commit进行提交是一种普通的方式
Vue还提供了另外一种风格, 它是一个包含type属性的对象

```js
  changeCount1(){
            this.$store.commit({
                type:'changeCount1',
                count:100
            })
        }
```

Mutation中的处理方式是将整个commit的对象作为payload使用, 所以代码没有改变, 依然如下

```js
    changeCount1(state,payload){
      state.count = payload.count
     }
```

###### Mutation响应规则

Vuex的store中的state是响应式的, 当state中的数据发生改变时, Vue组件会自动更新.
这就要求我们必须遵守一些Vuex对应的规则:
提前在store中初始化好所需的属性.
当给state中的对象添加新属性时, 使用下面的方式:
方式一: 使用Vue.set(obj, 'newProp', 123)
方式二: 用心对象给旧对象重新赋值
我们来看一个例子:
当我们点击更新信息时, 界面并没有发生对应改变.

```js
  updateInfo(state,payload){
      state.info['height'] = payload.info
     }
```

```js
   updateInfo(){
            this.$store.commit('updateInfo',{height:188})
        }
```

如何才能让它改变呢?
查看下面代码的方式一和方式二
都可以让state中的属性是响应式的.

```js
   updateInfo(state,payload){
      // state.info['height'] = payload.info
         // 方式一Vue.set
         Vue.set(state.info,'height',payload.height)
        //  方式二：给info赋值新的对象
        state.info={...state.info,'height': payload.height}
     }
```

###### Mutation常量类型– 概念

我们来考虑下面的问题:
在mutation中, 我们定义了很多事件类型(也就是其中的方法名称).
当我们的项目增大时, Vuex管理的状态越来越多, 需要更新状态的情况越来越多, 那么意味着Mutation中的方法越来越多.
方法过多, 使用者需要花费大量的经历去记住这些方法, 甚至是多个文件间来回切换, 查看方法名称, 甚至如果不是复制的时候, 可能还会出现写错的情况.
如何避免上述的问题呢?
在各种Flux实现中, 一种很常见的方案就是使用常量替代Mutation事件的类型.
我们可以将这些常量放在一个单独的文件中, 方便管理以及让整个app所有的事件类型一目了然.
具体怎么做呢?
我们可以创建一个文件: mutation-types.js, 并且在其中定义我们的常量.
定义常量时, 我们可以使用ES2015中的风格, 使用一个常量来作为函数的名称.

- Mutation常量类型 – 代码

 mutation-types.js

```js
export const UPDATE_INFO='UPDATE_INFO'
```

mutation

```js
//导入
import * as types from "./mutation-types";
[types.UPDATE_INFO](state,payload){
        state.info={...state.info,'height': payload.height}
     }
```

组件中

```js
//导入 
import {UPDATE_INFO} from "../store/mutation-types";
 updateInfo(){
            this.$store.commit(UPDATE_INFO,{height:188})
         
        }
```

###### Mutation同步函数

通常情况下, Vuex要求我们Mutation中的方法必须是同步方法.
主要的原因是当我们使用devtools时, 可以devtools可以帮助我们捕捉mutation的快照.
但是如果是异步操作, 那么devtools将不能很好的追踪这个操作什么时候会被完成.
比如我们之前的代码, 当执行更新时, devtools中会更新
但是, 如果Vuex中的代码, 我们使用了异步函数: 

你会发现state中的info数据一直没有被改变, 因为他无法追踪到.
So, 通常情况下, 不要再mutation中进行异步的操作

###### Action的基本定义

我们强调, 不要再Mutation中进行异步操作.
但是某些情况, 我们确实希望在Vuex中进行一些异步操作, 比如网络请求, 必然是异步的. 这个时候怎么处理呢?
Action类似于Mutation, 但是是用来代替Mutation进行异步操作的.
Action的基本使用代码如下:
context是什么?
context是和store对象具有相同方法和属性的对象.
也就是说, 我们可以通过context去进行commit相关的操作, 也可以获取context.state等.
但是注意, 这里它们并不是同一个对象, 为什么呢? 我们后面学习Modules的时候, 再具体说.
这样的代码是否多此一举呢?
我们定义了actions, 然后又在actions中去进行commit, 这不是脱裤放屁吗?
事实上并不是这样, 如果在Vuex中有异步操作, 那么我们就可以在actions中完成了.

1.在Vue组件中, 如果我们调用action中的方法, 那么就需要使用dispatch

```
 increment(){
            this.$store.dispatch('incrementAC')
        }
```

2.在action接收组件传过来的事件

```js
  actions: {
    incrementAC(context){
      context.commit('incrementMu')
    }
  },
```

3.mutation中处理action提交过来的事件

```js
incrementMu(){
	console.log('提交成功')
}
```

- 同样的, 也是支持传递payload

vue组件

```js
increment(){
            this.$store.dispatch('incrementAction',{count:100})
        }
```

action

```js
  actions: {
    incrementAction(context,payload){
      setTimeout(() =>{
      context.commit('incremenMuta',payload)
      },3000)
    }
  },
```

mutation

```
 incremenMuta(state,payload){
       state.count += payload.count
     }
```

###### Action返回的Promise

ES6语法中, Promise经常用于异步操作.

在Action中, 我们可以将异步操作放在一个Promise中, 并且在成功或者失败后, 调用对应的resolve或reject.

OK, 我们来看下面的代码:

vue组件:

```js
  increment(){
            // this.$store.dispatch('incrementAction',{count:100})
            this.$store.dispatch('incrementAction').then(res => {
                console.log('完成了操作')  
            })
        }
```

action:

```js
  incrementAction(context){
      return new Promise((resolve) =>{
        setTimeout(() => {
      context.commit('incremenMuta')
      resolve();
        },1000)
      })
    }
```

mutation:

```js
incremenMuta(state,payload){

     }
```

认识Module

Module是模块的意思, 为什么在Vuex中我们要使用模块呢?
Vue使用单一状态树,那么也意味着很多状态都会交给Vuex来管理.
当应用变得非常复杂时,store对象就有可能变得相当臃肿.
为了解决这个问题, Vuex允许我们将store分割成模块(Module), 而每个模块拥有自己的state、mutation、action、getters等

我们按照什么样的方式来组织模块呢? 


```js
import { createStore, storeKey } from 'vuex'
  const moduleA={
    state:{},
    mutations:{},
    actions:{},
    getters:{},
  }
  const modulB={
    state:{},
    mutations:{},
    actions:{},
    getters:{},
  }

export default createStore({

  modules: {
    a:moduleA,
    b:moduleB
  }
})
store.state.a //moduleA的状态
store.state.b //moduleB的状态


```

###### Module局部状态

上面的代码中, 我们已经有了整体的组织结构, 下面我们来看看具体的局部模块中的代码如何书写.
我们在moduleA中添加state、mutations、getters
mutation和getters接收的第一个参数是局部状态对象

```js
 computed:{
            count(){
                return this.$store.getters.dobCount
            }
    },
    methods:{
        increment(){
            this.$store.commit('increment')
        }
        }
```

```js
import { createStore, storeKey } from 'vuex'
  const moduleA={
    state:{
      count:1
    },
    mutations: {
        increment(state){
         state.count++
        },
      },
        getters:{
          dobCount(state){
            return state.count * 2
          }
        }
}
  const moduleB={
    state:{},
    mutations:{},
    actions:{},
    getters:{},
  }

export default createStore({
  modules: {
    a:moduleA,
    b:moduleB
  }
})



```

- Actions的写法

actions的写法呢? 接收一个context参数对象

局部状态通过 context.state 暴露出来，根节点状态则为 context.rootState

```js
     actions:{ 
          incrementSum({state,commit,rootState}){
            if((state.count+rootState.count) % 2===1 ){
              commit('increment')
            }
          }
        }
```

如果getters中也需要使用全局的状态, 可以接受更多的参数

```js
  getters:{
          sunRoot(state,getters,rootState){
           return state.count+rootState.count
          }
        },
```

###### 项目结构

当我们的Vuex帮助我们管理过多的内容时, 好的项目结构可以让我们的代码更加清晰.

store

|————index.js          组装并导出store的地方

|————actions.js       根级别的actions

|————mutations.js    根级别的mutations

|————getters.js    根级别的getters

|————modules    

​						|—— cart.js  购物车模块

​						|——product.js 产品模块

index.js

```js
import { createStore } from 'vuex'
import mutations from './mutations'
import actions from './actions'
import getters from './getters'

const state={
  cartList:[{}]
}
const store = createStore({
  state,
  getters,
  mutations,
  actions,
  modules: {

  }
})

export default store

```

getters.js   其他几个一样

```js
export default{
    cartLength(state){
        return state.cartList.length
    },
}
```

#### 十三，网络模块封装

##### 主要内容

常见的网络请求模块，以及优缺点对比。
JSONP的原理和封装
JSONP原理回顾
JSONP请求封装
axios的内容详解
认识axios网络模块
发送基本请求
axios创建实例
axios拦截器的使用

###### 选择什么网络模块?

Vue中发送网络请求有非常多的方式, 那么, 在开发中, 如何选择呢?

1.选择一: 传统的Ajax是基于XMLHttpRequest(XHR)

为什么不用它呢?
非常好解释, 配置和调用方式等非常混乱.
编码起来看起来就非常蛋疼.
所以真实开发中很少直接使用, 而是使用jQuery-Aja

2.选择二: 在前面的学习中, 我们经常会使用jQuery-Ajax

相对于传统的Ajax非常好用.
为什么不选择它呢?
首先, 我们先明确一点: 在Vue的整个开发中都是不需要使用jQuery了.
那么, 就意味着为了方便我们进行一个网络请求, 特意引用一个jQuery, 你觉得合理吗?
jQuery的代码1w+行.
Vue的代码才1w+行.
完全没有必要为了用网络请求就引用这个重量级的框架.
3.选择三: 官方在Vue1.x的时候, 推出了Vue-resource.

Vue-resource的体积相对于jQuery小很多.
另外Vue-resource是官方推出的.
为什么不选择它呢?
在Vue2.0退出后, Vue作者就在GitHub的Issues中说明了去掉vue-resource, 并且以后也不会再更新.
那么意味着以后vue-reource不再支持新的版本时, 也不会再继续更新和维护.
对以后的项目开发和维护都存在很大的隐患.
4.选择四: 在说明不再继续更新和维护vue-resource的同时, 作者还推荐了一个框架: axios为什么不用它呢?

axios有非常多的优点, 并且用起来也非常方便.
稍后, 我们对他详细学习.

###### jsonp

在前端开发中, 我们一种常见的网络请求方式就是JSONP
使用JSONP最主要的原因往往是为了解决跨域访问的问题.
JSONP的原理是什么呢?
JSONP的核心在于通过<script>标签的src来帮助我们请求数据.
原因是我们的项目部署在domain1.com服务器上时, 是不能直接访问domain2.com服务器上的资料的.
这个时候, 我们利用<script>标签的src帮助我们去服务器请求到数据, 将数据当做一个javascript的函数来执行, 并且执行的过程中传入我们需要的json.
所以, 封装jsonp的核心就在于我们监听window上的jsonp进行回调时的名称.
JSONP如何封装呢?
我们一起自己来封装一个处理JSONP的代码吧.

###### 为什么选择axios?

 作者推荐和功能特点

2016年11月作者公布axios

功能特点:
在浏览器中发送 XMLHttpRequests 请求
在 node.js 中发送 http请求
支持 Promise API
拦截请求和响应
转换请求和响应数据
等等

###### axiox请求方式

支持多种请求方式:
axios(config)
axios.request(config)
axios.get(url[, config])
axios.delete(url[, config])
axios.head(url[, config])
axios.post(url[, data[, config]])
axios.put(url[, data[, config]])
axios.patch(url[, data[, config]])
如何发送请求呢?
我们看一下左边的案例

###### 安装使用

安装axios

```
cnpm install axios --save
```

引入

```
import Axios from 'axios';
```

###### 发送get请求演示

```vue
<template>
</template>

<script>
import Axios from 'axios';
export default {
    name:"AXios_stu",
    created(){
       
        //为什么这里没有跨域问题
        //1.没有请求参数
        Axios.get('http://123.207.32.32:8000/category')
        .then(res => {
            console.log(res);
        }).catch(err => {
            console.log(err)
        })

        //2.有参数请求
        Axios.get('http://123.207.32.32:8000/home/data',
            {params:{type:'sell',page:1}})
            .then(res => {
                console.log(res)
        }).catch( err => {
            console.log(err)
        })

    },

}
</script>

```

###### 发送并发请求

有时候, 我们可能需求同时发送两个请求

使用axios.all, 可以放入多个请求的数组.

axios.all([]) 返回的结果是一个数组，使用 axios.spread 可将数组 [res1,res2] 展开为 res1, res2

```js
//发送并发请求
    axios.all([
        axios.get('http://123.207.32.32:8000/category'),
         axios.get('http://123.207.32.32:8000/home/data',
            {params:{type:'sell',page:1}})
            ]).then(axios.spread((res1,res2) => {
                console.log(res1)
                 console.log(res2)
            }))
    
```

###### 全局配置

在上面的示例中, 我们的BaseURL是固定的

事实上, 在开发中可能很多参数都是固定的.

这个时候我们可以进行一些抽取, 也可以利用axiox的全局配置

```js
axios.defaults.baseURL = ‘123.207.32.32:8000’
axios.defaults.headers.post[‘Content-Type’] = ‘application/x-www-form-urlencoded’;

```

```js
      //提取全局配置
    axios.defaults.baseURL = 'http://123.207.32.32:8000'
    
     //发送并发请求
    axios.all([
        axios.get('/category'),
         axios.get('/home/data',
            {params:{type:'sell',page:1}})
            ]).then(axios.spread((res1,res2) => {
                console.log(res1)
                 console.log(res2)
            }))
```

###### 常见的配置选项

1.请求地址 

```
url: '/user',
```


2.请求类型

```
 method: 'get', 
```

3.请根路径

```
baseURL: 'http://www.mt.com/api',
```

5.请求前的数据处理 

4.请求前的数据处理 

```
transformRequest:[function(data){}],
```

6.请求后的数据处理

```
transformResponse: [function(data){}],
```

7.自定义的请求头

```
headers:{'x-Requested-With':'XMLHttpRequest'},
```

8.URL查询对象

```
params:{ id: 12 },
```

9.查询对象序列化函数

```
paramsSerializer: function(params){ }
request body
data: { key: 'aa'},
```

10.超时设置s

```
timeout: 1000,
```

11.跨域是否带Token

```
withCredentials: false,
```

12.自定义请求处理

```
adapter: function(resolve, reject, config){},
```

13.身份验证信息

```
auth: { uname: '', pwd: '12'},
```

14.响应的数据格式 json / blob /document /arraybuffer / text / stream

```
responseType: 'json',
```

###### axios的实例

为什么要创建axios的实例呢?
当我们从axios模块中导入对象时, 使用的实例是默认的实例.
当给该实例设置一些默认配置时, 这些配置就被固定下来了.
但是后续开发中, 某些配置可能会不太一样.
比如某些请求需要使用特定的baseURL或者timeout或者content-Type等.
这个时候, 我们就可以创建新的实例, 并且传入属于该实例的配置信息

```js
    //创建新的实例
    const axiosInstance = axios.create({
        baseURL : 'http://123.207.32.32:8000',
        timeout:3000,
        headers:{
            'Content-Type':'application/x-www-form-urlencoded'
        }
    })
    axiosInstance({
        url:'/category',
        method:'get',
    }).then( res => {
        console.log(res)
    }).catch( err => {
        console.log(err)
    })

```

##### axios封装

```js
import OriginAxios from 'axios';

export default function axios (option){
    return new Promise ((resolve,reject) => {
        //1,创建axios的实例
        const instance = OriginAxios.create({
            baseURl:'/api',
            timeout:5000,
            headers:'',
        })
        //2,传入对象进行网络请求
        instance(option).then(res => {
            resolve (res)
        }).catch( err => {
            reject(err)
        })
    });
}
```

axios本身返回的就是一个promise，所以promise在这里是多余的，请求用以下方法就行

把instance返回，相当与返回promise

```js
import OriginAxios from 'axios';

export default function axios (config){
    // return new Promise ((resolve,reject) => {
        //1,创建axios的实例
        const instance = OriginAxios.create({
            baseURl:'http://123.207.32.32:8000',
            timeout:5000,
            headers:'',
        })
    
  // 2.发送真正的网络请求
  return instance(config)
}
```

组件中使用

```js
import axiosConfig from '../axios'
export default {
    name:"AXios_stu",
    created(){
      axiosConfig({
            url:'/category',
            methods:'get',
        }).then( res => {
            console.log(res)
        }).catch( err => {
            console.log(err)
        })
}
}
```



###### 如何使用拦截器？

axios提供了拦截器，用于我们在发送每次请求或者得到相应后，进行对应的处理。

如何使用拦截器呢？

```js
import OriginAxios from 'axios';

export default function axios (config){
        //1,创建axios的实例
        const instance = OriginAxios.create({
            baseURl:'http://123.207.32.32:8000',
            timeout:5000,
            headers:'',
        })
 
    //2.配置请求和响应拦截
    instance.interceptors.request.use(config => {
        console.log('来到了request拦截success中');
        return config
    }, err => {
        console.log('来到了request拦截failure中');
        return err
    })

    instance.interceptors.response.use(response => {
        console.log('来到了response拦截success中');
        return response
    }, err => {
        console.log('来到了response拦截failure中');
        return err
    })

    
  // 3.发送真正的网络请求
  return instance(config)
}
```

###### 拦截器中都做什么呢？

请求拦截可以做到的事情：

请求拦截中错误拦截较少，通常都是配置相关的拦截

可能的错误比如请求超时，可以将页面跳转到一个错误页面中。

```js
  //配置请求拦截
    instance.interceptors.request.use(config => {
        console.log('来到了request拦截success中');
        //  1.当发送网络请求是，在页面添加添加一个loading组件，作为动画
        //2.某些要求用户登录时，判断是否有token，如果没有跳转到login页面
        //3.对求请求的数据进行序列化
        config.data =qs.stringify(config.data)
        return config
    }, err => {
        console.log('来到了request拦截failure中');
        return err
    })
```

响应拦截中完成的事情：

响应的成功拦截中，主要是对数据进行过滤。

响应的失败拦截中，可以根据status判断报错的错误码，跳转到不同的错误提示页面。

```js
   // 配置响应拦截
    instance.interceptors.response.use(response => {
        console.log('来到了response拦截success中');
        return response.data
    }, err => {
        console.log('来到了response拦截failure中');
        if(err && err.response){
            switch(err.response.status){
                case 400:
                    err.message = '请求错误'
                break
                case 401 :
                    err.message = '未授权的访问'
                break
                }   
        }
        return err
    })

```

###### 引入element-ui

vue-cli4.5创建Vue3.x引入element-ui

在Vue3项目根目录下

```
vue add element-plus
npm install vue-cli-plugin-element-plus
```

全局引用 -自动生成

src/plugins/element.js

```
import ElementPlus from 'element-plus'
import 'element-plus/lib/theme-chalk/index.css'
export default (app) => {
  app.use(ElementPlus)
}
```

全局按需引入

```
import { createApp } from 'vue'
import App from './App.vue'
import 'element-plus/lib/theme-chalk/index.css'
import { ElButton, ElSelect } from 'element-plus';
const app = createApp(App)
app.use(ElButton)
app.use(ElSelect)
app.mount('#app')
```

注意App.vue会被重置，注意另存再整合

###### 拦截器loading

element-ui制作一个axios拦截器loading

```js
import OriginAxios from 'axios';
import { ElLoading } from 'element-plus';

export default function axios (config){

        //1,创建axios的实例
        const instance = OriginAxios.create({
            baseURl:'http://123.207.32.32:8000',
            timeout:5000,
            headers:'',
        })
 	//定义loading变量
    let loadingInstance 

    //配置请求拦截
    instance.interceptors.request.use(config => {
        console.log('来到了request拦截success中');
        //  1.当发送网络请求是，在页面添加添加一个loading组件，作为动画
        loadingInstance=  ElLoading.service({ fullscreen: true });
        return config
    }, err => {
        console.log('来到了request拦截failure中 ');
        return err
    })
   // 配置响应拦截
    instance.interceptors.response.use(response => {
        console.log('来到了response拦截success中');
        //响应拦截成功，如果loading存在，则关闭loading
            if(loadingInstance){
        loadingInstance.close()
        }
        return response.data
  
    }, err => {
        console.log('来到了response拦截failure中');
        if(err && err.response){
            switch(err.response.status){
                case 400:
                    err.message = '请求错误'
                break
                case 401 :
                    err.message = '未授权的访问'
                break
                case 404 :
                    err.message = '网页错误'
                break
                }   
        }
        return err
    })

    
  // 3.发送真正的网络请求
  return instance(config)
}

```

##### 图片本地路径放在data中

要加require才能识别

```
 list: [
 {old_image:require('../../assets/img/home/shanghai-pass.jpg'),}, { id: "123" }],
```

