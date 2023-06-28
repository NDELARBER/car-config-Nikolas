<script setup>
  import Calculation from './components/Calculation.vue'
  import Configuration from './components/Configuration.vue'
  import Footer from './components/Footer.vue'
  import Nav from './components/Nav.vue'
  import Checkout from './components/Checkout.vue'
  import {ref, onMounted} from "vue";
  import axios from "axios"

  
  const config = ref()
  var queryNew = ref("//localhost:8080/getOffer?model=Cursa&color=black&tires=big&interior=sport&motor=medium");

  function redoCalculation() {
    let queryModel = "Cursa";
    let queryColor = document.getElementById("colors").value;
    let queryTires = document.getElementById("tires").value;
    let queryInterior = document.getElementById("interior").value;
    let queryMotor = document.getElementById("motors").value;

    queryNew.value = `//localhost:8080/getOffer?model=${queryModel}&color=${queryColor.slice(0, -1)}&tires=${queryTires.slice(0, -1)}&interior=${queryInterior.slice(0, -1)}&motor=${queryMotor.slice(0, -1)}`;
  }

  function saveOffer() {
    let queryModel = "Cursa";
    let queryColor = document.getElementById("colors").value;
    let queryTires = document.getElementById("tires").value;
    let queryInterior = document.getElementById("interior").value;
    let queryMotor = document.getElementById("motors").value;

    axios.post(`//localhost:8080/postOffer?model=${queryModel}&color=${queryColor.slice(0, -1)}&tires=${queryTires.slice(0, -1)}&interior=${queryInterior.slice(0, -1)}&motor=${queryMotor.slice(0, -1)}`)
    console.log("offer saved");
  }

</script>




<template>

  <!-- NAV COMPONENT -->
  <Suspense>
    <template #default> <Nav /> </template>
    <template #fallback>Loading...</template>
  </Suspense>


  <main id="main-div" class="row d-flex justify-content-center">

    <!-- HEADING -->
    <div id="title" class="col col-8">
      <h3>Wählen Sie Ihre gewünschte Konfiguration für<br>Opal Cursa</h3>
    </div>
        

    <div class="col col-8">

      <div id="config-all" class="row d-flex justify-content-evenly flex-wrap">

        <!-- CONFIGURATION COMPONENT -->
        <Suspense>
          <template #default> <Configuration ref="config" @changedSelection="(redoCalculation())"/> </template>
          <template #fallback>Loading...</template>
        </Suspense>
        <br>
        
        <!-- CALCULATION COMPONENT -->
        <Suspense>
          <template #default> <Calculation ref="calc" :queryToChild="queryNew"/> </template>
          <template #fallback>Loading...</template>
        </Suspense>

        <!-- CHECKOUT COMPONENT -->
        <Suspense>
          <template #default> <Checkout @saveOffer="(saveOffer())"/> </template>
          <template #fallback>Loading...</template>
        </Suspense>

      </div>
    </div>

    <div id="placeholder" class="col col-12"></div>

  </main>

  <!-- FOOTER COMPONENT -->
  <Suspense>
    <template #default> <Footer /> </template>
    <template #fallback>Loading...</template>
  </Suspense>

  

</template>


<style src="../src/assets/main.css"></style>