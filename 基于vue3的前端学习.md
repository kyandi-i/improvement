# 基于Vue3的前端学习

## 1.什么是Vue？

---

* Vue是一款用于构建用户界面的JavaScript框架。基于标准HTML、CSS和JavaScript构建。

* 提供一套声明式的，组件化的编程模型，有助于高效开发。

```js
import { createApp, ref } from 'vue'

createApp({
  setup() {
    return {
      count: ref(0)
    }
  }
}).mount('#app')
```

```template
<div id="app">
  <button @click="count++">
    Count is: {{ count }}
  </button>
</div>
```

` Count is:0`

上面示例为Vue的两个核心功能:

* **声明式渲染**：Vue 基于标准 HTML 拓展了一套模板语法，使得我们可以声明式地描述最终输出的 HTML 和 JavaScript 状态之间的关系。

- **响应性**：Vue 会自动跟踪 JavaScript 状态并在其发生变化时响应式地更新 DOM。



## 2.快速尝试Vue

---

`前提：安装了最新版本的Node.js`

(1)以下命令行操作，并且确保在创建项目的目录：

```sh
npm create vue@latest
```

(2)接着会出现可选功能：

```sh
✔ Project name: … <your-project-name>
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add an End-to-End Testing Solution? … No / Cypress / Nightwatch / Playwright
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formatting? … No / Yes
✔ Add Vue DevTools 7 extension for debugging? (experimental) … No / Yes

Scaffolding project in ./<your-project-name>...
Done.
```

(3)项目创建完成后，通过以下命令来安装依赖以及启动开发服务器：

```sh
cd <your-project-name>
npm install
npm run dev
```

(4)准备将应用发布到生产环境时，运行以下命令：

```sh
npm run build
```

## 3.创建一个Vue应用

---

* 应用实例

​		每个Vue应用通过createApp函数创建一个新的应用实例:

```js
import { createApp } from 'vue'

const app = createApp({
  /* 根组件选项 */
})
```

* 根组件

​		传入createApp的对象，每个应用都需要一个根组件，其余叫做子组件。如果是单文件组件，可以直接从另一个文件中导入根组件。

```	js
import { createApp } from 'vue'
// 从一个单文件组件中导入根组件
import App from './App.vue'

const app = createApp(App)
```

* 挂载应用

​		应用实例需要调用`.mount()`方法后才能渲染出来。该方法接收一个“容器”参数，可以是一个DOM元素或是一个CSS选择器字符串：

```html
<div id="app"></div>
```

```js
app.mount('#app')
```

​		接着应用根组件内容会被渲染在容器元素中。

​		`.mount()` 方法应该始终在整个应用配置和资源注册完成后被调用。同时请注意，不同于其他资源注册方法，它的返回值是根组件实例而非应用实例。

* DOM中的根组件模板

​		根组件的模板通常是组件本身的一部分，但也可以直接通过在挂载容器内编写模板来单独提供：

```html
<div id="app">
  <button @click="count++">{{ count }}</button>
</div>
```

```js
import { createApp } from 'vue'

const app = createApp({
  data() {
    return {
      count: 0
    }
  }
})

app.mount('#app')
```

当根组件没有设置 `template` 选项时，Vue 将自动使用容器的 `innerHTML` 作为模板。

* 应用配置

​		应用实例会暴露一个 `.config` 对象允许我们配置一些应用级的选项，例如定义一个应用级的错误处理器，用来捕获所有子组件上的错误：

```js
app.config.errorHandler = (err) => {
  /* 处理错误 */
}
```

​		应用实例还提供了一些方法来注册应用范围内可用的资源，例如注册一个组件：

```js
app.component('TodoDeleteButton', TodoDeleteButton)
```

应用实例不局限于一个。createApp允许在一个页面中创建多个共存的Vue应用。

## 4.重点语法

---

### 4.1.OptionsAPI与CompositionAPI

* vue2的API设计是配置(OptionsAPI)风格的

	数据分散，不便于维护。

* vue3的API设计是组合(CompositionAPI)风格的

	利用函数的方式组织代码，让相关功能代码更有序组合。

