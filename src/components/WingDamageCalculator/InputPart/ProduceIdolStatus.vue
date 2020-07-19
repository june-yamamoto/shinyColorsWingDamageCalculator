<template>
  <div>
    <v-card flat class="elevation-2">
      <v-card-title>Pアイドル</v-card-title>
      <v-card-text>
        <v-form ref="statusForm">
          <v-row dense :change="this.updateIdolStatus()">
            <v-col cols="12" sm="3" md="3">
              <v-text-field v-model="produceIdolStatus.name" label="アイドル名" dense></v-text-field>
            </v-col>
            <v-col cols="12" sm="2" md="2">
              <v-text-field
                v-model.number="produceIdolStatus.vocalStatus"
                label="Voステ"
                dense
                :rules="statusRules"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="2" md="2">
              <v-text-field
                v-model.number="produceIdolStatus.danceStatus"
                label="Daステ"
                dense
                :rules="statusRules"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="2" md="2">
              <v-text-field
                v-model.number="produceIdolStatus.visualStatus"
                label="Viステ"
                dense
                :rules="statusRules"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="2" md="2"></v-col>
          </v-row>
        </v-form>
        <!-- ここからスキル -->
        <v-form ref="form">
          <v-row v-for="(skill, index) in produceIdolSkills" :key="index" dense>
            <v-col cols="12" sm="3" md="3">
              <v-text-field v-model="skill.skillName" label="スキル" dense></v-text-field>
            </v-col>
            <v-col cols="12" sm="2" md="2">
              <v-text-field
                v-model.number="skill.vocalMagnification"
                label="Vo倍率"
                dense
                :rules="skillRules"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="2" md="2">
              <v-text-field
                v-model.number="skill.danceMagnification"
                label="Da倍率"
                dense
                :rules="skillRules"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="2" md="2">
              <v-text-field
                v-model.number="skill.visualMagnification"
                label="Vi倍率"
                dense
                :rules="skillRules"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="3" md="3">
              <v-select
                label="スキルのタイプ"
                :items="skillTypeLists"
                v-model="skill.skillType"
                class="dropdown"
                dense
              ></v-select>
            </v-col>
          </v-row>
        </v-form>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {},
  data() {
    return {
      mounted: false,
      produceIdolStatus: {
        name: "",
        vocalStatus: 50,
        danceStatus: 50,
        visualStatus: 50
      },
      statusRules: [v => /^([1-9]\d*|0)$/.test(v) || "正の整数値"],
      skillRules: [v => (v >= 0 && !isNaN(v)) || "正の数"],
      produceIdolSkills: [],
      skillTypeLists: ["Normal", "Excellent"]
    };
  },
  mounted() {
    this.initializeIdol();
    this.mounted = true;
  },
  computed: {},
  methods: {
    initializeIdol() {
      const newObject = {
        skillName: "駅",
        vocalMagnification: 0,
        danceMagnification: 2,
        visualMagnification: 2,
        skillType: "Normal"
      };
      const produceIdolStatus = {
        name: "アルテマ夏葉",
        vocalStatus: 300,
        danceStatus: 515,
        visualStatus: 515
      };
      this.produceIdolStatus = Object.assign({}, produceIdolStatus);
      this.produceIdolSkills.push(Object.assign({}, newObject));
      this.produceIdolSkills.push(Object.assign({}, newObject));
      this.produceIdolSkills.push(Object.assign({}, newObject));
      this.produceIdolSkills.push(Object.assign({}, newObject));
    },
    updateIdolStatus() {
      if (this.mounted === true) {
        if (this.$refs.form.validate() && this.$refs.statusForm.validate()) {
          this.$emit(
            "updateIdolStatus",
            this.produceIdolStatus,
            this.produceIdolSkills
          );
        }
      }
    }
  }
};
</script>

<style scoped>
.card {
  margin: 10px;
}
</style>