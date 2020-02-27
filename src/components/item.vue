<template>
      <li 
      :class="light" 
      @mouseenter='light.light = true'
      @mouseleave='light.light = false'

      >
        <label>
          <input type="checkbox" 
          @change="change(item.id)" 
          v-model="item.checked"
          />
          <span>{{item.content}}</span>
        </label>
        <button 
        class="btn btn-danger"
        v-show="light.light"
        @click="delItem"
        >
        删除</button>
      </li>
      
</template>

<script>

export default {

  name: "myItem",
  props:['item'],
  data() {
    return {
      light:{
        light:false
      }
    } 
  },
  methods: {
    change(id){
      this.bus.$emit('change',id,this.checked)
    },
    delItem(){
      this.bus.$emit('delItem',this.item.id)
    }
  },
}
</script>

<style scoped>
/*item*/
.light{
  background:#da4f49;
}
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
  color:lightgreen;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
</style>
