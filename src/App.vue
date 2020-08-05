<template>
  <div id="app">
    <router-view/>
    <div class="todoApp">
      <div class="todo-title"> todos </div>
      <TodosList :todos="todos" :toggleTodo="toggleTodo" @todo-added="addTodo($event)" />
    </div>
  </div>
</template>

<script>
import TodosList from './components/TodosList'
export default {
  name: 'App',
  components: {TodosList},
  data () {
    return {
      todos: []
    }
  },
  methods: {
    toggleTodo (id) {
      this.$set(this.todos, id, { ...this.todos[id], completed: !this.todos[id].completed })
    },
    addTodo (todoText) {
      this.todos.push({
        id: this.todos.length,
        text: todoText,
        completed: false
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
html,
body {
    height: 100%;
    width: 100%;
}
body {
    background-image: url('https://images.unsplash.com/photo-1459695452562-46cc57bef5f6?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80');
    background-size: auto;
    background-repeat: no-repeat;
    background-position: center center;
    top: 0;
    position: absolute;
}
.App {
    text-align: center;
}

.App-logo {
    animation: App-logo-spin infinite 20s linear;
    height: 80px;
}

.App-header {
    background-color: #222;
    height: 150px;
    padding: 20px;
    color: white;
}

.App-title {
    font-size: 1.5em;
}

.App-intro {
    font-size: large;
}
.todoApp {
  width: 450px;
  display: block;
  margin: 0 auto;
  border-radius: 4px;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  margin-top: 120px;
  position: relative;
  background: #fff;
}

.todo-title {
  font-size: 100px;
  color: rgba(175, 47, 47, 0.15);
  position: absolute;
  top: -137px;
  width: 100%;
}

@keyframes App-logo-spin {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

</style>
