# Vue

## 基本结构

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Vue基础</title>
</head>

<body>
  <div id="app">
    {{ message }}
  </div>
  <!-- 开发环境版本，包含了有帮助的命令行警告 -->
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var app = new Vue({
      el:"#app",
      data:{
        message:" 你好 小黑! "
      }
    })
  </script>
</body>

</html>
```

一个html文件，一个js文件。

需要导入vue.js  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>



## el：挂载点

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>el:挂载点</title>
</head>

<body id="body">
  {{ message }}
  <h2 id="app" class="app">
    {{ message }}
    <span> {{ message }} </span>
  </h2>
  <!-- 开发环境版本，包含了有帮助的命令行警告 -->
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var app = new Vue({
      // el:"#app",
      // el:".app",
      // el:"div",
      el:"#body",
      data:{
        message:"黑马程序员"
      }
    })
  </script>
</body>

</html>
```

**vue作用范围：**

el选项命中的元素机器内部的后代元素。

**是否可以选择其他的选择器：**

可以,建议ID选择器#app(因为唯一性)，也可以用.app类选择器和div标签选择器。

**是否可以设置其他的dom元素：**

可以设置设置除了<html>和<body>外的所有双标签。



## data：数据

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>data:数据对象</title>
</head>

<body>
    <div id="app">
        {{ message }}
        <h2> {{ school.name }} {{ school.mobile }}</h2>
        <ul>
            <li>{{ campus[0] }}</li>
            <li>{{ campus[3] }}</li>
        </ul>
    </div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                message:"你好 小黑!",
                school:{
                    name:"黑马程序员",
                    mobile:"400-618-9090"
                },
                campus:["北京校区","上海校区","广州校区","深圳校区"]
            }
        })
    </script>
</body>

</html>
```

vue用到的数据定义在data中，可以写复杂数据如上图中对象school和数组campus，在html中取得时候遵循js语法。



## Vue指令

### v-text

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>v-text指令</title>
</head>

<body>
    <div id="app">
        <h2 v-text="message+'!'">深圳</h2>
        <h2 v-text="info+'!'">深圳</h2>
        <h2>{{ message +'!'}}深圳</h2>
    </div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                message:"黑马程序员!!!",
                info:"前端与移动教研部"
            }
        })
    </script>
</body>

</html>
```

作用：设置标签内容。

默认写法会替换全部内容，使用差值表达式{{}}可以替换指定内容。

内部可以追加如+‘’的表达式。



### v-html

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-html指令</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <p v-text="message"></p>
        <p v-html="message"></p>
    </div>
    <script>
        var temp = new Vue({
            el: "#app",
            data:{
                message:"<a href='http://www.baidu.com'>百度</a>"
            }
        })
    </script>
</body>
</html>
```

v-html会将message中的html结构解析为标签。



### v-on

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-on指令</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <ul>
            <li>
                <input type="button" value="v-on指令" v-on:click="playChess">
            </li>
            <li>
                <input type="button" value="v-on指令简写" @click="playChess">
            </li>
            <li>
                <input type="button" value="双击事件" @dblclick="playChess">
            </li>
            <li>
                <p @click="appendString">{{message}}</p>
            </li>
        </ul>
    </div>
    <script>
        var temp = new Vue({
            el:"#app",
            data:{
                message:"444寝室"
            },
            methods:{
                playChess:function () {
                    alert("下棋");
                },
                appendString:function () {
                    this.message += "牛逼！ "
                }
            }
        })
    </script>
</body>
</html>
```

作用：为元素绑定事件。

格式：v-on:事件名，简写为@事件名。

绑定的方法在methods属性中



### v-on补充

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>v-on补充</title>
</head>

<body>
    <div id="app">
        <input type="button" value="点击" @click="doIt(666,'老铁')">
        <input type="text" @keyup.enter="sayHi">
    </div>
    <!-- 1.开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            methods: {
                doIt:function(p1,p2){
                    console.log("做it");
                    console.log(p1);
                    console.log(p2);
                },
                sayHi:function(){
                    alert("吃了没");
                }
            },
        })
    </script>
