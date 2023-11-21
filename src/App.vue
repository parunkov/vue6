<template>
  <v-app>
    <v-main>
      <TagsList :tags="tags" />
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
        {text: '4,3'},
        {text: 'Фридланские ворота'},
        {text: '1,2 км от вас'}
      ]
  }),
};
</script>
