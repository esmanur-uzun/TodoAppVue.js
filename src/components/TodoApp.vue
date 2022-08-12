<script>
export default {
    name:"todoapp",
    data(){
        return{
            newTodo:"",
            todos: []
        }
    },
    methods: {
        addNewTodo(){
          if(this.newTodo === ""){
            return
          }
            this.todos.push({
              todo: this.newTodo,
              done: false 
            })
            this.newTodo = ""
        },
        removeTodo(index){
            this.todos.splice(index,1)
        },
        changeStatus(index){
          const item =this.todos[index]
            item.done = !item.done
        },
        clearAllTodos(){
          this.todos = []
        }
       
    },
    created (){
      this.todos = JSON.parse(localStorage.getItem('todo') || '[]')
    },
    watch:{
      todos:{
        deep: true,
        handler(){
          localStorage.setItem('todo',JSON.stringify(this.todos))
        }
      }
    }
}
</script>

<template>
    <div id="todoapp">
    <div class="form-container">
      <div class="title pb-2 mb-5 ">
        <h1 class="text-center">Todo List</h1>
      </div>
      <div class="form-box container col-lg-6 col-md-6 col-9 d-block  ">
          <form @submit.prevent="addNewTodo" class=" col-lg-8 pt-5 m-auto ">
            <div class="input-group">
              <input v-model="newTodo" type="text" class="form-control" placeholder="Add Todo" aria-label="Add Todo" aria-describedby="button-addon2">
              <button @click="addNewTodo" class="btn btn-submit btn-outline-secondary" type="button" id="button-addon2">Button</button>
            </div>
            <hr>
          </form>
          <div>
          <ul v-if="todos.length" class="list-group col-lg-6 m-auto list-group-flush mb-5">
            <li v-for="(item,index) in todos" :key="index" :class="{'done' :item.done}" class="list-group-item justify-content-between d-flex">
                <span>{{item.todo}}</span>
                <div class="d-flex  btn-container">
                    <button @click="changeStatus(index)" class="btn">check</button>
                    <button @click="removeTodo(index)"  class="btn">sil</button>
                </div>
                
            </li>
            
          </ul>
          
          <p v-else class="text-center">Your todo list is empty</p>
          <div class="d-flex justify-content-center pb-5"><button @click="clearAllTodos" class="col-lg-6 btn clearButton">Clear All Todos</button></div>
        </div>
      </div>
       
    </div> 
  </div>
</template>

<style scoped>
.form-container{
  height: 100vh;
}
.title{
  background-color: #3d314a;
}
h1{
  color:#e4f0d0;
}
.btn-submit{
  background-color: #3d314a;
  color: #e4f0d0;
}
.form-box{
  background-color: #B1ABC4;
  border-radius: 10px;
}
ul li{
  background-color: transparent !important;
  color: #540d6e;
}

img{
    height: 17px;
}
.clearButton{
    background-color: #941b0c;
    color: #fff;
}
.done span{
  text-decoration:line-through;
}
.btn-container :nth-child(1){
  background-color: #540d6e;
  color: #e4f0d0;
}
.btn-container :nth-child(2){
  background-color: #941b0c;
  color: #e4f0d0;
}

</style>