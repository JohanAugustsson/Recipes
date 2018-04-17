<template lang="html">
<div class="allRecipes-container">
  <div v-if="whichRecipeSite==='allRecipesSite'" v-for="(item,index) in loopThrough" class="recipeCard">
    <div v-bind:style="{ 'background-image': 'url(' + item.recipeImgUrl + ')' }" class="recipeImg-holder">
    </div>
    <div class="recipeInfo">
      <h3>{{item.title}}</h3>
      <p>{{item.textInfo}}</p>
      <div class="ingrediens-pickMe">
        <p> {{Object.keys(item.ingridience).length}} ingredienser</p>

        <a v-if="item.isFavo === false" @click.prevent='hartChosen(item,index)' href=""><i class="far fa-heart"></i> välj mig</a>
        <a v-if="item.isFavo === true" @click.prevent='hartChosen(item,index)' href=""><i class="fas fa-heart"></i> Vald</a>
      </div>
    </div>
  </div>

  <div v-if="whichRecipeSite==='myRecipesSite' && item.isFavo===true" v-for="item in loopThrough" class="recipeCard">
    <div class="recipeImg-holder">
    </div>
    <div class="recipeInfo">
      <h3>{{item.title}}</h3>
      <p>
        {{item.textInfo}}
      </p>
      <div class="ingrediens-pickMe">
        <p> {{ingrediens}} ingredienser</p>

        <a v-if="item.isFavo === true" @click.prevent='hartChosen(item,index)' href=""><i class="fas fa-heart"></i> Vald</a>
      </div>
    </div>
  </div>

  <!-- <div v-else-if="whichRecipeSite==='myRecipesSite' && item.isFavo===false" class="">
    <p>Du har för tillfället inte valt några recept</p>
  </div> -->
</div>

</template>

<script>
  import "../../../static/fontAwsome/fontawesome-all.js";
export default {
  props:['loop-through'],
  data: function() {
    return {
      ingrediens: 12,
      isFavorite: false,
      whichRecipeSite: 'allRecipesSite',
      chosenRecepieList: [],


    };
  }, // data
  methods: {
    hartChosen:function(item,index){
      this.$emit('chosen-recipe', {
        item:item,
        index:index
      })
    }

  } // methods
} // export default
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
  flex-wrap: wrap;
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
