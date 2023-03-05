# vuex crash course

vue create . //to create vue boilerplate in current folder
or
vue create appname

```bash showLineNumbers
npm install vuex
```

**scaffold**

https://vuejs.github.io/vetur/guide/snippet.html#customizable-scaffold-snippets

```jsx showLineNumbers
<vue for file scaffolding snippets
<template for template scaffolding snippets

<style for style scaffolding snippets
<script for script scaffolding snippets


<router-link to="/">Home</router-link> |

<template>
  <router-view />
</template>
```

#### Modules

https://vuex.vuejs.org/guide/modules.html#module-reuse

https://vuex.vuejs.org/guide/modules.html#module-local-state

#### Application Structure

https://vuex.vuejs.org/guide/structure.html

**Sample code repo for application architecture:**

https://github.com/abdulmoizshaikh/vuejs2-vuex-basics/tree/06-vuex-tricks

#### Getters

We only get state vaiables from getters

#### Actions

Actions are asyn here we can do side effects and API calling work and then commit mutations with result in payload

#### Mutations :

Here we change vuex state or application
