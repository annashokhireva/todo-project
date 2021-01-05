<template>
    <li class="todo-input" :class="{'completed': this.task.done}">
        <input 
            type="checkbox"
            :id="task.id" 
            class="checkbox" 
            v-model="task.done"
        >
        <label :for="task.id"></label>
        <input 
            class="task-input"  
            :placeholder="pickRandomTask"
            type="text" 
            v-model="task.text"
            ref="text" 
            @keydown.enter="$emit('enter')"
        >
        <span class="delete" v-on="$listeners">x</span>
    </li>
</template>

<script>

export default {

    props: {
        task: {
            type: Object,
            required: true
        }
    },

    data() {
        return{
            randomTasks: [
                'Come up with a new task',
                'Start coding',
                'Practice JS',
                'Cleane up your desk',
                'Do your homework'
            ]
        }
    },

    computed: {
        pickRandomTask() {
            let randomTask =  this.randomTasks[ Math.floor (Math.random() * this.randomTasks.length)];
            return randomTask
        }
    },

    mounted() {
        this.$refs.text.focus();
    }

}
</script>

<style>
    .todo-input {
        width: fit-content;
        width: 500px;
        padding: 0;
        margin: 0.3em 0;
        background-color: rgb(238, 238, 238);
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
    }

    .checkbox{
        position: absolute; 
        opacity: 0;
        display: none;
    }

    .checkbox + label {
        position: absolute;
        cursor: pointer;
        left: 0.7em;
        top: 50%;
        transform: translateY(-50%);
        width: 1.3em;
        height: 1.3em;
        border-radius: 50%;
        border: none;
        background-color: rgb(194, 194, 196);
    }

    .checkbox:checked + label:after{
        content: '';
        width: 1.3em;
        height: 1.3em;
        border-radius: 50%;
        border: none;
        background-color: rgb(96, 186, 96);
    }

    .checkbox:checked + label:after{
        display: block;
    }

    .task-input {
        height: 3em;
        box-sizing: border-box;
        padding: 1em 0;
        outline: none;
        border: none;
        background-color: transparent;
        color: rgb(173, 174, 176);
        font-weight: 600;
        font-size: 14px;
        width: 460px;
        margin-left: 3em;
    }

    ::placeholder {
        color: rgb(173, 174, 176);
        font-style: italic;
    }

    .completed {
        background-color: rgb(198, 238, 198);
        
    }

    .completed input {
        color: rgb(96, 186, 96);
        text-decoration: line-through;
    }

    .delete {
        cursor: pointer;
        position: absolute;
        top: 50%;
        right: 1.5em;
        transform: translateY(-50%);
        /* opacity: 0; */
        width: 0;
        color: rgb(220, 68, 57);
        transition: all ease-in 0.25s;
    }

    
</style>