<template>
    <p>total todos: {{ tasks.length }}</p>
</template>

<script>


export default {
    props: {
        tasks: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>
    p {
        font-style: italic;
        color: rgb(173, 174, 176);
        margin-top: 0.5em;
    }
</style>