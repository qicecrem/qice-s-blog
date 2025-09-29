# Vue 核心知识点整理笔记


## 一、Vue 基础概念
### 1. Vue 定义
Vue 是一个**构建用户界面的渐进式框架**（可按需引入功能，无需全量使用）。


## 二、创建 Vue 实例（核心步骤）
创建 Vue 实例需遵循 4 个核心步骤，确保数据能正常渲染到页面：
1. **准备容器**：在 HTML 中定义用于挂载 Vue 实例的 DOM 元素（如 `<div id="app"></div>`）。
2. **引入 Vue 包**：根据环境选择版本
   - 开发版：包含完整警告和调试功能（适合开发环境）。
   - 生产版：去除警告，体积更小（适合上线环境）。
3. **创建 Vue 实例**：通过 `new Vue()` 初始化实例。
4. **指定配置项（渲染数据）**：核心配置项有 2 个：
   - `el`：指定挂载点（关联 HTML 中的容器，如 `el: '#app'`）。
   - `data`：提供实例所需数据（如 `data: { msg: 'Hello Vue' }`）。


## 三、模板语法：插值表达式 `{{ }}`
插值表达式是 Vue 最基础的模板语法，用于渲染数据到页面。
1. **作用**：通过 JavaScript 表达式计算结果，将结果插入到 DOM 中。  
   （注：“表达式”指可求值的代码，如 `msg`、`1+1`、`user.age > 18 ? '成年' : '未成年'`）。
2. **语法**：`{{ 表达式 }}`（如 `<div>{{ msg }}</div>`）。
3. **注意事项**：
   - 表达式使用的数据必须在 `data` 中定义（否则报错）。
   - 仅支持**表达式**，不支持语句（如 `if`、`for` 等不能直接写）。
   - 不能在 HTML 标签属性中使用（如 `<div title="{{ msg }}"></div>` 无效，需用 `v-bind`）。


## 四、Vue 核心特点：响应式
- **定义**：当 `data` 中的数据发生变化时，页面视图会**自动更新**，无需手动操作 DOM。
- 核心原理：Vue 会对 `data` 中的数据进行“劫持”，监听数据变化，触发视图重新渲染。


## 五、Vue 指令（带 `v-` 前缀的特殊属性）
指令用于实现标签的动态功能，按功能分类整理如下：

| 指令          | 作用                                  | 语法/关键说明                                                                 |
|---------------|---------------------------------------|-----------------------------------------------------------------------------|
| `v-html`      | 设置元素的 `innerHTML`                | `v-html="表达式"`（可渲染 HTML 标签，注意 XSS 风险）                          |
| `v-show`      | 控制元素显示/隐藏（频繁切换场景）      | `v-show="表达式"` <br> 原理：切换 `display: none`（元素始终存在于 DOM 中）      |
| `v-if`        | 控制元素显示/隐藏（条件渲染）          | `v-if="表达式"` <br> 原理：条件判断是否创建 DOM 节点（元素可能从 DOM 中移除）    |
| `v-else`/`v-else-if` | 辅助 `v-if` 实现多条件判断 | 必须**紧接** `v-if` 使用（如 `v-if="age>18"` → `v-else="age<=18"`）              |
| `v-on`        | 注册事件（添加监听+处理逻辑）          | 语法：`v-on:事件名="处理逻辑"` <br> 简写：`@事件名="处理逻辑"` <br> 逻辑支持：内联语句（如 `@click="num++"`）或 `methods` 中的函数名（如 `@click="handleClick"`） |
| `v-bind`      | 动态设置 HTML 标签属性                | 语法：`v-bind:属性名="表达式"` <br> 简写：`:属性名="表达式"` <br> 常用场景：`src`、`href`、`title` 等（如 `<img :src="imgUrl">`） |
| `v-for`       | 基于数据循环渲染元素                  | 语法：`v-for="(item, index) in 数组/对象"` <br> 必须加 `:key="唯一标识"`（如 `:key="item.id"`），作用：给列表元素添加唯一标识，确保 Vue 正确排序和复用元素 |
| `v-model`     | 表单元素双向数据绑定                  | 语法：`v-model="变量"` <br> 适用元素：`input`、`select`、`textarea` 等 <br> 核心：变量变化 → 表单值更新；表单值变化 → 变量更新 |


### 指令修饰符（`.` 后缀，封装常用逻辑）
修饰符用于简化指令的常见操作，按类型分类：
1. **按键修饰符**：监听特定按键事件  
   如 `@keyup.enter`（仅监听“回车”按键抬起事件）。
2. **`v-model` 修饰符**：
   - `v-model.trim`：自动去除输入内容的首尾空格。
   - `v-model.number`：将输入内容转为数字类型（仅当输入为纯数字时生效）。
3. **事件修饰符**：
   - `@事件名.stop`：阻止事件冒泡（如 `@click.stop="handleClick"`）。
   - `@事件名.prevent`：阻止事件默认行为（如 `@submit.prevent` 阻止表单提交刷新页面）。


### `v-bind` 增强：控制样式（`class`/`style`）
#### 1. 操作 `class`（动态添加/移除类名）
- **对象语法**：键为类名，值为布尔值（`true` 则添加类，`false` 则移除）  
  示例：`<div :class="{ active: isActive, red: isRed }"></div>`。
- **数组语法**：数组中的所有类名都会添加到元素上（本质是 `class` 列表）  
  示例：`<div :class="[ 'active', 'red' ]"></div>` 或 `<div :class="[ activeClass, redClass ]"></div>`（`activeClass` 是 `data` 中的变量）。

#### 2. 操作 `style`（动态设置行内样式）
- **语法**：`:style="样式对象"`（键为 CSS 属性名，值为样式值）  
  示例：`<div :style="{ fontSize: '16px', color: textColor }"></div>`（`textColor` 是 `data` 中的变量）。


## 六、计算属性与侦听器
### 1. 计算属性（`computed`）
- **作用**：对已有数据进行计算处理，生成新数据（依赖数据变化时自动重新计算），避免模板中写复杂表达式。
- **语法结构**：
  ```js
  computed: {
    // 计算属性名（如 fullName）
    计算属性名: {
      // 获取计算结果（必须有返回值）
      get() {
        // 计算逻辑（依赖 data 中的数据）
        return this.firstName + ' ' + this.lastName;
      },
      // （可选）修改计算属性时触发（需手动实现反向逻辑）
      set(newValue) {
        // 修改逻辑（如将 newValue 拆分后赋值给依赖数据）
        const [first, last] = newValue.split(' ');
        this.firstName = first;
        this.lastName = last;
      }
    }
  }
  ```


### 2. 侦听器（`watch`）
- **作用**：监视 `data` 或 `computed` 中的数据变化，触发自定义业务逻辑（如异步操作、复杂数据处理）。
- **常见语法**：
  #### （1）基础写法（监视简单数据类型）
  ```js
  watch: {
    // 监视 data 中的 "msg" 数据
    msg(newValue, oldValue) {
      // newValue：变化后的值；oldValue：变化前的值
      console.log('msg 变化了：', newValue, oldValue);
    },
    // 监视对象中的属性（需用字符串包裹）
    'user.age'(newValue) {
      console.log('用户年龄变化了：', newValue);
    }
  }
  ```

  #### （2）完整写法（带额外配置项）
  适用于**深度监视**（复杂类型如对象、数组）或**初始化立即执行**：
  ```js
  watch: {
    // 监视 "user" 对象（复杂类型）
    user: {
      deep: true, // 深度监视：监视对象内部属性变化
      immediate: true, // 初始化时立即执行一次 handler
      // 处理函数（固定用 handler 命名）
      handler(newValue) {
        console.log('user 对象变化了：', newValue);
      }
    }
  }
  ```


## 七、Vue 生命周期
### 1. 生命周期定义
Vue 实例从**创建**到**销毁**的整个过程，分为 4 个核心阶段。

### 2. 4 个核心阶段
1. **创建阶段**：初始化实例、处理 `data` 响应式（此时模板未渲染）。
2. **挂载阶段**：将模板渲染为 DOM（此时可操作 DOM）。
3. **更新阶段**：`data` 变化时，重新计算并更新视图。
4. **销毁阶段**：销毁实例（清除事件监听、解除数据响应式等）。

### 3. 常用生命周期钩子（自动运行的函数）
- `created()`：实例创建完成，`data` 响应式已就绪（可发送初始化请求，如调用接口获取数据）。
- `mounted()`：模板渲染完成，DOM 已生成（可操作 DOM，如获取元素、初始化第三方插件）。


## 八、Vue CLI（Vue 脚手架）
### 1. 定义
Vue CLI 是 Vue 官方提供的**全局命令行工具**，用于快速创建标准化的 Vue 项目架子（集成了 Webpack 配置，无需手动配置构建工具）。

### 2. 使用步骤（4 步）
1. **全局安装**（仅需安装一次）：  
   `yarn global add @vue/cli` 或 `npm i @vue/cli -g`。
2. **查看版本**：验证安装是否成功  
   `vue --version`（显示版本号即成功）。
3. **创建项目**：  
   `vue create 项目名`（项目名不能含中文，如 `vue create vue-demo`）。
4. **启动项目**：进入项目目录后执行  
   `yarn serve` 或 `npm run serve`（启动后访问终端提示的地址，如 `http://localhost:8080`）。


### 3. 脚手架项目目录结构（核心文件/文件夹）
| 文件/文件夹         | 作用说明                                                                 |
|--------------------|--------------------------------------------------------------------------|
| `node_modules`     | 项目依赖包（第三方库，如 Vue、axios 等）                                 |
| `src`              | 源代码目录（核心开发目录）                                               |
| ├─ `assets`        | 静态资源目录（存放图片、字体、样式文件等）                               |
| ├─ `components`    | 通用组件目录（存放可复用的 Vue 组件，如 `HmHeader.vue`）                 |
| ├─ `App.vue`       | 根组件（项目运行时显示的核心内容，所有页面都嵌套在其中）                 |
| └─ `main.js`       | 入口文件（项目打包/运行时第一个执行的文件，用于初始化 Vue 实例）         |
| `index.html`       | HTML 模板文件（Vue 实例挂载的根容器在此定义）                            |
| `package.json`     | 项目配置文件（包含项目名、版本、脚本命令 `scripts`、依赖包列表等）       |
| `vue.config.js`    | Vue CLI 自定义配置文件（如配置跨域、修改端口等）                         |


