<template>
  <div>
    <v-card>
      <v-card-title>その他の設定</v-card-title>
      <v-card-text>
        <v-form refs="settingForm" v-model="valid">
          <v-row class="slider-col" :change="this.updateSettings()">
            <v-col cols="12" sm="3">
              <v-slider v-model.number="week"
                        :max="max"
                        :min="min"
                        :thumb-size="50"
                        thumb-label="always">
                <template v-slot:thumb-label="{value}">
                  {{ value === 33 ? "決勝" : value === 32 ? "準決勝" : value + "週目" }}
                </template>
              </v-slider>
            </v-col>
            <v-col cols="12" sm="3">
              <v-text-field v-model.number="buff.vocal"
                            label="Vocalバフ倍率"
                            dense
                            :rules="buffRules">
              </v-text-field>
            </v-col>
            <v-col cols="12" sm="3">
              <v-text-field v-model.number="buff.dance"
                            label="Danceバフ倍率"
                            dense
                            :rules="buffRules">
              </v-text-field>
            </v-col>
            <v-col cols="12" sm="3">
              <v-text-field v-model.number="buff.visual"
                            label="Visualバフ倍率"
                            dense
                            :rules="buffRules">
              </v-text-field>
            </v-col>
          </v-row>
        </v-form>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      valid: false,
      week: 1,
      max: 33,
      min: 1,
      buff: {
        vocal: 100,
        dance: 100,
        visual: 100
      },
      buffRules: [
        v => /^([1-9]\d*|0)$/.test(v) || "正の整数値"
      ]
    }
  },
  computed: {
    weekValue(value) {
      return value === 33 ? "決勝" : value === 32 ? "準決勝" : value;
    }
  },
  methods: {
    updateSettings() {
      if(this.valid) {
        this.$emit('updateSettings', this.week, this.buff);
      }
    }
  }
};
</script>

<style scoped>
.slider-col {
  margin-top: 27px;
}
</style>