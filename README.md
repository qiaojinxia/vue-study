## Vue快速入土指南

##### 一个最简单的vue入门demo

1.新建一个html网页,并且引入vue的js文件

><script src="https://cdn.jsdelivr.net/npm/vue"></script>

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Vue单文件例子</title>
  <script src="https://cdn.jsdelivr.net/npm/vue"></script>
</head>
<body>
 
</body>
</html>
```

2. 创建要绑定的div


```html

  <div id="box">
	</div>
```



2. 初始化 vue,并且绑定到 box

```javascript
<script type="text/javascript">
new Vue({
    el:"#box"
})
</script>
```



测试vue是否 引入成功,我们通过vue的插值运算符的结果来 测试,Vue会自动帮你运算渲染成30.

```html
<div id="box">
{{10+ 20}}
</div>

```



其他语法

```html
{{10 > 20 ? 'aaa':'bbb'}}//等价于 if 10 > 20 return 'aaa' else return'bbb'
```

~注意: 如果 aaa 不加单引号,那么 就会被当作一个变量,所以需要加单引号.

###### Vue定义变量

```html
<script type="text/javascript">
    new Vue({
        el:"#box"
        var1:20,
        var2:2,
        var:'<br>mytext'
    })
</script>
```

###### Mustache语法 {{}} 渲染文本变量

需求：后台数据 直接 渲染到表格、列表等。

分2不

1. 使用{{}}写入表达式
2. 如果表达式内有变量,提前在VUe中声明

```html
<div id="box">
    {{var1}} 
    {{var1 + var2}}
    {{var1 > var2 ? 'yes':'no'}}
</div>
```

###### v-html 渲染html内容

需求：有时候某些文章包含Html内容我们需要将这些数据返回给页面变成前端页面的一部分,最典型的是有些富文本编辑器文章是含html代码的,Vue为了安全 不支持通过{{}} 直接渲染内容,而是通过v-html = "变量" 来渲染html文本。

分2步

1. 不支持 直接{{var}}渲染,首先需要一个标签,在标签内添加 v-html
2. Vue中声明绑定的变量

```html
<div v-html="var">
</div>
```

###### v-model 绑定变量

需求：需要获取表单数据输入框的值。

分两步

1.设置标签绑定变量

2.Vue中声明绑定的变量

```html
<input type="text" v-model="blindvar" /> //绑定input
<textarea type="text" v-model="blindvar" ></textarea>//绑定多行文本
<label>{{blindvar}}</label>
<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
        blindvar:'',
    }
})
</script>
```

- 绑定checkBox

需求：我们需要直到表单里面check组件是否选中。

```html
<input type="checkbox" v-model="isChecked" /> //绑定checkbox
<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
       isChecked:true,
    }
})
</script>
```

- 绑定多个checkBox

  ```html
  <input type="checkbox" v-model="isCheckedList" value="Music" /> Music
  <input type="checkbox" v-model="isCheckedList" value="Running" /> Running
  <input type="checkbox" v-model="isCheckedList" value="Walk" /> Walk
  <input type="checkbox" v-model="isCheckedList" value="Swimming" /> Swimming
  <script type="text/javascript">
  new Vue({
      el:"#box",
      data:{
         isCheckedList:[],
      }
  })
  </script>
  ```

对于 多个 check 我们通过数组存储,为了区别每一个选项 我们需要加一个value 来代表每一个checkbox。

- 绑定单选框

  ```html
  <input type="radio" v-model="picked" value="Music" /> Music
  <input type="radio" v-model="picked" value="Running" /> Running
  <input type="radio" v-model="picked" value="Walk" /> Walk
  <input type="radio" v-model="picked" value="Swimming" /> Swimming
  <script type="text/javascript">
  new Vue({
      el:"#box",
      data:{
         picked:'',
      }
  })
  </script>
  ```

  

###### v-show 标签的显示隐藏

需求：需要根据后台返回数据显示隐藏某些元素、比如后台管理系统的菜单、按钮等或者通过某些点击事件,控制某些元素的隐藏显示。

分两步

1.设置标签绑定变量

2.Vue中声明绑定的变量

```html
<div v-show="!isshow" > //isshow = false 显示 div 第一步
    display false