</body>

</html>
```

doIt(666,'老铁'),在函数调用处加上参数可以传递数据。

在事件后面加上.修饰符可以限定事件。eg：@keyup.enter表示回车键按下时；@keyup.esc表示退出键 按下时。



### 案例一：计数器

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <title>计数器</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <link rel="stylesheet" href="./css/index.css"/>
</head>

<body>
    <!-- html结构 -->
    <div id="app">
        <!-- 计数器功能区域 -->
        <div class="input-num">
            <button @click="sub">
                -
            </button>
            <span>{{message}}</span>
            <button @click="add">
                +
            </button>
        </div>
        <img src="http://www.itheima.com/images/logo.png" alt=""/>
    </div>
    <script>
        var temp = new Vue({
            el:"#app",
            data:{
                message:1
            },
            methods:{
                sub:function () {
                    if(this.message<=0) alert("已经到达最小值！");
                    else this.message--;
                },
                add:function () {
                    if(this.message>=10) alert("已经到达最大值！")
                    else this.message++;
                }
            }
        })
    </script>
<!-- 编码 -->

</body>

</html>
```

methods中通过this关键字获取data中的数据。

其中涉及样式忽略不计。



### v-show

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <title>show</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <p>
            <input type="button" value="切换显示状态" @click="changeStatu">
            <img src="./img/monkey.gif" v-show="isShow">
        </p>
        <input type="button" value="减少年纪" @click="ageSub">
        <input type="button" value="增加年纪" @click="ageAdd">
        <p>
            现在年纪：{{age}}|显示需要年纪：18
        </p>
        <img src="./img/monkey.gif" v-show="age>=18">
    </div>
    <script>
        var temp = new Vue({
            el:"#app",
            data:{
                isShow:true,
                age:17
            },
            methods:{
                ageAdd:function () {
                    this.age++;
                },
                ageSub:function(){
                  this.age--;
                },
                changeStatu:function () {
                    this.isShow = !this.isShow;
                }
            }
        })
    </script>

</body>

</html>
```

作用：控制元素的显示和隐藏。

原理：修改元素的display属性，实现显示隐藏。

值为true显示，false隐藏。

指令后面的内容，最终都会解析为bool值，故而可以写例如age>=18这样的判断式。



### v-if

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>v-if指令</title>
</head>
<body>
    <div id="app">
        <input type="button" value="切换显示" @click="toggleIsShow">
        <p v-if="isShow">黑马程序员</p>
        <p v-show="isShow">黑马程序员 - v-show修饰</p>
        <h2 v-if="temperature>=35">热死啦</h2>
    </div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                isShow:false,
                temperature:20
            },
            methods: {
                toggleIsShow:function(){
                    this.isShow = !this.isShow;
                }
            },
        })
    </script>
</body>

</html>
```

作用：根据表达式的真假切换元素的显示状态。

本质：通过操纵dom树来切换显示状态。

表达式的值为true，元素在dom树中，反之则不在。

与v-show区别：当需要频繁切换状态时候用show，反之用if(if更安全)。



### v-bind

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <title>v-bind指令</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <style>
        .active{
            border: 3px solid red;
        }
    </style>
</head>

<body>
    <div id="app">
        <ul>
            <li>
                <img src="./img/black.png">
            </li>
            <li>
                <img src="./img/black.png" v-bind:title="imgTitle">
            </li>
            <li>
                <img src="./img/black.png" :title="imgTitle" :class="isActive?'active':''" @click="changeActive">
            </li>
            <li>
                <img src="./img/black.png" :title="imgTitle" :class="{active:isActive}" @click="changeActive">
            </li>
        </ul>
    </div>
    <script>
        var temp = new Vue({
            el:"#app",
            data:{
                imgTitle:"黑马程序员",
                isActive:false
            },
            methods:{
                changeActive:function () {
                    this.isActive = !this.isActive;
                }
            }
        })
    </script>