### 4. `App.vue` 结构（Vue 单文件组件 SFC）
每个 `.vue` 文件由 3 个部分组成，各司其职：
1. **`<template>`**：组件结构（必须有且仅有一个根元素，如 `<div></div>`）。
2. **`<script>`**：组件逻辑（导出组件配置，如 `data`、`methods`、`computed` 等）。
3. **`<style>`**：组件样式（可通过 `lang="less"` 支持 Less 语法）。


## 九、组件相关核心知识点
### 1. 组件注册（2 种方式）
组件需注册后才能使用，按作用域分为局部注册和全局注册。

#### （1）局部注册（仅在注册的组件内可用）
步骤：
1. 创建组件文件（如 `components/HmHeader.vue`，包含 `template`/`script`/`style`）。
2. 在使用组件的父组件中**导入 + 注册**：
   ```js
   // 1. 导入组件（路径需正确）
   import HmHeader from './components/HmHeader.vue';

   export default {
     // 2. 局部注册（在 components 选项中声明）
     components: {
       // 组件名: 组件对象（键值同名时可简写为 HmHeader）
       HmHeader: HmHeader
     }
   }
   ```
3. 使用组件：`<HmHeader></HmHeader>`（当成 HTML 标签使用）。

#### （2）全局注册（所有组件内都可用）
步骤：
1. 创建组件文件（同局部注册）。
2. 在 `main.js` 中**导入 + 全局注册**：
   ```js
   // 1. 导入组件
   import HmButton from './components/HmButton.vue';
   // 2. 全局注册（Vue.component(组件名, 组件对象)）
   Vue.component('HmButton', HmButton);
   ```
3. 使用组件：任意组件内直接写 `<HmButton></HmButton>`。

#### 组件名规范
推荐使用**大驼峰命名法**（如 `HmHeader`、`UserCard`），避免与 HTML 原生标签冲突。


### 2. 组件样式冲突（`scoped` 解决）
- **问题**：默认情况下，组件内的样式会**全局生效**，导致多个组件样式冲突。
- **解决方案**：给 `<style>` 标签添加 `scoped` 属性，使样式仅作用于当前组件：
  ```vue
  <style scoped>
  /* 此样式仅在当前组件生效 */
  .box { color: red; }
  </style>
  ```


### 3. 组件的 `data` 必须是函数
- **原因**：保证每个组件实例维护**独立的一份数据**（若 `data` 是对象，多个组件实例会共享同一个对象，导致数据污染）。
- **原理**：每次创建新组件实例时，会执行 `data` 函数，返回一个新的对象。
- **示例**：
  ```js
  export default {
    data() { // 必须是函数
      return {
        count: 0 // 每个实例的 count 都是独立的
      }
    }
  }
  ```


## 十、组件通信（数据传递）
组件数据是独立的，无法直接访问其他组件数据，需通过“组件通信”实现数据传递。按组件关系分类如下：


### 1. 父子组件通信（最常用）
#### （1）父 → 子：通过 `props` 传值
步骤：
1. **父组件**：给子组件标签添加自定义属性（属性值为要传递的数据）。  
   示例：`<Child :msg="parentMsg" :user="parentUser"></Child>`（`parentMsg`、`parentUser` 是父组件的 `data`）。
2. **子组件**：通过 `props` 选项接收父组件传递的数据。  
   示例：
   ```js
   export default {
     // 方式1：简单数组（仅声明属性名）
     props: ['msg', 'user'],
     // 方式2：带校验（推荐，便于调试）
     props: {
       msg: {
         type: String, // 类型校验（必须是字符串）
         required: true, // 非空校验（父组件必须传此属性）
         default: '默认值' // 默认值（父组件未传时生效）
       },
       user: {
         type: Object, // 复杂类型（对象）
         validator(value) { // 自定义校验（返回 true 则通过）
           return value.age >= 18; // 要求 user.age 至少 18
         }
       }
     }
   }
   ```
3. **子组件使用数据**：直接通过 `this.msg`、`this.user` 使用。


#### （2）子 → 父：通过 `$emit` 发送事件
步骤：
1. **子组件**：通过 `this.$emit('事件名', 数据)` 发送消息（数据可选）。  
   示例：
   ```js
   export default {
     methods: {
       sendToParent() {
         // 发送事件 "childMsg"，并传递数据 "Hello Parent"
         this.$emit('childMsg', 'Hello Parent');
       }
     }
   }
   ```
2. **父组件**：给子组件标签添加事件监听（事件名与子组件 `$emit` 的事件名一致），并定义处理函数。  
   示例：
   ```vue
   <!-- 监听子组件的 "childMsg" 事件，触发 handleChildMsg 函数 -->
   <Child @childMsg="handleChildMsg"></Child>

   <script>
   export default {
     methods: {
       handleChildMsg(data) {
         // data 是子组件传递过来的数据（"Hello Parent"）
         console.log('收到子组件消息：', data);
       }
     }
   }
   </script>
   ```


### 2. 非父子组件通信（跨层级/无直接关系）
#### （1）Event Bus（事件总线，适合简单场景）
- **作用**：通过一个空 Vue 实例作为“中间件”，实现非父子组件的消息传递（复杂场景推荐用 Vuex）。
- 步骤：
  1. **创建事件总线**：新建 `utils/EventBus.js` 文件，导出空 Vue 实例：
     ```js
     import Vue from 'vue';
     const Bus = new Vue(); // 空 Vue 实例（作为总线）
     export default Bus;
     ```
  2. **接收方组件（如 A 组件）**：监听总线事件（在 `created` 中监听，避免重复监听）：
     ```js
     import Bus from './utils/EventBus.js';

     export default {
       data() {
         return { msg: '' };
       },
       created() {
         // 监听 "sendMsg" 事件，接收数据
         Bus.$on('sendMsg', (data) => {
           this.msg = data; // 将接收的数据赋值给本地 msg
         });
       }
     }
     ```
  3. **发送方组件（如 B 组件）**：触发总线事件，传递数据：
     ```js
     import Bus from './utils/EventBus.js';

     export default {
       methods: {
         sendData() {
           // 触发 "sendMsg" 事件，传递数据 "Hello from B"
           Bus.$emit('sendMsg', 'Hello from B');
         }
       }
     }
     ```


#### （2）provide & inject（跨层级共享，适合祖先 → 子孙）
- **作用**：实现“祖先组件”向“任意层级的子孙组件”传递数据（无需逐层传递 `props`）。
- 步骤：
  1. **祖先组件（provide 提供数据）**：通过 `provide` 选项返回要共享的数据：
     ```js
     export default {
       data() {
         return {
           color: 'red',
           userInfo: { name: '张三', age: 20 } // 复杂类型（响应式）
         };
       },
       provide() {
         return {
           // 普通类型（非响应式：祖先数据变化，子孙不会更新）
           color: this.color,
           // 复杂类型（响应式：祖先数据变化，子孙会更新）
           userInfo: this.userInfo
         };
       }
     }
     ```
  2. **子孙组件（inject 接收数据）**：通过 `inject` 选项声明要接收的数据，直接使用：
     ```js
     export default {
       // 声明要接收的祖先数据（与 provide 中的键对应）
       inject: ['color', 'userInfo'],
       created() {
         console.log('接收的颜色：', this.color); // red
         console.log('接收的用户信息：', this.userInfo); // { name: '张三', ... }
       }
     }
     ```


#### （3）通用方案：Vuex
- **作用**：集中管理所有组件的共享状态（如用户信息、购物车数据），适合中大型项目。
- 核心：将共享数据存入 Vuex 的 `state`，组件通过 `this.$store` 访问或修改数据（需遵循 Vuex 规范，如通过 `mutations` 修改 `state`）。


## 十一、表单类组件封装（实战场景）
表单组件（如下拉选择、自定义输入框）需实现“父子数据双向绑定”，常见两种写法：

### 1. 普通写法（`props` + `$emit`）
```vue
<!-- 父组件：传递数据 + 监听事件 -->
<BaseSelect :cityId="selectId" @updateId="selectId = $event"></BaseSelect>

<script>
export default {
  data() {
    return { selectId: '1' }; // 父组件的选中 ID
  }
}
</script>
```

```vue
<!-- 子组件 BaseSelect.vue：接收数据 + 发送事件 -->
<template>
  <select :value="cityId" @change="handleChange">
    <option value="1">北京</option>
    <option value="2">上海</option>
  </select>
</template>

<script>
export default {
  props: {
    cityId: String // 接收父组件的选中 ID
  },
  methods: {
    handleChange(e) {
      // 发送事件，将新选中值传递给父组件
      this.$emit('updateId', e.target.value);
    }
  }
}
</script>
```


### 2. 简化写法（利用 `v-model`）
Vue 中 `v-model` 本质是 `value` 属性 + `input` 事件的语法糖，可简化父子双向绑定：
```vue
<!-- 父组件：直接用 v-model 绑定数据 -->
<BaseSelect v-model="selectId"></BaseSelect>

<script>
export default {
  data() {
    return { selectId: '1' };
  }
}
</script>
```

```vue
<!-- 子组件 BaseSelect.vue：接收 value + 触发 input 事件 -->
<template>
  <select :value="value" @change="handleChange">
    <option value="1">北京</option>
    <option value="2">上海</option>
  </select>
</template>

<script>
export default {
  props: {
    value: String // 必须用 "value" 作为 props 名（与 v-model 对应）
  },
  methods: {
    handleChange(e) {
      // 必须触发 "input" 事件（与 v-model 对应）
      this.$emit('input', e.target.value);
    }
  }
}
</script>
```


# Vue 进阶知识点整理笔记


## 一、.sync 修饰符（父子组件双向绑定简化）
### 作用
实现子组件与父组件数据的**双向绑定**，简化传统的 `props + $emit` 写法。