</div>
<div v-show="isshow" >//isshow = true 显示 div
    display true
</div>

<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
        isshow:false, //定义布尔值变量 第二步
    }
})
</script>
```



###### v-if 标签的创建与删除

需求：与v-show 不同的是,v-if 会真正操作DOM并且删除一些元素,但是v-show 节点并没有被删除,只是display变成none了,所以某些情况下,可以通过v-if 经行不同视图的切换。

分两步

1.设置标签绑定变量

2.Vue中声明绑定的变量

```html
<div v-if="iscreated" >//第一步
    be created
</div>
<script type="text/javascript">
new Vue({
  el:"#box",
  data:{
 iscreated:true,//第二步
      }
})

```

###### v-else-if|v-else 标签的创建与删除

需求：需要根据多种情况判断变量的值,来执行不同的分支,与v-if 合用,可以用于想购物车判断是否有数据展示不同的页面逻辑。

分两步

1.设置标签绑定变量

2.Vue中声明绑定的变量

```html
<div v-if="select === 1">
    branch 1
</div>
<div v-else-if="select === 2">
    branch 2
</div>
<div v-else="select === 3">
    branch 3
</div>

<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
        select:1,
    }
})
</script>

```



###### :class 动态绑定标签class

需求：根据变量值,动态的修改标签的样式。

分2步

1. 设置标签绑定变量
2. Vue中声明绑定的变量

```html
//css样式
<style>
.green{
    background: #50f470;

}
.blue{
    background:blue;

}
</style>

//第一步
<div :class="isActivate?'green':'blue'">
</div>

<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
        isActivate:true,//第二步
    }
})
</script>
```



需求2：上面只是简单的三目运算符,只能 非A 即 B 但显示场景 可能要绑定多个class。

- map绑定多个:class

分2步

1. 还是老样子绑定变量
2. 我们要绑定的 不是单个变量 而是一个map(K/V),key为class的名字,value为boolean 用来设定是否绑定在标签上。



```html
<div :class="classobj">//第一步
        test clss blind
</div>
<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
        var1:1,
        isActivate:false,
        classobj:{class1:true,class2:true,class3:true}//第二步 都设置为true那么 class1 class2 class3 都会 绑定在div上
    },
    methods:{
        classtransfer(){
           this.isActivate = !this.isActivate
        }
    }
})
</script>
```



- 通过数组绑定多个:class

```html
<div :class="classarray">
    test clss blind
</div>

  classarray:['css1','css2']
```

~注意:通过map 和数组 的区别是,数组 可以在渲染后再进行添加class操作,但是通过Map 如果通过 xx.classobj['classn] =true 再往里A面添加一个

k/v vue不会再次生成getsetter方法 修改了 也不会有什么效果,而数组是可以通过push 往里面添加元素的。

###### @click 绑定Click点击事件

需求：点击按钮触发指定了方法.

分2步

1. 首先标签 绑定@click 和要触发的函数
2. Vue中添加触发的函数

```html
 <button @click="classtransfer()" >Click Me</button>//第一步 绑定按钮点击事件
<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
        var1:1,
        isActivate:false,
    },
    methods:{
        classtransfer(){//第二步:在vue声明绑定的函数
           this.isActivate = !this.isActivate//这里是对上一个方法:class 的修改通过按钮click 来动态修改 标签的类
        }
    }
})
</script>
```



###### :style 动态修改标签css样式

需求：根据数据动态的修改css样式

- 绑定的数据直接变量

分2步

1. 将:style绑定好标签后,设置css 属性,css属性可以使变量、三目运算符返回。
2. Vue中添加变量

```html
<div :style="'background:' + color">
        dynamic style
</div>

<div :style="'background:' + (isActivate?'red':'yellow')">
    dynamic style
</div>

<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
        isActivate:true,
      	color:"red"
    }
})
</script>
```



- 绑定的数据通过VueMap对象

分2步

1. 将:style绑定好标签后,把Map对象作为数据源
2. Vue中添加Map键值对,css属性以键值存储在Map中,如果是xx-xx形式的css属性就改写成 驼峰形式xxXx形式。

```html
<div :style="styleobj">
        dynamic styleobj
