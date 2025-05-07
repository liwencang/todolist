<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="checkAll" />
    </label>
    <span>
      <span>已完成{{ completedTotal }}</span> / 全部{{ todosTotal }}
    </span>
    <button class="btn btn-danger" @click="deleteCompleted">
      清除已完成任务
    </button>
  </div>
</template>

<script>
export default {
  name: "TFooter",
  props: ["todos", "checkAlltodo"],
  methods: {
    deleteCompleted(){
      this.$emit('deleteCompleted')
    }
  },
  computed: {
    completedTotal() {
      return this.todos.reduce((pre, current) => {
        return pre + (current.completed == true ? 1 : 0);
      }, 0);
    },
    todosTotal() {
      return this.todos.length;
    },
    checkAll: {
      get() {
        return this.completedTotal == this.todosTotal && this.todosTotal > 0;
      },
      set(value) {
        this.$emit('checkAlltodo',value);
      },
    },
  },
};
</script>

<style>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>