</body>

</html>
```

作用：为元素绑定属性。

完整写法：v-bind:属性名。简写：:属性名。

若设置class样式，建议使用{css:boolean}对象的方式。



### 案例二：图片切换

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>图片切换</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <link rel="stylesheet" href="./css/index.css" />
</head>

<body>
    <div id="mask">
        <div class="center">
            <h2 class="title">
                <img src="./images/logo.png" alt="">
                深圳创维校区环境
            </h2>
            <!-- 图片 -->
            <img :src="imgList[index]" alt="" />
            <!-- 左箭头 -->
            <a href="javascript:void(0)"  class="left" v-show="index>0" @click="pre">
                <img src="./images/prev.png" alt="" />
            </a>
            <!-- 右箭头 -->
            <a href="javascript:void(0)" class="right" v-show="index<imgList.length-1" @click="next">
                <img src="./images/next.png" alt="" />
            </a>
        </div>
    </div>
    
    <script>
        var mask = new Vue({
            el:"#mask",
            data:{
                index:0,
                imgList: [
                    "./images/00.jpg",
                    "./images/01.jpg",
                    "./images/02.jpg",
                    "./images/03.jpg",
                    "./images/04.jpg",
                    "./images/05.jpg",
                    "./images/06.jpg",
                    "./images/07.jpg",
                    "./images/08.jpg",
                    "./images/09.jpg",
                    "./images/10.jpg",
                ]
            },
            methods:{
              pre:function () {
                this.index--;
              },
              next:function () {
                this.index++;
              }
            }
        })
    </script>

</body>

</html>
```

href="javascript:void(0)表示不做任何操作(防止跳转页面)，且页面上下相对位置不变。

列表数据通过数组传递，控制下标切换图片。



### v-for

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>v-for指令</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <input type="button" value="增加人员" @click="addPerson">
        <input type="button" value="裁减人员" @click="subPerson">
        <ul>
            <li v-for="(item,index) in message">
                {{index+1}} {{ item }}
            </li>
        </ul>
        <h3 v-for="item in arr">
            {{"姓名："+item.name+" 职务："+item.job}}
        </h3>
    </div>

    <script>
        var temp = new Vue({
            el:"#app",
            data:{
                message:[
                    "周显睿SB",
                    "郑泓SB",
                    "要旭晖SB",
                    "祝山山NB"
                ],
                arr:[
                    {name:"张三",job:"法外狂徒"},
                    {name:"李四",job:"厄运小姐"},
                    {name:"王五",job:"卡牌大师"}
                ]
            },
            methods:{
                addPerson:function () {
                    this.arr.push({name:"牛二",job:"流浪法师"});
                },
                subPerson:function () {
                    if(this.arr.length>0)
                        this.arr.pop();
                    else
                        alert("已经没人了！")
                }
            }
        })
    </script>

</body>

</html>
```

作用：根据数据生成列表结构。

经常和数组结合使用。

语法：(item,index) in arr ;其中index可以省略，写作item in arr (in是固定的，item和arr可以自己写)。

数组长度会同步更新到页面上，是响应式的。



### v-model(双向数据绑定)

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>v-model指令</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <input type="button" value="改变文本框信息" @click="updateM">
        <input type="text" v-model="message" @keyup.enter="getM">
        <h3>
            {{ message }}
        </h3>
    </div>
    <script>
        var temp = new Vue({
            el:"#app",
            data:{
                message:"我爱编程！"
            },
            methods:{
                updateM:function () {
                    this.message = "我仍然热爱编程！";
                },
                getM:function () {
                    alert(this.message);
                }
            }
        })
    </script>

</body>

</html>
```

v-model用于表单元素，代替value实现数据的双向绑定。

绑定的元素<->表单中的值 任一个改变都会改变另外一个。

