<template>
    <ul class="todo-main">
      <v-item 
      v-for="item in listArr" 
      :key="item.id"
      :item='item'
      ></v-item>
    </ul>

</template>

<script>
import myItem from './item'
export default {
    
  name: "myList",
  props:{
    listArr:Array
  },
  components: {
      'v-item':myItem
  }

}
</script>

<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>
