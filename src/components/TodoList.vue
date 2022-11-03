<template>
  <h1>{{ title }}</h1>
  <input type="text" v-model="newList" placeholder="内容"/>
  <button class="addBtn" @click.prevent="addTodo">追加</button>
  <button  class="deleteBtn" @click="deleteTodo">削除</button>


  <p v-if="lists.length === 0" class="warningMessage">Todoがありません！</p>
  <ul v-else>
<!--    <input type="text" v-model="query">検索-->

    <li v-for="(list, index) in lists" :key="index">
      <input type="checkbox" v-model="list.isDone" />
      <span :class="{'list-done':list.isDone }">{{ list.text }}</span>
      <div v-if="list.isActive">
        <span>
          <input type="text" v-model="list.text">
        </span>
        <button @click="updateDone(index)">完了</button>
      </div>
      <button class="editBtn" v-show="!list.isActive" @click="updateTodo(index)">編集</button>
    </li>
  </ul>

</template>

<script>
export default {
  name: "TodoList",
  data(){
    return{
      newList: '',
      lists: [
        {
          text: 'スーパーに行く',
        },
        {
          text: 'クリーニングを出す',
        },
        {
          text: 'ジムへ行く',
        },
      ],
      editTodo: false,
    }
  },
  methods:{
    //追加
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
    //編集
    updateTodo(index){
      this.lists[index].isActive = true
      this.lists[index].item = this.list[index].item
    },
    //完了
    updateDone(index){
      this.lists[index].isActive = false
    },
    //削除
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

.addBtn {
  margin: 5px;
}

.deleteBtn {
  background-color: red;
  color:white;
  margin: 5px;
}

.editBtn {
  margin: 5px;
}

.warningMessage {
  color: red;
}

</style>