### 4.2.set up

> setup是Vue3中一个新配置项，值是一个函数，它是CompositionAPI重要的环境，组件中的数据、方法、计算属性、监视等均配置在setup中。

特点如下：

* `setup`函数返回的对象中内容，可直接在模板中更新。
* `setup`中访问this是undefined。
* `setup`函数会在beforeCreate之前调用，它是优先执行的。

> data和methods能和setup同时存在
>
> data能够读取到setup里面的数据(this)

```vue
<!-- person.vue -->
<template>
    <div class="person">
        <h2>name:{{name}}</h2>
        <h2>age:{{age}}</h2>
        <button @click="changeName">修改名字</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="viewTel">查看电话</button>
    </div>
</template>

<script lang="ts">
    export default {
        name: 'Person',
        beforeCreate() {
            console.log('beforeCreate');
        },
        setup() {
        //setup中的this是undefined,vue3中开始弱化this的使用   
        //data
           let name = 'John Doe'//非响应式
           let age = 30
           let tel = '123-456-7890'

        //method
        function changeName() {
            console.log(1);
            
            name = 'Jane Smith';
        }
        function  changeAge(){
            console.log(2);
            
            age +=1
        }
        function viewTel(){
            console.log(3);
            
            alert(tel)
        } 
        //    return()=>'hhha'
        return {
            name,
            age,
            changeName,
            changeAge,
            viewTel
        }
        }
    }
</script>




<style scoped>
    .person {
    background-color: #307cee;
    box-shadow: 0 0 10px ;
    border-radius:10px;
    padding: 20px; 
  }
</style>
```

语法优化：

```vue
<!-- person.vue -->
<template>
    <div class="person">
        <h2>name:{{name}}</h2>
        <h2>age:{{age}}</h2>
        <button @click="changeName">修改名字</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="viewTel">查看电话</button>
    </div>
</template>

<script lang="ts">
    export default {
        name: 'Person'
        }
</script>

<script setup lang="ts">
    let name = 'John Doe'//非响应式
    let age = 30
    let tel = '123-456-7890'

        //method
        function changeName() {
            console.log(1);
            
            name = 'Jane Smith';
        }
        function  changeAge(){
            console.log(2);
            
            age +=1
        }
        function viewTel(){
            console.log(3);
            
            alert(tel)
        } 
</script>




<style scoped>
    .person {
    background-color: #307cee;
    box-shadow: 0 0 10px ;
    border-radius:10px;
    padding: 20px; 
  }
</style>
```

### 4.3.响应式数据

---

**ref**

> 可定义：基本类型、对象类型的响应式数据
>
> ref对象的value属性是响应式的
>
> js中操作数据需要.value。但模板中不需要.value，直接使用即可

```vue
<script setup lang="ts">
    import { ref } from 'vue'
    let name = ref('John Doe')//ref()响应式
    let age = ref(30)
    let tel = '123-456-7890'

        //method
        function changeName() {
            console.log(1);
            
            name.value = 'Jane Smith';//需要.value来确认响应数据更改
        }
        function  changeAge(){
            console.log(2);
            
            age.value +=1//需要.value来确认响应数据更改
        }
        function viewTel(){
            console.log(3);
            
            alert(tel)
        } 
</script>
```

**reactive**

> 只能定义：对象类型的响应式数据
>
> 不需要.value

```vue
<!-- person.vue -->
<template>
    <div class="person">
        <h2>Car Information</h2>
        <p>Brand: {{ car.brand }}</p>
        <p>Model: {{ car.model }}</p>
        <p>Year: {{ car.year }}</p>
        <p>Price: ${{ car.price }}</p>
        <button @click="changePrice">Increase Price by $5000</button>
        <h2>Games</h2>
        <ul>
            <li v-for="game in games" :key="game.id">{{ game.name }}</li>
        </ul>
        <button @click="changeFirstGameName">Change Name</button>
    </div>
</template>

<script setup lang="ts">
    import { reactive } from 'vue'
    //data
    const car = reactive({brand: 'Toyota',
                 model: 'Corolla', 
                 year: 2020,
                 price:20000
                })
    const games = reactive([
        {id:'aysdytfsatr01',name:'Football'},
        {id:'aysdytfsatr02',name:'Cricket'},
        {id:'aysdytfsatr03',name:'Basketball'},
        {id:'aysdytfsatr04',name:'Tennis'}
    ])
    
    
    //methods
    function changePrice() {
        car.price += 5000
    }
    function changeFirstGameName() {
        games[0].name = 'Soccer'
    }

</script>




<style scoped>
    .person {
    background-color: #307cee;
    box-shadow: 0 0 10px ;
    border-radius:10px;
    padding: 20px; 
  }
</style>
```

