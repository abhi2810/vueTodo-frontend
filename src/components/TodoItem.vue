<template>
  <li class="list-group-item" v-bind:class="{'is-complete':todo.completed}">
    <div class="text">
      <input type="checkbox" v-model="todo.completed" >
      {{todo.title}}
      <button class="btn btn-danger" @click="$emit('del-todo', todo.uid)">
          <span class="icon">X</span>
      </button>
    </div>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"]
};
</script>

<style>
.text{
    font-size: 30px;
}
input[type=checkbox]{
    margin: 10px;
}
.is-complete {
  text-decoration: line-through;
}
.icon{
    color: #fff;
    text-decoration-style: solid;
}
button{
    float: right;
    padding: 10px;
    cursor: pointer;
    border-radius: 50%;
}
</style>