注意：如果把@keyip.enter事件写在text文本框中，那么得先将光标移动到文本框内再按下enter才能生效。



### 案例三：记事本

```javascript
<html>
  <head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8" />
    <title>444记事本</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <link rel="stylesheet" type="text/css" href="./css/index.css" />
  </head>

  <body>
    <!-- 主体区域 -->
    <section id="todoapp">
      <!-- 输入框 -->
      <header class="header">
        <h1>444记事本</h1>
        <input v-model="inputValue" @keyup.enter="insertM"
          autofocus="autofocus"
          autocomplete="off"
          placeholder="请输入任务"
          class="new-todo"
        />
      </header>
      <!-- 列表区域 -->
      <section class="main">
        <ul class="todo-list">
          <li class="todo" v-for="(item,index) in messageList">
            <div class="view">
              <span class="index">{{index+1}}.</span>
              <label>{{item}}</label>
              <button class="destroy" @click="delM(index)"></button>
            </div>
          </li>
        </ul>
      </section>
      <!-- 统计和清空 -->
      <footer class="footer" v-show="messageList.length>0">
        <span class="todo-count"> <strong>{{messageList.length}}</strong> items left </span>
        <button class="clear-completed" @click="clearM">
          Clear
        </button>
      </footer>
    </section>

  <script>
    var temp = new Vue({
      el:"#todoapp",
      data:{
        messageList:[
                "要旭晖沙雕",
                "睿老板憨瘪",
                "泓M biss",
                "444真是太和谐了！"
        ],
        inputValue:""
      },
      methods:{
        insertM:function () {
          this.messageList.push(this.inputValue);
        },
        delM:function (index) {
          this.messageList.splice(index,1);
        },
        clearM:function () {
          this.messageList = [];
        }
      }
    })
  </script>
  </body>
</html>

```

设置提示灰色字体：placeholder="请输入任务"。

js数组增加：list.push

js数组删除：list.splice(开始索引，删除个数)

js数组清空：直接 list = []



## 网络应用

### axios

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>axios使用</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
</head>

<body>
    <div id="app">
        <input type="button" value="get请求" class="get">
        <input type="button" value="post请求" class="post">
    </div>
    <script>
        document.querySelector(".get").onclick = function () {
            axios.get("https://autumnfish.cn/api/joke/list?num=6")
            .then(function (response) {
                console.log(response.data);
            },function (err) {
                console.log(err);
            })
        }
        document.querySelector(".post").onclick = function () {
            axios.post("https://autumnfish.cn/api/user/reg",{username:"zxrSB"})
            .then(function (response) {
                console.log(response);
            },function (err) {
                console.log(err);
            })
        }
    </script>
</body>

</html>
```

导入：<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

基本格式见上面代码。

then中第一个函数在请求成功时触发，第二个函数在请求失败时触发。

then中函数参数可以携带响应内容或错误信息，get时候写get的网址即可，post时候需要传递需要的参数。



### post另一种方式

```javascript
selectProductByName:function () {
            var that = this;
             const params = new URLSearchParams();//不导入qs包，需定义一个可解析的json格式
             params.append("productName",that.inputName);
            axios.post("http://localhost:9000/selectProductByName",params)
                .then(function (message) {
                    console.log(that.inputName);
                    console.log(message.data);
                    that.products = message.data;
                }).catch(function (err){
                console.log(err);
            })
        }
```





### axios-vue

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>axios使用</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
</head>

<body>
    <div id="app">
        <input type="button" value="获取一个笑话" @click="getJoke">
        <br>
        {{joke}}
    </div>
    <script>
        var temp = new Vue({
            el:"#app",
            data:{
                joke:"一个笑话。"
            },
            methods:{
                getJoke:function () {
                    var that = this;
                    axios.get("https://autumnfish.cn/api/joke").then(
                        function (response) {
                            that.joke = response.data;
                        },function (err) {
                            console.log(err);
                        }
                    )
                }
            }
        })
    </script>
</body>

</html>
```

