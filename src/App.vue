<template>
  <v-app>
    <v-main>
      <div class="main">
        <TagsList :tags="tags" />
      </div>
    </v-main>
  </v-app>
</template>

<script>
import TagsList from './components/TagsList.vue';

export default {
  name: 'App',

  components: {
    TagsList
  },

  data: () => ({
    tags: [
      { text: '4,3' },
      { text: 'Фридланские ворота' },
      { text: '1,2 км от вас' }
    ]
  }),
};
</script>
<style lang="scss" scoped>
.main {
  padding: 20px;
  overflow-x: hidden;
  font-size: 40px;
}
</style>
