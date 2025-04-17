# Vue.js Overview

Vue.js is a progressive JavaScript framework for building user interfaces. It is designed from the ground up to be incrementally adoptable and can power advanced single-page applications when used in combination with modern tooling.

## 🌟 Key Features

- **Reactive data binding**: Automatically updates the DOM when data changes.
    
- **Component-based**: Build UIs from reusable, encapsulated components.
    
- **Declarative rendering**: Simplifies how the DOM is rendered.
    
- **Transitions and animations**: Built-in support for rich user interactions.
    
- **Dev tools**: Excellent developer tools for debugging and profiling.
    

## 🚀 Getting Started

### Installation with Vite (recommended)

```bash
npm create vite@latest my-vue-app -- --template vue
cd my-vue-app
npm install
npm run dev
```

### Hello World Example

```vue
<template>
  <h1>{{ message }}</h1>
</template>

<script>
export default {
  data() {
    return {
      message: 'Hello, Vue!'
    };
  }
};
</script>
```

## 🔁 Reactivity and Binding

```vue
<template>
  <input v-model="name" />
  <p>Hello, {{ name }}!</p>
</template>

<script>
export default {
  data() {
    return {
      name: ''
    };
  }
};
</script>
```

## 🧩 Components

```vue
<!-- HelloWorld.vue -->
<template>
  <p>Hello from {{ name }}!</p>
</template>

<script>
export default {
  props: ['name']
};
</script>
```

```vue
<!-- App.vue -->
<template>
  <HelloWorld name="Vue" />
</template>

<script>
import HelloWorld from './HelloWorld.vue';

export default {
  components: { HelloWorld }
};
</script>
```

## 🛠 State Management (Pinia)

```bash
npm install pinia
```

```javascript
// store.js
import { defineStore } from 'pinia';

export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0 }),
  actions: {
    increment() {
      this.count++;
    }
  }
});
```

```vue
<script setup>
import { useCounterStore } from './store';
const counter = useCounterStore();
</script>

<template>
  <button @click="counter.increment">Clicked {{ counter.count }} times</button>
</template>
```

## ✅ Use Cases

- Single Page Applications (SPA)
    
- Progressive Web Apps (PWA)
    
- Admin dashboards
    
- Interactive form-based systems
    

## 🔗 Related Tools

- **Vite**: Fast development build tool.
    
- **Pinia**: Modern store for Vue.
    
- **Vue Router**: Official routing library for Vue.
    
- **Vuetify / Tailwind CSS**: UI libraries and design systems.
    

---
tags: #vue #javascript #frontend #spa #web-development