<script>
export default {
  name: "Configuration",
  data() {
    return {
      query: "Link here",
    }
  }
}
</script>

<template>
  <select name="color" id="colors" @change="$emit('changedSelection')">
    <option value="">Red</option>
    <option value="">Blue</option>
    <!--<option disabled value="">Bitte auswählen</option>-->
  </select>
  <p></p>
  <select name="tires" id="tires" @change="$emit('changedSelection')">
    <option value="">Tire 1</option>
    <option value="">Tire 2</option>
  </select>

  <p></p>
  <select name="interior" id="interior" @change="$emit('changedSelection')">
    <option value="">Lush</option>
    <option value="">Beautiful</option>
  </select>
  <p></p>
  <select name="motor" id="motors" @change="$emit('changedSelection')">
    <option value="">150 PS</option>
    <option value="">200 PS</option>
  </select>

</template>