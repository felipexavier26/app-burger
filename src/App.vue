<template>
  <div>
    <NavBar :logo="logo_scr" :alt="app_name" />
    <router-view />
    <Footer />
  </div>
</template>



<script>
import NavBar from './components/header/NavBar.vue';
import Footer from './components/footer/Footer.vue';


export default {
  components: {
    NavBar,
    Footer,
  },
  data() {
    return {
      logo_scr: '/img/logo.png',
      app_name: 'Make Your Burger'
    }
  }
}
</script>



<style>
* {
  font-family: 'Helvetica';
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.main-container {
  margin: 50px;
  min-height: 350px;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}
</style>