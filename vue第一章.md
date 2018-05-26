# vue-Basics


刚开始接触vue的时候，可能会很疑惑，vue到底是个什么东西，应该怎么去用？

vue简介
vue是前端的一个js框架，支持双向绑定，核心是数据驱动，只关注视图，不关注dom，vue的语法和用法都比较容易上手，兼容大部分第三方库，用vue来做组件化开发以及单页面应用都是不错的选择

vue最简单的引入方式
vue有多种引入方式，直接引入，webpack安装等，我们先来看最简单的一种，直接引入，当成一个js文件去引入

直接使用script标签引入vue

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
看两个概念解释加深一下理解：
数据驱动：使用特殊语法，把DOM与底层数据进行绑定，DOM与数据是同步的，修改了数据，就会自动更新DOM

双向数据绑定：使用MVVM，数据模型与视图模型进行绑定，数据发生改变，更新DOM；修改视图，触发DOM，数据发生改变，应用最多的，就是表单输入，当我们在输入框输入内容时，不需要做其他操作，就可以直接拿到数据放到数据模型中，当直接修改数据时，视图中显示的内容也会发生变化

与jquery对比
在学习vue的相关语法之前，我们先对vue有一个整体的认识，以及它与平时使用的jquery编程方式上有什么不同

注意：在使用vue的文件中，除了部分插件必须使用jquery外，否则不需要再使用jquery

vue是数据驱动，所以是操作数据

jquery是操作dom

举个简单的例子，元素的显示和隐藏分别用jquery和vue实现

jquery版本：

<div class="btn">隐藏/显示div</div>
<div class="box"></div>
<script>
    $('.btn').on('click',function () {
        if ($('.box').display == 'none') {
            $('.box').show();
        } else {
            $('.box').hide();
        }
    })
</script>
vue版本：

<div class="btn" @click="toggleBox">隐藏/显示div</div>
<div class="box" v-show="isShowBox"></div>
<script>
    new Vue({
        data:{
            isShowBox: true
        },
        methods: {
            toggleBox () {
                if (this.isShowBox) {
                    this.isShowBox = false
                } else {
                    this.isShowBox = true
                }
            }
        }
    })
</script>
vue常用语法
v-for 列表循环（列表渲染）

v-for把数组数据进行渲染，在实际工作中是很常用的，使用 item in items的特殊语法
  items是源数据数组，item是数组的每一项
  
  常用场景：
<div class="content">
    <ul>
        <li v-for="(item,index) in lists" @click="doClick(index)">{{item.text}}</li>
    </ul>
</div>

<script>
    new Vue({
        data () {
            lists: [
                {text: '学习javascript'},
                {text: '学习vue'},
                {text: '做一个漂亮的app'}
            ],
            text: ''
        },
        methods: {
            doClick (index) {
                this.text = this.lists[index].text
            }
        }
    })
</script>
下面我们分析一下重要部分：
  
  (item,index) in lists   vue 的v-for语法结构，要加在循环语句上，在这里是li标签
  
  lists：要循环的数组列表
  
  item：数组中的每一项，在这里是一个对象
  
  index：数组元素的下标
  
  在绑定的click事件中，可以使用index值取到数组的每一项
v-if v-else v-show （条件渲染）

v-if和v-show都可以用于元素的显示和隐藏，v-else必须用于v-if或v-else-if之后，不可用于v-show之后
  v-if和v-show虽然都可以表示元素的显示和隐藏，但是它们的的渲染机制是不同的，v-if是只有在条件为true时，才会渲染，
  v-show基于css进行切换，相当于display：block；和display：none；
<div class="content">
    <div>
        <p v-if="this.type === 'ok'">This is ok</p>
        <p v-if="this.type === 'no'">This is no</p>
    </div>
</div>

<script>
    new Vue ({
        data: {
            type: 'ok'
        }
    })
</script>
根据data中的type值的切换，改变元素的显示和隐藏状态，当type的值改为no时，第一个p标签隐藏，第二个显示
绑定事件
在vue中，使用v-on监听事件，（@是v-on的简写）触发javascript代码
<div v-on:click="count ++">add</div>
一般实际项目中的逻辑都不会这么简单，所以把javascript代码直接写在html中不是很好的方法，因此v-on还可以接收方法名
<div @click="addNum">add</div>
<script>
new Vue ({
    data: {
        count: 1
    },
    methods: {
        addNum () {
            this.count ++
        }
    }
})
</script>
我们来解释一下上面这段代码：

    @click：给div绑定了click事件
    addNum：方法名，在methods中定义
事件修饰符
vue还提供了一些修饰符方便我们使用，比如常用的阻止默认事件、阻止事件冒泡
<div @click.stop="addNum">add</div> // 阻止事件继续向上传播
更多的修饰符请去官网看
