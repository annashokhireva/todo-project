<template>
  <div id="app">
    <list-header ListName="My ToDo List"/>
    <new-todo-btn @click="addElement"/>
    
    <div class="tasks">
      <ul>
        <todo-task 
          v-for="task in sortedTasks" :key="task.id" 
          :task="task" 
          @enter="addElement"
          @click="deleteTask(task)"
        />
      </ul>
    </div>

    <div class="total-counter">
      <total-todos :tasks="tasks" />
    </div>
  </div>
</template>

<script>
import ListHeader from './components/ListHeader.vue';
import NewTodoBtn from './components/NewTodoBtn.vue';
import TodoTask from './components/TodoTask.vue';
import TotalTodos from './components/TotalTodos.vue';
let taskIndex = 0;

export default {

  components: {
    ListHeader,
    TotalTodos,
    NewTodoBtn,
    TodoTask
  },

  data() {
    return {
      tasks: [
        { text: '',
          done: false,
          id: ++taskIndex}
      ]
    }
  },

  computed: {
    sortedTasks() {
      const sortedTasks = this.tasks.slice();

      sortedTasks.sort((a, b) => {
        if(a.done === b.done) return 0;

        return (a.done ? 1 : -1);
      });

      return sortedTasks;
    }
  },

  watch: {
    tasks: {
      handler: function() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      },
    
    deep: true
    }
  },

  methods: {
    addElement() {
      this.tasks.unshift({
        text: '',
        done: false,
        id: ++taskIndex
      })
      return true;
    },

    getTasks() {
      if (localStorage.getItem('tasks')) {
        this.tasks = JSON.parse(localStorage.getItem('tasks'));
      }
    },

    deleteTask(task){
      this.tasks.splice(this.tasks.indexOf(task), 1);
    }
  },

  mounted() {
    this.getTasks();
  }
    
}
</script>

<style>

  @import url('../node_modules/roboto-fontface/css/roboto/roboto-fontface.css');

  #app {
    font-family: 'Roboto';
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .new-task {
          width: 25em;
          height: 3em;
          margin: 0.5em;;
          background-color: rgb(244, 244, 244);
      }

  .radio-btn input {
      opacity: 0;
      width: 0;
      height: 0;
  }

  .radio-btn {
      margin: 0;
      width: 3em;
      height: 1.5em;
      color: gray;
  }

  input {
      height: 3em;
      width: 27em;
      box-sizing: border-box;
      padding: 1em 0;
      outline: none;
      border: none;
      background-color: transparent;
  }

  ul {
    padding: 0;
    margin: 0;
    width: 500px;
  }

  .checked {
    background-color: red;
  }

  .total-counter {
    display: flex;
    justify-content: flex-start; 
    align-items: flex-start;
    width: 500px;;  
  }
</style>
