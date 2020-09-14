<template>
  <div class="Home"> 
    <div class="HomeHeader">
      <h1 class="HomeTitle"><i class="fas fa-clipboard-list" style="margin-right: 12px"></i> <span class="animate__animated animate__slideInLeft"> Check list</span></h1>
      <ActionBar />
    </div>
    <div class="Content">
      <div class="Center NothingToShowUp" v-if="this.todoList == null || this.todoList.length <= 0 && error == null">
        Nothing to show up
      </div>
      <div class="Center" v-if="error != null" style="margin-top: 5px">
          {{error}}
      </div>
      <div class="ContentItemList"> 
        <TodoItem v-for="(item, index) in todoList" :key="index" :uid=item.uid :index=index /> 
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import ActionBar from '../components/ActionBar'
import TodoItem from '../components/TodoItem'

const URL = "http://localhost:3000/todo/all";

export default {
  name: 'Home',
  components: {
    ActionBar, 
    TodoItem
  },
  data() {
    return {
      todoList: null,
      error: null
    }
  },
  mounted() {
    axios.get(URL).then((e) => {
      console.log(e);
      this.todoList = e.data
    }).catch(err => { 
      this.error = err;
      
    })
  },
}
</script>

<style scoped> 
.Home {
  background: #fff;
  padding: 2em;
  border-radius: 21px;
  box-shadow: 3px 4px 6px 0px #e8e8e8;
}
.HomeHeader {
  display: flex;
  padding: 10px 20px;
}
.HomeHeader > * {
  display: block;
}
.HomeTitle {
  padding: 0;
  margin: 0;
  width: 100%;
  text-transform: uppercase;
  font-weight: 300;
}
.Center {
  text-align: center;
}
.ContentItemList {
  margin-top: 1em;
}
.NothingToShowUp {
  font-size: 18pt;
  font-weight: 300;
}
</style>