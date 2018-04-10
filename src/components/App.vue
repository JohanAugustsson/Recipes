<template>
  <div id="app">

    <p> Hej</p>
    <p>Hej på dig</p>
    <p>okej</p>
    <one-recipe :selected="selectedRecipe"/> <!--Visar ett recept -->
  </div>
</template>

<script>
  import oneRecipe from './oneRecipe/oneRecipe.vue';
  const recipesObject = require('../mocks/recipes.json');  // databas: json object med alla recept som vi har.
  console.log(recipesObject);

  export default {
    name: 'app',
    data: function(){
      return{
        recipesObject : recipesObject,
        selectedRecipe : recipesObject[0]
      }
    },
    components: {
      "one-recipe" : oneRecipe
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
