<template>
  <div class="ActionBar">
    <a v-on:click="init" class="ActionBarButton"><i class="fas fa-plus"></i></a>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "ActionBar",
  methods: {
    init: () => {
      // Init with axios
      axios.post("http://localhost:3000/todo/init").then(e => {
        console.log(e.data)
      })

      location.reload();
    }
  },
}
</script>

<style>
.ActionBar {
  padding: 0.5em; 
  direction: rtl;
  width: 100%;
  
}
.ActionBarButton {
  background: #df5959;
  padding: 12px 14px;
  border-radius: 50%;
  color: #fff;
  cursor: pointer;
}
.ActionBarButton:hover {
  transform: rotate(90deg);
}
</style>