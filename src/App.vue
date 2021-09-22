<template>
<div id="app">
  <div class="container">
    <h1>People Maker</h1>
    <h6>Powered by: Vue 3 | Vuex 4 | Ruby on Rails 6 | SQL</h6>
  </div>
  <Todos/>

  <Users/>

</div>
  
</template>

<script>
import Todos from '@/components/Todos.vue'
import Users from '@/components/Users.vue'

export default {
  name: "App",
  components: {
    Todos,
    Users
  },
};
</script>

<style>
#app {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  line-height: 1.6;
  /* background: lightcoral; */
}
.container {
  max-width: 1100px;
  margin: auto;
  overflow: auto;
  padding: 0 2rem;
}
h6, h1 {
  margin: 0;
}
</style>
