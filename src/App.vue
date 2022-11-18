<template>
  <div class="page-content page-container" id="page-content">
    <div class="padding">
      <div class="row container d-flex justify-content-center">
        <div class="col-md-12">
          <div class="card px-3">
            <div class="card-body">
              <h4 class="card-title">vue Todo list</h4>
              <todo-add-form @todo-text="addTodo"></todo-add-form>
              <div class="list-wrapper">
                <ul class="d-flex flex-column-reverse todo-list">
                  <todo v-for="(todo, index) in todos"
                  :item="todo"
                  :key="index"
                  @edit-todo="editTodo"
                  @delete-todo="deleteTodo"
                  @do-todo="doTodo"
                  ></todo>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";
import TodoAddForm from "./components/TodoAddForm.vue";
export default {
  components: {
    TodoAddForm,
    Todo,
  },
  data() {
    return {
      // todos : JSON.parse(this.$cookies.get('todo')) || []
      todos : JSON.parse(localStorage.getItem('todo')) || []
    };
  },
  methods : {
    refreshTodos() {
      // this.$cookies.set('todo', JSON.stringify(this.todos))
      localStorage.setItem('todo', JSON.stringify(this.todos))
    },
    addTodo(value) {
      let now = new Date();
      this.todos.push({
        id : Date.now(),
        done : false,
        text : value,
        date : now.toLocaleDateString('fa', {weekday:"long"}) + ' ' + now.toLocaleDateString('fa') + ' ساعت ' + now.toLocaleTimeString('fa')
      });
      this.refreshTodos()
    },
    editTodo(id, text) {
      this.todos = this.todos.map(item => {
         if(item.id == id) item.text = text
         return item
       })
      this.refreshTodos()
    },
    deleteTodo(id, text) {
      let ok = confirm('are you sure want to delete following todo?' + "\n" + text)
      if(ok)
        this.todos = this.todos.filter(item => item.id != id)
      this.refreshTodos()
    },
    doTodo(id, done) {
       this.todos = this.todos.map(item => {
         if(item.id == id) item.done = done
         return item
       })
      this.refreshTodos()
    }
  }
};
</script>

