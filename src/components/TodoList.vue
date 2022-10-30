<template>
  <h1>{{ title }}</h1>
  <input type="text" v-model="newList"/>
  <button @click.prevent="addTodo">追加する</button>
  <button @click="deleteTodo">削除</button>


  <p v-if="lists.length === 0">ToDoがありません！</p>
  <ul v-else>
    <li v-for="(list, index) in lists" :key="index">
      <input type="checkbox" v-model="list.isDone" />
      <span :class="{'list-done':list.isDone }">{{ list.text }}</span>
      <button @click="editTodo = true">編集</button>
    </li>
  </ul>

</template>

<!--<template v-model="editTodo">-->
<!--  ダイアログ-->
<!--</template>-->


<script>
export default {
  name: "TodoList",
  data(){
    return{
      newList: '',
      lists: [],
      editTodo: false,
    }
  },
  methods:{
    addTodo(){
      if(!this.newList){
        alert('文字を入力して下さい')
        return
      }
      this.lists.push({
        isDone: false,
        text: this.newList,
      })
      this.newList = ''
    },
    // editTodo(){
    //   console.log('あたり')
    // },
    deleteTodo(){
      this.lists = this.lists.filter((list) => !list.isDone)
    },
  },
  props:{
    title:String,
  },
}
</script>

<style scoped>
.list-done {
  text-decoration: line-through;
}

body {
  background-color: rgba(16, 206, 1, 0.98);
}
</style>
