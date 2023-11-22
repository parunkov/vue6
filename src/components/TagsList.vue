<template>
    <div class="tags-list" :class="{'tags-list_justify_space': isSpace}" :key="elementKey" >
        <template v-for="(tag) in tagsData">
            <div 
                v-if="tag.id > 0" 
                :key="tag.spacerKey" 
                class="tags-list__spacer" 
                :class="{'tags-list__spacer_hidden': tag.hidden}"
            >
                <v-icon>mdi-circle-small</v-icon>
            </div>
            <TagsItem 
                :text="tag.text" 
                :icon="tag.icon"
                :index="tag.id" 
                :key="tag.id" 
                class="tags-list__tag" 
                :class="{'tags-list__tag_hidden': tag.hidden}"
                @mounted="onMounted"
            />
            
        </template>
    </div>
</template>
<script>
import TagsItem from './TagsItem.vue';
const checkRight = (object) => {
    object.right = object.$el.getBoundingClientRect().right;
    object.tagsData.forEach((item) => {
        console.log(item.right, ' - ', object.right);
        if (item.right > object.right) item.hidden = true;
    });
    object.elementKey += 1;
    // console.log(object.elementKey);
}
export default {
    props: {
        tags: { type: Array, required: true },
        space: { type: Boolean },
    },
    data: () => ({
        tagsData: [],
        isSpace: false,
        right: 0,
        elementKey: 0,
    }),
    components: { TagsItem },
    methods: {
        onMounted(payload) {
            console.log('mounted');
            this.tagsData[payload.index].right = payload.right;
            if (payload.index === this.tagsData.length - 1 && this.space) {
                this.isSpace = true;
            }
        }
    },
    created() {
        this.tagsData = this.tags.map((item, index) => ({
            id: index, 
            spacerKey: `spacer${index}`, 
            text: item.text,
            icon: item.icon,
        }));
    },
    mounted() {
        // this.right = this.$el.getBoundingClientRect().right;
        checkRight(this);
        window.addEventListener('resize', () => {
            // this.right = this.$el.getBoundingClientRect().right;
            checkRight(this);
        })
    },
}
</script>
<style lang="scss" scoped>
.tags-list {
    display: flex;
    flex-wrap: nowrap;
    white-space: nowrap;
    &_justify_space {
        justify-content: space-between;
    }
    &__spacer,
    &__tag {
        &_hidden {
            display: none;
        }
    }
}
</style>