``axios回调函数中的this已经改变，无法访问到data中的数据，需要另外定义一个变量保存this。``

### 传输复杂数据

一定用json格式传输！设置headers:{'content-type':'application/json'}，后端用map或者list接收，然后通过get(“key”)提取所需信息



### 案例四：天知道

```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>天知道</title>
    <link rel="stylesheet" href="css/reset.css" />
    <link rel="stylesheet" href="css/index.css" />
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <!-- 官网提供的 axios 在线地址 -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <!-- 自己的js -->
  </head>

  <body>
    <div class="wrap" id="app">
      <div class="search_form">
        <div class="logo"><img src="img/logo.png" alt="logo" /></div>
        <div class="form_group">
          <input v-model="city" @keyup.enter="searchWeather"
            type="text"
            class="input_txt"
            placeholder="请输入查询的城市"
          />
          <button class="input_sub" @click="searchWeather">
            搜 索
          </button>
        </div>
        <div class="hotkey">
          <a href="javascript:" v-for="item in cityList" @click="clickSearch(item)">{{item}}</a>
        </div>
      </div>
      <ul class="weather_list">
        <li v-for="item in weatherInfo">
          <div class="info_type"><span class="iconfont">{{item.type}}</span></div>
          <div class="info_temp">
            <b>{{item.low}})</b>
            ~
            <b>{{item.high}}</b>
          </div>
          <div class="info_date"><span>{{item.date}}</span></div>
        </li>
      </ul>
    </div>
    <script>
      var temp = new Vue({
        el:"#app",
        data:{
          city:"",
          cityList:[
                  "北京",
                  "上海",
                  "广州",
                  "深圳"
          ],
          weatherInfo:[]
        },
        methods:{
          searchWeather:function () {
            var that = this;
            axios.get("http://wthrcdn.etouch.cn/weather_mini?city="+this.city)
            .then(function (message) {
              that.weatherInfo = message.data.data.forecast;
            }).catch(function (err) {
              console.log(err);
            })
          },
          clickSearch:function (clickCity) {
            this.city = clickCity;
            this.searchWeather();
          }
        }
      })
    </script>


  </body>
</html>

```



### 案例五：音乐播放器

###### **html部分**

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />
  <title>悦听player</title>
  <!-- 样式 -->
  <link rel="stylesheet" href="./css/index.css">
</head>

<body>
  <div class="wrap">
    <!-- 播放器主体区域 -->
    <div class="play_wrap" id="player">
      <div class="search_bar">
        <img src="images/player_title.png" alt="" />
        <!-- 搜索歌曲 -->
        <input type="text" autocomplete="off" v-model="query" @keyup.enter="searchMusic" />
      </div>
      <div class="center_con">
        <!-- 搜索歌曲列表 -->
        <div class='song_wrapper'>
          <ul class="song_list">
           <li v-for="item in musicList">
             <a href="javascript:;" @click="playMusic(item.id)"></a> <b>{{item.name}}</b>
             <span>
               <i v-if="item.mvid!=0" @click="playMv(item.mvid)"></i>
             </span>
           </li>
          </ul>
          <img src="images/line.png" class="switch_btn" alt="">
        </div>
        <!-- 歌曲信息容器 -->
        <div class="player_con" class="playing" :class="{playing:isPlay}">
          <img src="images/player_bar.png" class="play_bar" />
          <!-- 黑胶碟片 -->
          <img src="images/disc.png" class="disc autoRotate" />
          <img :src="musicPictureURL" class="cover autoRotate" />
        </div>
        <!-- 评论容器 -->
        <div class="comment_wrapper">
          <h5 class='title'>热门留言</h5>
          <div class='comment_list'>
            <dl v-for="item in hotComments">
              <dt><img :src="item.user.avatarUrl" alt=""></dt>
              <dd class="name">{{item.user.nickname}}</dd>
              <dd class="detail">
                {{item.content}}
              </dd>
            </dl>
          </div>
          <img src="images/line.png" class="right_line">
        </div>
      </div>
      <div class="audio_con">
        <audio ref='audio'  v-bind:src="musicURL" @play="play" @pause="pause"
               controls autoplay loop class="myaudio"></audio>
      </div>
      <div class="video_con" v-show="isShowMv" >
        <video  controls="controls" :src="mvURL" autoplay="true"></video>
        <div class="mask" @click="closeMv"></div>
      </div>
    </div>
  </div>
  <!-- 开发环境版本，包含了有帮助的命令行警告 -->
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <!-- 官网提供的 axios 在线地址 -->
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  <!--自己的js-->
  <script src="./js/myjs.js"></script>
