<template lang="html">
  <div class="container-Selected">
    <div class="selectedTitle">

        <h2>{{ selected.title }}</h2>

      <div class="container-btn">
          <button ref="btnEdit" @click="editRecipe"><i class="fas fa-pencil-alt"></i> Redigera </button>
          <button><i class="fas fa-heart"></i> Ta bort </button>
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
    <img src="./pancake.jpg" alt="pancake" />
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
      this.$emit('add-HowToCook', {
           type: "update",
           index: index,
           textToAdd : event.target.value

			});
    },
    removeHowToCook: function(index){
      this.$emit('add-HowToCook', {
        type: "remove",
        index: index
			});
    },
    addHowToCook: function(event){
      let textToAdd = this.$refs.textToAdd
      let fail = false;
      if(textToAdd.value==""){fail = true}

      if(!fail){
        this.$emit('add-HowToCook', {
          type: "add",
          textToAdd : textToAdd.value
        });
        textToAdd.value="";
        textToAdd.focus();
      }
    },
    updateIngridience: function (event,index){
      console.log( "event:" , event.target );
      console.log( "index:" , index );
    },
    removeIngridience: function (index){
      console.log( "index:" , index);
    },
    addIngridience: function(event){
      let textToAddToIngridience = this.$refs.textToAddToIngridience
      let fail = false;
      if(textToAddToIngridience.value==""){fail = true}
      if(!fail){
        this.$emit('add-HowToCook', {
          type: "addIngridience",
          textToAdd : textToAddToIngridience.value
        });
        textToAddToIngridience.value="";
        textToAddToIngridience.focus();
      }
      console.log( "ingridience" , textToAddToIngridience.value);
    }
  }
}


</script>

<style scoped lang="css">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .container-Selected{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  .selectedTitle{
    position: relative;
    display: flex;
    flex-wrap: wrap;
    font-size: 1.3em;
    display: block;
    flex: 1 100%;
    margin: 50px;
  }
  .selectedTitle h2{
    flex: 1 20%;
  }
  .selectedTitle .container-btn{
    position: absolute;
    right: 10%;
    top: 10px;

  }
  .container-Ingridience, .container-HowToCook{
    display: flex;
    flex-wrap: wrap;
    flex: 1 49%;
    padding: 5px;
    justify-content: center;
  }
  .container-HowToCook{
    display: flex;
    flex-wrap: wrap;
    flex: 1 40%;
    padding: 5px;
    justify-content: center;
    margin-left: 40px;
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
    margin: 5px 0px;

  }
  button{
    padding: 5px;

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
