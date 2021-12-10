<template>
        <li  
          class="list-group-item d-flex justify-content-between">

          <!-- se sono in edtiMode mostro il l'input altrimenti solo il testo -->
          <input
           v-if="editMode" 
           v-model="todoItem.value"
           @keyup.enter="$emit('editTodo',todoItem),editMode = false"
           type="text" class="form-control inputTodo">
          <span v-else>{{todoItem.value}}</span>
          <div>

            <!-- se sono in edtiMode mostro il floppy altrimenti la matita -->
            <i v-if="!editMode" @click="editMode = true" class="fas fa-pencil-alt"></i>
            <!-- al click del floppy saìcateno l'evento emit-->
            <i v-else
              @click="$emit('editTodo',todoItem),editMode = false"
               class="far fa-save"></i>
            <i @click="deleteItem(todoItem)" class="fas fa-times ms-2"></i>
          </div>
        </li>
        
</template>

<script>
export default {
  name:"ListItem",
  data(){
    return{
      editMode: false
    }
  },
  props:{
    todoItem: Object
  },
  methods:{
    deleteItem(item){
      if(confirm(`Confermi l'eleminazione di: ${item.value}?`)){
        this.$emit('deleteItem',item.id);
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.fas, .far{
  cursor: pointer;
  &:hover{
    color: #30CAF0;
  }
}
.inputTodo{
  width: 500px;
}
</style>