### 特点
- 与 `v-model` 不同，`prop` 属性名**可自定义**（非固定为 `value`）。
- 本质是语法糖：`父组件:属性.sync="数据"` 等价于 `父组件:属性="数据" @update:属性="数据=$event"`。

### 适用场景
常用于封装弹框类组件（如控制显示/隐藏的 `visible` 属性）。

### 示例
```vue
<!-- 父组件（F） -->
<BaseDialog :visible.sync="isShow" />
<!-- 等价于 -->
<BaseDialog :visible="isShow" @update:visible="isShow = $event" />

<script>
export default {
  data() {
    return { isShow: false }; // 控制弹框显示的状态
  }
}
</script>
```

```vue
<!-- 子组件（S） -->
<template>
  <div v-if="visible">弹框内容</div>
</template>

<script>
export default {
  props: {
    visible: Boolean // 接收父组件的状态
  },
  methods: {
    close() {
      // 发送事件更新父组件状态（事件名固定为 "update:属性名"）
      this.$emit('update:visible', false);
    }
  }
}
</script>
```


## 二、ref 和 $refs（获取DOM/组件实例）
### 作用
- 获取当前组件内的**DOM元素**或**子组件实例**，比 `document.querySelector` 更精确（仅在当前组件内查找）。

### 使用方式
#### 1. 获取 DOM 元素
```vue
<template>
  <!-- 1. 给目标DOM添加 ref 属性 -->
  <div ref="chartRef">我是图表容器</div>
</template>

<script>
export default {
  mounted() {
    // 2. 在合适时机（如 mounted）通过 this.$refs.xxx 获取
    const dom = this.$refs.chartRef;
    console.log('获取到的DOM元素：', dom);
  }
}
</script>
```

#### 2. 获取子组件实例
```vue
<template>
  <!-- 1. 给目标组件添加 ref 属性 -->
  <BaseForm ref="baseForm"></BaseForm>
</template>

<script>
import BaseForm from './BaseForm.vue';
export default {
  components: { BaseForm },
  methods: {
    callChildMethod() {
      // 2. 通过 this.$refs.xxx 获取组件实例，调用其方法
      this.$refs.baseForm.validate(); // 假设子组件有 validate 方法
    }
  }
}
</script>
```


## 三、$nextTick（DOM更新后执行）
### 作用
等待当前DOM更新完成后，再执行函数体内的逻辑（解决数据更新后立即操作DOM但DOM未更新的问题）。

### 语法
```js
this.$nextTick(函数体);
```

### 示例
```vue
<template>
  <div ref="content">{{ msg }}</div>
</template>

<script>
export default {
  data() {
    return { msg: '初始内容' };
  },
  methods: {
    updateMsg() {
      this.msg = '更新后的内容'; // 数据更新
      // 此时直接获取DOM，内容仍是旧的（DOM未更新）
      console.log(this.$refs.content.textContent); // 输出 "初始内容"

      // 用 $nextTick 等待DOM更新后执行
      this.$nextTick(() => {
        console.log(this.$refs.content.textContent); // 输出 "更新后的内容"
      });
    }
  }
}
</script>
```


## 四、自定义指令（扩展DOM操作）
### 作用
封装常用DOM操作，为标签扩展额外功能（如自动聚焦、设置颜色等）。

### 注册方式
#### 1. 全局注册（所有组件可用）
```js
// 在 main.js 中
import Vue from 'vue';

// 注册全局指令（指令名不带 v-）
Vue.directive('focus', {
  // inserted 钩子：指令所在元素被插入到页面时触发
  inserted(el) {
    el.focus(); // 自动聚焦
  }
});
```

#### 2. 局部注册（仅当前组件可用）
```vue
<template>
  <input v-focus type="text">
</template>

<script>
export default {
  directives: {
    // 注册局部指令
    focus: {
      inserted(el) {
        el.focus();
      }
    }
  }
}
</script>
```

### 带值的自定义指令
#### 需求
实现 `v-color` 指令，根据传入的值设置元素文字颜色。

#### 示例
```vue
<template>
  <div v-color="textColor">动态颜色文本</div>
</template>

<script>
export default {
  data() {
    return { textColor: 'red' };
  },
  directives: {
    color: {
      // 元素插入时设置初始颜色
      inserted(el, binding) {
        el.style.color = binding.value; // binding.value 是指令传入的值
      },
      // 指令值更新时触发（如 textColor 变化）
      update(el, binding) {
        el.style.color = binding.value;
      }
    }
  }
}
</script>
```


## 五、插槽（组件内容自定义）
插槽用于让组件内部的部分结构支持自定义，按功能分为以下类型：

### 1. 默认插槽（基础用法）
- 组件内用 `<slot>` 标记可自定义区域，使用组件时填入的内容会替换 `<slot>`。

```vue
<!-- 子组件 MyDialog.vue -->
<template>
  <div class="dialog">
    <div class="dialog-content">
      <slot></slot> <!-- 插槽位置 -->
    </div>
  </div>
</template>

<!-- 父组件使用 -->
<MyDialog>
  <p>这是自定义的内容</p> <!-- 填入插槽的内容 -->
</MyDialog>
```


### 2. 后备内容（默认值）
- 在 `<slot>` 标签内放置内容，作为默认显示（若使用组件时未填入内容则显示）。

```vue
<!-- 子组件 MyDialog.vue -->
<template>
  <div class="dialog">
    <slot>默认显示的内容</slot> <!-- 后备内容 -->
  </div>
</template>

<!-- 父组件使用 -->
<MyDialog></MyDialog> <!-- 显示 "默认显示的内容" -->
<MyDialog>自定义内容</MyDialog> <!-- 显示 "自定义内容" -->
```


### 3. 具名插槽（多区域自定义）
- 当组件内有多个自定义区域时，用 `name` 属性区分插槽。
- 使用时通过 `template` + `v-slot:插槽名`（简写 `#插槽名`）指定内容。

```vue
<!-- 子组件 MyDialog.vue -->
<template>
  <div class="dialog">
    <div class="header">
      <slot name="header"></slot> <!-- 头部插槽 -->
    </div>
    <div class="content">
      <slot name="content"></slot> <!-- 内容插槽 -->
    </div>
  </div>
</template>

<!-- 父组件使用 -->
<MyDialog>
  <template #header> <!-- 简写，等价于 v-slot:header -->
    <h3>标题</h3>
  </template>
  <template #content>
    <p>正文内容</p>
  </template>
</MyDialog>
```


### 4. 作用域插槽（插槽传参）
- 组件内的插槽可绑定数据（传给使用组件的父组件），父组件可根据数据自定义内容。

```vue
<!-- 子组件 MyTable.vue -->
<template>
  <table>
    <tr v-for="item in list" :key="item.id">
      <td>{{ item.name }}</td>
      <td>
        <!-- 给插槽绑定数据（row 是自定义属性名） -->
        <slot :row="item" msg="操作提示"></slot>
      </td>
    </tr>
  </table>
</template>

<script>
export default {
  props: { list: Array } // 接收父组件传入的列表数据
}
</script>
```

```vue
<!-- 父组件使用 -->
<MyTable :list="userList">
  <!-- 通过 #default="obj" 接收插槽传递的数据（obj 是包含所有绑定属性的对象） -->
  <template #default="obj">
    <button @click="del(obj.row.id)">删除 {{ obj.row.name }}</button>
    <!-- obj 结构：{ row: { id: 1, name: '张三' }, msg: '操作提示' } -->
  </template>
</MyTable>

<script>
export default {
  data() {
    return { userList: [{ id: 1, name: '张三' }, { id: 2, name: '李四' }] };
  },
  methods: { del(id) { /* 删除逻辑 */ } }
}
</script>
```


## 六、单页应用（SPA）与 VueRouter
### 1. 单页应用（SPA）
- **定义**：Single Page Application，整个应用只有一个HTML页面，通过JS动态切换内容。
- **适用场景**：系统类网站、内部平台、文档类应用、移动端应用。
- **对比多页应用**：多页应用（如公司官网、电商网站）有多个HTML页面，跳转时刷新页面。


### 2. VueRouter 基本使用（5+2步骤）
VueRouter 是 Vue 官方路由工具，用于管理路径与组件的映射关系。

#### （1）5 个核心步骤
1. **下载依赖**（Vue2 对应 VueRouter@3.x）：  
   `yarn add vue-router@3.6.5`

2. **引入 VueRouter**：  
   `import VueRouter from 'vue-router'`

3. **安装注册**：  
   `Vue.use(VueRouter)`

4. **创建路由实例**：  
   `const router = new VueRouter({ /* 路由配置 */ })`

5. **注入 Vue 实例**：  
   ```js
   new Vue({
     render: h => h(App),
     router // 注入路由实例，使整个应用可使用路由功能
   }).$mount('#app')
   ```

#### （2）2 个关键配置
- **路由规则**：定义路径与组件的映射。
- **路由出口**：指定匹配的组件显示位置。


### 3. 路由配置与使用
#### （1）创建组件与配置规则
```js
// 1. 导入组件（通常放在 views 目录）
import Find from './views/Find.vue';
import My from './views/My.vue';

// 2. 配置路由规则
const router = new VueRouter({
  routes: [
    { path: '/find', component: Find }, // 路径 /find 对应 Find 组件
    { path: '/my', component: My }      // 路径 /my 对应 My 组件
  ]
});
```

#### （2）配置导航与出口
```vue
<!-- 导航链接（替代 a 标签） -->
<div class="nav">
  <a href="#/find">发现</a> <!-- hash 模式需加 # -->
  <a href="#/my">我的</a>
</div>

<!-- 路由出口：匹配的组件会显示在这里 -->
<router-view></router-view>
```


### 4. 路由模块封装
将路由相关代码集中到 `router/index.js`，便于维护：

```js
// router/index.js
import Vue from 'vue';
import VueRouter from 'vue-router';
import Find from '@/views/Find.vue'; // @ 指代 src 目录
import My from '@/views/My.vue';

Vue.use(VueRouter);

const router = new VueRouter({
  routes: [
    { path: '/find', component: Find },
    { path: '/my', component: My }
  ]
});

export default router;
```

