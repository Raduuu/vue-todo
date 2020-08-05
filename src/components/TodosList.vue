
<template>
  <div class="todos-wrapper">
    <input
      type="text"
      class="todo-input"
      placeholder="What needs to be done?"
      autofocus="true"
      @keydown="(ev) => handleEnter(ev)"
      @change="(ev) => handleChange(ev)"
      v-model="newTodo"
    />
    <div class="todos-list">
      <ul>
          <Todo v-for="todo in todos" :key="todo.id" :todo="todo" :toggleTodo="toggleTodo"/>
      </ul>
      <p>{{ completed }} of {{ todos.length }} completed</p>
    </div>
  </div>
</template>

<script>
import Todo from './Todo'

export default {
  name: 'TodosList',
  components: { Todo },
  props: {
    todos: {
      type: Array,
      default: () => [],
      required: true
    },
    toggleTodo: {
      type: Function,
      default: () => {},
      required: true
    },
    todo: {
      type: Object
    }
  },
  data () {
    return {
      newTodo: ''
    }
  },
  methods: {
    handleEnter (ev) {
      if (ev.key === 'Enter' && ev.target.value !== '') {
        document.getElementsByClassName('.todo-input').value = ''
        this.$emit('todo-added', ev.target.value)
        this.newTodo = ''
      }
    },
    handleChange (ev) {
      this.newTodo = ev.target.value
    }
  },
  computed: {
    completed: function () {
      return this.$props.todos.filter((todo) => todo.completed).length || 0
    }
  }
}
</script>

<style>
  .todo-input {
    width: 100%;
    height: 48px;
    border: none;
    padding-left: 30px;
    font-size: 30px;
    font-weight: 100;
    box-sizing: border-box;
    outline: none;
  }
  .todos-list ul {
    padding: 0;
    margin: 0;
  }

  .todos-list li {
    position: relative;
    font-size: 24px;
    border-bottom: 1px solid #ededed;
    white-space: pre-line;
    word-break: break-all;
    display: block;
    line-height: 1.2;
    transition: color 0.4s;
    list-style: none;
    font-weight: 300;
    text-align: left;
    cursor: pointer;
    outline: none;
  }
  .todos-list li:hover {
    color: grey;
  }
  .todos-list li label {
    word-break: break-all;
    padding: 15px 15px 15px 60px;
    display: block;
    line-height: 1.2;
    transition: color 0.4s;
    outline: none;
  }

  .todos-list li .toggle {
    background-color: initial;
    box-sizing: border-box;
    text-align: center;
    width: 40px;
    height: auto;
    position: absolute;
    top: 0;
    bottom: 0;
    margin: auto 0;
    border: none;
    appearance: none;
    outline: none;
  }

  .todos-list li .toggle + label {
    background-image: url('../circle-regular.svg');
    background-repeat: no-repeat;
    background-position: center left;
    background-size: 25px 25px;
    background-position: 15px 15px;
    outline: none;
  }

  .todos-list li.completed {
    text-decoration: line-through;
  }
  .todos-list li.completed .toggle + label {
    background-image: url('../check-circle-regular.svg');
    text-decoration: line-through;
  }

</style>
