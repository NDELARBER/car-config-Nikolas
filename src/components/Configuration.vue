<script setup>
    import axios from "axios"
    import { ref, watch, onMounted } from "vue";

    //Hier den Get-Befehl anpassen:
    //Mehrere Variablen und Gets erstellen, um die Konfigurationsmöglichkeiten für Farbe, Reifen, ... zu speichern
    const responseColor = await axios.get("//localhost:8080/getColors?model=Cursa")
    const responseTires = await axios.get("//localhost:8080/getTires")
    const responseInterior = await axios.get("//localhost:8080/getInteriors?model=Cursa")
    const responseMotors = await axios.get("//localhost:8080/getMotors?model=Cursa")


    //const 
    //const selectedColor = ref()

    //watch()

    function testtest() {
        console.log("It's alive!");
    }

        // To do: Von JS in Vue.js konvertieren?

    function createLists() {
        for (let i = 0; i<responseColor.data.length; i++) {
            document.getElementById("colors").innerHTML += ("<option value=" + responseColor.data[i] + "\">" + responseColor.data[i] + "</option>");
        }

        for (let i = 0; i<responseTires.data.length; i++) {
            document.getElementById("tires").innerHTML += ("<option value=" + responseTires.data[i] + "\">" + responseTires.data[i] + "</option>");
        }

        for (let i = 0; i<responseInterior.data.length; i++) {
            document.getElementById("interior").innerHTML += ("<option value=" + responseInterior.data[i] + "\">" + responseInterior.data[i] + "</option>");
        }

        for (let i = 0; i<responseMotors.data.length; i++) {
            document.getElementById("motors").innerHTML += ("<option value=" + responseMotors.data[i] + "\">" + responseMotors.data[i] + "</option>");
        }

    }


    onMounted(() => {
        createLists();
    })

</script>

<script>
    
</script>

<template>
    <select name="color" id="colors" @change="$emit('changedSelection')">
              <!--<option disabled value="">Bitte auswählen</option>-->
            </select>
            <p></p>
            <select name="tires" id="tires" @change="$emit('changedSelection')"></select>
            <p></p>
            <select name="interior" id="interior" @change="$emit('changedSelection')"></select>
            <p></p>
            <select name="motor" id="motors" @change="$emit('changedSelection')"></select>

</template>