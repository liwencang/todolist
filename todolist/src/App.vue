<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <THeader @addtodo="addtodo" />
        <TList
          :todos="todos"
          @change="updateToDoStatus()"
          :updateToDoStatus="updateToDoStatus"
          :deleteTodo="deleteTodo"
        />
        <TFooter
          :todos="todos"
          @deleteCompleted="deleteCompleted"
          @checkAlltodo="checkAlltodo"
        />
      </div>
    </div>
  </div>
</template>

<script>
import THeader from "./components/THeader.vue";
import TList from "./components/TList.vue";
import TFooter from "./components/TFooter.vue";
import { nanoid } from "nanoid";

export default {
  name: "App",
  components: {
    THeader,
    TList,
    TFooter,
  },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [],
    };
  },
  methods: {
    //添加todo
    addtodo(e) {
      const todoObj = {
        id: nanoid(),
        title: e.target.value,
        completed: false,
      };
      this.todos.unshift(todoObj);
    },
    updateToDoStatus(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed;
        }
      });
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      console.log("deleteTodo()");
    },
    deleteCompleted() {
      this.todos = this.todos.filter((todo) => todo.completed == false);
    },
    checkAlltodo(value) {
      this.todos.forEach((todo) => {
        todo.completed = value
      });
    },
    
    editBlur(id, value) {
      if (!value.trim()) return alert("标题不能为空");
      this.todos.forEach((todo) => {
        if (todo.id == id) {
          todo.title = value
          todo.isEdit = false
        }
      });
    },
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        // console.log(value);
        localStorage.setItem("todos", JSON.stringify(value));
      },
    },
  },
  mounted() {
    this.$bus.$on("delTodo", this.deleteTodo);
    this.$bus.$on("updateToDoStatus", this.updateToDoStatus);
    this.$bus.$on("editTodo", this.editTodo);
    this.$bus.$on("editBlur", this.editBlur);
  },
  beforeDestroy() {
    this.$bus.$off("delTodo");
    this.$bus.$off("updateToDoStatus");
  },
};
</script>

<style>
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-edit {
  color: rgb(0, 119, 255);
  background-color: skyblue;
  border: 1px solid rgb(42, 187, 244);
  margin-right: 5px;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
