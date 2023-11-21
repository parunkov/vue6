<template>
    <div>
        <template v-for="(tag, index) in tags">
            <div v-if="index > 0" :key="tag.text">-</div>
            <div :key="tag.text">{{ tag.text }}</div>
        </template>
    </div>
</template>
<script>
export default {
    props: ['tags']
}
</script>