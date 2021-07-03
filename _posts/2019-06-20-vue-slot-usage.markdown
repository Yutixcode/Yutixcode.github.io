---
layout: post
title:  "vue slot 用法"
date:   2019-06-20
categories: vue
---

### Vue slot 基础用法

##### 组件注册

在模板 `template` 属性中使用 `slot` 组件，`name` 属性为模板名，无此属性时为默认的`default`，数据绑定方式使用 `v-bind:[propname]="[data]"` 写法

```javascript
Vue.component("SlotComponent", {
  // 使用组件时请求传入数据`datalist`，在通过数据绑定传到slot作用域
  props: ["dataList"],
  // 使用 v-bind:[propname]="[data]" 方式，将数据绑定到 slot 上
  // 使用 name="[slotname]" 指定slot名称
  template: `
    <div>
      <slot></slot>
      <slot v-bind:slot-list="dataList" name="a"></slot>
      <slot v-bind:slot-list="dataList" name="b"></slot>
      <slot v-bind:slot-list="dataList" name="c"></slot>
    </div>
  `
});
```

##### 组件使用

```html
<!-- slotList: ["a", "b", "c"] -->
<slot-component :data-list="slotList">
  <div>this is a default slot</div>
  <!-- 使用v-slot:[slotname]="[namespace]"方式，给指定slot传值，值为对象，支持对象解构 -->

  <!-- 使用[namespace][propname]来取得绑定的数据 -->
  <template v-slot:a="slotProps">
    <p>这是第0个slot:{{slotProps.slotList[0]}}</p>
  </template>

  <!-- 解构方式 -->
  <template v-slot:b="{ slotList }">
    <p>这是第1个slot:{{slotList[1]}}</p>
  </template>

  <template v-slot:c="slotProps">
    <p>这是第2个slot:{{slotProps.slotList[2]}}</p>
  </template>

</slot-component>
```

##### 输出结果

>  this is a default slot
>
>  这是第0个slot:a
>
>  这是第1个slot:b
>
>  这是第2个slot:c


------


### Vue slot for循环用法

模板中 `slot` 组件的 for 循环用法与 slot 名的动态绑定，当需要动态添加 `slot` 组件，且 slot 名不一样时，推荐使用此方式。

##### 组件注册

```javascript
Vue.component("NavSlotComponent", {
  props: ["navList"],
  template: `
    <div>
      <template v-for="item in navList">
        <slot v-bind:name="item">{{item}}</slot>
      </template>
    </div>
  `
});
```

##### 组件使用

```html
<!-- nav: ["home", "about", "contact"] -->
<nav-slot-component :nav-list="nav">
  <!-- **该方式的 slot 中可访问父级作用域** -->
  <!-- 关键步骤：使用 `[value]` 动态参数来指定 slot 名 -->
  <!-- for循环创建多个元素填充到指定slot -->
  <!-- v-slot 指令只能用在template上 -->
  <template v-for="(item,index) in nav" v-slot:[item]>
    <p :key="index">Nav{{index}}:{{item}}</p>
  </template>
</nav-slot-component>
```

##### 输出结果

> Nav0:home
> 
> Nav1:about
> 
> Nav2:contact


------


### Vue slot for循环与复用模板用法

模板使用for循环创建多个包含 `slot` 组件的节点，使用相同的 slot 名，当需要动态添加 `slot` 组件，且 slot 名一致时，推荐使用此方式。

##### 组件注册

```javascript
Vue.component("TodoList", {
  props: ["todos"],
  // 创建多个节点，内容由 slot 提供
  template: `
    <div>
      <p
        v-for="todo in todos"
        v-bind:key="todo.id"
      >
        <slot name="todo" v-bind:todo="todo">
          {{ todo.text }}
        </slot>
      </p>
    </div>
  `
});
```

##### 组件使用

```html
<!-- 
  todos: [
    {
      id: 0,
      isFinished: true,
      text: "上班"
    },
    {
      id: 1,
      isFinished: false,
      text: "搬砖"
    },
    {
      id: 2,
      isFinished: false,
      text: "下班"
    },
    {
      id: 3,
      isFinished: false,
      text: "睡觉"
    }
  ] 
-->
<todo-list :todos="todos">
  <!-- 模板可复用，slot 名都是todo -->
  <!-- 需要绑定数据给 slot 作用域使用 -->
  <template v-slot:todo="{ todo }">
    <span v-if="todo.isFinished">✓</span>
    {{ todo.id }}:{{ todo.text }}
  </template>
</todo-list> 
```

##### 输出结果

>✓ 0:上班
>
>1:搬砖
>
>2:下班
>
>3:睡觉


------


### Vue slot render JSX用法

JSX 中 slot 的混合用法，具备编程能力的方式。

[JSX 说明文档](https://github.com/vuejs/jsx)

[JSX 转换说明](https://github.com/vuejs/babel-plugin-transform-vue-jsx)

JSX 写法不支持 for 、 if 语句。

使用数组的 `map` 方法替代 for 语句，或将 for 语句写在立即执行函数中。

使用 `condition && <CustomComponent/>` 或 `condition ? <FooComponent/> : <BarComponent/>` 代替 if 条件判断，或将 if 语句写在立即执行函数中。

##### 组件注册

```javascript
Vue.component("TextComponent", {
  props: ["user"],
  render() {
    return (
      <div>
        <header>这是{this.$slots.header}</header>

        <slot name="username">用户名：{this.user}</slot>

        <div>{this.$slots.default}</div>

        <footer>这是{this.$slots.footer}</footer>
      </div>
    );
  }
});
```

##### 组件使用

```html
<text-component user="tom">
  <template v-slot:header>header</template>
  <p>小名：jerry</p>
  <template v-slot:footer>footer</template>
</text-component>
```

##### 输出结果

> 这是header
>
> 用户名：tom
>
> 小名：jerry
>
> 这是footer

------



