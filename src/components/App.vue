<template>
  <div id="app">


    <landing-page/>
   <all-recipes :loopThrough="allFoodObj"/>   <!--loopar igenom alla recept -->

    <one-recipe v-on:add-HowToCook="editRecipe" :selected="selectedRecipe"/> <!--Visar ett recept -->

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
        allFoodObj: recipesObject

      }
    },
    components: {
      "one-recipe" : oneRecipe,
      "all-recipes": allRecipes,
      "landing-page": landingPage
    },
    methods: {
      editRecipe: function(Obj){
        if(Obj.type === "add"){
          let sum = Object.keys((this.selectedRecipe.howToCook))  //tittar på nyckeln som ligger sist och adderar 1.
          sum = Number(sum[sum.length-1])
          if(!isNaN(sum)){
            sum++
          }else{
            sum = 1;
          }
          console.log(sum);
          this.$set(this.selectedRecipe.howToCook, sum, Obj.textToAdd) // måste använda $set för att vue ska detektera uppdateringen
        }
        if(Obj.type === "update"){
          this.$set(this.selectedRecipe.howToCook, Obj.index, Obj.textToAdd)
        }
        if(Obj.type === "remove"){
          this.$delete(this.selectedRecipe.howToCook, Obj.index);
        }

      }
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
