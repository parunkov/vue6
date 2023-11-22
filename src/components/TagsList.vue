<template>
    <div class="tags-list" :class="{'tags-list_justify_space': isSpace}" :key="elementKey" >
        <template v-for="(tag) in tagsData">
            <div 
                v-if="tag.id > 0" 
                :key="tag.spacerKey" 
                class="tags-list__spacer" 
                :class="{'tags-list__spacer_hidden': tag.hidden, 'tags-list__spacer_invisible': isResize}"
            >
                <v-icon color="black">mdi-circle-small</v-icon>
            </div>
            <div 
                class="tags-list__tag" 
                :class="{'tags-list__tag_hidden': tag.hidden, 'tags-list__tag_invisible': isResize}"
                :key="tag.id"
            >
                <div v-if="tag.icon" class="tags-list__tag-icon">
                    <v-icon color="black">{{ tag.icon }}</v-icon>
                </div>
                <div class="tags-list__tag-text">{{ tag.text }}</div>
            </div>
            
        </template>
    </div>
</template>
<script>
const checkRight = (object) => {
    object.isSpace = false;
    object.tagsData.forEach((item) => {
        item.hidden = false;
    });
    object.elementKey += 1;
    setTimeout(() => {
        object.right = object.$el.getBoundingClientRect().right;
        const tagElements = object.$el.querySelectorAll('.tags-list__tag');
            tagElements.forEach((item, index) => {
            const right = item.getBoundingClientRect().right;
            object.tagsData[index].right = right;
            });
        object.tagsData.forEach((item) => {
            if (item.right > object.right) {
                item.hidden = true;
            } else {
                item.hidden = false;
            }
        });
        if (object.space) object.isSpace = true;
        object.elementKey += 1;
    }, 200);
}
export default {
    props: {
        tags: { type: Array, required: true },
        space: { type: Boolean },
    },
    data: () => ({
        tagsData: [],
        isSpace: false,
        isResize: false,
        right: 0,
        elementKey: 0,
    }),
    created() {
        this.tagsData = this.tags.map((item, index) => ({
            id: index, 
            spacerKey: `spacer${index}`, 
            text: item.text,
            icon: item.icon,
        }));
    },
    mounted() {
        checkRight(this);
        let isResize;
        window.addEventListener('resize', () => {
            this.isResize = true;
            clearTimeout(isResize)
            isResize = setTimeout(() => {
                setTimeout(() => {
                    this.isResize = false;
                }, 200);
                checkRight(this);
            }, 300);
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
        display: flex;
        &_hidden {
            display: none;
        }
        &_invisible {
            visibility: hidden;
        }
    }
    &__tag-icon {
        margin-right: 5px;
    }
}
</style>