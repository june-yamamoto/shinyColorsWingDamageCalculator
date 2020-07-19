<template>
  <div>
    <v-card flat class="elevation-2">
      <v-card-title>Pアイドル</v-card-title>
      <v-card-text>
        <v-row dense :change="$emit('updateIdolStatus', this.produceIdolStatus, this.produceIdolSkills)">
          <v-col cols="12" sm="3" md="3">
            <v-form ref="form">
              <v-text-field v-model="produceIdolStatus.name"
                            label="アイドル名"
                            dense></v-text-field>
            </v-form>
          </v-col>
          <v-col cols="12" sm="2" md="2">
            <v-form ref="form">
              <v-text-field v-model="produceIdolStatus.vocalStatus"
                            label="Voステ"
                            dense></v-text-field>
            </v-form>
          </v-col>
          <v-col cols="12" sm="2" md="2">
            <v-form ref="form">
              <v-text-field v-model="produceIdolStatus.danceStatus"
                            label="Daステ"
                            dense></v-text-field>
            </v-form>
          </v-col>
          <v-col cols="12" sm="2" md="2">
            <v-form ref="form">
              <v-text-field v-model="produceIdolStatus.visualStatus"
                            label="Viステ"
                            dense></v-text-field>
            </v-form>
          </v-col>
          <v-col cols="12" sm="2" md="2"></v-col>
        </v-row>
        <!-- ここからスキル -->
        <v-row
          v-for="(skill, index) in produceIdolSkills"
          :key="index"
          dense
        >
          <v-col cols="12" sm="3" md="3">
            <v-form ref="form">
              <v-text-field v-model="skill.skillName" label="スキル" dense></v-text-field>
            </v-form>
          </v-col>
          <v-col cols="12" sm="2" md="2">
            <v-form ref="form">
              <v-text-field v-model="skill.vocalMagnification" label="Vo倍率" dense></v-text-field>
            </v-form>
          </v-col>
          <v-col cols="12" sm="2" md="2">
            <v-form ref="form">
              <v-text-field v-model="skill.danceMagnification" label="Da倍率" dense></v-text-field>
            </v-form>
          </v-col>
          <v-col cols="12" sm="2" md="2">
            <v-form ref="form">
              <v-text-field v-model="skill.visualMagnification" label="Vi倍率" dense></v-text-field>
            </v-form>
          </v-col>
          <v-col cols="12" sm="3" md="3">
            <v-form ref="form">
              <v-select label="スキルのタイプ"
                        :items="skillTypeLists"
                        v-model="skill.skillType"
                        class="dropdown"
                        dense></v-select>
            </v-form>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {},
  data() {
    return {
      produceIdolStatus: {
        name: "",
        vocalStatus: 50,
        danceStatus: 50,
        visualStatus: 50
      },
      produceIdolSkills: [],
      skillTypeLists: ["Normal", "Excellent"]
    };
  },
  mounted() {
    console.log("mounted");
    this.initializeIdol();
  },
  computed: {},
  methods: {
    initializeIdol() {
      console.log("initialize");
      const newObject = {
        skillName: "",
        vocalMagnification: 0,
        danceMagnification: 0,
        visualMagnification: 0,
        skillType: 0
      };
      this.produceIdolSkills.push(Object.assign({}, newObject));
      this.produceIdolSkills.push(Object.assign({}, newObject));
      this.produceIdolSkills.push(Object.assign({}, newObject));
      this.produceIdolSkills.push(Object.assign({}, newObject));
      console.log(this.produceIdolSkills);
    }
  }
};
</script>

<style scoped>
.card {
  margin: 10px;
}
</style>