**ref对比reactive**

* 宏观角度

	> 定义类型不同

* 区别：

	> 1.ref创建变量必须使用.value(可以使用volar插件自动添加.value)。
	>
	> 2.reactive重新分配一个新对象，会失去响应式(可以使用Object.assign去整体替换)。

* 使用原则：

	> 1.若需要一个基本类型的响应式数据，必须使用`ref`
	>
	> 2.若需要一个响应式对象，层级不深，`ref`和`reactive`都可以
	>
	> 3.若需要一个响应式对象，层级较深，推荐使用`reactive`

**torefs和toref**

```vue
<!-- person.vue -->
<template>
    <div class="person">
        <h2>Person Component</h2>
        <p>Name: {{ name }}</p>
        <p>Age: {{ age }}</p>
        <button @click="updateName">Update Name</button>
        <button @click="updateAge">Update Age</button>
    </div>
</template>

<script setup lang="ts">
    import { reactive,toRefs } from 'vue';

    //data
    let person = reactive({
        name: 'John Doe',
        age: 20,
    });

    let {name, age} = toRefs(person);

    function updateName() {
        name.value += '!';
    }
    function updateAge() {
        age.value += 1;
    }

</script>
```

### 4.4.computed计算属性

```vue
<!-- person.vue -->
<template>
    <div class="person">
        姓：<input type="text" v-model="lastName"><br>
        名：<input type="text" v-model="firstName"><br>
        全名：<span>{{ fullName }}</span>
    </div>
</template>

<!-- 计算属性 -->
<script setup lang="ts">
    import { ref, computed } from 'vue';

    //data
    let lastName = ref('张');
    let firstName = ref('三');

    let fullName = computed(() => {
        return lastName.value.slice(0,1).toUpperCase()+lastName.value.slice(1) + firstName.value.slice(0,1).toUpperCase()+firstName.value.slice(1);
    });
</script>

```

### 4.5.watch

---

> watch能够监视数据的变化
>
> 只能监视以下四种数据
>
> 1. ref定义的数据。
> 2. reactive定义的数据。
> 3. 函数返回一个值（getter）。
> 4. 一个包含上述内容的数组。

**情况一：**

`监视ref定义的基本类型数据：直接写数据名，监视其value值的改变`

watch(监视,返回)

```vue
<!-- person.vue -->
<template>
    <div class="person">
    <h1>监视ref定义的基本类型数据</h1>
    <h2>当前求和为：{{ sum }}</h2>
    <button @click="changeSum">sum + 1</button>
    </div>
</template>

<!-- 计算属性 -->
<script setup lang="ts">
    import { ref,watch } from 'vue';
    //data
    let sum = ref(0);

    //methods
    function changeSum(){
        sum.value++;
    }

    //watch
    const stopwatch = watch(sum,(newvalue,oldvalue)=>{
        console.log('sum的值被修改了',newvalue,oldvalue)
        if(newvalue>=10){
            stopwatch(); //停止监视
            console.log('sum的值已经到达10，停止监视')
        }
    })

</script>
```

**情况二：**

`监视器ref定义的对象类型数据：直接写数据名，监视是对象的地址值，若想要监视对象内部的数据，需要手动开启深度监视`

> 注意：
>
> * 若修改的是ref定义的对象中的属性，newValue都是新值，因为它们是同一个对象。
> * 若修改整个ref定义的对象，newValue是新值，oldValue是旧值，因为不是同一个对象了。