```js
// main.js 中引入
import router from './router/index.js';

new Vue({
  render: h => h(App),
  router
}).$mount('#app');
```


### 5. 声明式导航（router-link 组件）
VueRouter 提供 `<router-link>` 组件替代 `<a>` 标签，优势：
- 无需手动加 `#`，直接通过 `to` 属性指定路径。
- 自动添加高亮类（可自定义）。

#### 基本用法
```vue
<router-link to="/find">发现</router-link>
<router-link to="/my">我的</router-link>
```

#### 高亮类自定义
默认高亮类：
- `router-link-active`：模糊匹配（如 `/my` 匹配 `/my`、`/my/detail`）。
- `router-link-exact-active`：精确匹配（仅 `/my` 匹配 `/my`）。

自定义类名：
```js
const router = new VueRouter({
  routes: [...],
  linkActiveClass: 'active',      // 替换模糊匹配类
  linkExactActiveClass: 'exact-active' // 替换精确匹配类
});
```


### 6. 声明式导航 - 传参
#### （1）查询参数传参（多参数）
- 语法：`to="/path?参数1=值1&参数2=值2"`
- 接收：`this.$route.query.参数名`

```vue
<!-- 传参 -->
<router-link to="/search?keyword=音乐&type=1">搜索</router-link>

<!-- 接收参数（Search 组件） -->
<script>
export default {
  mounted() {
    console.log(this.$route.query.keyword); // 音乐
    console.log(this.$route.query.type); // 1
  }
}
</script>
```

#### （2）动态路由传参（单参数）
- 配置动态路由：`path: '/search/:参数名'`（`:参数名` 为占位符）。
- 可选参数：加 `?` 表示参数可选（`path: '/search/:keyword?'`）。
- 传参：`to="/search/参数值"`。
- 接收：`this.$route.params.参数名`。

```js
// 配置动态路由
const router = new VueRouter({
  routes: [
    { path: '/search/:keyword', component: Search }
  ]
});
```

```vue
<!-- 传参 -->
<router-link to="/search/周杰伦">搜索周杰伦</router-link>

<!-- 接收参数（Search 组件） -->
<script>
export default {
  mounted() {
    console.log(this.$route.params.keyword); // 周杰伦
  }
}
</script>
```


### 7. 路由高级配置
#### （1）重定向
匹配特定路径后，强制跳转到目标路径：
```js
const router = new VueRouter({
  routes: [
    { path: '/', redirect: '/home' }, // 访问 / 时跳转到 /home
    { path: '/home', component: Home }
  ]
});
```

#### （2）404 页面
当路径匹配不到任何规则时，显示 404 页面（需放在路由规则最后）：
```js
import NotFound from './views/NotFound.vue';

const router = new VueRouter({
  routes: [
    // ...其他规则
    { path: '*', component: NotFound } // * 匹配所有未匹配的路径
  ]
});
```

#### （3）路由模式
- **hash 模式**（默认）：路径带 `#`（如 `http://localhost:8080/#/home`），兼容性好。
- **history 模式**：路径无 `#`（如 `http://localhost:8080/home`），需后端配合配置。

```js
const router = new VueRouter({
  mode: 'history', // 启用 history 模式
  routes: [...]
});
```


### 8. 编程式导航（JS 控制跳转）
通过 `this.$router.push()` 实现路由跳转，适合在事件处理中使用。

#### （1）基本跳转
```js
// 方式1：直接传路径
this.$router.push('/find');

// 方式2：传配置对象（path）
this.$router.push({ path: '/find' });

// 方式3：传配置对象（name，需给路由配置 name）
this.$router.push({ name: 'Find' }); // 路由规则需配置 { name: 'Find', path: '/find', ... }
```

#### （2）编程式导航 - 传参
##### ① query 传参
```js
// 方式1：路径拼接
this.$router.push('/search?keyword=音乐&type=1');

// 方式2：配置对象
this.$router.push({
  path: '/search',
  query: { keyword: '音乐', type: 1 }
});

// 方式3：name + query（推荐）
this.$router.push({
  name: 'Search',
  query: { keyword: '音乐', type: 1 }
});

// 接收：this.$route.query.keyword
```

##### ② 动态路由传参
```js
// 方式1：路径拼接
this.$router.push('/search/周杰伦');

// 方式2：配置对象（path）
this.$router.push({ path: '/search/周杰伦' });

// 方式3：name + params
this.$router.push({
  name: 'Search', // 路由规则需配置 { name: 'Search', path: '/search/:keyword', ... }
  params: { keyword: '周杰伦' }
});

// 接收：this.$route.params.keyword
```


### 9. 二级路由（嵌套路由）
通过 `children` 配置项实现路由嵌套，适用于页面内有子模块的场景（如首页包含推荐、排行榜）。

#### 配置步骤
1. **父组件中添加二级路由出口**：
```vue
<!-- 父组件 Home.vue -->
<template>
  <div>
    <h2>首页</h2>
    <!-- 二级导航 -->
    <router-link to="/home/recommend">推荐</router-link>
    <router-link to="/home/rank">排行榜</router-link>
    <!-- 二级路由出口：子组件显示在这里 -->
    <router-view></router-view>
  </div>
</template>
```

2. **配置二级路由规则**：
```js
// router/index.js
import Home from '@/views/Home.vue';
import Recommend from '@/views/Home/Recommend.vue'; // 子组件
import Rank from '@/views/Home/Rank.vue'; // 子组件

const router = new VueRouter({
  routes: [
    {
      path: '/home',
      component: Home,
      // 二级路由规则（children 是数组）
      children: [
        { path: 'recommend', component: Recommend }, // 子路径无需加 /
        { path: 'rank', component: Rank }
      ]
    }
  ]
});
```

3. **访问二级路由**：  
   路径为 `/父路径/子路径`（如 `/home/recommend`）。


# Vue 进阶核心知识点（续）


## 一、组件缓存：`keep-alive`
### 1. 基本定义
`keep-alive` 是 Vue 的**内置抽象组件**，用于包裹动态组件时，**缓存不活动的组件实例**（而非销毁）。  
- 特性：自身不会渲染为 DOM 元素，也不会出现在父组件链中。


### 2. 核心作用与优点
- **核心作用**：在组件切换时保留组件状态（如表单输入值、列表滚动位置），避免重复创建/销毁组件。
- **优点**：
  1. 减少 DOM 重复渲染，降低性能消耗。
  2. 缩短组件切换加载时间，提升用户体验。


### 3. 3 个关键属性
| 属性名   | 类型       | 作用描述                                                                 |
|----------|------------|--------------------------------------------------------------------------|
| `include` | 字符串/数组 | 仅**匹配名称**的组件会被缓存（组件名需与 `component.name` 一致）。       |
| `exclude` | 字符串/数组 | 仅**匹配名称**的组件不会被缓存（优先级高于 `include`）。                 |
| `max`     | 数字       | 限制缓存的组件实例数量，超出时销毁最早缓存的实例。                       |


### 4. 使用示例
```vue
<template>
  <!-- 仅缓存名为 "LayoutPage" 的组件 -->
  <keep-alive :include="['LayoutPage']">
    <!-- 动态组件/路由出口（被包裹的组件会被缓存） -->
    <router-view></router-view>
  </keep-alive>
</template>

<script>
export default {
  // 注意：被缓存的组件需定义 name 属性（与 include 匹配）
  name: 'LayoutPage'
}
</script>
```


## 二、Vue 项目自定义创建流程（Vue CLI）
通过 Vue CLI 自定义创建项目，按需选择功能模块（步骤中“空格”用于选中/取消）：

1. **启动创建命令**：  
   在终端执行 `vue create 项目名`（如 `vue create vue-demo`）。

2. **选择创建模式**：  
   上下键切换，回车确认 → 选择 **Manually select features**（自定义功能）。

3. **勾选所需功能**（空格选中，回车下一步）：  
   - 必选：`Babel`（ES6 转 ES5）、`Router`（路由）、`CSS Pre-processors`（CSS 预处理）。  
   - 可选：`Linter / Formatter`（代码规范检查）。

4. **选择 Vue 版本**：  
   选择 **2.x**（匹配后续 Vuex、VueRouter 3.x 版本）。

5. **配置 VueRouter**：  
   - 问“是否使用 history 模式？” → 选 **No**（默认 hash 模式，无需后端配置）。

6. **选择 CSS 预处理器**：  
   上下键切换 → 选择 **Less**（常用且学习成本低）。

7. **选择代码规范（若勾选 Linter）**：  
   选择 **ESLint + Standard config**（行业常用规范，强制统一代码风格）。  
   接着问“何时检查代码？” → 选择 **Lint on save**（保存时自动检查）。

8. **配置文件存放位置**：  
   选择 **In dedicated config files**（将配置分散到单独文件，如 `babel.config.js`、`vue.config.js`，便于维护）。

9. **是否保存为模板**：  
   选 **No**（首次创建无需保存，后续可按需选择 Yes）。

10. **等待创建**：  
    CLI 自动安装依赖，完成后进入项目目录（`cd 项目名`），执行 `yarn serve` 启动项目。


## 三、Vuex（状态管理工具）
### 1. 基本概念
Vuex 是 Vue 官方的**全局状态管理工具**，用于集中管理多个组件共享的数据（如用户信息、购物车数据）。


### 2. 适用场景与优势
#### （1）适用场景
- 某一状态需在**多个组件**中使用（如用户登录状态）。
- 多个组件需**共同修改**同一份数据（如购物车添加/删除商品）。

#### （2）优势
- 数据**集中化管理**，避免组件间频繁通信。
- 数据响应式，状态变化时关联组件自动更新。
- 操作可追溯，便于调试（结合 Vue DevTools）。


### 3. Vuex 安装与初始化（Vue 2 对应 Vuex 3.x）
#### （1）安装依赖
```bash
yarn add vuex@3
```

#### （2）创建 Vuex 仓库（`store/index.js`）
```js
// store/index.js
import Vue from 'vue'
import Vuex from 'vuex'

// 1. 安装 Vuex（全局注册）
Vue.use(Vuex)

// 2. 创建仓库实例（核心配置）
const store = new Vuex.Store({
  // 后续核心配置（state、mutations 等）写在这里
})

// 3. 导出仓库，供 main.js 挂载
export default store
```

