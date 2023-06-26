<script setup>
    import axios from "axios"
    import { ref, watch, onMounted, computed } from "vue";

    var response = await axios.get("//localhost:8080/getOffer?model=Cursa&color=black&tires=big&interior=sport&motor=medium");

    const props = defineProps({
        queryToChild: {
            type: String,
            default: 'No content found!'
        }
    });

    async function getNewResponse() {
        response = await axios.get(props.queryToChild);
        document.getElementById("modelCalc").innerHTML = `Modell: ${ response.data.model } --- ${ (response.data.modelPrice /100).toLocaleString() } €`;
        document.getElementById("colorCalc").innerHTML = `Farbe: ${ response.data.color } --- ${ (response.data.colorPrice /100).toLocaleString() } €`;
        document.getElementById("tiresCalc").innerHTML = `Reifen: ${ response.data.tires } --- ${ (response.data.tiresPrice /100).toLocaleString() } €`;
        document.getElementById("interiorCalc").innerHTML = `Innenausstattung: ${ response.data.interior } --- ${ (response.data.interiorPrice /100).toLocaleString() } €`;
        document.getElementById("motorCalc").innerHTML = `Motor: ${ response.data.motor } --- ${ (response.data.motorPrice /100).toLocaleString() } €`;
    }

    watch(
        () => props.queryToChild,
        () => {
            getNewResponse();
            
    })

    onMounted(() => {
        //debugInitResponse();
        document.getElementById("modelCalc").innerHTML = `Modell: ${ response.data.model } --- ${ (response.data.modelPrice /100).toLocaleString() } €`;
        document.getElementById("colorCalc").innerHTML = `Farbe: ${ response.data.color } --- ${ (response.data.colorPrice /100).toLocaleString() } €`;
        document.getElementById("tiresCalc").innerHTML = `Reifen: ${ response.data.tires } --- ${ (response.data.tiresPrice /100).toLocaleString() } €`;
        document.getElementById("interiorCalc").innerHTML = `Innenausstattung: ${ response.data.interior } --- ${ (response.data.interiorPrice /100).toLocaleString() } €`;
        document.getElementById("motorCalc").innerHTML = `Motor: ${ response.data.motor } --- ${ (response.data.motorPrice /100).toLocaleString() } €`;
    })

</script>


<template>
    <div class="card col col-5 child-box" style="padding:0;">
          <h3 class="card-header">Kalkulation</h3>
        <div class="card-body" style="text-align: right">

            <!-- Berechnung der einzelnen Bauteile und der Gesamtkosten -->
            <p id="modelCalc">Modell: {{ response.data.model }} --- {{ (response.data.modelPrice /100).toLocaleString() }} €</p>
            <p id="colorCalc">Farbe: {{ response.data.color }} --- {{ (response.data.colorPrice /100).toLocaleString() }} €</p>
            <p id="tiresCalc">Reifen: {{ response.data.tires }} --- {{ (response.data.tiresPrice /100).toLocaleString() }} €</p>
            <p id="interiorCalc">Innenausstattung: {{ response.data.interior }} --- {{ (response.data.interiorPrice /100).toLocaleString() }} €</p>
            <p id="motorCalc">Motor: {{ response.data.motor }} --- {{ (response.data.motorPrice /100).toLocaleString() }} €</p>
            ___________________
            <br>
            <p>Gesamt: {{ (response.data.totalCost /100).toLocaleString() }} €</p>            
        </div>
    </div>
</template>

<style src="../assets/main.css"></style>