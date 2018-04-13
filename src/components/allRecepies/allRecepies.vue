<template lang="html">
<div class="allRecipes-container">
  <div v-for="item in loopThrough" class="recipeCard">
    <div class="recipeImg-holder">
    </div>
    <div class="recipeInfo">
      <h3>{{item.title}}</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
        incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud
        exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
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
  props:['loopThrough'],
  data: function() {
    return {
      ingrediens: 12,
    };
  }
}
</script>

<style scoped lang="css">

h3,p,a{
  font-family: arial,sans-serif;
}

a{
  text-decoration: none;
  color: navy;
  font-weight: bold;
}

.allRecipes-container *{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.allRecipes-container{
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;

}
.recipeCard{
  margin: 1rem 2rem;
  width: 45%;
  min-width: 320px;

  background-color: powderblue;
  display: flex;
  flex-basis: 45%;
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
  margin: 1rem 2rem 1rem 0;
  width: 100%;
  flex-direction: column;

  justify-content: space-between;
}
.recipeInfo>h3{
  text-transform: capitalize;
}
.recipeInfo>p{
  margin: 0.5rem 0 2rem 0;
}
.ingrediens-pickMe{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.ingrediens-pickMe>p{
  font-weight: bold;
}


</style>
