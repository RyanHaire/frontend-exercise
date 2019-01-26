<template>
  <div id="app">
    <StudentListView />
  </div>
</template>

<script>
import StudentListView from './components/StudentListView.vue'
export default {
  name: 'app',
  components: {
    StudentListView
  }
}
</script>

<style>
#app {
  height: 100vh;
}
</style>
