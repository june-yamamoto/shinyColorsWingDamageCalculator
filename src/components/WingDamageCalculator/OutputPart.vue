<template>
  <div>
    <v-card flat class="elevation-2">
      <v-card-title>
        計算結果
      </v-card-title>
      <v-card-text>
        <v-row>
          <v-col cols="12" sm="3">
            {{this.supportIdol[0].name}}
          </v-col>
          <v-col cols="12" sm="3">
            
          </v-col>
          <v-col cols="12" sm="3">
            
          </v-col>
          <v-col cols="12" sm="3">
            
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
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
    },
    produceIdolStatus: {
      name: String,
      vocalStatus: Number,
      danceStawtus: Number,
      visualStatus: Number
    },
    produceIdolSkills: {
      skillName: String,
      vocalMagnification: Number,
      danceMagnification: Number,
      visualMagnification: Number,
      skillType: String
    },
    week: Number,
    buff: {
      vocal: Number,
      dance: Number,
      visual: Number
    }
  },
  mounted() {
    console.log('supportIdol', this.supportIdol);
    console.log('produceIdolStatus', this.produceIdolStatus);
    console.log('produceIdolSkills', this.produceIdolSkills);
    console.log('week', this.week);
    console.log('buff', this.buff);
  },
  methods: {
  }
}
</script>