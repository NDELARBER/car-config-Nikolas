<script setup>
    import axios from "axios"
    import { ref, watch, onMounted, computed } from "vue";

    var response = await axios.get("//localhost:8080/getOffer?model=Cursa&color=black&tires=small&interior=sport&motor=medium");
    console.log(response.data)

    /*
    const props = defineProps(['query'])
    console.log("Debug: log props.query in Calculation");
    console.log(props.query);
    */
    console.log("Debug: Log in Calculation script setup")

    function updateCalculation() {
                console.log("Calculation changed");
            }
</script>


<script>
    
    export default {
        name: "Calculation",
        props: ['query'],
        
        watch: {
            query:
            function(newValue, oldValue) {
                queryChanged();
                console.log("watching");
                
            }
        },
        setup(props) {
            console.log("Debug: log props.query in Calculation");
            console.log(props.query);
        },
        methods: {
            logTest() {
                console.log("Debug: log props.query in Calculation");
                console.log(props);
            },
            updateCalculation() {
                console.log("Calculation changed");
            }
        }
        
    };

    
    

    /*
    watch(query, (currentValue, oldValue) => {
        console.log("Test456");
    })
    */

    console.log("Props: ");
    //console.log(props);
    console.log("Props Ende");
    

    async function queryChanged() {
        response = await axios.get(query);
        console.log("Function queryChanged()");
        console.log("Query" + response);
    }

    /*
    function logTest() {
        console.log("Debug: log props.query in Calculation");
        console.log(props);
    }
    */

</script>

<template>

    <div class="card-body" style="text-align: right">
            <p id="modelCalc">Modell: {{ response.data.model }} --- {{ (response.data.modelPrice /100).toLocaleString() }} €</p>
            <p id="colorCalc">Farbe: {{ response.data.color }} --- {{ (response.data.colorPrice /100).toLocaleString() }} €</p>
            <p id="tiresCalc">Reifen: {{ response.data.tires }} --- {{ (response.data.tiresPrice /100).toLocaleString() }} €</p>
            <p id="interiorCalc">Innenausstattung: {{ response.data.interior }} --- {{ (response.data.interiorPrice /100).toLocaleString() }} €</p>
            <p id="motorCalc">Motor: {{ response.data.motor }} --- {{ (response.data.motorPrice /100).toLocaleString() }} €</p>
            ___________________
            <br>
            <p>Gesamt: {{ (response.data.totalCost /100).toLocaleString() }} €</p>
            <p>{{ query }}</p>
          </div>

          <button @click="logTest()"></button>
</template>