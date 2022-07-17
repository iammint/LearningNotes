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
import { createApp} from 'vue'
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
    console.log(newObject === this.someObject)
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

