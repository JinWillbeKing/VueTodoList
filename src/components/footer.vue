<template>
    <div class="todo-footer">
      <label>
        <input type="checkbox" v-model="checkAll" />
      </label>
      <span>
        <span>已完成{{overCount}}</span> / 全部{{listArr.length}}
      </span>
      <button class="btn btn-danger" @click="delTrue">清除已完成任务</button>
    </div>
</template>

<script>

export default {

  name: "myFooter",
  props:{
    listArr:Array
  },
  computed: {
     overCount(){
      return this.listArr.reduce((adder,item)=>{
        return adder + (item.checked ? 1 : 0)
      },0)
    },
     checkAll:{
       get(){
         return this.overCount === this.listArr.length && this.overCount !==0 && this.listArr.length !==0;
       },
       set(val){
         this.bus.$emit("checkAll",val)
       }
     }
  },
  methods: {
    delTrue(){
      this.$emit("delTrue")
    },
  },
}
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
  color:skyblue;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}

</style>