```vue
<!-- person.vue -->
<template>
    <div class="person">
    <h1>监视ref定义的对象类型数据</h1>
    <h2>姓名：{{ person.name }}</h2>
    <h2>年龄：{{ person.age }}</h2>
    <button @click="changeName">updateName</button>
    <button @click="changeAge">updateAge</button>
    <button @click="changeAll">updateAll</button>
    </div>
</template>

<!-- 计算属性 -->
<script setup lang="ts">
    import { ref,watch } from 'vue';
    
    //data
    let person = ref({
        name:'张三',
        age:18
    })


    //methods
    function changeName(){
        person.value.name += '~'
    }
    function changeAge(){
        person.value.age += 1
    }
    function changeAll(){
        person.value = {
            name:'李四',
            age:20
        }
    }
    //watch：若想监视对象内部属性变化，需要手动开启深度监视
    watch(person, (newVal, oldVal) => {
        console.log('person changed:',newVal, oldVal);
    }, { deep: true });

</script>
```

**情况三：**

`监视reactive定义的对象类型数据是默认开启深度监视的功能`

```vue
<!-- person.vue -->
<template>
    <div class="person">
    <h1>监视reactive定义的对象类型数据</h1>
    <h2>姓名：{{ person.name }}</h2>
    <h2>年龄：{{ person.age }}</h2>
    <button @click="changeName">updateName</button>
    <button @click="changeAge">updateAge</button>
    <button @click="changeAll">updateAll</button>
    </div>
</template>

<!-- 计算属性 -->
<script setup lang="ts">
    import { reactive,watch } from 'vue';
    
    //data
    let person = reactive({
        name:'张三',
        age:18
    })


    //methods
    function changeName(){
        person.name += '~'
    }
    function changeAge(){
        person.age += 1
    }
    function changeAll(){
        Object.assign(person,{
            name:'李四',
            age:20
        })
    }
    
    //watch：监视reactive定义的对象类型数据是默认开启深度监视的功能
    watch(person, (value) => {
        console.log('person changed:',value);
    }, { deep: true });

</script>
```

**情况四：**

`监视ref或reactive定义的对象类型数据中的某个属性`

> 注意：
>
> * 若该属性值不是对象类型，需要写成函数形式。
> * 若该属性值依然是对象类型，可直接编，也可以写成函数。
>
> 结论：监视的若是对象里的属性，则最优写函数式，若是对象监视的是地址值，需要关注对象内部，需要手动开启深度监视。

```vue
<!-- person.vue -->
<template>
    <div class="person">
    <h2>{{ person.Name }}</h2>
    <h2>{{ person.age }}</h2>
    <p>Car: {{ person.car.brand }} {{ person.car.model }} ({{ person.car.year }})</p>
    <button @click="updateName">updateName</button>
    <button @click="updateAge">updateAge</button>
    <button @click="updateCarBrand">updateCarBrand</button>
    <button @click="updateCarModel">updateCarModel</button>
    <button @click="updateCarYear">updateCarYear</button>
    <button @click="updateCarAll">updateCarAll</button>
    </div>
</template>

<!-- 计算属性 -->
<script setup lang="ts">
    import { reactive,watch } from 'vue';
    
    //data
    let person = reactive({
        Name: 'John',
        age: 28,
        car:{
            brand:'Ford',
            model:'Mustang',
            year:1969
        }
    });

    //methods
    function updateName(){
        person.Name += '~';
    }   
    function updateAge(){
        person.age += 2;
    }
    function updateCarBrand(){
        person.car.brand = 'Chevrolet';
    }
    function updateCarModel(){
        person.car.model = 'Camaro';
    }
    function updateCarYear(){
        person.car.year = 1970;
    }
    function updateCarAll(){
        person.car = {
            brand: 'Dodge',
            model: 'Charger',
            year: 1971
        };
    }

    // watch(() => {return person.Name}, (newVal, oldVal) => {
    //     console.log('Person changed:', newVal);
    // }, { deep: true });
    watch(() => person.car, (newVal, oldVal) => {
        console.log('Car changed:', newVal);
    }, { deep: true });

</script>
```

**情况五：**

