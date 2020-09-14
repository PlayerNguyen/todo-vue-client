<template>
  <div id="app"> 
    <Navigator />

    <!-- Content view -->
    <div class="Content">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import Navigator from './components/Navigator'
export default {
  components: {
    Navigator
  }
}
</script>

<style> 
body {
  margin: 0;
  padding: 0;
  background: #f5f5f5;
}
#app, input {
  font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Oxygen-Sans,Ubuntu,Cantarell,"Helvetica Neue",sans-serif;
}
.Content {
  padding: 1.8em;
}
</style>
