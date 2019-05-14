<template>
  <div>
    <form @submit.prevent="addTodo">
      <input
        class="form-control"
        type="text"
        v-model="title"
        name="title"
        placeholder="Add Todo..."
      >
      <input class="btn btn-primary" type="submit" value="Submit">
    </form>
  </div>
</template>

<script>
import uuid from 'uuid';
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo() {
      const newTodo = {
        uid : uuid.v4(),
        title: this.title,
        completed: false
      };
      // Send up to parent
      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
  margin-top: 10px;
  margin-bottom: 20px;
  margin-left: 30px;
  margin-right: 30px;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
  margin-right: 10px;
}
input[type="submit"] {
  flex: 2;
}
</style>
