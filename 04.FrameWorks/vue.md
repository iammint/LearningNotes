# Single-File Components
> A Vue SFC encapsulates the component's logic (JavaScript), template (HTML), and styles (CSS) in a single file. 

# API Styles
> Vue components can be authored in two different API styles: **Options API** and **Composition API**.


> The Options API is the recommended way to define a Vue component. Properties defined by options are exposed on `this` inside functions, which points to the component instance.


> The Composition API is a more flexible way to define a Vue component. Properties defined by composition are not exposed on `this` inside functions, but instead are passed as arguments to the component's constructor.

# 1. Basics
## 1.1 Under the hood
> Reference to the vue codebase

```HTML
<script src="https://unpkg.com/vue@3"></script>

<div id="app">{{ message }}</div>

<script>
    //Desturcturing assignment
  const { createApp } = Vue

  createApp({
    data() {
      return {
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```

## 1.2 Reference by ESModule
> While the global build works, we will be primarily using ES Modules syntax for consistency.

**We can import directly from `vue` for the `<script type="importmap">` block. We can add entries for other dependencies to the import map - just make sure they point to the ES modules version of the library you intend to use.** 

```HTML
<script type="importmap">
  {
    "imports": {
      "vue": "https://unpkg.com/vue@3/dist/vue.esm-browser.js"
    }
  }
</script>

<div id="app">{{ message }}</div>

<script type="module">
    //Using ESModules here
  import { createApp } from 'vue'

  createApp({
    data() {
      return {
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```

# 2. Essentials
## 2.1 Creating a Vue Application
### The application instance
> Create a Vue application by creating a Vue instance. Every Vue application starts by creating a new application instance with the `createApp` function:

```HTML
import { createApp } from 'vue'
const app = createApp({
    <!-- root component options -->
})
```

### The Root Component
> The object we are passing into `createApp` is a component. Every app requies a "root component" that can contain other components as its children.

If you are using SFC, we typically `import` the root component from another SFC file.

```HTML
import { createApp } from 'vue'
import App from './App.vue'
const app = createApp(App)
```

### Mounting the application
> An application instance is a Vue instance that expects a "container" argument.

```HTML
<!-- In html, -->
<div id="app"></div>
```

```js
//In js,
app.mount('#app')
```

### In-DOM Root Component Template
When using Vue without a build step, we can write our root component's template directly inside the mount container.

```html
<!-- In html, -->
<div id="app">
    <button @click="counter++">{{ count }}</button>
</div>
```

```js
//In js,
const app = createApp({
    data() {
        return {
            count: 0
        }
    }
})
app.mount("#app")
```

### App Configurations
> The application instance exposes a `.config` object that allows us to configure a few app-level options. 

Make sure to apply all app configurations before mounting the app.

## 2.2 Template syntax
### 1. Text Interpolation
> The most basic form of data binding is text interpolation using the `Mustache` syntax.

```html
<span> Message: {{ message }} </span>
```

### 2. Raw HTML
> The double mustaches interprets the data as plain text. And in order to output real HTML, you will need to use the `v-html` directive.

```html
<!-- In html, -->
  <div id="app" class="demo">
    <p>Using mustaches: {{ rawHtml }}</p>
    <p>Using v-html directive: <span v-html="rawHtml"></span></p>
  </div>
```

```js
//In js,
    const component = {
      data() {
        return {
          rawHtml: '<span style="color: pink">This should be pink<span>'
        }
      }
    }
    createApp(component).mount("#app")
```

### 3. Attribute Binding
> Mustaches cannot be used inside HTML attributes. Instead, use a `v-bind` directive:
```html
<!-- In html -->
<div v-bind:id="dynamicId"></div>
<!-- shorthand -->
<div :id="dynamicId"></div>
```

### 4. Dynamically Binding Multiple Attributes
```js
//In js,
    const component = {
      data() {
        return {
          objectOfAttrs: {
            id: 'container',
            class: 'wrapper'
          }
        }
      }
    }
    createApp(component).mount("#app")
```

```html
<!-- In html -->
<div id="app" v-bind="objectOfAttrs"></div>
```

### 5. Using JavaScript Expressions
> So far we've only been binding to simple property keys in our templates. But Vue actually supports the full power of JavaScript expressions inside all data bindings:

