## Vue.js 代码风格指南  

> 本文档内容均摘录自<a href="https://cn.vuejs.org/v2/style-guide/#/" target="_blank">Vue.js官方风格指南</a>。

### 目录

- [命名](#命名)  
   + [单例组件名](#单例组件)  
   + [基础组件名](#基础组件)  
   + [全局组件名](#全局组件名)
   + [单文件组件文件名](#单文件组件文件名)  
   + [模板中的组件名](#模板中的组件名)  
   + [JS/JSX中的组件名](#JS/JSX中的组件名)  
- [prop](#prop)  
- [attribute](#attribute)  
- [组件](#组件)

### 命名

<a name="单例组件"></a>
- **单例组件名**

  只应该拥有单个活跃实例的组件应该以 The 前缀命名，以示其唯一性。

  > 这不意味着组件只可用于一个单页面，而是每个页面只使用一次。这些组件永远不接受任何 `prop`，因为它们是为你的应用定制的，而不是它们在你的应用中的上下文。如果你发现有必要添加 `prop`，那就表明这实际上是一个可复用的组件，只是目前在每个页面里只使用一次。
  
  ```javascript
  
  // bad
  components/
  |- Heading.vue
  |- MySidebar.vue
  
  // good
  components/
  |- TheHeading.vue
  |- TheSidebar.vue
  
  ```

<a name="基础组件名"></a>
- **基础组件名**  

  应用特定样式和约定的基础组件 (也就是展示类的、无逻辑的或无状态的组件) 应该全部以一个特定的前缀开头，比如 Base、App 或 V。
  
  ```javascript
  
  // bad
  components/
  |- MyButton.vue
  |- VueTable.vue
  |- Icon.vue
  
  //good
  components/
  |- BaseButton.vue
  |- BaseTable.vue
  |- BaseIcon.vue

  components/
  |- AppButton.vue
  |- AppTable.vue
  |- AppIcon.vue

  components/
  |- VButton.vue
  |- VTable.vue
  |- VIcon.vue
  
  ```

<a name="全局组件名"></a>
- **全局组件名**

  `Vue.component` 进行全局组件注册时，使用 `kebab-case` 命名。
  
  ```javascript
  
  // bad 
  Vue.component('myComponent', {
    // ...
  })

  // good 
  Vue.component('MyComponent', {
    // ...
  })

  // best
  Vue.component('my-component', {
    // ...
  })
  
  ```
  
<a name="单文件组件文件名"></a>
- **单文件组件文件名**  

  `单文件组件` 的 `文件名` 应该是 `PascalCase` 风格。
  
  > `kebab-case` 风格也可取，但是出于一致性考虑，尽量使用 `PascalCase` 风格。
  
  ```javascript
  
  // bad 
  components/
  |- mycomponent.vue
    
  components/
  |- myComponent.vue
    
  // good 
  components/
  |- my-component.vue
    
  // best
  components/
  |- MyComponent.vue
  
  ```

<a name="模板中的组件名"></a>
- **模板中的组件名**
  
  在 `单文件组件` 和 `字符串模板` 中使用组件时组件名应该总是 `PascalCase` 风格的——但是在 `DOM 模板` 中使用组件时组件应该是 `kebab-case` 风格的。
  
  ```javascript

  // bad 
  // 单文件组件
  <template>
    <myComponent></myComponent>
    <hiscomponent></hiscomponent>
  </template>

  // 字符串模板
  new Vue({
    template: '<div><myComponent></myComponent><hiscomponent></hiscomponent></div>'
  })

  // DOM模板
  <html>
    <body>
      <div id="templateId">
        <MyComponent></MyComponent>
        <yourComponent></yourComponent>
        <hiscomponent></hiscomponent>
      </div>
      <script>
        new Vue({
          el: '#template'
        });
      </script>
    </body>
  </html>

  // good
  // 单文件组件
  <template>
    <MyComponent></MyComponent>
    <his-component></his-component>
  </template>

  // 字符串模板
  new Vue({
    template: '<div><MyComponent></MyComponent><his-component></his-component></div>'
  })

  // DOM模板
  <html>
    <body>
      <div id="templateId">
        <my-component></my-component>
      </div>
      <script>
        new Vue({
          el: '#template'
        });
      </script>
    </body>
  </html>
  
  ```

<a name="JS/JSX中的组件名"></a>
- **`JS/JSX` 中的组件名**  
  
  `JS/JSX` 中的组件名应该始终是 `PascalCase` 的，仅在使用 `Vue.component` 进行全局组件注册时，采用 `kebab-case` 风格。
  
  ```javascript
  
  // bad
  import myComponent from './MyComponent.vue'
  
  export default {
    name: 'myComponent',
    // ...
  }
  
  export default {
    name: 'my-component',
    // ...
  }
  
  Vue.component('myComponent', {
    // ...
  })
  
  // good
  import MyComponent from './MyComponent.vue'
  
  export default {
    name: 'MyComponent',
    // ...
  }
  
  Vue.component('my-component', {
    // ...
  })

  ```


### prop

- `prop` 定义应该尽量详细。  

  > 在你提交的代码中，`prop` 的定义应该尽量详细，至少需要指定其类型。  
  
  ```javascript

   // bad
   // 这样做只有开发原型系统时可以接受
   props: ['status']

   // good
   props: {
     status: String
   }

   // best
   props: {
     status: {
       type: String,
       required: true,
       validator: function (value) {
         return [
           'syncing',
           'synced',
           'version-conflict',
           'error'
         ].indexOf(value) !== -1
       }
     }
   }
   
  ```

### attribute

- 多个 `attribute` 的元素应该分多行撰写，每个 `attribute` 一行。  

  ```javascript
  
  // bad
  <img class="classname" id="imgId" src="https://vuejs.org/images/logo.png" alt="Vue Logo">
  
  // good
  <img 
    class="classname" 
    id="imgId"
    src="https://vuejs.org/images/logo.png"
    alt="Vue Logo"
  >
  
  ```

- 元素 (包括组件) 的 attribute 应该有统一的顺序。

  > 这是我们为组件选项推荐的默认顺序。它们被划分为几大类，所以你也能知道新添加的自定义 attribute 和指令应该放到哪里。
  
&emsp;&emsp;1. 定义 (提供组件的选项)  
&emsp;&emsp;&emsp;· `is`  

&emsp;&emsp;2. 列表渲染 (创建多个变化的相同元素)  
&emsp;&emsp;&emsp;· `v-for`  
     
&emsp;&emsp;3. 条件渲染 (元素是否渲染/显示)  
&emsp;&emsp;&emsp;· `v-if`  
&emsp;&emsp;&emsp;· `v-else-if`  
&emsp;&emsp;&emsp;· `v-else`  
&emsp;&emsp;&emsp;· `v-show`  
&emsp;&emsp;&emsp;· `v-cloak`  
     
&emsp;&emsp;4. 渲染方式 (改变元素的渲染方式)  
&emsp;&emsp;&emsp;· `v-pre`  
&emsp;&emsp;&emsp;· `v-once`  
     
&emsp;&emsp;5. 全局感知 (需要超越组件的知识)  
&emsp;&emsp;&emsp;· `id`  
     
&emsp;&emsp;6. 唯一的 attribute (需要唯一值的 attribute)  
&emsp;&emsp;&emsp;· `ref`  
&emsp;&emsp;&emsp;· `key`  
     
&emsp;&emsp;7. 双向绑定 (把绑定和事件结合起来)  
&emsp;&emsp;&emsp;· `v-model`  
     
&emsp;&emsp;8. 其它 attribute (所有普通的绑定或未绑定的 attribute)  
     
&emsp;&emsp;9. 事件 (组件事件监听器)  
&emsp;&emsp;&emsp;· `v-on`  

&emsp;&emsp;10. 内容 (覆写元素的内容)  
&emsp;&emsp;&emsp;· `v-html`  
&emsp;&emsp;&emsp;· `v-text`  


- 为 v-for 设置键值。

  > 在组件上总是必须用 key 配合 v-for，以便维护内部组件及其子树的状态。甚至在元素上维护可预测的行为，比如动画中的对象固化 (object constancy)，也是一种好的做法。
  
  ```javascript
  
  //bad
  <ul>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ul>
  
  // good
  <ul>
    <li
      v-for="todo in todos"
      :key="todo.id"
    >
      {{ todo.text }}
    </li>
  </ul>
  
  ```
  
- 避免 `v-if` 和 `v-for` 同时用在同一个元素上。

  > 一般我们在两种常见的情况下会倾向于这样做：
  
   * 为了过滤一个列表中的项目 (比如 v-for="user in users" v-if="user.isActive")。在这种情形下，请将 users 替换为一个计算属性 (比如 activeUsers)，让其返回过滤后的列表。
   
   * 为了避免渲染本应该被隐藏的列表 (比如 v-for="user in users" v-if="shouldShowUsers")。这种情形下，请将 v-if 移动至容器元素上 (比如 ul、ol)。
 
  ```javascript
  
  // bad
  <ul>
    <li
      v-for="user in users"
      v-if="user.isActive"
      :key="user.id"
    >
      {{ user.name }}
    </li>
  </ul>
  
  <ul>
    <li
      v-for="user in users"
      v-if="shouldShowUsers"
      :key="user.id"
    >
      {{ user.name }}
    </li>
  </ul>
  
  // good
  <ul>
    <li
      v-for="user in activeUsers"
      :key="user.id"
    >
      {{ user.name }}
    </li>
  </ul>
  
  <ul v-if="shouldShowUsers">
    <li
      v-for="user in users"
      :key="user.id"
    >
      {{ user.name }}
    </li>
  </ul>
  
  ```

### 组件

- 组件/实例的选项应该有统一的顺序。

  > 这是我们推荐的组件选项默认顺序。它们被划分为几大类，所以你也能知道从插件里添加的新 property 应该放到哪里。
  
&emsp;&emsp;1. 副作用 (触发组件外的影响)  
&emsp;&emsp;&emsp;· `el`  
     
&emsp;&emsp;2. 全局感知 (要求组件以外的知识)    
&emsp;&emsp;&emsp;· `name`  
&emsp;&emsp;&emsp;· `parent`  
  
&emsp;&emsp;3. 组件类型 (更改组件的类型)  
&emsp;&emsp;&emsp;· `functional`  
   
&emsp;&emsp;4. 模板修改器 (改变模板的编译方式)  
&emsp;&emsp;&emsp;· `delimiters`
&emsp;&emsp;&emsp;· `comments`  
   
&emsp;&emsp;5. 模板依赖 (模板内使用的资源)  
&emsp;&emsp;&emsp;· `components`  
&emsp;&emsp;&emsp;· `directives`  
&emsp;&emsp;&emsp;· `filters`  
   
&emsp;&emsp;6. 组合 (向选项里合并 property)  
&emsp;&emsp;&emsp;· `extends`  
&emsp;&emsp;&emsp;· `mixins`  

&emsp;&emsp;7. 接口 (组件的接口)  
&emsp;&emsp;&emsp;· `inheritAttrs`  
&emsp;&emsp;&emsp;· `model`  
&emsp;&emsp;&emsp;· `props/propsData`  
   
&emsp;&emsp;8. 本地状态 (本地的响应式 property)  
&emsp;&emsp;&emsp;· `data` 
&emsp;&emsp;&emsp;· `computed`  

&emsp;&emsp;9. 事件 (通过响应式事件触发的回调)  
&emsp;&emsp;&emsp;· `watch`  
&emsp;&emsp;&emsp;· `生命周期钩子 (按照它们被调用的顺序)`  
&emsp;&emsp;&emsp;&emsp;- `beforeCreate`  
&emsp;&emsp;&emsp;&emsp;- `created`  
&emsp;&emsp;&emsp;&emsp;- `beforeMount`  
&emsp;&emsp;&emsp;&emsp;- `mounted`  
&emsp;&emsp;&emsp;&emsp;- `beforeUpdate`  
&emsp;&emsp;&emsp;&emsp;- `updated`  
&emsp;&emsp;&emsp;&emsp;- `activated`  
&emsp;&emsp;&emsp;&emsp;- `deactivated`  
&emsp;&emsp;&emsp;&emsp;- `beforeDestroyed`  
&emsp;&emsp;&emsp;&emsp;- `destroyed`  

&emsp;&emsp;10. 非响应式的 property (不依赖响应系统的实例 property)  
&emsp;&emsp;&emsp;· `methods`  

&emsp;&emsp;11. 渲染 (组件输出的声明式描述)  
&emsp;&emsp;&emsp;· `template/render`  
&emsp;&emsp;&emsp;· `renderError`  


- 单文件组件的顶级元素的顺序。

  单文件组件应该总是让 `script`、`template` 和 `style` 标签的顺序保持一致。且 `style` 要放在最后，因为另外两个标签至少要有一个。  

  ```javascript

  // bad
  <style>...</style>
  <script>...</script>
  <template>...</template>

  // ComponentA.vue
  <script>...</script>
  <template>...</template>
  <style>...</style>

  // ComponentB.vue
  <template>...</template>
  <script>...</script>
  <style>...</style>

  // good
  // ComponentA.vue
  <script>...</script>
  <template>...</template>
  <style>...</style>

  // ComponentB.vue
  <script>...</script>
  <template>...</template>
  <style>...</style>

  // ComponentA.vue
  <template>...</template>
  <script>...</script>
  <style>...</style>

  // ComponentB.vue
  <template>...</template>
  <script>...</script>
  <style>...</style>

  ```


