<template>
  <div>
    <img src="./LandingPageView/assets/logo.png" alt="electron-vue">
    <h1>Welcome.</h1>
    <current-page></current-page>
    <versions></versions>
    <tr-status></tr-status>
    <links></links>
  </div>
</template>

<script>
  import CurrentPage from './LandingPageView/CurrentPage';
  import Links from './LandingPageView/Links';
  import Versions from './LandingPageView/Versions';
  import TrStatus from './LandingPageView/TrStatus';
  export default {
    components: {
      CurrentPage,
      Links,
      Versions,
      TrStatus,
    },
    name: 'landing-page',
  };
</script>

<style scoped>
  img {
    margin-top: -25px;
    width: 450px;
  }
</style>
