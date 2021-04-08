<template>
  <div id="app">
    <Header></Header>
    <div class="main">
      <router-view name="slidebar"></router-view>
      <router-view name="main"></router-view>
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from "./components/Header";
import PostList from "./components/PostList";
import Footer from "./components/Footer";

export default {
  name: 'App',
  components:{
    Header,
    Footer
  }
}
</script>

<style scoped>
.main{
  /*width: 80%;*/
  margin: 15px auto;
  padding: 0 10%;
  min-height: 85vh;
}
@media only screen and (min-width: 0px) and (max-width: 414px) {
  #app {
    font-size: 14px;
  }
}
</style>