`监视上述的多个数据`

```vue
    watch([() => {return person.car},person.car], (newVal, oldVal) => {
        console.log('Car changed:', newVal);
    }, { deep: true });
```

**watchEffect:**

`不用明确指出监视的数据(函数中用到哪些属性，那就监视哪些属性)。`

```vue
<!-- person.vue -->
<template>
    <div class="person">
    <h2>当水温为60度，或者水位达到80cm时，发送请求</h2>
    <h2>当前水温为{{temp}}摄氏度</h2>
    <h2>当前水位为{{height}}</h2>
    <button @click="temp_up">temp+10</button>
    <button @click="height_up">height+10</button>
    </div>
</template>


<script setup lang="ts">
    import { ref,watch,watchEffect } from 'vue';
    
    //data
    let temp = ref(0);
    let height = ref(0);

    //methods
    function temp_up(){
        temp.value += 10;
    }
    function height_up(){
        height.value += 10;
    }

    //watch
    // watch([temp,height],(value)=>{
        
    //     let [newTemp,newHeight] = value;
    //     console.log(value);
    //     if(newTemp >= 60 || newHeight >= 80){
    //         console.log("发送请求");
    //     }
    // })
    watchEffect(() => {
        if (temp.value >= 60 || height.value >= 80) {
            console.log("发送请求");
        }
    })
        

</script>
```

### 4.6.标签的ref属性

`用于注册模板引用`

> * 用在普通DOM标签上，获取的是DOM结点。
> * 用在组件标签上，获取的是组件实例对象。

## 5.接口,自定义,泛型回顾

```vue
<!-- person.vue -->
<template>
    <div class="person">
        ？？？
    </div>
</template>


<script setup lang="ts">   
    import { type PersonInter,type Persons } from '@/types/index'
    
    //data
    let person: PersonInter = {
        id:114514,
        name: '张三',
        age: 18
    }
    
    let personlist:Persons =[
        {
            id: 1,
            name: '李四',
            age: 20
        },
        {
            id: 2,
            name: '王五',
            age: 22
        },
        {
            id: 3,
            name: '赵六',
            age: 19
        }
    ]

    //methods
    

</script>


<style scoped>
    .person {
    background-color: #307cee;
    box-shadow: 0 0 10px ;
    border-radius:10px;
    padding: 20px; 
  }
</style>
```

```ts
// index.ts
//定义一个接口，用于限制对象的结构
export interface PersonInter {
    id: number;
    name: string;
    age: number;
}
//定义一个类型，表示PersonInter对象的数组
export type Persons = Array<PersonInter>
```

### 5.1.props

```vue
<!-- person.vue -->
<template>
    <div class="person">
    <!-- <h2>{{ a }}</h2> -->
    <ul>
        <li v-for="k in list" :key="k.id">
            {{ k.id }} -- {{ k.age }}
        </li>
    </ul>
    </div>
</template>


<script setup lang="ts">   
    import { type Persons } from '@/types/index'
    //接受list+限制类型+限制必要性+指定默认值
    withDefaults(defineProps<{list: Persons}>(), {
        list: () => [{ id: 0, name: '默认', age: 0 }]
    })
    // 接受list+限制类型
    // defineProps<{list: Persons}>()

    //只接受list
    // defineProps(['list'])

    // defineProps(['a','list'])     

    //接收a，同时将props保存起来
    // let x = defineProps(['a']) 

    // console.log(x);
    
</script>


<style scoped>
    .person {
    background-color: #307cee;
    box-shadow: 0 0 10px ;
    border-radius:10px;
    padding: 20px; 
  }
</style>
```

```vue
<template>
  <Person a="hhhhh" :list="personlist"/>
</template>

<script setup lang="ts">
  import { reactive } from 'vue';
  import Person from './components/person.vue'
  import { type Persons } from '@/types/index'

  let personlist = reactive<Persons>([
    { id: 1, name: '李四', age: 20 },
    { id: 2, name: '王五', age: 22 },
    { id: 3, name: '赵六', age: 19 ,x : 9}
  ])

  console.log(personlist);
  

</script>


```

