<template>
  <div class="todolist">
    <h1 class="mb-3">To Do List</h1>
    <form v-on:submit.prevent="addNewTodoTask">
        <div class="input-group mb-3 task-input">
            <input v-model="newTodoTaskText" class="form-control" type="text" placeholder="Add new task here" aria-describedby="validationServer05Feedback" required>
            <button class="btn btn-outline-info add-btn" type="submit" id="button-addon2">Add Task</button>
            <div id="validationServer05Feedback" class="invalid-feedback">
              Please provide a valid zip.
            </div>
        </div>
    </form>
    <div class="d-grid gap-4 d-md-flex mb-3 justify-content-evenly">
        <button type="button" class="btn btn-warning btn-lg" @click="removeFinishedTasks">Remove finished tasks</button>
        <button type="button" class="btn btn-danger btn-lg" @click="removeAllTasks">Clear all tasks</button>
    </div>
    <h3 class="mb-3">Tasks</h3>
    <div id="list" class="flex m-10">
        <ul id="todoListItems">
          <draggable class="dragArea list-group w-full" :list="todos">
            <transition-group>
              <ToDoListTasks class="list-group-item" v-for="(todo, index) in todos" :key="todo.title" :title="todo.title" @remove="todos.splice(index, 1)" :class="{'isCompleted':todo.completed}" @complete="completeTask(todo)" draggable></ToDoListTasks>
            </transition-group>
          </draggable>
        </ul>
    </div>
  </div>
  <!-- <HelloWorld msg="Welcome to Vue"/> -->
</template>

<script>
import ToDoListTasks from './components/ToDoListTasks.vue'
import { VueDraggableNext } from 'vue-draggable-next'
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    ToDoListTasks,
    draggable: VueDraggableNext
  },

  data() {
    return {
      newTodoTaskText: '',
      enabled: true,
      todos: [
        {
          id: 1,
          title: 'Hello There',
          completed: true
        },

        {
          id: 2,
          title: 'Take out the trash',
          completed: false
        },

        {
          id: 3,
          title: 'Take out the dishes',
          completed: false
        },
      ],
      dragging: false,
      nextTodoId: 4,
    }
  },

  methods: {
    addNewTodoTask() {
      this.todos.push({
        id: this.nextTodoId++,
        title: this.newTodoTaskText
      })
      this.newTodoTaskText = ''
    },

    removeAllTasks() {
      this.todos = [];
    },

    removeFinishedTasks() {
      this.todos = this.todos.filter(todo => !todo.completed)
    },

    completeTask(todo) {
      todo.completed = !todo.completed;
    }
  }
}
</script>

<style>
    body {
      background-color: darkslateblue;
    }

    #app {
      font-family: Avenir, Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      text-align: center;
      color: #92a8be;
      margin-top: 60px;
    }

    h1 {
            font-weight: bold;
    }

    .task-input {
        width: 50% !important;
        /* padding: 10px; */
        margin: auto;
    }

    .form-control, .add-btn {
        box-shadow: none;
    }

    ul {
        padding: 0;
    }

    ul li {
        cursor: pointer;
        font-size: 18px;
        padding: 10px;
        list-style-type: none;
        background-color: black;
        color: white;
        width: 30%;
        margin: auto;
        transition: all 0.4s ease;
    }

    ul li:hover {
        background-position: 100% 100%;
        transform: translateY(-5px) scale(1.1);
        transition: all 0.1s ease-in-out;
        color: black;
        /* box-shadow: 0 0 1px darkslateblue; */
    }

    li {
        background: linear-gradient(black, black 50%, crimson 50%, crimson);
        background-size: 100% 200%;
        outline: 1px solid transparent;
    }

    button {
        height: 42px;
    }

    .isCompleted {
      text-decoration: line-through;
    }

    .notCompleted {
      text-decoration: none;
    }

    .ghost {
      opacity: 0.5;
      background: #c8ebfb;
    }
</style>
