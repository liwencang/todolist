<template>
  <div class="todo-header">
    <input type="text" @keyup.enter="add" v-model="title" placeholder="请输入你的任务名称，按回车键确认" />
  </div>
</template>

<script>
export default {
  name: "THeader",
  data(){
    return {
      title:""
    }
  },
  methods:{
    //添加todo
    //把新增的数据校验，通过调用App.vue函数的方式传给App.vue
    add(e){
      if(!this.title.trim()) {
        this.title = ''
        return
      }
      this.$emit('addtodo',e)
      this.title = ''
    }
  }
};
</script>

<style>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>