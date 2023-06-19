<script>
  import {ref} from "vue";
  import Calculation from './components/Calculation.vue'
  import Configuration from './components/Configuration.vue'

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

  export default {
    name: "App",
    components: { Calculation, Configuration },
    data() {
      return {
        query: "Link herse"
      }
    },
    mounted() {
      console.log("hallo vueee")
      console.log("hallo vusdfse")
      console.log(this)
    },
    methods: {
    }
  }
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
            <input
                :value="query"
                @input="event => query = event.target.value">
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