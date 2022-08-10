<template>
  <div class="warp-todo">
     <div class="todo">
      <h1> Add todolist</h1>
      <input class="app-input" type="text" placeholder="Nhập vào đây" v-model="formData.nameTodo">
      <button 
      @click="addTodo()"
      :danger="!!edit"
      >
      {{edit ? "Edit Todo" : "add Todo"}}
      </button>
    </div>

     <div class="todo1">
      <h1>Todolist</h1>
      <div 
        class="list" v-for="(todo,index) in todoList" :key="index">
        <div>
          {{`${index+1}. ${todo.nameTodo}`}}
        </div>
        <span class="icon">
          <p>
            <i class="fa-solid fa-pen" @click="editTodo(todo,index)"></i>
          </p>
          <p>
            <i class="fa-regular fa-trash-can" @click="deleteTodo(index)"></i>
          </p>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      todoList:[
        {nameTodo:'Đi làm'},
        {nameTodo:'Đi chơi'}
      ],
      formData:{
        nameTodo:""
      },
      edit:"",
    }
  },
  methods:{
    addTodo(){
      if(!this.edit){
        this.todoList.push({...this.formData})
        this.formData.nameTodo=""
      }else {
        this.todoList[this.edit-1]= {...this.formData}
        this.formData.nameTodo=""
        this.edit=""
      }
    },
    deleteTodo(index){
      this.todoList.splice(index,1)
    },
    editTodo(todo,index){
      this.formData.nameTodo=todo.nameTodo
      this.edit=index+1
    }
  }
}
</script>

<style>
  .warp-todo {
    display:flex;
    justify-content: center;
    align-items: center;
  }
  .todo1 {
    width: 500px;
    height: 500px;
    background-color: aquamarine;
    margin-right: 12px;
    padding: 0 12px;
  }
   .todo {
    display:flex;
    flex-direction: column;
    align-items: center;
    width: 500px;
    height: 500px;
    background-color: rgb(9, 76, 54);
    margin-right: 12px;
    padding: 0 12px;
  }
  .list {
    display:flex;
    align-items: center;
    justify-content:space-between;
    background-color: burlywood;
    padding:0 8px;
    line-height: 14px;
    border-radius:8px;
    color:darkred;
    margin-bottom: 4px;
    font-size: 14px;
  }
  p:nth-child(1) {
    margin-right: 12px;
  }
  .icon {
    display:flex;
  }
  h1 {
     text-align: center;
  }
  .app-input {
    width: 80%;
    height: 30px;
    border-radius:4px;
    border:1px solid #ccc;
    padding: 5px;
  }
  button {
    margin-top: 12px;
    width: 80%;
    height: 40px;
    padding: 8px;
    border-radius:4px;
    border:1px solid #ccc;
    background-color:dodgerblue;  
  }
  .danger {
    background-color: maroon;
  }
  
</style>