<script setup>
  import {ref, onMounted} from "vue";
  const count = ref(0);

  
  const config = ref()
  //var queryValues = ref(null)

  var modelQuery = "Cursa";
  var colorQuery = "red";
  var tiresQuery = "small";
  var interiorQuery = "super";
  var motorQuery = "big";
  
  const queryValues = ref({
    model: modelQuery,
    color: colorQuery,
    tires: tiresQuery,
    interior: interiorQuery,
    motor: motorQuery
  })

  //var currentQuery = "//localhost:8080/getOffer?model=Cursa&color=black&tires=small&interior=sport&motor=medium"
  //var query = "//localhost:8080/getOffer?model=Cursa&color=black&tires=small&interior=sport&motor=medium"
  /*
  const props = defineProps(['query'])
  console.log("App: console.log(props.query):")
  console.log(props.query)

  props.query = "//localhost:8080/getOffer?model=Cursa&color=black&tires=small&interior=sport&motor=medium"
  console.log("App: console.log(props.query):")
  console.log(props.query)
  */

  const props = defineProps(['query'])
  //props.query = "test374"

  var query = "testvalue"
  
  

  onMounted(() => {
    console.log(config.value);
    //queryValues = ref(document.getElementById("colors").value)
    console.log("Debug: log props.query in App")
    console.log(props.query)
    query = "onMounted test value debug"
  })


  function changedColor() {
    console.log(config.value);
  }


  

</script>

<script>
  import Calculation from './components/Calculation.vue'
  import Configuration from './components/Configuration.vue'

  import axios from "axios"

  //var query = "//localhost:8080/getOffer?model=Cursa&color=black&tires=small&interior=sport&motor=medium"

  
  export default {
    name: "App",
    components: { Calculation },
    data() {
      return {
        query: "Link here"
      }
    },
    mounted() {
      console.log("hallo vue")
      console.log(this)
    },
    methods: {
      updateQuery(newValue) {
        this.query = newValue;
        console.log("TESTTEST" + newValue);
      },
      redoCalculation() {
        /*console.log("test123");
        console.log(queryValues.value.color);

        queryValues.value.model = "Cursa";
        queryValues.value.color = document.getElementById("colors").value;
        queryValues.value.tires = document.getElementById("tires").value;
        queryValues.value.interior = document.getElementById("interior").value;
        queryValues.value.motor = document.getElementById("motors").value;

        query = "//localhost:8080/getOffer?model=Cursa&color=" + queryValues.value.color.slice(0, -1) + "&tires=" + queryValues.value.tires.slice(0, -1) + "&interior=" + queryValues.value.interior.slice(0, -1) + "&motor=" + queryValues.value.motor.slice(0, -1)

        console.log("Debug: log query in App");
        console.log(query);

        console.log(queryValues.value.color.slice(0, -1));*/
        console.log("test")
        this.$refs['calc'].updateCalculation();

      }
    }
  }


  /*
  export default {
    props: ['query'],
    setup(props) {
      setup()
      console.log("Debug: log props.query")
      console.log(props.query)
    }
  }
  */
  
</script>



<template>

    
  <nav id="navid" class="navbar navbar-expand navbar-dark bg-primary d-flex justify-content-center row border-bottom border-dark">
    <div class="col col-8 d-flex justify-content-between">
      <a class="navbar-brand" href="#">Opal Autokonfigurator</a>
      <div id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <a class="nav-item nav-link active" href="#">Startseite</a>
          <a class="nav-item nav-link" href="#">Features</a>
          <a class="nav-item nav-link" href="#">Preise</a>
        </div>
      </div>
    </div>
  </nav>


  <main id="main-div" class="row d-flex justify-content-center">

    <div id="title" class="col col-8">
      <h3>Wählen Sie Ihre gewünschte Konfiguration für<br>Opal Cursa</h3>
    </div>
        

    <div class="col col-8">

      <div id="config-all" class="row d-flex justify-content-evenly flex-wrap">
   
        <div class="card col col-5 child-box" style="padding:0;">
          <h3 class="card-header">Konfiguration</h3>
          <div class="card-body">
              <Suspense>
                <template #default> <Configuration ref="config" @changedSelection="(redoCalculation())"/> </template>
                <template #fallback>Loading...</template>
              </Suspense>
            <br>
          </div>
        </div>

        <div class="card col col-5 child-box" style="padding:0;">
          <h3 class="card-header">Kalkulation</h3>
          <Suspense>
            <template #default> <Calculation ref="calc" v-bind:query="query"/> </template>
            <template #fallback>Loading...</template>
          </Suspense>
        </div>

        <div id="checkout" class="col col-12 child-box" style="padding:0;">
          <div class="d-flex justify-content-center">
            <a href="#" class="btn btn-primary btn-checkout">Speichern</a>
            <a href="#" class="btn btn-primary btn-checkout">Anfragen</a>
          </div>
        </div>
      </div>

      <!--
      <h1>{{ count }}</h1>
      <button @click="count--">-</button>
      <button @click="count++">+</button>
      -->

    </div>

    <div id="placeholder" class="col col-12">

    </div>

  </main>


  <footer class="bg-light d-flex justify-content-center border-top border-dark">
    <div id="footer-bar">
      <a class="footer-link text-muted" href="">Datenschutzerklärung</a>
      <a class="footer-link text-muted" href="">Impressum</a>
      <a class="footer-link text-muted" href="">Rechtliche Hinweise</a>
    </div>
  </footer>


</template>


<style src="../src/styles/style.css"></style>