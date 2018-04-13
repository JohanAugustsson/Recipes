<template lang="html">
  <div class="container-Selected">
    <div class="selectedTitle">
      <h2>{{ selected.title }}</h2>
    </div>

    <div class="container-HowToCook">
      <h3>Så här gör du:</h3>
      <ul>
        <li v-for="(steps ,index ) in selected.howToCook">

          <label class="wrapper-checkbox">
              <input type="checkbox" />  <!-- checkbox som är osynlig -->
              <div class="iconForChecked"><i class="fas fa-arrow-circle-right fa-lg"></i></div> <!-- synlig när checkbox är checked -->
              {{ index }}
              {{ steps }}
          </label>
        </li>
      </ul>
    </div>

    <div class="container-Ingridience">
      <h3>Ingridienser:</h3>
      <ul>
        <li v-for="item in selected.ingridience">
          {{ item.unit }}
          {{ item.name }}
        </li>
      </ul>
    </div>
    <img src="./pancake.jpg" alt="pancake" />








  </div>
</template>

<script>

export default {
  props: ["selected"]
}
</script>

<style scoped lang="css">
  .container-Selected{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  .selectedTitle{
    font-size: 1.3em;
    display: block;
    flex: 1 100%;
  }
  .container-Ingridience{
    flex: 1 40%;
    padding: 5px;
  }
  .container-HowToCook{
    flex: 1 40%;
    padding: 5px;
  }

  ul{
    list-style-type: none;
  }
  ul li{
    margin: 10px;
    font-size: 1.1em;
  }
  input {
    display: none;
  }

  .iconForChecked{
    display: none;
    position: absolute;
    left: 15px;
  }

  input:checked ~ .iconForChecked{
    display: inline-block;
    position: absolute;
    color: rgb(69, 168, 21);
  }

</style>
