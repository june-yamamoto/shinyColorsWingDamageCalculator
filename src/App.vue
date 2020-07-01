<template>
  <v-app>
    <v-content>
      <NavigationBar></NavigationBar>
      <WingDamageCalculator></WingDamageCalculator>
    </v-content>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import NavigationBar from "./components/NavigationBar.vue"
import WingDamageCalculator from "./components/WingDamageCalculator.vue"

export default Vue.extend({
  name: "App",

  components: {
    NavigationBar,
    WingDamageCalculator
  },

  data: () => ({
    supportIdol: []
  })
});
</script>
