<template>
  <v-card class="root-card">
    <InputStatusPart></InputStatusPart>
    <OutputPart></OutputPart>
  </v-card>
</template>

<script>
import InputStatusPart from "./WingDamageCalculator/InputStatusPart"
import OutputPart from "./WingDamageCalculator/OutputPart"

export default {
  components: {
    InputStatusPart,
    OutputPart
  },
  data() {
    return {
      supportIdol : [],
      produceIdolStatus : [],
      produceIdolSkill : []
    }
  }
}
</script>

<style scoped lang="scss">
.root-card {
  margin: 10px;
}
</style>