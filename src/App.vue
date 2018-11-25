<template>
  <div id="app">
    <ItemList>
    </ItemList>
  </div>
</template>

<script>
import ItemList from './components/ItemList.vue'

export default {
  name: 'app',
  components: {
    ItemList
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Dosis');

body {
  font-family: 'Dosis', sans-serif;
}


</style>
