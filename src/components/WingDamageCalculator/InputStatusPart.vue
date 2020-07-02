<template>
  <div>
    <SupportIdolStatus
      @addSupportIdol="addSupportIdol"
      @editSupportIdol="editSupportIdol"
      :supportIdol="supportIdol"></SupportIdolStatus>
  </div>
</template>

<script>
import SupportIdolStatus from "./InputPart/SupportIdolStatus"

export default {
  components: {
    SupportIdolStatus
  },
  props: {
    supportIdol: {
        name: String,
        idolName: Number,
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
      this.$emit('addSupportIdol', idolObject);
    },
    editSupportIdol(idolObject, index) {
      this.$emit('editSupportIdol', idolObject, index);
    }
  }
}
</script>

<style scoped lang="scss">

</style>