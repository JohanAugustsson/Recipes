<template lang="html">
  <div class="landing-container">
    <div class="logo-container">
      <img class="logo"src="../../../img/logo.png" alt="NomNom logo">
    </div>
    <div class="landing-text">
      <h1>Välkommen till NomNom</h1>
      <p>Receptsidan där du får de bästa matipsen</p>
      <button class="cta-all" type="button" name="button">Upptäck våra bästa recept</button>
    </div>

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

h1,p{
  font-family: arial, sans-serif;
  color: #232332;
}
.landing-container, .landing-container *{
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;
  align-items: center;
  align-content: center;
}
.logo-container{
  padding: 1rem;
  width: 100%;
  display: flex;
  justify-content: flex-start;
  flex-direction: row;
  align-items: center;
  align-content: center;
}
.logo-container>h1{
  padding-left: 1rem;
  color: #fff;
  font-family: arial,sans-serif;
}
.landing-text{
  margin-top: 2rem;
  padding: 2rem;
  background-color: rgba(225,225,225,0.8);
  width: 60%;
  min-width: 300px;
  height: 300px;
  border-radius: 5px;
}
.landing-text>h1, .landing-text>p{
  text-align: center;
}
.landing-text>p{
  font-style: italic;
  margin-top: 1.5rem;
}
.cta-all{
  margin-top: 4rem;
  padding: 0.7rem 2rem;
  background-color: #254991;
  border: none;
  border-radius: 10px;
  color: #fff;
  font-weight: bold;
}
.cta-all:hover{
    background-color: #1a366d;
}

.landing-container{
  background: url('../../../img/background-home.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  background-color: pink;
  width: 100;
  height: 100vh;
}
.logo{
  width: 90px;
}

</style>
