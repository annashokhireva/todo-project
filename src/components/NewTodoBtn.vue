<template>
    <div>
        <button class="newTodo" v-on="$listeners">
            New todo...
        </button>
    </div>
</template>

<script>

export default {
    
}
</script>

<style>
    .newTodo {
        background-color: rgb(173, 174, 176);
        width: 500px;
        height: 3em;
        text-align: center;
        border: none;
        padding: 0;
        font-weight: 600;
        color: #ffffff;
        font-size: 16px;
    }
</style>