<template>
  <div class="todo">
    <li :click="onClick" :class="todo.completed ? 'completed' : ''" key={todo.id}>
      <div>
        <input
            type="checkbox"
            class="toggle"
            name="checkbox"
            @click="() => toggleTodo(todo.id)"
            :checked="todo.completed"
        />
        <label for="checkbox">{{todo.text}}</label>
      </div>
    </li>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    'todo': Object,
    toggleTodo: Function
  }
}
</script>
