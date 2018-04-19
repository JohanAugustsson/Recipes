<template lang="html">
<div class="allRecipes-container">
  <div class="siteHeadlineContainer">
    <h1 class="siteHeadline" v-if="currentSiteStatus==='allRecipesSite'" >Alla Recept</h1>
    <h1 class="siteHeadline" v-if="currentSiteStatus==='favoRecipeSite'" >Valda Recept</h1>
  </div>
  <div v-if="currentSiteStatus==='allRecipesSite'" v-for="(item,index) in loopThrough" class="recipeCard">
    <div @click="showRecipe(index)" v-bind:style="{ 'background-image': 'url(' + item.recipeImgUrl + ')' }" class="recipeImg-holder">
    </div>
    <div class="recipeInfo">
      <h3 @click="showRecipe(index)">{{item.title}}</h3>
      <p @click="showRecipe(index)">{{item.textInfo}}</p>
      <div class="ingrediens-pickMe">
        <p class="ingrediensStyle"> {{Object.keys(item.ingridience).length}} ingredienser</p>

        <a v-if="item.isFavo === false" v-on:click.prevent='hartChosen(item,index)' href="" key='emtyHart' title="Välj och spara mig Valda recept"><i class="far fa-heart"></i> välj mig</a>
        <a v-else v-on:click.prevent='hartChosen(item,index)' href="" key='fullHart' title="Ta bort det här receptet från Valda recept"><i class="fas fa-heart"></i> Vald</a>
      </div>
    </div>
  </div>
  <div v-if="currentSiteStatus==='favoRecipeSite' && item.isFavo===true" v-for="(item,index) in loopThrough" class="recipeCard">
    <div @click="showRecipe(index)" v-bind:style="{ 'background-image': 'url(' + item.recipeImgUrl + ')' }" class="recipeImg-holder">
    </div>
    <div class="recipeInfo">
      <h3 @click="showRecipe(index)">{{item.title}}</h3>
      <p @click="showRecipe(index)">{{item.textInfo}}</p>
      <div class="ingrediens-pickMe">
        <p> {{Object.keys(item.ingridience).length}} ingredienser</p>

        <a v-if="item.isFavo === true" v-on:click.prevent='hartChosen(item,index)' href="" title="Ta bort det här receptet från Valda recept"><i class="fas fa-times"></i> Ta bort</a>
      </div>
    </div>
  </div>

  <!-- <div v-else-if="whichRecipeSite==='myRecipesSite' && item.isFavo===false" class="">
    <p>Du har för tillfället inte valt några recept</p>
  </div> -->
</div>

</template>

<script>
//import "../../../static/web-fonts-with-css/css/fontawesome-all.css";
 import "../../../static/fontAwsome/fontawesome-all.js";
export default {
  props:['loopThrough', 'currentSiteStatus'],
  data: function() {
    return {
      ingrediens: 12,
      isFavorite: false,
      currentRecipeSite: this.currentSiteStatus,
      chosenRecepieList: []



    };
  }, // data
  methods: {
    hartChosen:function(item,index){
      this.$emit('chosen-recipe', {
        type:'changeFavo',
        item:item,
        index:index
      })
    },
    showRecipe:function(index){
      this.$emit('chosen-recipe',{
        type:'selectMe',
        index:index
      })
    }

  } // methods
} // export default
</script>

<style scoped lang="css">
h1{
font-family: 'Varela Round', sans-serif;
}
p,h3{
  font-family: 'Raleway', sans-serif;
}

a,.ingrediensStyle{
  font-family: arial,sans-serif;
}

a{
  text-decoration: none;
  color: navy;
  font-weight: bold;
}
.siteHeadlineContainer{
  width: 100%;
  display: flex;

}
h1.siteHeadline{
  margin-left: 6.5rem;

  align-self: flex-start;
}
.allRecipes-container *{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.allRecipes-container{
  margin-top: 1rem;
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-between;

}
.recipeCard{
  margin: 1rem 0rem;
  width: 45%;
  min-width: 320px;

  background-color: powderblue;
  display: flex;
  flex-basis: 40%;
}

.allRecipes-container>.recipeCard:nth-child(even){
  margin-left: 6.5rem;
}
.allRecipes-container>.recipeCard:nth-child(odd){
  margin-right: 6.5rem;
}
.recipeImg-holder{
  margin-right: 1rem;
  width: 400px;
  min-width: 200px;
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

@media all and (max-width:1300px){

  .allRecipes-container{
    flex-direction: column;
    align-items: center;
    flex-wrap: nowrap;
  }
  .recipeCard{
    width: 80%;
    flex-basis: 100%;
  }
  .allRecipes-container>.recipeCard:nth-child(even){
    margin-left: 0;
  }
  .allRecipes-container>.recipeCard:nth-child(odd){
    margin-right: 0;
  }
  .siteHeadlineContainer{
    width: 80%;
  }
  h1.siteHeadline{
    margin-left: 0;
    align-self: flex-start;
  }

}
@media all and (max-width:600px){
  .recipeCard{
    width: 100%;
  }
  .siteHeadlineContainer{
    align-items: center;
    text-align: center;
  }
  h1.siteHeadline{
    text-align: center;
    align-self: center;
  }
}
@media all and (max-width:500px){
  .ingrediens-pickMe{
    width: 100%;
    flex-direction: column;
  }
  .ingrediens-pickMe>p{
    margin-bottom: 1rem;
  }
}

</style>
