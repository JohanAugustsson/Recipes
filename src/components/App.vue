<template>
  <div id="app">
    <i class="fas fa-heart"></i>

    <landing-page/>
    <all-recipes/>

    <one-recipe :selected="selectedRecipe"/> <!--Visar ett recept -->
  </div>
</template>

<script>
  import "../../static/fontAwsome/fontawesome-all.js";
  import landingPage from './landingpage/landingpage.vue'
  import oneRecipe from './oneRecipe/oneRecipe.vue';
  import allRecipes from './allRecepies/allRecepies.vue'
  const recipesObject = require('../mocks/recipes.json');  // databas: json object med alla recept som vi har.

  console.log(recipesObject);

  export default {
    name: 'app',
    data: function(){
      return{
        recipesObject : recipesObject,
        selectedRecipe : recipesObject[0],

      }
    },
    components: {
      "one-recipe" : oneRecipe,
      "all-recipes": allRecipes,
      "landing-page": landingPage
    }
  }
</script>

<!-- CSS libraries -->
<style src="normalize.css/normalize.css"></style>

<!-- Global CSS -->
<style>

</style>

<!-- Scoped component css -->
<!-- It only affect current component -->
<style scoped>

</style>
