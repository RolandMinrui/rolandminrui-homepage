<script setup>
import Header from './components/Header.vue'
import Sidebar from './components/Sidebar.vue'
import { ref, watch } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const transitionName = ref('page')

// Watch for route changes to determine transition direction
watch(() => route.path, (toPath, fromPath) => {
  const routes = ['/', '/publication', '/cv', '/project']
  const fromIndex = routes.indexOf(fromPath)
  const toIndex = routes.indexOf(toPath)
  
  if (fromIndex === -1 || toIndex === -1) {
    transitionName.value = 'page'
  } else if (toIndex > fromIndex) {
    transitionName.value = 'slide-right'
  } else if (toIndex < fromIndex) {
    transitionName.value = 'slide-left'
  } else {
    transitionName.value = 'page'
  }
})
</script>

<template>
  <Header />
  <div class="content-container">
    <Sidebar />
    <router-view v-slot="{ Component }">
      <transition :name="transitionName" mode="out-in">
        <component :is="Component" :key="route.path" />
      </transition>
    </router-view>
  </div>
</template>

<style>
/* Global styles */
.content-container {
  display: flex;
  margin-top: 8vh;
  min-height: 92vh;
  width: 100%;
  box-sizing: border-box;
}

/* Responsive design */
@media (max-width: 1023px) {
  .content-container {
    flex-direction: column;
    margin-top: 7vh;
    min-height: 93vh;
  }
}

@media (max-width: 768px) {
  .content-container {
    margin-top: 6vh;
    min-height: 94vh;
  }
}

@media (max-width: 480px) {
  .content-container {
    margin-top: 6vh;
    min-height: 94vh;
  }
}

/* Ensure proper scrolling and layout */
html, body {
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}

#app {
  width: 100%;
  overflow-x: hidden;
}
</style>