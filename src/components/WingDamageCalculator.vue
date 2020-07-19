<template>
  <div class="root-card">
    <v-row justify="center">
      <v-col cols="12" lg="8" md="10" sm="12">
        <v-card>
          <InputStatusPart
            :supportIdol="supportIdol"
            @addSupportIdol="addSupportIdol"
            @editSupportIdol="editSupportIdol"
            @deleteSupportIdol="deleteSupportIdol"
            @updateProduceIdolStatus="updateProduceIdolStatus"></InputStatusPart>
        </v-card>
        <v-card>
          <OutputPart></OutputPart>
        </v-card>
      </v-col>
    </v-row>
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
      produceIdolStatus : {
        name: "",
        vocalStatus: 50,
        danceStatus: 50,
        visualStatus: 50
      },
      produceIdolSkills : []
    }
  },
  methods: {
    initializeIdols() {
      const defaultSupportIdol = {
        name: "駅真乃",
        idolId: 0,
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
    },
    deleteSupportIdol(index) {
      this.supportIdol.splice(index, 1);
    },
    updateProduceIdolStatus(produceIdolStatus, produceIdolSkills) {
      this.produceIdolStatus.name = produceIdolStatus.name;
      this.produceIdolStatus.vocalStatus = produceIdolStatus.vocalStatus;
      this.produceIdolStatus.danceStatus = produceIdolStatus.danceStatus;
      this.produceIdolStatus.visualStatus = produceIdolStatus.visualStatus;
      this.produceIdolSkills = produceIdolSkills;
      console.log('updateProduceIdolStatus', this.produceIdolStatus);
      console.log('updateProduceIdolSkills', this.produceIdolSkills);
    }
  }
}
</script>

<style scoped lang="scss">
.root-card {
  margin: 10px;
}
</style>