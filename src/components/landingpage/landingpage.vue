<template lang="html">
  <div class="landing-container">
    <h1>landingPage??</h1>
    <img class="logo"src="../../../img/logo.png" alt="NomNom logo">

  </div>

</template>

<script>
export default {
  props: [],
  data:function(){
    return {
      img:''

    };
  }
}
</script>

<style scoped lang="css">
.landing-container, .landing-container *{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
h1{
  margin: 1rem;
  color: #fff;
  font-family: arial,sans-serif;
}

.landing-container{
  background: url('../../../img/background-home.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  background-color: pink;
  width: 100;
  height: 80vh;
}
.logo{
  width: 100px;
}

</style>