</div>
	
<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
         styleobj:{
            "backgroundColor":"blue",//注意background-color 这种 x-x 形式的属性 改成驼峰写法
        }
    },
  }
})
</script>
```

上面的方式缺点是,可以修改已有的样式但是没法在已有的样式上添加新的样式。 而下面一种方法 可以完美解决这个问题。

- 绑定的数据通过数组的形式

```html
<div :style="stylearr">
    dynamic stylearr
</div>
    <button @click="pushstyle()" >Push Style</button> //压入样式
    <button @click="deletestyle()" >Pop Style</button>//弹出样式
<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
        stylearr:[]
    },
  	methods:{
        pushstyle(){
            this.stylearr.push({"background":"red"})
        },
        deletestyle(){
            this.stylearr.pop("background");
        }
    }
 
  }
})
</script>
```



###### v-for 循环渲染数据

- 遍历对象生成li列表

```html
 <ul>
        <li v-for="(val,key) in|of dataobj"> //of 和 in 作用相同 
            {{key+'  '+val}}
        </li>
    </ul>

<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
         dataobj:{
            'name':"caomao",
            'age':"1",
            'sex':"xx",
            'favor':"sleep",
        },
    },
  }
})
</script>
```



- 遍历数组生成li列表

```html
<label>v-for循环列表</label>
<ul>
    <li v-for="(data,index) in datalist"> 
        {{data,index}} //数组的值和数组索引
    </li>
</ul>

<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
         datalist:["content1","content2","content3","content4"]
    },
  }
})
</script>
```



修改方法

```html
//通过数组形式生成列表的增删改
this.datalist.push(this.lidata);//添加
this.datalist.pop(this.lidata);//弹出顶部
this.datalist.splice(this.datalist.indexOf(this.lidata), 1)//删除数据
//通过Vue提供的方法 用索引给 vue修改值 
Vue.set(this.datalist,0,'caomao')
 this.datalist.splice(this.couponSelected, 1,this.lidata )
```

其他相关方法

>push() pop() shift() unshift() splice() sort() reverse() 直接改变原数组

> filter(),contact()和slice(),map() 返回新数组



~注意:通过Vue.set 我们可以对map进行属性的增加 Vue.set(this.dataobj,'caomao',true)



~注意: 对于更新数据时,我们可以通过设置一个不重复的id,来作为一句来跟新数据而不是覆盖掉原有的所有数据,这样可以减少dom的操作

```html
<ul>
    <li v-for="(data,index) in datalist" key="data"> //把数组索引作为 依据 如果原来 [0,1] 跟新后 是[1,0] 那么 那会比较索引 再去修改,如果是对象 可以设置为 每条数据的id,每次修改时 按照id去比较。
        {{data}}
    </li>
</ul>
```

###### @input 绑定input改变触发事件

需求：根据输入框输入的值,去触发后台请求,如搜索引擎会有搜索提示,另外可以对网页表格里面的值进行匹配筛选。

分2步：

1. input标签绑定@input和出发函数
2. 在methods声明要出发的函数

```html
<input type="text" v-model="myevent" @input="myinput">
<label>{{inputevent}}</label>
<script type="text/javascript">
new Vue({
    el:"#box",
    data:{
        myevent:'',
        inputevent:'',
    },
  methods:{
    myinput(){
            this.inputevent = this.myevent;
            console.log(this.myevent);

        }
  	}
  }
})
</script>
```

###### @change  绑定input焦点离开触发事件





##### 事件修饰符

###### @click.stop阻止事件冒泡

在Dom中点击时间,会向上冒泡 也就是说 你点击 一个按钮 他会把这个点击时间不停往上的传递,最终他父元素和更上面的元素都得到所以有时候我们需要阻止这种默认的传递,我们需要 代码阻止向上传递.

```html
<button @click="handler($event)"> Click Me</button>
new Vue().....
....
handler(e) {
            console.log(e);
            //阻止事件向上冒泡
            e.stopPropagation();

        }