```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div :id="`list-${id}`"></div>
```

### 6. Expressions only
> Each binding can only contain `one single expression`. An expression is a piece of code that can evaluate to a value. A simple check is whether it can be used after `return`.

❌No statement, No If
```html
❌The following will NOT work
{{ var a = 1}}
{{ if (ok) {return message}}}
```

### 7. Calling functions
> It's possible to call a component-exposed method inside a binding expression. 

```html
<span :title="toTitleDate(date)">
  {{ formatDate(date) }}
</span>
```

### 8. Dynamic arguments
> It's possible to pass dynamic arguments to a component-exposed method inside a binding expression. 

```html
<a v-bind: [attributeName] = "url"> ... </a>
```


![Snipaste_2022-07-17_20-32-23.png](https://media.haochen.me/Snipaste_2022-07-17_20-32-23.png)

## 2.3 Reactivity Fundamentals
### Reactive Proxy vs. Original
> Data is made reactive by leveraging JavaScript Proxies.

```js
export default {
  data() {
    return {
      someObject: {}
    }
  },
  mounted() {
    const newObject = {}
    this.someObject = newObject
    console.log(newObject === this.someObject) //false
  }
}
```
When you access `this.someObject` after assigning it, the value is a reactive proxy of the original `newObject`.

### DOM Update Timing
> To wait for the DOM update to complete after a state change, you can use the `nextTick` global API:

```js
import { nextTick } from 'vue'

export default {
  methods: {
    increment() {
      this.count++
      nextTick(() => {
        // access updated DOM
      })
    }
  }
}
```

### Stateful methods
In some cases, we may need to dynamically create a method function, for example creating a debounced event handler.

However, this approach is problematic for components that are reused because a debounced function is **stateful**: it maintains some internal state on the elapsed time. If multiple component instances share the same debounced function, they will interfere with one another.

> To keep each component instance's debounced function independent of the others, we can create the debounced version in the `created` lifecycle hook:

```js
export default {
  created() {
    // each instance now has its own copy of debounced handler
    this.debouncedClick = _.debounce(this.click, 500)
  },
  unmounted() {
    // also a good idea to cancel the timer
    // when the component is removed
    this.debouncedClick.cancel()
  },
  methods: {
    click() {
      // ... respond to click ...
    }
  }
}
```

## 2.4 Computed Properties
> Computed properties are functions that are computed based on the state of other properties.

```js
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  },
  computed: {
    // a computed getter
    publishedBooksMessage() {
      // `this` points to the component instance
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  }
}
```

```html
<!-- In HTML -->
<p>Has published books: </p>
<span>{{ publishedBooksMessage }}</span>
```

### 1. Computed Caching VS. Methods
> Instead of a computed property, we can define the same function as a method. However, the difference is that **computed properties are cached based on their reactive dependencies.** 

This means as long as `author.books` has not changed, multiple access to `publishedBooksMessage` will immediately return the previously computed value.


### 2. Writable Computed
> Computed properties are by default getter-only. You can create one that is writable by providing both a `getter` and a `setter`.

```js
export default {
  data() {
    return {
      firstName: 'John',
      lastName: 'Doe'
    }
  },
  computed: {
    fullName: {
      // getter
      get() {
        return this.firstName + ' ' + this.lastName
      },
      // setter
      set(newValue) {
        // Note: we are using destructuring assignment syntax here.
        [this.firstName, this.lastName] = newValue.split(' ')
      }
    }
  }
}
```

```html
<button @click="this.fullName='Min Tu'"></button>
<div>
  firstName: {{ firstName }}
  lastName: {{ lastName }}
</div>
```

### 3. 侦听器
> 虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器。这就是为什么 Vue 通过 `watch `选项提供了一个更通用的方法来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

```html
<div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
</div>
```

```html
<!-- 因为 AJAX 库和通用工具的生态已经相当丰富，Vue 核心代码没有重复
提供这些功能以保持精简。这也可以让你自由选择自己更熟悉的工具。  -->
<script src="https://cdn.jsdelivr.net/npm/axios@0.12.0/dist/axios.min.js"></script>
<script>
  const watchExampleVM = Vue.createApp({
    data() {
      return {
        question: '',
        answer: 'Questions usually contain a question mark. ;-)'
      }
    },
    watch: {
      // 每当 question 发生变化时，该函数将会执行
      question(newQuestion, oldQuestion) {
        if (newQuestion.indexOf('?') > -1) {
          this.getAnswer()
        }
      }
    },
    methods: {
      getAnswer() {
        this.answer = 'Thinking...'
        axios
          .get('https://yesno.wtf/api')
          .then(response => {
            this.answer = response.data.answer
          })
          .catch(error => {
            this.answer = 'Error! Could not reach the API. ' + error
          })
      }
    }
  }).mount('#watch-example')
</script>
```


## 2.5 Class and Style Bindings
> We can use `v-bind` to assign a class or style to an element. However, vue provides a more convenient syntax for this: `class` and `style`. In addition to strings, the expressions can also evaluate to objects or arrays.

### 1. Binding HTML Classes
#### 1.1 Binding to objects
We can pass an object to `:class`(`v-bind:class`) to dynamically toggle classes:
```html
<div :class="{ active: isActive }"></div>
```
Because the truthiness of a data property means the presence, the above syntax means the presence of `active` class will be determined by the truthiness of the data property `isActive`.

 ```html
 <div
  class="static"
  :class="{ active: isActive, 'text-danger': hasError }"
></div>
```

```js
data() {
  return {
    isActive: true,
    hasError: false
  }
}
```

It will render:
```HTML
<div class="static active"></div>
```

We can also bind a computed property that returns an object:
```js
data() {
  return {
    isActive: true,
    error: null
  }
},
computed: {
  classObject() {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}
```

```html
<div :class="classObject"></div>
```

#### 2. Binding to Arrays
> We can bind `:class` to an array to apply a list of classes.

```js
data() {
  return {
    activeClass: 'active',
    errorClass: 'text-danger'
  }
}
```

```html
<div :class="[isActive ? activeClass : '', errorClass]"></div>
```

However, this can be a bit verbose if you have multiple conditional classes. That's why it's also possible to use the object syntax inside array syntax:

```html
<div :class="[{ active: isActive }, errorClass]"></div>
```

#### 3. With Components
> When you use the `class` attribute on a component with a single root element, those classes will be added to the component's root element, and merged with any existing class already on it.

<!-- child component template -->
```html
<p class="foo bar"><span></span></p>
```

```html
  <BlogPostVue class="baz boo"/>
```

Now rendered HTML will be 
```html
<p class="foo bar baz boo"><span class="baz boo"></span></p>
```

You can also use `$attrs` to define which element will receive this class:
```html
< p :class="$attrs.class">Hi~</p>
<span>This is a child component</span>
```


### 2. Binding Inline Styles
#### 1. Binding to Objects/Arrays
```js
data() {
  return {
    activeColor: 'yellow',
    fontSize: '30px'
  }
}
```
:style supports both camelCase and kebab-cased.
```html
<div :style="{ color: activeColor, fontSize: fontSize}"</div>
<div :style="{ color: activeColor, font-size: fontSize}"</div>
```

It's often a good idea to bind to a style object directly.

```js
data() {
  return {
    styleObject: {
      color: 'red',
      fontSize: '30px'
    },
    styleArr: [ color: 'red', fontSize: '30px' ]
  }
}
```

```html
<div :style="styleObject"></div>
<div :style="styleArr"></div>
```


#### 2. Auto-prefixing
When you use a CSS property that requires a vendor prefix in `:style`, Vue will automatically add the appropriate prefix. For example, if you use `:style="{ transition: 'all' }`, Vue will add `-webkit-transition: all`.

#### 3. Multiple Values
You can provide an array of multiple (prefixed) values to a style property:
```html
<div :style="{ display: ["['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
//注意style={[]}
```

This will only render the last value in the array which the browser supports. In this example, it will render `display: flex` for browsers that support the unprefixed version of flexbox.

## 2.6 Conditional Rendering
### 1. `v-if`
> The directive `v-if` is used to coonditionally render a block. The block will only be rendered if the directive's expression returns a truthy value.

```html
<h1 v-if="awesome">Vue is awesome!</h1>
```

### 2. `v-else`
> You can use the `v-else` directive to indicate an "else block" for `v-if`:

```html
<button @click="awesome = !awesome">Toggle</button>

<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

A `v-else` element must immediately follow a `v-if `or a `v-else-if` element - otherwise it will not be recognized.

### 3. `v-else-if`
```html
  <div v-if="count === 221">I'm v-if</div>
  <div v-else-if="count === 222">I'm v-else-if</div>
  <div v-else>I'm v-else</div>
```

### 4. `v-if`/`v-else`/`v-else-if` on `<template>`
```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

### 5. `v-show`
> Another option for conditionally displaying an element is the `v-show` directive.

The difference is that `v-show` only toggles the ` display` CSS property of the element.

### 6. `v-if` vs.`v-show`

`v-if` 是“真正”的条件渲染，因为它会确保在切换过程中，条件块内的事件监听器和子组件适当地被销毁和重建。

`v-if` 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

相比之下，`v-show` 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

一般来说，`v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。

## 2.7 List Rendering
### 1. `v-for`
We can use the `v-for` directive to render a list of items based on an array. 

Inside the `v-for` scope, template expressions have access to all parent scope properties. In addition, `v-for` also supports an optional second alias for the index of the current item.

Actually we can use destructuring on the `v-for` item alias.

### 2. `v-for` with an Object
> You can also use `v-for` to iterate through the properties of an object. The iteration order will be based on the result of calling `Object.keys()` on the object

### 3. `v-for` with a Range
```html
<span v-for="n in 10"> {{ n }} </span>
```

### 4. `v-for` with `v-if`
**❌Not recommended**
When they exist on the same node, `v-if` has a higher priority than `v-for`. **That means the `v-if` condition will not have access to variables from the scope of `v-for`.**

```html
<!-- This will throw an error because property "todo" is not defined on instance. -->
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo.name }}
</li>
```

But this can be fixed by moving `v-for` outside.
```html
  <ul v-for="todo in todos">
  <!-- Using `v-show` is better, cuz `v-if` still shows empty list -->
  <li v-show="!todo.done">
  {{ todo.text }}
