<template>
    <!-- <a href="#/">Home</a> |
  <a href="#/sales">Sales</a> | -->
  <component :is="currentView" />
  <!-- <HomeIndex msg="This is the Index"/>
  <SalesIndex msg="This is the SalesIndex"/> -->
</template>

<script setup>
import { ref, computed } from 'vue'
import HomeIndex from './components/HomeIndex.vue'
import SalesIndex from './components/SalesIndex.vue'

const routes = {
  '/': HomeIndex,
  '/sales': SalesIndex
}

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || HomeIndex
})


// export default {
//   name: 'App',
//   components: {
//     HomeIndex,
//   }
// }
</script>

<style>

</style>
