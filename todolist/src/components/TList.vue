<template>
  <ul class="todo-main">
    <TItem v-for="t in todos" :key="t.id" :todo="t" :updateToDoStatus="updateToDoStatus"/>
  </ul>
</template>

<script>
import TItem from "./TItem.vue";
export default {
  name: "TList",
  components: {
    TItem,
  },
  props:['todos','updateToDoStatus']
};
</script>

<style>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>