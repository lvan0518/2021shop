<template>
  <div id="home" class="wrapper">
    <navbar class="home-nav">
      <div slot="center">购物街</div>
    </navbar>
  </div>
</template>

<script>
  import navbar from '../../components/common/navBar/NavBar'
  export default {
    name:"Home",
    components:{
      navbar
    }
  }
</script>

<style scoped>
  .home-nav {
    background-color:var(--color-tint);
    color:#fff;
  }
</style>
