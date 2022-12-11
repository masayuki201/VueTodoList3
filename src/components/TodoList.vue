<script setup>
import { computed, reactive, ref } from 'vue';

const keyword = ref('');
const newList = ref('');
const lists = reactive([
  {
    isDone: false,
    text: 'スーパーに行く',
  },
  {
    isDone: false,
    text: 'クリーニングを出す',
  },
  {
    isDone: false,
    text: 'ジムへ行く',
  },
]);

const props = defineProps({
  title: String,
});

//  検索
const filteredLists = computed(() => {
  const searchKeyword = keyword.value;
  if (searchKeyword === '') return lists;
  return lists.filter((list) => list.text.includes(searchKeyword));
});

//  追加
const addTodo = () => {
  if (!newList.value) {
    alert('文字を入力して下さい');
    return;
  }
  lists.push({
    isDone: false,
    text: newList.value,
  });
  newList.value = '';
};

//  編集
const editTodo = (index) => {
  lists[index].isActive = true;
};

//  完了
const updateTodo = (index) => {
  lists[index].isActive = false;
};

//  削除
const deleteTodo = (index) => {
//  選択したindexを1列だけ削除
//   filteredLists.value.splice(index, 1);
  console.log(index);
  console.log(filteredLists);
  filteredLists.value.splice(index, 1);

  console.log(filteredLists.value);
  console.log(lists);
};

</script>

<template>
  <div>
    <h1>{{ props.title }}</h1>
    <input type="text" v-model="newList" placeholder="内容"/>
    <button class="addBtn" @click.prevent="addTodo">追加</button>
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
            <button class="doneBtn" @click="updateTodo(index)">完了</button>
          </div>
          <button class="editBtn" v-show="!list.isActive" @click="editTodo(index)">編集</button>
          <button class="deleteBtn" @click="deleteTodo(index)">削除</button>
        </li>
      </ul>
    </div>
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
