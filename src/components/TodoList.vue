<template>
  <div>
    <input type="text" name="" v-model="newTodo" id="" class="todo-input" placeholder="What needs to be done" @keyup.enter="addtodo()">
      <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
        <div class="todo-item-left">
          <input type="checkbox" name="" v-model="todo.completed" id="">
            <div v-if="!todo.editing" class="todo-item-label" @dblclick="editTodo(todo)">{{ todo.title }} </div>
            <input v-else class="todo-item-edit" type="text" name="" id="" 
            v-model="todo.title" @keyup.enter="doneEdit(todo)"  @keyup.esc="cancelEdit(todo)"  @blur="doneEdit(todo)" v-focus>
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
      beforeEditCache: '',
      todos: [
        {
          'id': 1,
          'title': 'Finish Vue Screencast',
          'completed': false,
          'editing': false
        },
        {
          'id': 2,
          'title': 'Task is good',
          'completed': false,
          'editing': false
        }

      ]
    }
  },
  directives: {
    focus: {
      inserted: function(el){
        el.focus()
      }
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

    editTodo(todo){
      this.beforeEditCache = todo.title
      todo.editing = true
    },

    doneEdit(todo){
      if(todo.title.trim() == '') {
        todo.title = this.beforeEditCache
      }
      todo.editing = false
    },

    cancelEdit(todo){
      todo.title = this.beforeEditCache
      todo.editing = false
    },

    removeTodo(index){
      this.todos.splice(index,1)
    }

  }
}
</script>

<style lang="scss">
*{
  font-size: 24px;
}
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

    .todo-item-left{
      display: flex;
      align-items: center;
    }
    .todo-item-label {
      padding:10px;
      border: 1px solid white;
      margin-left: 12px;
    }
    .todo-item-edit {
      font-size: 24px;
      color: #2c3e50;
      margin-left: 12px;
      width: 100%;
      padding:10px;
      border: 1px solid #ccc;
      font-family: 'Avenir', Helvetica, Arial, Sans-serif;

      &:focus {
        outline: none;
      }
    }
</style>
