<template>
    <div class="app">
        <div class="container">
            <div class="row header">
                <form @submit.prevent="submitTodo" class="col s6 offset-s3">
                    <div class="input-field">
                        <i class="material-icons prefix grey-text">list</i>
                        <textarea
                            v-model="newTodo"
                            id="icon_prefix2"
                            class="materialize-textarea grey-text" />
                        <label for="icon_prefix2">What do you want to do?</label>
                    </div>
                    <button class="btn waves-effect col s12">Add</button>
                </form>
            </div>
            <div class="row">
                <ul class="collection col s6 offset-s3">
                    <li class="collection-item grey darken-4" v-for="todo in todos" :key="todo.id">
                        <p>
                            <label>
                                <input
                                    type="checkbox"
                                    :checked="todo.done"
                                    @change="todo.done = !todo.done"
                                />
                                <span>{{todo.title}}</span>
                                <span>
                                    <a @click.prevent="deleteTodo(todo)">
                                        <i class="material-icons right teal-text">delete</i>
                                    </a>
                                </span>
                            </label>
                        </p>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      todos: [],
      newTodo: '',
    };
  },
  watch: {
    todos: {
      handler() {
        localStorage.todos = JSON.stringify(this.todos);
      },
      deep: true,
    },
  },
  mounted() {
    if (localStorage.todos) {
      this.todos = JSON.parse(localStorage.todos);
    }
  },
  methods: {
    submitTodo() {
      this.todos.push({
        title: this.newTodo,
        done: false,
      });
      this.newTodo = '';
    },
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
  },
};
</script>

<style lang="scss">
.header {
    margin-top: 20px;
}
</style>
