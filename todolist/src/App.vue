<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <THeader :addtodo="addtodo"/>
        <TList :todos="todos"/>
        <TFooter/>
      </div>
    </div>
  </div>
</template>

<script>
import THeader from './components/THeader.vue'
import TList from './components/TList.vue'
import TFooter from './components/TFooter.vue'
import { nanoid } from 'nanoid'

export default {
  name: 'App',
  components: {
    THeader,
    TList,
    TFooter
  },
  data() {
    return {
      todos: [
        { id: "001", title: "学习", completed: true },
        { id: "002", title: "看书", completed: false },
        { id: "003", title: "早睡", completed: true },
      ],
    }
  },
  methods:{
    //添加todo
    addtodo(e){
      const todoObj = {
        id:nanoid(),
        title:e.target.value,
        completed:false
      }
      this.todos.unshift(todoObj)
    }
  }
}
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
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
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
