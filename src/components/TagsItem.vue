<template>
    <div class="tag">
        <div v-if="icon" class="tag__icon">
            <v-icon>{{ icon }}</v-icon>
        </div>
        <div class="tag__text">{{ text }}</div>
    </div>
</template>
<script>
export default {
    props: ['text', 'icon', 'index'],
    data: () => ({
        rootElement: null,
    }),
    methods: {
    },
    mounted() {
        const right = this.$el.getBoundingClientRect().right;
        this.$emit('mounted', {index: this.index, right});
    },
}
</script>
<style lang="scss" scoped>
.tag {
    display: flex;
    align-items: start;
    &__icon {
        margin-right: 5px;
    }
}
</style>