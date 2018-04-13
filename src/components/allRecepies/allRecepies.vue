<template lang="html">

  <div  class="recipeCard">
    <div class="recipeImg-hoder">
      <img class="recipeImg" src="https://aomeassetsprod.blob.core.windows.net/editorial/import/images/2011-11-09/mandel-och-majspannkakor.jpg" alt="bild">

    </div>
    <div class="recipeInfo">
      <h3>tilel på recept</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
         incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud
         exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure.
       </p>
       <div class="ingrediens-pickMe">
         <p> {{antalIngred}} ingredienser</p>
         <a href=""><i class="fas fa-heart"></i> välj mig</a>
       </div>
    </div>
  </div>

</template>

<script>
export default {
}
</script>

<style scoped lang="css">

.recipeImg-hoder{
  margin-right: 1rem;
  width: 200px;
}
.recipeImg{
  margin-top: 1rem;
  width: 100%;
}
.recipeCard{
  width: 40%;
  min-width: 320px;

  background-color: powderblue;
  display: flex;
}
.recipeInfo{
  width: 100%;
  flex-direction: column;

}
.ingrediens-pickMe{
  display: flex;
  flex-direction: row;
  justify-content: space-between;

}
</style>