....
```

在Vue中可以使用它提供@click.stop的方法来阻止事件冒泡的行为.

```html
<button @click.stop="handler($event)"> Click Me</button>
```



###### @click.prevent 阻止事件默认行为

需求：在某些情况下,比如提交表单 点击链接 我们 想先对数据进行校验 不让行为立马触发。

```html
<a href="http://www.baidu.com/" @click="defaulthandler($event)"> Default Action</a>
<a href="http://www.baidu.com/" @click.prevent="defaulthandler($event)">Prevent Default Action</a>
```

###### @click.self 不响应 Child事件

需求：某些情况下,我们不希望Sub的节点向上冒泡而导致自己事件被响应。

```html
<ul @click.self="justhandlermyevent($event)">
    <li @click="handlerevent($event)"> 123</li>
</ul>

....
handlerevent(e){
            alert(e);
        },justhandlermyevent(e){
            alert(e);
        }
....
```

###### @click.once 只响应一次事件

需求：某个抽奖页面,只能点击一次之后就不会有事件再去响应了。

```html
<ul @click.self="justhandlermyevent($event)">
    <li @click.once="handlerevent($event)" >once click event</li>
</ul>
....
handlerevent(e){
            alert(e);
        },justhandlermyevent(e){
            alert(e);
        }
....
```

#### 小结：实现一个文本跑马灯

1.首先我们初始化一个空的Vue项目。







##### 按键修饰符

###### @keyup.enter 响应回车键事件

```HTML
<input type="text" @keyup.enter="handlerenter($event)" />
....
handlerenter(e){
            alert(e);
        }
....
```

######  @keyup.[keynum] 按键弹起响应时间

```HTML
<input type="text" @keyup.13="handlerenter($event)" />
....
handlerenter(e){
            alert(e);
        }
....
```





#### 小结: 用Vue 实现一个购物车

1. 首先我们初始化一个空的Vue项目。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Vue单文件例子</title>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
</head>
<body>

<div id="cart">

</div>
</body>
<script type="text/javascript">
    new Vue({
        el:"#cart"
    })
</script>
</html>
```

2. 准备好数据。

```json
datalist:[

    {
        id:1,
        name:"Good1",
        price:10,
        number:1,

    },{
        id:2,
        name:"Good2",
        price:23,
        number:1,

    },{
        id:3,
        name:"Good3",
        price:43,
        number:1,

    },{
        id:4,
        name:"Good4",
        price:15,
        number:1,

    },{
        id:5,
        name:"Good5",
        price:17,
        number:1,

    },{
        id:6,
        name:"Good6",
        price:41,
        number:1,

    },{
        id:7,
        name:"Good7",
        price:32,
        number:1,

    },
]
```

3. 数据用列表方式展示,我们用v-for 生成购物车列表,购物车都是多选框选中的,所以我们还需要再放一个多选框,在列表里.

```html
<ul>
    <li v-for="good in datalist">
       <input type="checkbox"  >
            {{good}}
  	</li>
</ul>
```

4.我们需要 获取选中的check来计算价格 用v-model 绑定一个数组来记录选中的商品。

```html
<div id="cart">
    <ul>
        <li v-for="good in datalist">
            <input type="checkbox" v-model="checkarr"  >
            {{good}}
        </li>
    </ul>
    {{checkarr}}
    <p>总金额:</p>
</div>
```

5. 绑定后我们用:value="xxx" 动态绑定 也就是xxx解析为变量,而不是文本。然后我们给checkbox赋值,为 数量 * 价格

```html
<div id="cart">
    <ul>
        <li v-for="good in datalist">
            <input type="checkbox" v-model="checkarr" :value="good.price * good.number" >
            {{good}}
        </li>

    </ul>
    {{checkarr}}
    <p>总金额:{{getsummary()}}</p>
</div>
```

6. 如果我们需要每次勾选后就计算一次,其中一个思路每次勾选触发一次计算,另一种做法是 在{{ }}中写一个函数 每次 如果函数中的某些变量被改变了Vue 会自动把相关的函数执行一遍。

```html
//计算所有金额
getsummary(){
    var sum = 0;
    for(var i in this.checkarr){
        sum+= this.checkarr[i];
    }
    return sum;
}
```

7. 在购物车中经常有 全选这样的功能,如果全选  就把数据 更新为 [] 或者 [价格1,价格2]

