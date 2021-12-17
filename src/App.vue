<template>
  <div id="app" class="full-container">
    <div class="row mt-1 ml-5 pl-0" id="tree-type">
        <TreeType />
    </div>
    <div>
        <TreeControl />
    </div>
  </div>
</template>

<script>
import TreeType from './components/TreeTypes/TreeType.vue'
import TreeControl from './components/MainTree/TreeControl.vue'

export default {
  name: 'App',
  components: {
    TreeControl,
    TreeType
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#tree-type {
  margin-left: 10px;
}

@import'~bootstrap/dist/css/bootstrap.css'
</style>
