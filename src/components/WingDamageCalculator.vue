<template>
  <div class="root-card">
    <v-card>
      <InputStatusPart
        :supportIdol="supportIdol"
        @addSupportIdol="addSupportIdol"
        @editSupportIdol="editSupportIdol"></InputStatusPart>
    </v-card>
    <v-card>
      <OutputPart></OutputPart>
    </v-card>
  </div>
</template>

<script>
import InputStatusPart from "./WingDamageCalculator/InputStatusPart"
import OutputPart from "./WingDamageCalculator/OutputPart"

export default {
  components: {
    InputStatusPart,
    OutputPart
  },
  mounted() {
    this.initializeIdols();
  },
  data() {
    return {
      supportIdol : [],
      produceIdolStatus : [],
      produceIdolSkill : []
    }
  },
  methods: {
    initializeIdols() {
      const defaultSupportIdol = {
        name: "駅真乃",
        idolName: 0,
        vocalStatus: 150,
        danceStatus: 240,
        visualStatus: 300,
        vocalMagnification: 0,
        danceMagnification: 2,
        visualMagnification: 2,
        skillType: "Normal"
      }
      this.addSupportIdol(defaultSupportIdol);
    },
    addSupportIdol(idolObject) {
      this.supportIdol.push(idolObject);
    },
    editSupportIdol(idolObject, index) {
      Object.assign(this.supportIdol[index], idolObject);
    }
  }
}
</script>

<style scoped lang="scss">
.root-card {
  margin: 10px;
}
</style>