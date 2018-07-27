<template>
  <div>
    <input type="text" name="" v-model="newTodo" id="" class="todo-input" placeholder="What needs to be done" @keyup.enter="addtodo()">
      <div v-for="todo in todos" :key="todo.id" class="todo-item">
        {{ todo.title }}
      </div>
  </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newTodo: '',
      id: 3,
      todos: [
        {
          'id': 1,
          'title': 'Finish Vue Screencast',
          'completed': false
        },
        {
          'id': 2,
          'title': 'Task is good',
          'completed': false
        }

      ]
    }
  },

  methods: {
    addtodo () {
      if(this.newTodo.trim() == 0) return
     this.todos.push({
       id: this.id,
       title: this.newTodo,
       completed: false,
     })

     this.newTodo = ''
     this.id++
    }
  }
}
</script>

<style lang="scss">
  .todo-input{
    width: 100%;
    padding:10px 18px;
    font-size:18px;
    margin-bottom: 16px;

    &:focus {
      outline:0;
    }
  }
</style>
