<template>
  <div class="top d-flex my-5">
      <input
        v-model.trim="newTodo"
        @keyup.enter="$emit('addTodo',newTodo), newTodo = ''"
       type="text" class="form-control" placeholder="Cose devo fare?">
      <button
        @click="$emit('addTodo',newTodo, newTodo = '')"
       class="btn btn-info ms-3">Invia</button>
  </div>
</template>

<script>
export default {
  name: 'InsertTodo',
  data(){
    return{
      newTodo: ''
    }
  }
}
</script>

<style lang="scss" scoped>

</style>