#### （3）在 main.js 中挂载
```js
// main.js
import Vue from 'vue'
import App from './App.vue'
import store from './store/index.js' // 导入 Vuex 仓库

new Vue({
  render: h => h(App),
  store // 挂载到 Vue 实例，全局可通过 this.$store 访问
}).$mount('#app')
```


### 4. Vuex 核心模块：`state`（存储数据）
#### （1）定义 `state`（提供公共数据）
```js
// store/index.js
const store = new Vuex.Store({
  state: {
    // 定义共享数据（类似组件的 data）
    count: 100, // 示例：计数器
    userInfo: { name: '张三', age: 18 } // 示例：用户信息
  }
})
```

#### （2）使用 `state` 数据（3 种方式）
| 使用场景         | 语法示例                                  |
|------------------|-------------------------------------------|
| 组件模板中       | `{{ $store.state.count }}`                |
| 组件逻辑中（JS） | `this.$store.state.userInfo.name`         |
| 独立 JS 模块中   | `import store from './store'` + `store.state.count` |

#### （3）辅助函数 `mapState`（简化语法）
用于将 `state` 数据自动映射到组件的**计算属性**中，避免重复写 `$store.state`。

```vue
<template>
  <div>{{ count }} - {{ userInfo.name }}</div>
</template>

<script>
// 1. 导入 mapState
import { mapState } from 'vuex'

export default {
  computed: {
    // 2. 映射 state 数据（两种写法）
    // 写法1：数组形式（映射同名属性）
    ...mapState(['count', 'userInfo']), 
    // 写法2：对象形式（自定义属性名）
    ...mapState({
      myCount: 'count', // 组件中用 myCount 对应 state.count
      myUser: 'userInfo'
    })
  }
}
</script>
```


### 5. Vuex 核心模块：`mutations`（修改数据）
#### （1）核心规则
- **唯一途径**：修改 `state` 数据必须通过 `mutations`（禁止直接修改 `state`，如 `this.$store.state.count++`）。
- **必须同步**：`mutations` 中只能写同步代码（异步操作需用 `actions`）。

#### （2）定义 `mutations`
```js
// store/index.js
const store = new Vuex.Store({
  state: { count: 100 },
  mutations: {
    // 定义修改方法（参数1：state 实例；参数2：可选，外部传入的参数）
    addCount(state, num) {
      state.count += num // 修改 state 数据
    },
    subCount(state, num) {
      state.count -= num
    }
  }
})
```

#### （3）调用 `mutations`（2 种方式）
1. **直接调用**：通过 `this.$store.commit('mutation名', 参数)`  
   ```js
   // 组件逻辑中
   this.$store.commit('addCount', 10) // 调用 addCount，传入参数 10
   ```

2. **辅助函数 `mapMutations`**：映射到组件的 `methods` 中，简化调用。  
   ```vue
   <script>
   import { mapMutations } from 'vuex'

   export default {
     methods: {
       // 映射 mutations 方法
       ...mapMutations(['addCount', 'subCount']),
       // 调用时直接当方法使用
       handleAdd() {
         this.addCount(10) // 等价于 this.$store.commit('addCount', 10)
       }
     }
   }
   </script>
   ```


### 6. Vuex 核心模块：`actions`（处理异步）
#### （1）核心作用
处理**异步操作**（如接口请求、定时器），异步完成后通过调用 `mutations` 修改 `state`（不能直接修改 `state`）。

#### （2）定义 `actions`
```js
// store/index.js
const store = new Vuex.Store({
  state: { count: 100 },
  mutations: {
    changeCount(state, newCount) {
      state.count = newCount
    }
  },
  actions: {
    // 定义异步方法（参数1：context 上下文，类似 $store；参数2：外部传入的参数）
    setAsyncCount(context, num) {
      // 异步操作（如定时器、接口请求）
      setTimeout(() => {
        // 异步完成后，调用 mutations 修改 state
        context.commit('changeCount', num)
      }, 1000)
    }
  }
})
```

#### （3）调用 `actions`（2 种方式）
1. **直接调用**：通过 `this.$store.dispatch('action名', 参数)`  
   ```js
   // 组件逻辑中
   this.$store.dispatch('setAsyncCount', 200) // 1秒后 count 变为 200
   ```

2. **辅助函数 `mapActions`**：映射到组件的 `methods` 中。  
   ```vue
   <script>
   import { mapActions } from 'vuex'

   export default {
     methods: {
       ...mapActions(['setAsyncCount']),
       handleAsync() {
         this.setAsyncCount(200) // 等价于 this.$store.dispatch('setAsyncCount', 200)
       }
     }
   }
   </script>
   ```


### 7. Vuex 核心模块：`getters`（计算派生数据）
#### （1）核心作用
类似组件的**计算属性**，对 `state` 数据进行加工处理（如过滤、排序），返回派生数据，且结果会被缓存（依赖不变时不会重复计算）。

#### （2）定义 `getters`
```js
// store/index.js
const store = new Vuex.Store({
  state: {
    list: [1, 2, 3, 4, 5, 6, 7, 8] // 原始数据
  },
  getters: {
    // 定义计算方法（参数：state 实例）
    filterList(state) {
      // 返回大于 5 的数据（派生数据）
      return state.list.filter(item => item > 5)
    },
    listLength(state, getters) {
      // 可依赖其他 getters（参数2：getters 实例）
      return getters.filterList.length // 返回过滤后数组的长度
    }
  }
})
```

#### （3）使用 `getters`（2 种方式）
1. **直接调用**：`this.$store.getters.getter名`  
   ```vue
   <template>
     <div>{{ $store.getters.filterList }}</div> <!-- 显示 [6,7,8] -->
   </template>
   ```

2. **辅助函数 `mapGetters`**：映射到组件的 `computed` 中。  
   ```vue
   <script>
   import { mapGetters } from 'vuex'

   export default {
     computed: {
       ...mapGetters(['filterList', 'listLength'])
     }
   }
   </script>
   ```


### 8. Vuex 模块：`module`（拆分复杂状态）
当项目规模较大时，将 `state`、`mutations` 等按业务拆分到独立模块（如 `user` 模块、`cart` 模块），避免仓库过于臃肿。

#### （1）模块拆分步骤
##### 步骤 1：创建子模块文件（如 `store/modules/user.js`）
```js
// store/modules/user.js
const state = {
  userInfo: { name: '张三', age: 18 } // 模块私有状态
}

const mutations = {
  updateName(state, newName) {
    state.userInfo.name = newName // 修改模块内的 state
  }
}

const actions = {
  asyncUpdateName(context, newName) {
    setTimeout(() => {
      context.commit('updateName', newName)
    }, 1000)
  }
}

const getters = {
  userNameLength(state) {
    return state.userInfo.name.length // 模块内的 getters
  }
}

export default {
  namespaced: true, // 开启命名空间（关键！避免模块间方法冲突）
  state,
  mutations,
  actions,
  getters
}
```

##### 步骤 2：在根仓库中注册子模块
```js
// store/index.js
import Vue from 'vue'
import Vuex from 'vuex'
import user from './modules/user' // 导入子模块

Vue.use(Vuex)

const store = new Vuex.Store({
  modules: {
    user // 注册子模块（模块名：user）
  }
})

export default store
```

#### （2）模块数据/方法的访问（开启命名空间后）
| 模块内容   | 直接调用语法                              | 辅助函数映射语法（以 user 模块为例）                          |
|------------|-------------------------------------------|---------------------------------------------------------------|
| state      | `$store.state.user.userInfo.name`         | `...mapState('user', ['userInfo'])`                            |
| getters    | `$store.getters['user/userNameLength']`   | `...mapGetters('user', ['userNameLength'])`                    |
| mutations  | `$store.commit('user/updateName', '李四')`| `...mapMutations('user', ['updateName'])`                      |
| actions    | `$store.dispatch('user/asyncUpdateName')` | `...mapActions('user', ['asyncUpdateName'])`                   |


### 关键注意点
- 模块必须开启 `namespaced: true`，否则模块的 `mutations`、`actions` 会挂载到全局，可能与其他模块冲突。
- 模块内的 `state` 是**私有**的，需通过 `$store.state.模块名.xxx` 访问；`getters`、`mutations`、`actions` 需通过 `模块名/xxx` 访问。

# Vue 组件库与 Vue3 核心知识点整理笔记


## 一、Vue 组件库（PC端/移动端）
### 1. 常用组件库分类
| 应用场景 | 推荐组件库                | 特点                     |
|----------|---------------------------|--------------------------|
| PC端     | Element UI、Ant Design Vue | 组件丰富，适配桌面端交互 |
| 移动端   | Vant、Mint UI、Cube UI    | 轻量，适配移动端屏幕与手势 |

### 2. 移动端组件库：Vant（重点）
Vant 是 Vue 生态中最常用的移动端组件库，支持**全部导入**和**按需导入**（推荐按需导入，减少打包体积）。

#### （1）全部导入（简单，适合小型项目）
1. **安装 Vant**（Vue2 对应 Vant@2，Vue3 对应 Vant@3+）：  
   ```bash
   yarn add vant@latest-v2 # Vue2 项目
   ```
2. **在 main.js 中全局注册**：  
   ```js
   import Vue from 'vue'
   import Vant from 'vant' // 导入所有组件
   import 'vant/lib/index.css' // 导入全局样式

   Vue.use(Vant) // 全局注册 Vant 组件
   ```

#### （2）按需导入（推荐，减少打包体积）
1. **安装 Vant 与插件**：  
   ```bash
   yarn add vant@latest-v2 # 安装 Vant
   yarn add babel-plugin-import --dev # 安装按需导入插件
   ```
2. **配置 babel.config.js**：  
   ```js
   module.exports = {
     presets: ['@vue/cli-plugin-babel/preset'],
     plugins: [
       // 配置 Vant 按需导入
       ['import', {
         libraryName: 'vant', // 组件库名
         libraryDirectory: 'es', // 模块目录
         style: true // 自动导入组件样式
       }, 'vant']
     ]
   }
   ```