```

### 5. Mainting State with `key`
Using `key` to maintain state when the order of the data items has changed. Vue will patch each element in-place and make sure it reflects what should be rendered at that particular index.

```html
  <ul v-for="todo in todos" :key="todo.text">
  <li v-show="!todo.done">
  {{ todo.text }}
  </li>
  </ul>
```
The `key` binding expects primitive values(strings and numbers). Do not use objects as `v-for` keys.

**It's recommended to provide a `key` attribute with `v-for` whenever possible.**

### 6. `v-for` with a component
You can directly use v-for on a component, like any normal element (don't forget to provide a key).

However, this won't automatically pass any data to the component, because components have isolated scopes of their own. In order to pass the iterated data into the component, we should also use props:

```html
<MyComponent
  v-for="(item, index) in items"
  :item="item"
  :index="index"
  :key="item.id"
/>
```
不自动将 `item` 注入到组件里的原因是，这会使得组件与 `v-for` 的运作紧密耦合。明确组件数据的来源能够使组件在其他场合重复使用。


### 7. Array Change Detection
```js
data() {
  return {
    numbers: [1, 2, 3, 4, 5]
  }
},
computed: {
  evenNumbers() {
    return this.numbers.filter(n => n % 2 === 0)
  }
}
```

```html
<li v-for="n in evenNumbers">{{ n }}</li>
```

In situations where computed properties are not feasible (e.g. when the data is being fetched from a server, or inside nested `v-for` loops), you can use a method.

Be careful with `reverse()` and `sort()` in a computed property! These two methods will mutate the original array, which should be avioded in computed getters. 

```js
- return numbers.reverse()
+ return [...numbers].reverse()
```


## 2.8 Form Input Bindings
### 1. Tetx
插值在form中不起作用，需要使用`v-model`
```html
<input v-model="message" placeholder='edit me' />
<p>Message is {{ message }}</p>
```

```html
<textarea v-model="message1" placeholder='edit me' />
<p style="white-space: pre-line">{{ message1 }}</p>
```

```js
data() {
  return {
    message: '',
    message1: ''
  }
}
```

### 2. checkbox && radio
