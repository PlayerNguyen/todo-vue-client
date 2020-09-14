<template>
  <div class="TodoItem animate__animated animate__fadeIn animate__delay-1s" :style="{'animation-duration': (index+1)/2 + 's'}" v-if="appearance"> 
    <!-- Remove -->
    <div class="TodoItemRemove animate__animated  animate__bounceIn animate__delay-1s" :style="{'--animate-delay': (index+2)/2+'s'}" @click="remove"> 
      <i class="fas fa-trash"></i>
    </div> 
    <!-- Circle checkbox -->
    <div class="TodoItemCheckBox" @click="toggleText" >
      <div class="TodoItemCheckBoxSpan animate__animated animate__bounceIn animate__delay-1s" v-if="itemData.checked == false" :style="{'--animate-delay': (index+2)/2+'s'}"></div>
      <div class="TodoItemCheckBoxSpan Active animate__animated animate__bounceIn animate__delay-1s" v-else :style="{'--animate-delay': (index+2)/2+'s'}">
        <!-- <span class="fas fa-check"></span> -->
      </div>
    </div> 
    <!-- TextComponents content -->
    <div class="TodoItemContent" :style="{'--animate-delay': (index+2)/2+'s'}"> 
      <input type="text"  @blur="update" v-model="itemData.contents" placeholder="Input your work here..." @keyup.enter="$event.target.blur()">
    </div>
  </div>
</template>

<script> 
import axios from 'axios'
export default {
  name: "TodoItem",
  props: [ 
    "uid", 
    "index"
  ],
  data() { 
    return {
      itemData: [], 
      appearance: true
    } 
  }, 
  created: function() {
    console.log("Position: " + this.index)
    axios.get(`http://localhost:3000/todo/id/${this.uid}`).then( (e) => {
      // console.log(this)
      this.itemData = e.data.message;
    }) 
  },
  methods: {
    set(e) {
      this.itemData.contents = e.target.textContent
    },
    toggleText() { 
      this.itemData.checked = !this.itemData.checked;
      this.update()
    },
    update: function () { 
      let _data = {
        uid: this.itemData.uid, 
        contents: this.itemData.contents,
        checked: this.itemData.checked
      }
      axios.post(`http://localhost:3000/todo/update`, _data).then(() => {
        // console.log(_data);
        // console.log(e.data);
      })
    },
    remove: function () {
      let _data = {
        uid: this.itemData.uid
      }
      axios.post(`http://localhost:3000/todo/remove`, _data).then(() => {
        console.info("Delete succeed " + _data.uid)
        this.appearance = false
      })
    }
  }
} 
</script> 

<style scoped>
.TodoItem {
  overflow:hidden;
  display: flex;
  cursor: pointer; 
  margin-bottom: 12px; 
}

.TodoItemCheckBox { 
  display: block;
  padding: 5px;
}
.TodoItemCheckBoxSpan {
  padding: 1em;

  margin: 10px;
  background: #808080;
  border-radius: 50%;
  transition: ease .2s;
}
.TodoItemCheckBoxSpan:hover {
  background: #bb7171;
}
.TodoItemCheckBoxSpan:active {
  background: #df5959;
}
.TodoItemContent {
  /* padding: 5px; */
  width: 100%;
  outline: 0;
  cursor: auto;
  font-size: 16pt; 
}
.TodoItemContent input {
  padding: 15px;
  width: 100%;
  outline: 0;
  cursor: auto;
  font-size: 16pt;
  background: transparent;
  border: 0;
  font-weight: 300;
  transition: ease .5s; 
}
.TodoItemContent input:focus {
  background: #f5f5f5;
}
.Active, .Active:hover {
  background: #df5959;
  /* border-bottom: 2px solid #794747; */
    /* border-right: 2px solid #794747; */
}
.TodoItemRemove {
  /* padding: 15px; */
  padding: 6px;
}
.TodoItemRemove i {
  padding: 15px;
  /* margin: 15px; */
  background: #fff;
  color: #cccbcb;
  border-radius: 50%;
  transition: ease .5s;
}
.TodoItemRemove i:hover {
  color: #df5959;
}
</style>