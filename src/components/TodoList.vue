<script setup>
import {ref, reactive, computed} from 'vue';

const keyword = ref('');
const newList = ref('');
const lists = reactive([
  {
    text: 'スーパーに行く',
  },
  {
    text: 'クリーニングを出す',
  },
  {
    text: 'ジムへ行く',
  },
]);

//検索
const filteredLists = computed(() => {
  console.log('1')

  // const lists = [];
  console.log('2')
  console.log(lists)

  for (const i in lists) {
    console.log('3')
    console.log(lists[i].text)

    const list = lists[i].text;
    console.log(list)

    if (list.indexOf(keyword.value) !== -1) {
      console.log('ifの中')

      lists.text.push(list);


    }
  }
  console.log('4')
  return lists;
})

//追加
const addTodo = () => {
  if (!newList.value) {
    alert('文字を入力して下さい')
    return
  }
  lists.push({
    isDone: false,
    text: newList.value,
  })
  newList.value = ''
}



// props: {
//     title: String,
// },

// export default {
//   name: "TodoList",
//   data() {
//     return {
//       keyword: '',
//       newList: '',
//       lists: [
//         {
//           text: 'スーパーに行く',
//         },
//         {
//           text: 'クリーニングを出す',
//         },
//         {
//           text: 'ジムへ行く',
//         },
//       ],
//       editTodo: false,
//     }
//   },
//   computed: {
//     filteredLists: function () {
//       const lists = [];
//       for (const i in this.lists) {
//         const list = this.lists[i];
//         if (list.text.indexOf(this.keyword) !== -1) {
//           lists.push(list);
//         }
//       }
//       return lists;
//     }
//   },
//   methods: {
//     //追加
//     addTodo() {
//       if (!this.newList) {
//         alert('文字を入力して下さい')
//         return
//       }
//       this.lists.push({
//         isDone: false,
//         text: this.newList,
//       })
//       this.newList = ''
//     },
//     //編集
//     updateTodo(index) {
//       this.lists[index].isActive = true
//       this.lists[index].text = this.list[index].text
//     },
//     //完了
//     updateDone(index) {
//       this.lists[index].isActive = false
//     },
//     //削除
//     deleteTodo() {
//       this.lists = this.lists.filter((list) => !list.isDone)
//     },
//   },
//   props: {
//     title: String,
//   },
// }
</script>

<template>
<!--  <h1>{{ title }}</h1>-->
  <input type="text" v-model="newList" placeholder="内容"/>
  <button class="addBtn" @click.prevent="addTodo">追加</button>
  <button class="deleteBtn" @click="deleteTodo">削除</button>
  <br>
  <input class="searchText" type="text" v-model="keyword" placeholder="検索">

  <div class="contents">
    <p v-if="lists.length === 0" class="warningMessage">Todoがありません！</p>
    <ul class="contents_ul" v-else>
      <li class="contents_li" v-for="(list, index) in filteredLists" :key="index">
        <input type="checkbox" v-model="list.isDone"/>
        <span :class="{'list-done':list.isDone }">{{ list.text }}</span>
        <div v-if="list.isActive">
        <span>
          <input type="text" v-model="list.text">
        </span>
          <button class="doneBtn" @click="updateDone(index)">完了</button>
        </div>
        <button class="editBtn" v-show="!list.isActive" @click="updateTodo(index)">編集</button>
      </li>
    </ul>
  </div>

</template>



<style scoped>
.list-done {
  text-decoration: line-through;
}

.contents {
  margin: 16px auto;
  text-align: center;
}

.contents_ul {
  padding-left: 0;
  list-style: none;
  display: inline-block;
}

.contents_li {
  list-style: none;
  text-align: left;
}

.searchText {
  margin: 5px;
}

.addBtn {
  background-color: deepskyblue;
  margin: 5px;
}

.deleteBtn {
  background-color: red;
  color: white;
  margin: 5px;
}

.editBtn {
  margin: 5px;
}

.doneBtn {
  background-color: deepskyblue;
  margin: 5px;
}

.warningMessage {
  color: red;
}

</style>