3. **在 main.js 中按需注册组件**：  
   ```js
   import Vue from 'vue'
   import { Button, Toast } from 'vant' // 只导入需要的组件

   Vue.use(Button) // 注册 Button 组件
   Vue.use(Toast) // 注册 Toast 组件
   ```


## 二、vw 适配（postcss-px-to-viewport）
移动端适配方案之一，将 `px` 自动转换为 `vw`（视口宽度单位），适配不同屏幕尺寸。

### 实现步骤
1. **安装插件**：  
   ```bash
   yarn add postcss-px-to-viewport@1.1.1 -D # -D 表示开发依赖
   ```
2. **创建 postcss.config.js 配置文件**：  
   ```js
   module.exports = {
     plugins: {
       'postcss-px-to-viewport': {
         viewportWidth: 375, // 设计稿宽度（通常为 375px 或 750px）
         viewportUnit: 'vw', // 转换后的单位
         propList: ['*'] // 需要转换的 CSS 属性（* 表示所有）
       }
     }
   }
   ```
3. **使用**：  
   开发时直接写 `px`（如 `width: 100px`），插件会自动转换为 `vw`（如 `width: 26.666vw`，基于 375px 设计稿）。


## 三、Toast 轻提示（Vant）
用于显示简短的提示信息，支持组件内/外调用。

### 1. 注册（按需导入时已注册，见上文 Vant 按需导入）
```js
import Vue from 'vue'
import { Toast } from 'vant'
Vue.use(Toast)
```

### 2. 两种调用方式
| 调用场景       | 语法示例                          |
|----------------|-----------------------------------|
| 组件内/外（导入） | `import { Toast } from 'vant'` + `Toast('提示内容')` |
| 组件内（this 调用） | `this.$toast('提示内容')`（Vue 原型已挂载） |

### 示例
```js
// 组件内调用
handleClick() {
  // 方式1：this 调用
  this.$toast('操作成功')
  
  // 方式2：导入调用
  import { Toast } from 'vant'
  Toast({
    message: '带图标提示',
    icon: 'success', // 图标类型
    duration: 2000 // 显示时长（ms）
  })
}
```


## 四、页面访问拦截（路由导航守卫）
通过 `router.beforeEach` 实现路由跳转前的拦截（如登录验证、权限控制）。

### 核心语法
```js
// 在 router/index.js 中配置
router.beforeEach((to, from, next) => {
  // to：即将跳转到的路由对象（目标路由）
  // from：当前要离开的路由对象（来源路由）
  // next()：是否放行（核心）
  // - next()：直接放行，进入 to 路由
  // - next('/login')：拦截，跳转到 /login 路由
  // - next(false)：阻止跳转

  // 示例：未登录时拦截非登录页，跳转到登录页
  const token = localStorage.getItem('token') // 获取登录令牌
  if (!token && to.path !== '/login') {
    next('/login') // 未登录且目标不是登录页，拦截到登录页
  } else {
    next() // 已登录或目标是登录页，放行
  }
})
```


## 五、Mixins（跨组件逻辑复用）
用于提取多个组件的公共逻辑（如弹窗提示、登录验证），实现代码复用。

### 实现步骤
1. **创建 Mixin 文件**（如 `mixins/loginConfirm.js`）：  
   ```js
   // mixins/loginConfirm.js
   export default {
     methods: {
       // 公共方法：登录验证提示
       checkLogin() {
         if (!localStorage.getItem('token')) {
           this.$toast('请先登录')
           return false
         }
         return true
       }
     }
   }
   ```
2. **在组件中导入并使用**：  
   ```vue
   <script>
   // 导入 Mixin
   import loginConfirm from '@/mixins/loginConfirm.js'

   export default {
     // 注入 Mixin（可注入多个，数组形式）
     mixins: [loginConfirm],
     methods: {
       handleSubmit() {
         // 调用 Mixin 中的公共方法
         if (!this.checkLogin()) return
         // 后续业务逻辑
       }
     }
   }
   </script>
   ```


## 六、Vue 项目打包与优化
### 1. 打包命令与结果
- **打包命令**：  
  ```bash
  yarn build # 或 npm run build
  ```
- **打包结果**：项目根目录生成 `dist` 文件夹，内含静态资源（HTML/CSS/JS），直接部署到服务器即可访问。

### 2. 配置 publicPath（解决双击 HTML 无法运行的问题）
默认打包后需部署到服务器根目录，若需双击 HTML 运行，需配置相对路径：  
```js
// vue.config.js（项目根目录，无则新建）
module.exports = {
  publicPath: './' // 配置为相对路径
}
```

### 3. 打包优化：路由懒加载
#### 问题
默认打包会将所有路由组件合并为一个 JS 文件，体积过大，影响首屏加载速度。

#### 解决方案：路由懒加载
将路由组件拆分为独立代码块，仅当访问路由时才加载对应组件。

#### 实现步骤
```js
// router/index.js
const router = new VueRouter({
  routes: [
    // 传统写法（非懒加载）：import ProDetail from '@/views/prodetail'
    // 懒加载写法：异步导入组件
    {
      path: '/prodetail/:id',
      component: () => import('@/views/prodetail') // 异步组件
    },
    {
      path: '/pay',
      component: () => import('@/views/pay') // 异步组件
    }
  ]
})
```


## 七、Vue3 核心知识点
### 1. Vue3 项目创建（create-vue）
#### 步骤
1. **安装 Node.js**（需 v14.18+ 版本）。  
2. **执行创建命令**：  
   ```bash
   npm init vue@latest # 或 yarn create vue
   ```
3. **按需选择配置**（按回车确认/空格选中）：  
   - 项目名称、是否使用 TypeScript、ESLint、Vue Router、Pinia（Vue3 状态管理）等。
4. **安装依赖并启动**：  
   ```bash
   cd 项目名 # 进入项目目录
   npm install # 安装依赖
   npm run dev # 启动开发服务器
   ```


### 2. setup 选项（Vue3 核心入口）
`setup` 是 Vue3 组件的逻辑入口，替代 Vue2 的 `data`、`methods` 等选项，支持两种写法：

#### （1）原始写法（选项式 API 中使用）
```vue
<script>
export default {
  setup() {
    // 1. 声明数据（非响应式，需配合 ref/reactive 使其响应式）
    const mes = 'this is a message'
    
    // 2. 声明方法
    const Msg = () => {
      console.log('Msg 方法被调用')
    }
    
    // 3. 返回数据/方法，供模板使用
    return { mes, Msg }
  }
}
</script>
```

#### （2）简化写法（`<script setup>` 语法糖，推荐）
无需 `export default` 和 `return`，声明的变量/方法直接供模板使用：
```vue
<script setup>
// 声明数据
const mes = 'this is a message'

// 声明方法
const Msg = () => {
  console.log('Msg 方法被调用')
}
</script>

<template>
  <div>{{ mes }}</div>
  <button @click="Msg">调用方法</button>
</template>
```

#### setup 核心特点
- 响应式数据：需通过 `ref`/`reactive` 函数声明（见下文）。
- 解构 `props`：需用 `toRefs` 保持响应式（否则解构后失去响应）。
- 生命周期：需导入 `onMounted`/`onUpdated` 等钩子（无 `beforeCreate`/`created`，直接写在 setup 顶层）。


### 3. 响应式 API：ref 与 reactive
Vue3 通过函数创建响应式数据，替代 Vue2 的 `Object.defineProperty`。

| API       | 适用数据类型       | 脚本中访问/修改方式       | 模板中访问方式 |
|-----------|--------------------|--------------------------|----------------|
| `ref`     | 简单类型（Number/String/Boolean）、复杂类型 | 需加 `.value`（如 `count.value++`） | 直接访问（如 `count`） |
| `reactive`| 复杂类型（Object/Array） | 直接访问（如 `state.name = '张三'`） | 直接访问（如 `state.name`） |

#### 示例：ref
```vue
<script setup>
import { ref } from 'vue'

// 1. 创建响应式数据（简单类型）
const count = ref(0) // 初始值为 0

// 2. 修改响应式数据（需加 .value）
const increment = () => {
  count.value++
}
</script>

<template>
  <div>count: {{ count }}</div> <!-- 模板中无需 .value -->
  <button @click="increment">+1</button>
</template>
```

#### 示例：reactive
```vue
<script setup>
import { reactive } from 'vue'

// 1. 创建响应式数据（复杂类型）
const user = reactive({
  name: '张三',
  age: 18
})

// 2. 修改响应式数据（直接访问属性）
const updateUser = () => {
  user.name = '李四'
  user.age = 20
}
</script>

<template>
  <div>name: {{ user.name }}, age: {{ user.age }}</div>
  <button @click="updateUser">更新用户</button>
</template>
```


### 4. 计算属性：computed 函数
替代 Vue2 的 `computed` 选项，通过函数创建计算属性，支持只读和读写两种模式。

#### （1）只读模式（默认）
```vue
<script setup>
import { ref, computed } from 'vue'

const count = ref(0)
// 创建计算属性：count 的 2 倍
const doubleCount = computed(() => {
  return count.value * 2
})
</script>

<template>
  <div>count: {{ count }}</div>
  <div>doubleCount: {{ doubleCount }}</div> <!-- 直接访问 -->
</template>
```

#### （2）读写模式（配置 get/set）
```vue
<script setup>
import { ref, computed } from 'vue'

const count = ref(0)
// 读写模式的计算属性
const plusOne = computed({
  // 获取值
  get() {
    return count.value + 1
  },
  // 设置值（修改计算属性时触发）
  set(val) {
    count.value = val - 1
  }
})

// 修改计算属性（触发 set）
const updatePlusOne = () => {
  plusOne.value = 10 // 此时 count.value 变为 9
}
</script>
```

#### 注意事项
- 计算属性中**不能有副作用**（如异步请求、修改 DOM）。
- 只读计算属性**不能直接修改**（否则报错）。


### 5. 侦听器：watch 函数
替代 Vue2 的 `watch` 选项，用于监听响应式数据变化，支持单个/多个数据、深度监听等。

