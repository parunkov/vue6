<template>
    <div class="tag" v-intersect="{
        handler: onIntersect,
        options: {
            threshold: [1.0]
        }
    }">{{ text }}</div>
</template>
<script>
export default {
    props: ['text', 'index'],
    data: () => ({
        isIntersecting: true,
    }),
    methods: {
        onIntersect(entries) {
            this.isIntersecting = entries[0].intersectionRatio >= 1;
            console.log('index - ', this.index, ': ', this.isIntersecting);
        },
    },
}
</script>