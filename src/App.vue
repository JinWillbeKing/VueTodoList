<template>


  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <v-header @addItem = "addItem"></v-header>
        <v-list :listArr='listArr'></v-list>
        <v-footer :listArr='listArr' @delTrue = "delTrue"></v-footer> 
      </div>
    </div>
  </div>

</template>

<script>
import myHeader from './components/header'
import myList from './components/list'
import myFooter from './components/footer'



export default {
  name: 'App',

  data() {
    return {
      listArr:[
        {
          id:0,
          content:'达姆哥哥每个视频都很"短"',
          checked:false
        },
        {
          id:1,
          content:'达姆哥哥讲课都很"细"',
          checked:false
        },
        {
          id:2,
          content:'达姆哥哥说话很"快"',
          checked:false
        },
      
      ],
    }
  },
  methods: {
    addItem(item){
      this.listArr.unshift(item)
    },
    delTrue(){
      this.listArr = this.listArr.filter((item)=>{
        return !item.checked
      })
    }
  },
  components:{
    'v-header':myHeader,
    'v-list':myList,
    'v-footer':myFooter,
  },
  mounted() {
    this.bus.$on('checkAll',(checked)=>{
      this.listArr.forEach((item)=>{
        // console.log(item)
        // this.$set(item,'checked',checked)
            item.checked = checked
        })
    }),
    this.bus.$on('change',(id,checked)=>{
      this.listArr.forEach((item)=>{
        if(item.id === id){
          item.checked = checked
        }
      })
    }),
    this.bus.$on('delItem',(id)=>{
      this.listArr = this.listArr.filter((item)=>{
        return item.id !== id
      })
    })
       
  },

  created() {
    if(JSON.parse(localStorage.getItem("listArr"))){
      this.listArr = JSON.parse(localStorage.listArr)
    }
  },
  updated() {
    console.log(localStorage)
    localStorage.setItem("listArr",JSON.stringify(this.listArr))
  },

}



</script scoped>

<style>
  /*app*/
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

</style>
