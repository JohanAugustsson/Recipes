<template lang="html">
  <div class="container-Selected">

    <div class="container-btn">
      <span v-if="!editText">
        <button key="redigera" ref="btnEdit" @click="editRecipe">
          <i class="fas fa-pencil-alt"></i> Redigera
        </button>
      </span>
      <span v-else>
        <button key="spara" ref="btnEdit" @click="editRecipe">
          <i class="fas fa-save"></i> Spara
        </button>
      </span>

      <span>
        <button v-if="selected.isFavo === false" key='emtyHart' @click="changeFavo"><i class="far fa-heart"></i> välj mig</button>
        <button v-else key='fullHart' @click="changeFavo"><i class="fas fa-times"></i> Stryk från vald</button>
      </span>
    </div>

    <div class="selectedTitle">




      <div class="container-edit">
        <span v-if="!editText">
          <h2> {{ selected.title }} </h2>
          <p> {{ selected.textInfo }} </p>
        </span>

        <span v-else>
          Titel: <br/>
          <h2><textarea ref="updateTitelText" :value="selected.title" @change="updateTitle($event)" /></h2><br/>
          Infotext: <br/>
          <textarea class="textAreaForInfoText" ref="updateInfoText" :value="selected.textInfo" @change="updateInfoText($event)" /><br/>
          Url för bild:<br/>
          <input class="inputForUpdateImg"  type="text" ref="updateUrlForImage" :value="selected.recipeImgUrl" @change="updateImageUrl($event)" />
        </span>
      </div>






    </div>

    <div class="container-HowToCook">
      <ul>
        <h3>Så här gör du:</h3>

        <li v-for="(steps ,index ) in selected.howToCook">
          <div v-if="!editText">
            <label class="wrapper-checkbox">
              <input class="inputCheckbox" type="checkbox" />  <!-- invisible checkbox -->
              <span></span>
              <div class="iconForChecked"><i class="far fa-check-square fa-lg"></i></div> <!-- icon is visible when checkbox is checked -->
              {{ steps }}
            </label>
          </div>
          <div v-else class="inputForTodoList"> <!-- Edit text in todo list -->
            <textarea :value="steps" @change="updateHowToCook($event,index)" />
            <button @click="removeHowToCook(index)"><i class="far fa-trash-alt"></i></button>
          </div>
        </li>

          <div v-if="editText" class="inputForTodoList"> <!-- Add to todo list -->
            <textarea ref="textToAdd" />
            <button @click="addHowToCook" class="btnAddHowToCook"><i class="fas fa-plus"></i></button>
          </div>
      </ul>
    </div>

    <div class="container-Ingridience">
      <ul>
        <h3>Ingridienser:</h3>
        <li v-for="(item,index) in selected.ingridience">
          <div v-if="!editText">
            {{ item }}

            <hr/>
          </div>
          <div v-else class="inputForIngridienceList"> <!-- Edit text in ingridience list -->
            <textarea :value="item" @change="updateIngridience($event,index)" />
            <button @click="removeIngridience(index)"><i class="far fa-trash-alt"></i></button>
          </div>
        </li>

        <div v-if="editText" class="inputForIngridienceList"> <!-- Add to ingridience list -->
          <textarea ref="textToAddToIngridience" />
          <button @click="addIngridience" class="btnAddHowToCook"><i class="fas fa-plus"></i></button>
        </div>

      </ul>
    </div>

  </div>
</template>