#### （1）侦听单个 ref 数据
```vue
<script setup>
import { ref, watch } from 'vue'

const count = ref(0)

// 侦听 count 变化
watch(count, (newValue, oldValue) => {
  console.log(`count 从 ${oldValue} 变为 ${newValue}`)
}, {
  immediate: true, // 初始化时立即执行一次
  deep: false // 简单类型无需深度监听（默认 false）
})
</script>
```

#### （2）侦听多个数据
```vue
<script setup>
import { ref, watch } from 'vue'

const count = ref(0)
const name = ref('张三')

// 侦听 count 和 name 两个数据
watch(
  [count, name], // 第一个参数：数组，包含要侦听的所有数据
  ([newCount, newName], [oldCount, oldName]) => { // 第二个参数：回调，接收新/旧值数组
    console.log(`count: ${oldCount} → ${newCount}`)
    console.log(`name: ${oldName} → ${newName}`)
  },
  { immediate: true }
)
</script>
```

#### （3）侦听 reactive 数据（深度监听）
```vue
<script setup>
import { reactive, watch } from 'vue'

const user = reactive({
  name: '张三',
  age: 18
})

// 方式1：直接侦听 reactive 对象（自动深度监听）
watch(user, (newUser) => {
  console.log('user 变化：', newUser)
})

// 方式2：精确侦听对象的某个属性（需用函数返回）
watch(
  () => user.age, // 函数返回要侦听的属性
  (newAge) => {
    console.log('age 变化：', newAge)
  }
)
</script>
```


### 6. Vue3 生命周期钩子
Vue3 生命周期钩子需从 `vue` 中导入，且只能在 `setup` 中使用（无 `beforeCreate`/`created`，直接写在 setup 顶层）。

| Vue3 钩子函数       | 作用（对应 Vue2）                |
|---------------------|-----------------------------------|
| `onBeforeMount`     | 组件挂载前（`beforeMount`）       |
| `onMounted`         | 组件挂载后（`mounted`）           |
| `onBeforeUpdate`    | 组件更新前（`beforeUpdate`）      |
| `onUpdated`         | 组件更新后（`updated`）           |
| `onBeforeUnmount`   | 组件卸载前（`beforeDestroy`）     |
| `onUnmounted`       | 组件卸载后（`destroyed`）         |

#### 示例
```vue
<script setup>
import { onMounted, onUnmounted } from 'vue'

// 组件挂载后执行
onMounted(() => {
  console.log('组件挂载完成，可操作 DOM')
})

// 组件卸载前执行
onUnmounted(() => {
  console.log('组件即将卸载，清理资源')
})
</script>
```


### 7. Vue3 组件通信
#### （1）父传子（defineProps）
替代 Vue2 的 `props` 选项，通过 `defineProps` 声明接收的父组件数据。

```vue
<!-- 父组件（Parent.vue） -->
<script setup>
import { ref } from 'vue'
import Son from './Son.vue'

// 父组件数据（响应式）
const parentVal = ref(10)
</script>

<template>
  <!-- 给子组件绑定属性（静态/动态） -->
  <Son message="静态文本" :val="parentVal"></Son>
</template>
```

```vue
<!-- 子组件（Son.vue） -->
<script setup>
// 声明接收的父组件数据（指定类型）
const props = defineProps({
  message: String, // 静态文本（String 类型）
  val: Number // 动态数据（Number 类型）
})

// 使用 props 数据（无需 .value，已自动解包）
console.log(props.message) // 静态文本
console.log(props.val) // 10
</script>

<template>
  <div>{{ message }}</div>
  <div>{{ val }}</div>
</template>
```

#### （2）子传父（defineEmits）
替代 Vue2 的 `$emit`，通过 `defineEmits` 声明可触发的事件。

```vue
<!-- 父组件（Parent.vue） -->
<script setup>
import Son from './Son.vue'

// 父组件方法：接收子组件数据
const getSonMsg = (msg) => {
  console.log('子组件传递的消息：', msg)
}
</script>

<template>
  <!-- 给子组件绑定事件（kebab-case 命名） -->
  <Son @get-message="getSonMsg"></Son>
</template>
```

```vue
<!-- 子组件（Son.vue） -->
<script setup>
// 声明可触发的事件（数组形式，kebab-case 命名）
const emit = defineEmits(['get-message'])

// 子组件方法：触发事件并传递数据
const sendMsg = () => {
  emit('get-message', 'this is son msg') // 第二个参数为传递给父组件的数据
}
</script>

<template>
  <button @click="sendMsg">给父组件发消息</button>
</template>
```


### 8. 模板引用（获取 DOM/组件实例）
替代 Vue2 的 `ref` 属性，通过 `ref` 函数创建引用对象，绑定到 DOM 或组件上。

#### （1）获取 DOM 元素
```vue
<script setup>
import { ref, onMounted } from 'vue'

// 1. 创建引用对象（初始值为 null）
const h1Ref = ref(null)

// 2. 组件挂载后才能获取 DOM（onMounted 钩子）
onMounted(() => {
  console.log('获取到的 h1 元素：', h1Ref.value) // <h1>标题</h1>
  h1Ref.value.style.color = 'red' // 修改 DOM 样式
})
</script>

<template>
  <!-- 3. 将引用对象绑定到 DOM 元素（ref 属性值与引用对象名一致） -->
  <h1 ref="h1Ref">标题</h1>
</template>
```

#### （2）获取子组件实例（defineExpose）
`<script setup>` 语法糖下，子组件的属性/方法默认不暴露给父组件，需通过 `defineExpose` 显式暴露。

```vue
<!-- 子组件（Son.vue） -->
<script setup>
import { ref } from 'vue'

// 子组件私有属性
const count = ref(999)

// 子组件私有方法
const sonMethod = () => {
  console.log('子组件方法被调用')
}

// 显式暴露属性和方法（供父组件访问）
defineExpose({
  count,
  sonMethod
})
</script>
```

```vue
<!-- 父组件（Parent.vue） -->
<script setup>
import { ref, onMounted } from 'vue'
import Son from './Son.vue'

// 1. 创建引用对象
const sonRef = ref(null)

// 2. 挂载后访问子组件暴露的属性/方法
onMounted(() => {
  console.log('子组件 count：', sonRef.value.count) // 999
  sonRef.value.sonMethod() // 调用子组件方法
})
</script>

<template>
  <!-- 3. 绑定引用对象到子组件 -->
  <Son ref="sonRef"></Son>
</template>
```


### 9. 跨层通信：provide 与 inject
替代 Vue2 的 `provide/inject`，用于祖先组件向子孙组件跨层传递数据（无需逐层 props）。

#### （1）祖先组件（provide 提供数据）
```vue
<script setup>
import { ref, provide } from 'vue'

// 祖先组件数据（响应式）
const theme = ref('light')

// 提供数据：第一个参数为 key，第二个参数为数据
provide('themeKey', theme)
</script>
```

#### （2）子孙组件（inject 获取数据）
```vue
<script setup>
import { inject } from 'vue'

// 获取数据：参数为祖先组件提供的 key
const theme = inject('themeKey')

console.log('祖先组件传递的主题：', theme.value) // light
</script>
```


### 10. defineOptions（定义组件选项）
用于在 `<script setup>` 中定义 Options API 选项（如 `name`、`components` 等），除 `props`、`emits`、`expose`、`slots` 外均可定义。

```vue
<script setup>
// 定义组件名称（用于递归组件、缓存等场景）
defineOptions({
  name: 'MyComponent',
  // 其他选项（如 components、filters 等）
  components: { /* ... */ }
})
</script>
```


### 11. defineModel（简化双向绑定）
Vue3.4+ 新增，简化父子组件双向绑定（无需手动定义 `props` 和 `emits`）。

```vue
<!-- 子组件（Child.vue） -->
<script setup>
import { defineModel } from 'vue'

// 定义双向绑定的属性（数组形式）
const { childData } = defineModel(['childData'])
</script>

<template>
  <!-- 直接使用 childData 双向绑定 -->
  <input v-model="childData" placeholder="输入内容" />
</template>
```

```vue
<!-- 父组件（Parent.vue） -->
<script setup>
import { ref } from 'vue'
import Child from './Child.vue'

// 父组件数据（与子组件双向绑定）
const parentData = ref('Initial Data')
</script>

<template>
  <!-- 直接用 v-model 绑定父组件数据 -->
  <Child v-model:childData="parentData"></Child>
  <!-- 父组件数据会随子组件输入实时更新 -->
  <p>父组件数据：{{ parentData }}</p>
</template>
```

# Pinia 与 Vue 生态工具链知识点整理


## 一、Pinia（Vue 状态管理新方案）
Pinia 是 Vue 官方推荐的状态管理工具，作为 Vuex 的替代品，具有更简洁的 API 和更好的 TypeScript 支持。

### 1. 核心优势
- 简化 API，去掉 `modules` 概念，每个 Store 都是独立模块。
- 天然支持 TypeScript，类型推断更友好。
- 支持 Vue2 和 Vue3，兼容性强。
- 无需嵌套，代码结构更清晰。


### 2. 安装与初始化
#### （1）安装 Pinia
```bash
npm install pinia
# 或 pnpm install pinia
```

#### （2）创建 Pinia 实例并挂载
```js
// main.js
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'

// 创建 Pinia 实例
const pinia = createPinia()
const app = createApp(App)

// 挂载到 Vue 应用
app.use(pinia)
app.mount('#app')
```


### 3. 定义 Store
使用 `defineStore` 定义 Store，第一个参数为唯一 ID（字符串），第二个参数为设置函数（类似 Vue3 的 `setup`）。

```js
// store/counter.js
import { defineStore } from 'pinia'
import { ref, computed } from 'vue'

// 定义并导出 Store（命名规范：useXxxStore）
export const useCounterStore = defineStore('counter', () => {
  // 1. 状态（响应式数据，类似 Vuex 的 state）
  const count = ref(0)

  // 2. 计算属性（类似 Vuex 的 getters）
  const doubleCount = computed(() => count.value * 2)

  // 3. 方法（类似 Vuex 的 mutations + actions，支持同步和异步）
  function increment() {
    count.value++
  }

  // 返回需要暴露的状态、计算属性和方法
  return { count, doubleCount, increment }
})
```


