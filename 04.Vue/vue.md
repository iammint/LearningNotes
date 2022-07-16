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

## 1.2 Refenrence by ESModule
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
import { createApp} from 'vue'
import App from './App.vue'
const app = createApp(App)
```

### Mounting the application
> An application instance is a Vue instance that expects a "container" argument.

```HTML
//In html,
<div id="app"></div>
```

```js
//In js,
app.mount('#app')
```

### In-DOM Root Component Template
When using Vue without a build step, we can write our root component's template directly inside the mount container.

```html
//In html,
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

## 2.2 Template syntax
