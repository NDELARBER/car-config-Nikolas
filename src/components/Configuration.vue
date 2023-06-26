<script setup>
    import axios from "axios"
    import { ref, watch, onMounted } from "vue";

    //DB-Anfragen zum Erhalten der verschiedenen Optionen für die Dropdown-Menüs
    const responseColor = await axios.get("//localhost:8080/getColors?model=Cursa")
    const responseTires = await axios.get("//localhost:8080/getTires")
    const responseInterior = await axios.get("//localhost:8080/getInteriors?model=Cursa")
    const responseMotors = await axios.get("//localhost:8080/getMotors?model=Cursa")


    // To do: Von JS in Vue.js konvertieren?
    // To do: JSON-Datei zum Übersetzen des Codes/Keys? (red -> Rot)
    //Funktionen zum Erstellen der Optionen der verschiedenen Selects
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

    //Erstellen der Optionen der verschiedenen Selects beim Mounten der Komponente
    onMounted(() => {
        createLists();
    })

</script>


<template>
    <div class="card col col-5 child-box" style="padding:0;">
        <h3 class="card-header">Konfiguration</h3>
        <div class="card-body">
        <select name="color" id="colors" @change="$emit('changedSelection')">
                </select>
                <p></p>
                <select name="tires" id="tires" @change="$emit('changedSelection')"></select>
                <p></p>
                <select name="interior" id="interior" @change="$emit('changedSelection')"></select>
                <p></p>
                <select name="motor" id="motors" @change="$emit('changedSelection')"></select>
        </div>
    </div>

</template>

<style src="../assets/main.css"></style>