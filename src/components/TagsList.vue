<template>
    <div class="tags-item">
        <template v-for="(tag, index) in tags">
            <div v-if="index > 0" :key="index">
                <v-icon>mdi-circle-small</v-icon>
            </div>
            <TagsItem :text="tag.text" :index="index" :key="tag.text" />
        </template>
    </div>
</template>
<script>
import TagsItem from './TagsItem.vue';

export default {
    props: ['tags'],
    comments: {
        TagsItem
    },
    components: { TagsItem }
}
</script>
<style lang="scss" scoped>
.tags-item {
    display: flex;
    flex-wrap: nowrap;
    white-space: nowrap;
}
</style>