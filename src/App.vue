<template>
  <v-app>
    <v-main>
      <div class="main">
        <div class="main__item">
          <TagsList :tags="tags" />
        </div>
        <div class="main__item">
          <TagsList :tags="tags" space />
        </div>
        <div class="main__items">
          <div class="main__item main__item_type_flex main__item_order_first">
            <TagsList :tags="tags" />
          </div>
          <div class="main__item main__item_type_flex">
            <TagsList :tags="tags" space />
          </div>
        </div>
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
      { text: '4,3', icon: 'mdi-star-outline' },
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
  font-size: 24px;
  line-height: 36px;
  &__items {
    display: flex;
    width: 100%;
    justify-content: space-between;
  }
  &__item {
    width: 100%;
    border: 1px solid lightgray;
    padding: 5px 10px;
    margin-bottom: 10px;
    &_type_flex {
      width: calc(50% - 5px);
    }
    &_order_first {
      margin-right: 10px;
    }
  }
}
</style>