<script>
export default {
  props: ["selected"],
  data: function(){
    return{
      editText : false
    }
  },
  methods:{
    editRecipe: function(index){
      this.editText = !this.editText;
    },
    updateHowToCook: function(event,index){
      this.$emit('edit-recipe', {
           type: "update",
           index: index,
           textToAdd : event.target.value
			});
    },
    removeHowToCook: function(index){
      this.$emit('edit-recipe', {
        type: "remove",
        index: index
			});
    },
    addHowToCook: function(event){
      let textToAdd = this.$refs.textToAdd
      let fail = false;
      if(textToAdd.value==""){fail = true}
      if(!fail){
        this.$emit('edit-recipe', {
          type: "add",
          textToAdd : textToAdd.value
        });
        textToAdd.value="";
        textToAdd.focus();
      }
    },
    updateIngridience: function (event,index){
      this.$emit('edit-recipe', {
           type: "updateIngridience",
           index: index,
           textToAdd : event.target.value
			});
    },
    removeIngridience: function (index){
      this.$emit('edit-recipe', {
        type: "removeIngridience",
        index: index
      });
    },
    addIngridience: function(event){
      let textToAddToIngridience = this.$refs.textToAddToIngridience
      let fail = false;
      if(textToAddToIngridience.value==""){fail = true}
      if(!fail){
        this.$emit('edit-recipe', {
          type: "addIngridience",
          textToAdd : textToAddToIngridience.value
        });
        textToAddToIngridience.value="";
        textToAddToIngridience.focus();
      }
    },
    updateTitle: function(event){
      let updateTitelText = this.$refs.updateTitelText
      this.$emit('edit-recipe', {
        type: "updateTitle",
        textToAdd: updateTitelText.value
      });
    },
    updateInfoText: function(event){
      let updateInfoText = this.$refs.updateInfoText

      this.$emit('edit-recipe', {
        type: "updateInfoText",
        textToAdd: updateInfoText.value
      });
    },
    updateImageUrl : function(event){
      this.$emit('edit-recipe', {
        type: "updateImgUrl",
        textToAdd: event.target.value
      });
    },
    changeFavo: function(){
      let favoStatus = !this.selected.isFavo
      this.$emit('edit-recipe', {
        type: "changeFavo",
        favoStatus: favoStatus
      });
    }
  }
}
</script>

<style scoped lang="css">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Raleway', sans-serif;
  }
  h1,h3,h2{
  font-family: 'Varela Round', sans-serif;
  }
  .container-edit p{
    margin-top: 1rem;
  }
  .container-Selected{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    width: 80%;
    margin: 1rem auto;
  }
  .selectedTitle{
    position: relative;
    display: flex;
    flex-wrap: wrap;
    font-size: 1.3em;
    flex: 1 100%;
    margin: 50px;
  }
  textarea{
    resize: none;
    width: 80%;
  }
  .selectedTitle div{
    flex: 1 40%;
  }
  .container-btn{
    display: flex;
    justify-content: flex-end;
    flex-wrap: nowrap;
    width: 100%;
  }
  .container-Ingridience, .container-HowToCook{
    display: flex;
    flex-wrap: wrap;
    flex: 1 30%;
    padding: 5px;
    justify-content: center;
  }
  .container-HowToCook{
    flex: 1 46%;
    margin-left: 40px;
  }
  .inputForUpdateImg{
    width: 80%;
    font-size: 0.8em;
  }
  h3{
    flex: 1 95%;
  }
  ul{
    list-style-type: none;
    min-width: 300px;
    padding: 0px;
    flex: 1 90%;
  }
  ul li{
    margin: 1.5rem 0px 1.5rem 0px;
  }
  .container-HowToCook>ul>li{
    margin: 1.5rem 0px 1.5rem 0px;
  }
  button{
    padding: 5px;
  }
  .container-btn button{
    width: 200px;
    background: none;
    border: none;
    outline: none;
    font-size: 1.5em;
  }
  .container-HowToCook label:hover{
    cursor: pointer;
  }
  .container-btn button:hover{
    cursor: pointer;
  }
  .btnAddHowToCook{
    background-color: rgb(96, 239, 107);
  }
  .inputForTodoList, .inputForIngridienceList{
    display: flex;
  }
  .inputForTodoList textarea, .inputForIngridienceList textarea{
    flex: 1 80%;
    padding: 5px;
  }
  .textAreaForInfoText{
    height: 200px;
    margin-bottom: 1rem;
  }
  /* För checkbox*/
  .inputCheckbox {
    display: none;
  }
  .iconForChecked{
    position: absolute;
    left: -30px;
    top: -2px;
    visibility: hidden;
    opacity: 0;
    transition: visibility 0s, opacity 0.2s linear;
  }
  .inputCheckbox:checked ~ .iconForChecked{
    visibility: visible;
    opacity: 1;
    position: absolute;
    color: rgb(69, 168, 21);
  }
  .wrapper-checkbox{
    position: relative;
  }
  .wrapper-checkbox  span{
    width: 18px;
    height: 18px;
    border: 1px solid #c8c8c8;
    position: absolute;
    left: -30px;
    border-radius: 3px;
  }
/* För checkbox END*/
</style>