### 4. 使用 Store
在组件中导入并调用 Store 函数，即可访问其状态和方法。

```vue
<script setup>
// 导入 Store
import { useCounterStore } from '@/store/counter'

// 获取 Store 实例
const counterStore = useCounterStore()
</script>

<template>
  <!-- 访问状态 -->
  <div>count: {{ counterStore.count }}</div>
  <div>doubleCount: {{ counterStore.doubleCount }}</div>
  
  <!-- 调用方法 -->
  <button @click="counterStore.increment">+1</button>
</template>
```


### 5. 异步操作（无需区分 mutations 和 actions）
Pinia 中无需区分同步（mutations）和异步（actions），直接在方法中写异步逻辑即可。

```js
// store/channel.js
import { defineStore } from 'pinia'
import { ref } from 'vue'
import axios from 'axios'

export const useChannelStore = defineStore('channel', () => {
  // 状态：频道列表
  const list = ref([])

  // 异步方法：获取频道数据
  const getList = async () => {
    const { data } = await axios.get('/api/channels')
    list.value = data.channels // 更新状态
  }

  return { list, getList }
})
```

```vue
<!-- 组件中使用 -->
<script setup>
import { useChannelStore } from '@/store/channel'

const channelStore = useChannelStore()

// 调用异步方法
channelStore.getList()
</script>

<template>
  <ul>
    <li v-for="item in channelStore.list" :key="item.id">
      {{ item.name }}
    </li>
  </ul>
</template>
```


### 6. Store 解构（保持响应性）
直接解构 Store 会丢失响应性，需使用 `storeToRefs` 工具函数。

```vue
<script setup>
import { storeToRefs } from 'pinia'
import { useCounterStore } from '@/store/counter'

const counterStore = useCounterStore()

// 解构响应式状态（使用 storeToRefs）
const { count, doubleCount } = storeToRefs(counterStore)

// 方法可直接解构（无需 storeToRefs）
const { increment } = counterStore
</script>

<template>
  <div>{{ count }}</div> <!-- 仍保持响应性 -->
  <button @click="increment">+1</button>
</template>
```


### 7. 持久化存储（pinia-plugin-persistedstate）
通过插件将 Store 状态持久化到 `localStorage` 或 `sessionStorage`。

#### （1）安装插件
```bash
npm i pinia-plugin-persistedstate
# 或 pnpm install pinia-plugin-persistedstate
```

#### （2）配置插件
```js
// main.js
import { createPinia } from 'pinia'
import piniaPluginPersistedstate from 'pinia-plugin-persistedstate'

const pinia = createPinia()
// 注册持久化插件
pinia.use(piniaPluginPersistedstate)

app.use(pinia)
```

#### （3）在 Store 中启用持久化
```js
// store/user.js
import { defineStore } from 'pinia'
import { ref } from 'vue'

export const useUserStore = defineStore(
  'user',
  () => {
    const token = ref('')
    return { token }
  },
  {
    // 启用持久化
    persist: true
  }
)
```

#### （4）自定义持久化内容（`pick` 选项）
通过 `pick` 指定需要持久化的字段（点表示法）。

```js
export const useUserStore = defineStore(
  'user',
  () => {
    const info = ref({
      name: '张三',
      age: 18,
      token: 'xxx'
    })
    return { info }
  },
  {
    persist: {
      // 只持久化 info.token 和 info.name
      pick: ['info.token', 'info.name']
    }
  }
)
```


## 二、pnpm（高效包管理工具）
pnpm 是替代 npm/yarn 的包管理工具，具有更快的安装速度和更优的磁盘空间利用。

### 常用命令
| 功能               | 命令                                          |
|--------------------|-----------------------------------------------|
| 创建 Vue 项目      | `pnpm create vue`                             |
| 安装依赖           | `pnpm install`（简写 `pnpm i`）               |
| 启动开发服务器     | `pnpm dev`                                    |
| 安装生产依赖       | `pnpm add <包名>`（如 `pnpm add pinia`）       |
| 安装开发依赖       | `pnpm add -D <包名>`（如 `pnpm add -D eslint`）|
| 卸载依赖           | `pnpm remove <包名>`                          |
| 运行脚本           | `pnpm run <脚本名>`（如 `pnpm run build`）    |

### 示例：安装常用依赖
```bash
pnpm add pinia@^2.1.7 vue-router@^4.2.5 element-plus@^2.4.1 axios@^1.6.2 dayjs@^1.11.10
pnpm add -D sass@^1.69.5 normalize.css@^8.0.1 @element-plus/icons-vue@^2.1.0 pinia-plugin-persistedstate
```


## 三、ESLint 配置与代码检查工作流
### 1. ESLint 配置文件（`eslint.config.js`）
用于定义代码规范（如缩进、命名、语法检查等）。

```js
// 基础配置示例（需安装 eslint 及相关插件）
import globals from 'globals'
import pluginVue from 'eslint-plugin-vue'

export default [
  {
    files: ['**/*.{vue,js}'],
    languageOptions: {
      globals: globals.browser,
      parserOptions: {
        ecmaVersion: 'latest',
        sourceType: 'module'
      }
    },
    plugins: {
      vue: pluginVue
    },
    rules: {
      // 禁止未使用的变量
      'no-unused-vars': 'warn',
      // 强制使用单引号
      quotes: ['error', 'single'],
      // 语句末尾必须加分号
      semi: ['error', 'always']
    }
  }
]
```


### 2. 代码检查工作流（husky + pre-commit）
通过 husky 在 git 提交前自动执行代码检查，确保代码符合规范。

#### （1）初始化 husky
```bash
# 初始化 husky（生成 .husky 目录）
pnpm dlx husky-init && pnpm install
```

#### （2）配置 pre-commit 钩子
编辑 `.husky/pre-commit` 文件，添加代码检查命令：
```sh
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

# 提交前执行 lint 检查
pnpm lint
```

#### （3）执行检查
```bash
# 手动执行 lint 检查
pnpm lint
```

提交代码时，husky 会自动触发 `pre-commit` 钩子，若 lint 失败则阻止提交。


## 四、Element Plus（Vue3 桌面端组件库）
Element Plus 是 Vue3 版本的 Element UI，提供丰富的 PC 端组件。

### 1. 安装与自动导入
#### （1）安装 Element Plus
```bash
pnpm install element-plus
```

#### （2）安装自动导入插件
```bash
pnpm add -D unplugin-vue-components unplugin-auto-import
```

#### （3）配置 Vite（`vite.config.js`）
```js
import { defineConfig } from 'vite'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  plugins: [
    // 自动导入 Element Plus 相关函数（如 ElMessage）
    AutoImport({
      resolvers: [ElementPlusResolver()]
    }),
    // 自动导入 Element Plus 组件
    Components({
      resolvers: [ElementPlusResolver()]
    })
  ]
})
```


### 2. 表单组件与校验
Element Plus 的表单组件主要包括 `el-form`（表单容器）、`el-form-item`（表单项）、`el-input`（输入框）等，支持强大的校验功能。

#### 基本用法
```vue
<template>
  <!-- 表单容器：绑定数据和校验规则 -->
  <el-form
    :model="ruleForm"  <!-- 绑定表单数据对象 -->
    :rules="rules"     <!-- 绑定校验规则 -->
    ref="ruleFormRef"  <!-- 表单引用（用于手动触发校验） -->
    label-width="100px"
  >
    <!-- 表单项：用户名 -->
    <el-form-item label="用户名" prop="username">
      <!-- 输入框：绑定表单数据的属性 -->
      <el-input v-model="ruleForm.username" />
    </el-form-item>

    <!-- 表单项：密码 -->
    <el-form-item label="密码" prop="password">
      <el-input v-model="ruleForm.password" type="password" />
    </el-form-item>

    <el-form-item>
      <el-button type="primary" @click="submitForm">提交</el-button>
    </el-form-item>
  </el-form>
</template>

<script setup>
import { ref } from 'vue'

// 表单数据
const ruleForm = ref({
  username: '',
  password: ''
})

// 校验规则
const rules = ref({
  username: [
    { required: true, message: '请输入用户名', trigger: 'blur' },
    { min: 3, max: 10, message: '长度在 3-10 个字符', trigger: 'blur' }
  ],
  password: [
    { required: true, message: '请输入密码', trigger: 'blur' },
    { pattern: /^[0-9a-zA-Z]{6,}$/, message: '密码至少 6 位', trigger: 'blur' }
  ]
})

// 表单引用
const ruleFormRef = ref(null)

// 提交表单
const submitForm = async () => {
  // 手动触发校验
  const valid = await ruleFormRef.value.validate()
  if (valid) {
    // 校验通过，执行提交逻辑
    console.log('提交数据：', ruleForm.value)
  }
}
</script>
```

#### 校验核心属性
- `el-form`: `:model` 绑定表单数据，`:rules` 绑定校验规则。
- `el-form-item`: `prop` 指定当前项对应的校验规则字段（需与 `rules` 中的 key 一致）。
- 表单元素（如 `el-input`）: `v-model` 绑定 `model` 中的具体属性。


## 五、VueQuill（富文本编辑器）
VueQuill 是基于 Quill 的 Vue 富文本编辑器组件，支持格式化、图片上传、表格等功能。

### 基本使用
#### （1）安装 VueQuill
```bash
pnpm add @vueup/vue-quill@latest
```

#### （2）在组件中使用
```vue
<template>
  <QuillEditor
    v-model:content="content"  <!-- 绑定富文本内容 -->
    contentType="html"        <!-- 内容格式（html 或 delta） -->
  />
</template>

<script setup>
import { ref } from 'vue'
import { QuillEditor } from '@vueup/vue-quill'
import '@vueup/vue-quill/dist/vue-quill.snow.css' // 导入样式

// 富文本内容
const content = ref('<p>初始内容</p>')
</script>
```

VueQuill 支持自定义工具栏、图片上传配置等，可根据需求扩展功能。