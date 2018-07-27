<template>
  <div>
    <input type="text" name="" v-model="newTodo" id="" class="todo-input" placeholder="What needs to be done" @keyup.enter="addtodo()">
      <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
        <div>
            {{ todo.title }} 
        </div>
        <div class="remove-item" @click="removeTodo(index)">
          &times;
        </div>
       
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
      if(this.newTodo.trim().length == 0) return
     this.todos.push({
       id: this.id,
       title: this.newTodo,
       completed: false,
     })

     this.newTodo = ''
     this.id++
    },
    removeTodo(index){
      this.todos.splice(index,1)
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

    .todo-item{
      margin-bottom:12px;
      display:flex;
      align-items: center;
      justify-content: space-between;

    }

    .remove-item{
      cursor: pointer;
      margin-left: 14px;
      &:hover {
        color:black;
      }
    }
</style>
