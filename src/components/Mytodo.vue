<template>
    <div class="section">
      <div class="container">
          <h1>Todo  list</h1>
          <div class="todo__list">
              <div class="input__todo">
                  <input type="text" placeholder="Enter todo item..." v-model="title">
                  <button @click="add">Add</button>
              </div>
              <div class="todolist__body">
                  <ul>
                      <li v-for="todo in todos">
                          <span>{{ todo }}</span>
                          <button class="remove" @click="remove(todo)">delete</button>
                      </li>
                  </ul>
              </div>
          </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, watch , onMounted} from 'vue';
  
  const title = ref('');
  
  const todos = ref ([]);
  const add = () => {
      todos.value.push(title.value);
      title.value = '';
  }
  
  const remove = (todo) => {
   todos.value = todos.value.filter((i) => i !== todo);
  }
  
  watch(todos, (newValue) => {
  localStorage.setItem('todos', JSON.stringify(newValue))
  }, {
      deep: true
  })
  
  onMounted(() => {
    if(JSON.parse(localStorage.getItem('todos') !== null)) {
        todos.value = JSON.parse(localStorage.getItem('todos'));
    }
})
  

  </script>
  
  <style lang="scss" scoped>
  .section{
      .container{
          display: flex;
          flex-direction: column;
          align-items: center;
          justify-content: center;
          background: white;
          border-radius: 40px;        
          h1{
              font-size: 50px ;
              color: dodgerblue;
              text-align: center;
          }
          .todo__list{
              max-width: 600px;
              width: 100%;
              
              
              .input__todo{
                  display: flex;
                  margin-top: 80px;
                  border: 2px solid dodgerblue;
                  border-radius: 10px;
                  overflow: hidden;
                  
                  input{
                      width: 100%;
                      font-size: 18px;
                      padding: 8px ;
                      border: none;
                      outline: none;
                      
                    }
                    button{
                      font-size: 20px;
                      color:white;
                      background: dodgerblue;
                      padding: 10px 15px;
                      border: none;
                      border-radius: 8px;
                      cursor: pointer;
                      margin-left: 8px;
                      &:hover{
                          opacity: .5;
                        }
                        
                    }
                    
                }
                
                .todolist__body{
                    margin: 80px 0 40px;
                    width: 100%;
                    ul{
                        display: grid;
                        gap: 30px;
                        
                        li{
                            background: rgb(189, 179, 179);
                            display: flex;
                            justify-content: space-between;
                          align-items: center;
                          border: 2px solid dodgerblue;
                          padding: 10px;
                          font-size: 22px;
                          border-radius: 8px;
                          
                          .remove{
                              font-size: 18px;
                              padding: 8px;
                              border: none;
                              background: red;
                              border-radius: 8px;
                              color: white;
                              text-transform: initial;
                              cursor: pointer;
                              &:hover{
                                  background: black;
                              }
                              
                          }
  
                      }
                  }
                  
              }
          }
  
  
      }
      }
  </style>