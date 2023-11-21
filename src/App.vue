<template>
  <div id="app">
    <TagsList :tags="tags" />
  </div>
</template>

<script>
import TagsList from './components/TagsList.vue';

export default {
  name: 'App',
  data() {
    return {
      tags: [
        {text: '4,3'},
        {text: 'Фридланские ворота'},
        {text: '1,2 км от вас'}
      ]
    }
  },
  components: {
    TagsList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
