<template>
  <h1>{{ title }}</h1>
  <input type="text" v-model="newList"/>
  <button @click="addLists">追加する</button>

  <li v-for="(list, index) in lists" :key="index">
<!--    <input type="text" />-->
    <span>{{ list.text }}</span>
    <button @click="deleteLists">削除</button>
  </li>
</template>

<script>
export default {
  name: "TodoList",
  data(){
    return{
      newList:"",
      list: [],
      lists: [{
        text: 'やること1',
      },
        {
          text: 'やること2',
        },

      ]
    }
  },
  methods:{
    addLists(){
      if(!this.newList){
        alert('文字を入力して下さい')
        return
      }
      this.list.push({
        text: this.newList,
      })
      this.newList = ''
    },
  },
  props:{
    title:String,
  },
}
</script>

<style scoped>

</style>
