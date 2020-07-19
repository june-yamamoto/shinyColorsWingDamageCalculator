<template>
  <div>
    <SupportIdolStatus
      @addSupportIdol="addSupportIdol"
      @editSupportIdol="editSupportIdol"
      @deleteSupportIdol="deleteSupportIdol"
      :supportIdol="supportIdol"
    ></SupportIdolStatus>
    <ProduceIdolStatus @updateIdolStatus="updateIdolStatus"></ProduceIdolStatus>
  </div>
</template>

<script>
import SupportIdolStatus from "./InputPart/SupportIdolStatus";
import ProduceIdolStatus from "./InputPart/ProduceIdolStatus";

export default {
  components: {
    SupportIdolStatus,
    ProduceIdolStatus
  },
  props: {
    supportIdol: {
      name: String,
      idolId: Number,
      vocalStatus: Number,
      danceStatus: Number,
      visualStatus: Number,
      vocalMagnification: Number,
      danceMagnification: Number,
      visualMagnification: Number,
      skillType: String
    }
  },
  methods: {
    addSupportIdol(idolObject) {
      this.$emit("addSupportIdol", idolObject);
    },
    editSupportIdol(idolObject, index) {
      this.$emit("editSupportIdol", idolObject, index);
    },
    deleteSupportIdol(index) {
      this.$emit("deleteSupportIdol", index);
    },
    updateIdolStatus(produceIdolStatus, produceIdolSkills) {
      console.log("updateIdolStatus", produceIdolStatus, produceIdolSkills);
      this.$emit("updateProduceIdolStatus", produceIdolStatus, produceIdolSkills);
    }
  }
};
</script>

<style scoped lang="scss"></style>
