<script>
export default {
  name: "Calculation",
  props: ['query'],

  watch: {
    query:
        function (newValue, oldValue) {
          queryChanged();
        }
  },
  methods: {
    logTest() {
      console.log("Debug: log props.query in Calculation");
      console.log(query);
    },
    updateCalculation() {
      console.log("Calculation changed");
      console.log(query)
    },
    queryChanged() {
      console.log("Function queryChanged()");
      console.log("Calculation would be triggered here")
      this.updateCalculation()
    }
  }

}

</script>

<template>

  <div class="card-body" style="text-align: right">
    <p id="modelCalc">Modell: Car €</p>
    <p id="colorCalc">Farbe: 5 €</p>
    <p id="tiresCalc">Reifen: 10 €</p>
    <p id="interiorCalc">Innenausstattung: 15 €</p>
    <p id="motorCalc">Motor: 20 €</p>
    ___________________
    <br>
    <p>Gesamt: 1 Billion €</p>
    <p>{{ query }}</p>
  </div>

  <button @click="logTest()"></button>
</template>