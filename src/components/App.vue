<template>
  <div id="app">


    <landing-page :landingImg='currentLandingImg'/>
    <div class="navMenu">
      <button @click="changeSite('allRecipesSite')"  type="button" name="button">Alla Recept</button>
      <button @click="changeSite('favoRecipeSite')"  type="button" name="button">Valda Recept</button>
    </div>


    <!-- <button @click="addRecipe">Lägg till recept</button> -->
   <all-recipes v-if="currentSite==='allRecipesSite' || currentSite==='favoRecipeSite' " v-on:chosen-recipe="chosenRecipe"  :loopThrough="allFoodObj" :currentSiteStatus="currentSite"/>   <!--loopar igenom alla recept -->

    <one-recipe v-else v-on:edit-recipe="editRecipe" :selected="selectedRecipe"/> <!--Visar ett recept -->
  </div>
</template>

<script>
  //import "../../static/web-fonts-with-css/css/fontawesome-all.css";
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
        allFoodObj: recipesObject,
        currentSite: 'allRecipesSite',
        currentLandingImg: '../../../img/background-home.jpg'

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
          this.$set(this.selectedRecipe.howToCook, sum, Obj.textToAdd) // måste använda $set för att vue ska detektera uppdateringen
        }

        if(Obj.type === "update"){
          this.$set(this.selectedRecipe.howToCook, Obj.index, Obj.textToAdd)
        }

        if(Obj.type === "remove"){
          this.$delete(this.selectedRecipe.howToCook, Obj.index);
        }

        if(Obj.type === "addIngridience"){
          let sum = Object.keys((this.selectedRecipe.ingridience))  //tittar på nyckeln som ligger sist och adderar 1.
          sum = Number(sum[sum.length-1])
          if(!isNaN(sum)){
            sum++;
          } else {
            sum = 1;
          }
          this.$set(this.selectedRecipe.ingridience, sum, Obj.textToAdd) // måste använda $set för att vue ska detektera uppdateringen
        }

        if(Obj.type === "removeIngridience"){
            this.$delete(this.selectedRecipe.ingridience, Obj.index);
        }

        if(Obj.type === "updateIngridience"){
            this.$set(this.selectedRecipe.ingridience, Obj.index, Obj.textToAdd)
        }

        if(Obj.type === "updateTitle"){
            this.$set(this.selectedRecipe, "title", Obj.textToAdd)
        }
      },
      addRecipe : function(){
        let sum = this.recipesObject.length
        sum = this.recipesObject[sum-1].id + 1; // tar sista objektets id och plussar på 1.

        let obj = {
          "id" : sum,
          "title" : "Ange Titel",
          "cookingTime" : "",
          "ingridience" :{
            "1" : "Ingridienser"
          },
          "howToCook" : {
              "1" : "Fyll i hur du tillagar"
          }
        }
        this.selectedRecipe = this.recipesObject[sum-1] // väljer de nya receptet
        this.recipesObject.push(obj)

      },
      chosenRecipe:function(obj){

       if (obj.type === 'changeFavo') {
         obj.item.isFavo = !obj.item.isFavo;
         this.$set(this.allFoodObj, obj.index, obj.item)
       }
       if (obj.type === 'selectMe') {
          console.log(obj.index);
          this.currentSite = 'oneRecipeSite';
          this.selectedRecipe = this.recipesObject[obj.index];
          this.currentLandingImg = this.recipesObject[obj.index].recipeImgUrl;
          console.log(this.currentLandingImg);
       }

      },
      changeSite:function(site){
        console.log(site);
        this.currentSite = site;
        this.currentLandingImg = '../../../img/background-home.jpg';

      }
    } // methods End

  }
</script>

<!-- CSS libraries -->
<style src="normalize.css/normalize.css"></style>

<!-- Global CSS -->
<style>
@import url('https://fonts.googleapis.com/css?family=Raleway|Varela+Round');
h1{
font-family: 'Varela Round', sans-serif;
}
p{
  font-family: 'Raleway', sans-serif;
}

</style>

<!-- Scoped component css -->
<!-- It only affect current component -->
<style scoped>

  #app{
    margin-bottom: 50vh;
  }
  .navMenu{
    position: -webkit-sticky;
    position: sticky;
    top: -1px;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    width: 100%;

    display: flex;
  }
  .navMenu>*{
    width: 50%;
    height: 100%;
    padding: 0.5rem;

    border: none;
  }
  .navMenu>button:first-child{
    background-color: #232332;
    color: #fff;
    font-weight: bold;
  }
  .navMenu>button:last-child{
    background-color: #0fd857;
    color: #232323;
    font-weight: bold;
  }
</style>