</body>

</html>
```

###### **js部分**

```javascript
var temp = new Vue({
    el:"#player",
    data:{
        query:"",
        musicList:[],
        musicURL:"",
        musicPictureURL:"",
        hotComments:[],
        userInfo:[],
        isPlay:false,
        mvURL:"",
        isShowMv:false
    },
    methods:{
        //搜索歌曲
        searchMusic:function () {
            var that = this;
            axios.get("https://autumnfish.cn/search?keywords="+that.query)
                .then(function (message) {
                    that.musicList = message.data.result.songs;
                    //console.log(that.musicList);
                }),function (err) {
                    console.log(err);
            }
        },
        //播放歌曲
        playMusic:function (musicId) {
            var that = this;
            //获取歌曲地址
            axios.get("https://autumnfish.cn/song/url?id="+musicId)
                .then(function(message){
                    //console.log(message);
                    that.musicURL = message.data.data[0].url;
                    //console.log(that.musicURL);
                }),function (err) {
                    console.log(err);
            }
            //获取专辑图片地址
            axios.get("https://autumnfish.cn/song/detail?ids="+musicId)
                .then(function (message) {
                    //console.log(message);
                    that.musicPictureURL = message.data.songs[0].al.picUrl;
                    //console.log(that.musicPictureURL);
                }),function (err) {
                console.log(err);
            }
            //获取评论
            axios.get("https://autumnfish.cn/comment/hot?type=0&id="+musicId)
                .then(function (message) {
                    //console.log(message);
                    that.hotComments = message.data.hotComments;
                }),function (err) {
                console.log(err);
            }
        },
        //播放
        play:function () {
            this.isPlay = true;
            console.log(this.isPlay);
        },
        //暂停
        pause:function () {
            this.isPlay = false;
            console.log(this.isPlay);
        },
        //播放mv
        playMv(mvId) {
            var that = this;
            //获取mv地址
            axios.get("https://autumnfish.cn/mv/url?id="+mvId)
                .then(function (message) {
                    that.mvURL = message.data.data.url;
                    that.isShowMv = true;
                }),function (err) {
                console.log(err);
            }
        },
        //点击遮罩关闭mv
        closeMv() {
            this.mvURL = "";
            this.isShowMv = false;
        }
    }
})
```

## 引用alibaba icon

①搜索需要的icon，添加入库

![image-20201115112556480](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115112556480.png)

②打开自己的库，选择添加到项目（先得自己创建一个项目）

![image-20201115112742794](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115112742794.png)

③进入我的项目，下载图标

![image-20201115112900044](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115112900044.png)![image-20201115112925915](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115112925915.png)

④最后在vue项目中创建icon项目，将下列文件添加进去

![image-20201115113044023](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115113044023.png)



⑤在前端通过下列方式引用![image-20201115113219594](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115113219594.png)

### 一些格式控制技巧

1.控制横向位置：

![image-20201115113412352](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115113412352.png)

2.控制输入只有数字

![image-20201115113554759](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115113554759.png)

3.控制输入只有数字和小数点

![image-20201115113619367](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115113619367.png)

4.背景图片添加

![image-20201115113924175](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115113924175.png)![image-20201115113936852](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201115113936852.png)

通过id+#id css样式控制

