<template lang="html">
  <div v-bind:style="{ 'background-image': 'url('+ landingImg +')' }" class="landing-container">
    <div class="logo-container">
      <img class="logo"src="../../../img/logo.png" alt="NomNom logo">
    </div>
    <div class="landing-text">
      <img class="logo-big"src="../../../img/logo.png" alt="NomNom logo">
      <!-- <h1>Välkommen till NomNom</h1> -->
      <h1>Receptsidan där du får de bästa matipsen</h1>
      <!-- <button class="cta-all" type="button" name="button">Upptäck våra bästa recept</button> -->
    </div>

  </div>

</template>

<script>
export default {
  props: ['landingImg'],
  data:function(){
    return {
      img:''

    };
  }
}
</script>

<style scoped lang="css">

h1{
font-family: 'Varela Round', sans-serif;
}
p{
  font-family: 'Raleway', sans-serif;
}

h1,p{
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
  z-index: 3;
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
  margin-top: 10rem;
  padding: 2rem;
  background-color: rgba(225,225,225,0.8);
  width:100%;
  min-width: 300px;
  height: 300px;


  display: flex;

  align-items: center;
  flex-direction: column;
  position: absolute;
}
.logo-big{
  width: 200px;
  position: relative;
  top: -8rem;

}
.landing-text>h1{
  text-align: center;
  position: relative;
  bottom: 6rem;
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
  /* background: url('../../../img/background-home.jpg'); */
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  background-color: pink;
  width: 100;
  height: 100vh;
}
.logo{
  width: 70px;
  position: fixed;
  top: 1rem;
}

</style>