```html
<input type="checkbox" v-model="selectall"  @change="selecta()" >

selecta(){
    if(!this.selectall){
        this.checkarr =[];
    }else{
        var arr =[];
        for(var i in this.datalist){
            arr[i] =  this.datalist[i].price * this.datalist[i].number;
        }
        console.log(arr);
        this.checkarr =arr;
    }
```



8. 为了更好的用户体验,当我们 一个个去选 都选中时,那个全选按钮应该也会被选中,反之 如果所有按钮都没全中全选按钮就不会选中,我们要实现这种动态联动的效果。那么其实最简单的就是判断数组的长度 如果全选中那么长度和列表的长度一样否则  如果全不选长度就是0,为此我们需要为checkbox绑定一个@click事件。

   ```html
    <input type="checkbox" v-model="checkarr"  @change="checkselect()" :value="good.price * good.number" >//绑定 checkselect 事件
   checkselect(){
       if(this.checkarr.length === this.datalist.length){
           this.selectall = true;
       }else if(this.checkarr.length === 0){
           this.selectall = false;
       }
   }
   ```



9. 购物车 还需要实现对商品 添加和 减少 为此 我们需要增加2个按钮,绑定@click和相应的事件并且我们需要修改当前对象所以 需要传入要修改的对象,当然 在做减商品逻辑时当数量为 1时 在去减就要出发删除操作了,吧对象从列表里删除,所以我们要用this.datalist.splice(this.datalist.indexOf(good), 1)//删除数据 我们传入的时候也要把这个对象在list里面索引也传递给处理方法以便于删除.

```html
 <button @click="makeadd(good)" >+</button>
            {{good.number}}
            <button @click="makesub(good,index)" >-</button>
makeadd(good){
    good.number ++;

},
makesub(good){
    if(good.number == 1){
        this.datalist.splice(this.datalist.indexOf(good), 1)//删除数据
    }
    good.number --;

}
```



完整实现：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Vue单文件例子</title>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
</head>
<body>

<div id="cart">
    <input type="checkbox" v-model="selectall"  @change="selecta()" >
    <ul>
        <li v-for="(good,index) in datalist">
            <input type="checkbox" v-model="checkarr"  @change="checkselect()" :value="good.price * good.number" >

            {{good}}
            <button @click="makeadd(good)" >+</button>
            {{good.number}}
            <button @click="makesub(good,index)" >-</button>
        </li>



    </ul>
    {{checkarr}}
    <p>总金额:{{ getsummary()}}</p>
</div>
</body>
<script type="text/javascript">
    new Vue({
        el:"#cart",
        data:{
            checkarr:[],
            selectall:false,
            datalist:[

                {
                    id:1,
                    name:"Good1",
                    price:10,
                    number:1,

                },{
                    id:2,
                    name:"Good2",
                    price:23,
                    number:1,

                },{
                    id:3,
                    name:"Good3",
                    price:43,
                    number:1,

                },{
                    id:4,
                    name:"Good4",
                    price:15,
                    number:1,

                },{
                    id:5,
                    name:"Good5",
                    price:17,
                    number:1,

                },{
                    id:6,
                    name:"Good6",
                    price:41,
                    number:1,

                },{
                    id:7,
                    name:"Good7",
                    price:32,
                    number:1,

                },
            ],
        },
        methods:{
            getsummary(){
                var sum = 0;
                for(var i in this.checkarr){
                    sum+= this.checkarr[i];
                }
                return sum;
            },
            selecta(){
                if(!this.selectall){
                    this.checkarr =[];
                }else{
                    var arr =[];
                    for(var i in this.datalist){
                        arr[i] =  this.datalist[i].price * this.datalist[i].number;
                    }
                    console.log(arr);
                    this.checkarr =arr;
                }
            },
            checkselect(){
                if(this.checkarr.length === this.datalist.length){
                    this.selectall = true;
                }else if(this.checkarr.length === 0){
                    this.selectall = false;
                }
            },
            makeadd(good){
                good.number ++;

            },
            makesub(good){
                if(good.number == 1){
                    this.datalist.splice(this.datalist.indexOf(good), 1)//删除数据
                }
                good.number --;

            }
        }
    })
</script>
</html>
```



