<template lang="html">
<div class="allRecipes-container">
  <div  class="recipeCard">
    <div class="recipeImg-holder">

    </div>
    <div class="recipeInfo">
      <h3>tilel på recept</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
        incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud
        exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure.
      </p>
      <div class="ingrediens-pickMe">
        <p> {{ingrediens}} ingredienser</p>
        <a href=""><i class="fas fa-heart"></i> välj mig</a>
      </div>
    </div>
  </div>
</div>

</template>

<script>
export default {
  data:function(){
    return {
      ingrediens: 12,
    };
  }
}
</script>

<style scoped lang="css">

.allRecipes-container *{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.allRecipes-container{
  width: 100%;
}
.recipeCard{
  margin: 1rem;
  width: 45%;
  min-width: 320px;

  background-color: powderblue;
  display: flex;
}

.recipeImg-holder{
  margin-right: 1rem;
  width: 400px;
  background: url('https://i.ytimg.com/vi/FLd00Bx4tOk/maxresdefault.jpg');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;

}
.recipeImg{
  margin-top: 1rem;
  width: 100%;
}
.recipeInfo{
  margin: 1rem;
  width: 100%;
  flex-direction: column;

  justify-content: space-between;

}
.ingrediens-pickMe{
  display: flex;
  flex-direction: row;
  justify-content: space-between;

}
</style>
