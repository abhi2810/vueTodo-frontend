<template>
  <div id="home">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import * as axios from "axios";
export default {
  name: "Home",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      //this.todos = this.todos.filter(todo => todo.uid !== id);
      axios
        .post(
          "https://x6rwaxz226.execute-api.us-east-1.amazonaws.com/default/notesbackend",
          {
            operation: "delete",
            payload: {
              TableName: "todos",
              Key: {
                uid: id
              }
            }
          }
        )
        .then(res => (this.todos = this.todos.filter(todo => todo.uid !== id)))
        .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      //this.todos = [...this.todos, newTodo];
      const { uid, title, completed } = newTodo;
      axios
        .post(
          "https://x6rwaxz226.execute-api.us-east-1.amazonaws.com/default/notesbackend",
          {
            operation: "create",
            payload: {
              TableName: "todos",
              Item: {
                uid: uid,
                title: title,
                completed: completed
              }
            }
          }
        )
        .then(res => (this.todos = [...this.todos, res.data]))
        .catch(err => console.log(err));
    }
  },
  created() {
    axios({
      method: "post",
      url:
        "https://x6rwaxz226.execute-api.us-east-1.amazonaws.com/default/notesbackend",
      data: {
        operation: "list",
        payload: {
          TableName: "todos"
        }
      },
      headers: {
        "Content-Type": "application/json"
      }
    })
      .then(res => (this.todos = res.data))
      .catch(err => console.log(err));
  }
};
</script>