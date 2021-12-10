<template>
  <main>
    <InsertTodo @addTodo="addTodo" />
    <div class="bottom">
      <ul class="list-group">
        <ListItem 
          v-for="item in todoList" 
          :key="item.id"
          :todoItem = "item"
          @deleteItem="deleteItem"
          @editTodo="editTodo"
        />
      </ul>
    </div>
  </main>
</template>

<script>

import axios from 'axios';
import InsertTodo from './InsertTodo'
import ListItem from './ListItem'

export default {
  name: 'Main',
  components:{
    InsertTodo,
    ListItem
  },
  data(){
    return{
      apiUrl: 'http://localhost:3000/todos/',
      todoList: []
    }
  },
  methods:{
    // funzione che richiamo tutte le volte che si aggiornano i dati
    printTodos(){
      axios.get(this.apiUrl)
       .then( r => this.todoList = r.data)
    },
    // aggiunta di un item tramite POST
    addTodo(text){
      if(text.length > 2){
        axios.post(this.apiUrl, {
          value: text
        }).then( () =>  this.printTodos() )
      }
    },
    // eliminzione di un item tramite DELETE
    deleteItem(id){
      axios.delete(this.apiUrl+id)
      .then( () =>  this.printTodos() )
    },
    // modifica di un item trimite PUT
    editTodo(item){
      axios.put(this.apiUrl+item.id,{
        value: item.value
      }).then( () =>  this.printTodos() )
    }
  },
  mounted(){
    this.printTodos();
  }

}
</script>

<style lang="scss" scoped>
main{
  width: 80%;
  max-width: 600px;
  margin: 0 auto;
}
</style>