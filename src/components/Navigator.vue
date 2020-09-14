<template>
  <div class="Navigator">

    <div class="NavContent"> 
      <ul>
        <li><router-link to="/">Home</router-link></li>
        <li><router-link to="/about">About</router-link></li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navigator",
   data() {
     return {
       
     }
   },
}
</script>

<style>
.Navigator {
  background: #fff;
  padding: .5em;
  border-bottom: 2px solid rgb(227, 227, 227);
}
.Navigator ul {
  list-style-type: none;
  display: inline-block;
  padding: 0;
  margin: 0;
}
.Navigator ul li {
  display: inline-block;
  /* padding: 1.2em; */
}
.Navigator ul li a{
  text-decoration: none;
  color: rgb(223, 90, 90);
  font-size: 15pt;
  text-transform: uppercase;
  font-weight: 500;
  margin-right: 1.8em;
}
.NavContent {
  padding: 1.2em;
}
</style>