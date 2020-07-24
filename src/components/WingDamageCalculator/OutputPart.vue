<template>
  <div>
    <v-card flat class="elevation-2">
      <v-card-title>
        計算結果
        <v-spacer></v-spacer>
        <v-checkbox v-model="visiblePerfect" label="Perfect"></v-checkbox>
        <v-checkbox v-model="visibleGood" label="Good"></v-checkbox>
        <v-checkbox v-model="visibleNormal" label="Normal"></v-checkbox>
      </v-card-title>
      <v-card-text class="output-part">
        <v-row v-for="(appeal,index) in calculateAppeal" :key="index" class="one-part">
          <v-col cols="2" align-self="center" align="right" class="self-dense">
            {{ index > 3 ? "サポート" : "プロデュース"}}
          </v-col>
          <v-col cols="2" align-self="center" align="right" class="self-dense">
            {{appeal.skillName}}
          </v-col>
          <v-row >
            <template v-if="visiblePerfect">
              <v-col cols="2" class="self-dense">Perfect</v-col>
              <v-col cols="2" class="self-dense vocal-part">
                {{appeal.vocalPerfect}}
              </v-col>
              <v-col cols="2" class="self-dense dance-part">
                {{appeal.dancePerfect}}
              </v-col>
              <v-col cols="2" class="self-dense visual-part">
                {{appeal.visualPerfect}}
              </v-col>
              <v-col cols="4" class="self-dense"></v-col>
            </template>
            <template v-if="visibleGood">
              <v-col cols="2" class="self-dense">Good</v-col>
              <v-col cols="2" class="self-dense vocal-part">
                {{appeal.vocalGood}}
              </v-col>
              <v-col cols="2" class="self-dense dance-part">
                {{appeal.danceGood}}
              </v-col>
              <v-col cols="2" class="self-dense visual-part">
                {{appeal.visualGood}}
              </v-col>
              <v-col cols="4" class="self-dense"></v-col>
            </template>
            <template v-if="visibleNormal">
              <v-col cols="2" class="self-dense">Normal</v-col>
              <v-col cols="2" class="self-dense vocal-part">
                {{appeal.vocalNormal}}
              </v-col>
              <v-col cols="2" class="self-dense dance-part">
                {{appeal.danceNormal}}
              </v-col>
              <v-col cols="2" class="self-dense visual-part">
                {{appeal.visualNormal}}
              </v-col>
              <v-col cols="4" class="self-dense"></v-col>
            </template>
          </v-row>
        </v-row>
      </v-card-text>
    </v-card>
    <v-card>
      <v-card-title>
        思い出アピール
      </v-card-title>
      <v-card-text>
        <v-row v-for="(appeal,index) in calculateMemoryAppeal" :key="index" class="one-part">
          <v-col cols="2" align-self="center" align="right" class="self-dense">
            {{appeal.level}}
          </v-col>
          <v-col cols="2" align-self="center" align="right" class="self-dense vocal-part">
            {{appeal.vocal}}
          </v-col>
          <v-col cols="2" align-self="center" align="right" class="self-dense dance-part">
            {{appeal.dance}}
          </v-col>
          <v-col cols="2" align-self="center" align="right" class="self-dense visual-part">
            {{appeal.visual}}
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
  computed: {
    combineSkills() {
      const skillLists = [];
      for(let i = 0 ;  i < 4 ; i++) {
        const skill = this.produceIdolSkills[i];
        const skillObject = {};
        skillObject.skillName = skill.skillName;
        skillObject.vocalMagnification = skill.vocalMagnification;
        skillObject.danceMagnification = skill.danceMagnification;
        skillObject.visualMagnification = skill.visualMagnification;
        skillObject.skillType = skill.skillType;
        skillLists.push(skillObject);
      }
      for(let i = 0 ;  i < 4 ; i++) {
        const skill = this.supportIdol[i];
        const skillObject = {};
        skillObject.skillName = skill.name;
        skillObject.vocalMagnification = skill.vocalMagnification;
        skillObject.danceMagnification = skill.danceMagnification;
        skillObject.visualMagnification = skill.visualMagnification;
        skillObject.skillType = skill.skillType;
        skillLists.push(skillObject);
      }
      // console.log('skillLists', skillLists);
      return skillLists;
    },
    produceIdolBaseAppeal() {
      const baseAppeal = {};
      baseAppeal.vocal = Number.parseInt((this.produceIdolStatus.vocalStatus * 2) + ((this.supportIdol[0].vocalStatus + this.supportIdol[1].vocalStatus + this.supportIdol[2].vocalStatus + this.supportIdol[3].vocalStatus) * 0.2) * (1 + (0.1 * this.week)));
      baseAppeal.dance = Number.parseInt((this.produceIdolStatus.danceStatus * 2) + ((this.supportIdol[0].danceStatus + this.supportIdol[1].danceStatus + this.supportIdol[2].danceStatus + this.supportIdol[3].danceStatus) * 0.2) * (1 + (0.1 * this.week)));
      baseAppeal.visual = Number.parseInt((this.produceIdolStatus.visualStatus * 2) + ((this.supportIdol[0].visualStatus + this.supportIdol[1].visualStatus + this.supportIdol[2].visualStatus + this.supportIdol[3].visualStatus) * 0.2) * (1 + (0.1 * this.week)));
      // console.log('baseAppeal', baseAppeal);
      return baseAppeal;
    },
    supportIdolBaseAppeal() {
      const supportIdolBaseAppeal = [];
      for(let i = 0 ;  i < 4 ; i++) {
        const baseAppeal = {};
        const supportIdol = this.supportIdol[i];
        const notSupportIdol = this.supportIdol.filter((idol, index) => index !== i);
        baseAppeal.vocal = Number.parseInt(((this.produceIdolStatus.vocalStatus * 0.5) + (((supportIdol.vocalStatus * 4) + notSupportIdol[0].vocalStatus + notSupportIdol[1].vocalStatus + notSupportIdol[2].vocalStatus) * 0.2) * (1 + (0.1 * this.week))));
        baseAppeal.dance = Number.parseInt((this.produceIdolStatus.danceStatus * 0.5 + ((supportIdol.danceStatus * 4 + notSupportIdol[0].danceStatus + notSupportIdol[1].danceStatus + notSupportIdol[2].danceStatus) * 0.2) * (1 + 0.1 * this.week)));
        baseAppeal.visual = Number.parseInt(((this.produceIdolStatus.visualStatus * 0.5) + (((supportIdol.visualStatus * 4) + notSupportIdol[0].visualStatus + notSupportIdol[1].visualStatus + notSupportIdol[2].visualStatus) * 0.2) * (1 + (0.1 * this.week))));
        supportIdolBaseAppeal.push(baseAppeal);
      }
      return supportIdolBaseAppeal;
    },
    calculateAppeal() {
      const produceAppeal = [];
      const baseAppeal = this.produceIdolBaseAppeal;
      for(let i = 0 ; i < 4 ; i++) {
        const appeal = {};
        const skill = this.combineSkills[i];
        appeal.skillName = skill.skillName;
        if(skill.skillType === "Normal") {
          appeal.vocalPerfect =    (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.5 * this.buff.vocal * 2)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.5 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.5 * this.buff.visual)) * skill.visualMagnification));
          appeal.dancePerfect =    (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.5 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.5 * this.buff.dance) * 2) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.5 * this.buff.visual)) * skill.visualMagnification));
          appeal.visualPerfect =    (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.5 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.5 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.5 * this.buff.visual * 2)) * skill.visualMagnification));
          appeal.vocalGood =    (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.1 * this.buff.vocal * 2)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.1 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.1 * this.buff.visual)) * skill.visualMagnification));
          appeal.danceGood =    (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.1 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.1 * this.buff.dance * 2)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.1 * this.buff.visual)) * skill.visualMagnification));
          appeal.visualGood =    (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.1 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.1 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.1 * this.buff.visual * 2)) * skill.visualMagnification));
          appeal.vocalNormal =    (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.0 * this.buff.vocal * 2)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.0 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.0 * this.buff.visual)) * skill.visualMagnification));
          appeal.danceNormal =    (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.0 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.0 * this.buff.dance * 2)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.0 * this.buff.visual)) * skill.visualMagnification));
          appeal.visualNormal =    (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.0 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.0 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.0 * this.buff.visual * 2)) * skill.visualMagnification));
          produceAppeal.push(appeal);
          // console.log('appeal', appeal);
        } else if(skill.skillType === "Excellent") {
          appeal.vocalPerfect = (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.5 * this.buff.vocal * 2)) * skill.vocalMagnification));
          appeal.dancePerfect = (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.5 * this.buff.dance * 2)) * skill.vocalMagnification));
          appeal.visualPerfect = (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.5 * this.buff.visual * 2)) * skill.vocalMagnification));
          appeal.vocalGood = (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.1 * this.buff.vocal * 2)) * skill.vocalMagnification));
          appeal.danceGood = (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.1 * this.buff.dance * 2)) * skill.vocalMagnification));
          appeal.visualGood = (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.1 * this.buff.visual * 2)) * skill.vocalMagnification));
          appeal.vocalNormal = (Number.parseInt((Number.parseInt(baseAppeal.vocal * 1.0 * this.buff.vocal * 2)) * skill.vocalMagnification));
          appeal.danceNormal = (Number.parseInt((Number.parseInt(baseAppeal.dance * 1.0 * this.buff.dance * 2)) * skill.vocalMagnification));
          appeal.visualNormal = (Number.parseInt((Number.parseInt(baseAppeal.visual * 1.0 * this.buff.visual * 2)) * skill.vocalMagnification));
          produceAppeal.push(appeal);
        }
      }
      const supportBaseAppeal = this.supportIdolBaseAppeal;
      for(let i = 0 ; i < 4 ; i++) {
        const appeal = {};
        const skill = this.combineSkills[i+4];
        appeal.skillName = skill.skillName;
        if(skill.skillType === "Normal") {
          appeal.vocalPerfect =    (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.5 * this.buff.vocal * 2)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.5 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.5 * this.buff.visual)) * skill.visualMagnification));
          appeal.dancePerfect =    (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.5 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.5 * this.buff.dance * 2)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.5 * this.buff.visual)) * skill.visualMagnification));
          appeal.visualPerfect =    (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.5 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.5 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.5 * this.buff.visual * 2)) * skill.visualMagnification));
          appeal.vocalGood =    (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.1 * this.buff.vocal * 2)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.1 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.1 * this.buff.visual)) * skill.visualMagnification));
          appeal.danceGood =    (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.1 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.1 * this.buff.dance * 2)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.1 * this.buff.visual)) * skill.visualMagnification));
          appeal.visualGood =    (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.1 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.1 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.1 * this.buff.visual * 2)) * skill.visualMagnification));
          appeal.vocalNormal =    (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.0 * this.buff.vocal * 2)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.0 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.0 * this.buff.visual)) * skill.visualMagnification));
          appeal.danceNormal =    (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.0 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.0 * this.buff.dance * 2)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.0 * this.buff.visual)) * skill.visualMagnification));
          appeal.visualNormal =    (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.0 * this.buff.vocal)) * skill.vocalMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.0 * this.buff.dance)) * skill.danceMagnification))
                                 + (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.0 * this.buff.visual * 2)) * skill.visualMagnification));
          produceAppeal.push(appeal);
          // console.log('appeal', appeal);
        } else if(skill.skillType === "Excellent") {
          appeal.vocalPerfect = (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.5 * this.buff.vocal * 2)) * skill.vocalMagnification));
          appeal.dancePerfect = (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.5 * this.buff.dance * 2)) * skill.vocalMagnification));
          appeal.visualPerfect = (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.5 * this.buff.visual * 2)) * skill.vocalMagnification));
          appeal.vocalGood = (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.1 * this.buff.vocal * 2)) * skill.vocalMagnification));
          appeal.danceGood = (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.1 * this.buff.dance * 2)) * skill.vocalMagnification));
          appeal.visualGood = (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.1 * this.buff.visual * 2)) * skill.vocalMagnification));
          appeal.vocalNormal = (Number.parseInt((Number.parseInt(supportBaseAppeal[i].vocal * 1.0 * this.buff.vocal * 2)) * skill.vocalMagnification));
          appeal.danceNormal = (Number.parseInt((Number.parseInt(supportBaseAppeal[i].dance * 1.0 * this.buff.dance * 2)) * skill.vocalMagnification));
          appeal.visualNormal = (Number.parseInt((Number.parseInt(supportBaseAppeal[i].visual * 1.0 * this.buff.visual * 2)) * skill.vocalMagnification));
          produceAppeal.push(appeal);
        }
      }
      // console.log('produceAppeal', produceAppeal);
      return produceAppeal;
    },
    calculateMemoryAppeal() {
      const memoryAppealLists = [];
      const memoryAppealMagnification = [0.8,1.0,1.2,1.4,2.0];
      for(let i = 0; i < 5; i++) {
        const memoryAppeal = {};
        memoryAppeal.level = (i + 1) + "";
        memoryAppeal.vocal = (Number.parseInt((Number.parseInt(this.produceIdolBaseAppeal.vocal * 1.5 * this.buff.vocal)) * memoryAppealMagnification[i] * 2)) + (Number.parseInt((Number.parseInt(this.produceIdolBaseAppeal.dance * 1.5 * this.buff.dance)) * memoryAppealMagnification[i])) + (Number.parseInt((Number.parseInt(this.produceIdolBaseAppeal.visual * 1.5 * this.buff.visual)) * memoryAppealMagnification[i]));
        memoryAppeal.dance = (Number.parseInt((Number.parseInt(this.produceIdolBaseAppeal.vocal * 1.5 * this.buff.vocal)) * memoryAppealMagnification[i])) + (Number.parseInt((Number.parseInt(this.produceIdolBaseAppeal.dance * 1.5 * this.buff.dance)) * memoryAppealMagnification[i] * 2)) + (Number.parseInt((Number.parseInt(this.produceIdolBaseAppeal.visual * 1.5 * this.buff.visual)) * memoryAppealMagnification[i]));
        memoryAppeal.visual = (Number.parseInt((Number.parseInt(this.produceIdolBaseAppeal.vocal * 1.5 * this.buff.vocal)) * memoryAppealMagnification[i])) + (Number.parseInt((Number.parseInt(this.produceIdolBaseAppeal.dance * 1.5 * this.buff.dance)) * memoryAppealMagnification[i])) + (Number.parseInt((Number.parseInt(this.produceIdolBaseAppeal.visual * 1.5 * this.buff.visual)) * memoryAppealMagnification[i] * 2));
        memoryAppealLists.push(memoryAppeal);
      }
      // console.log('memoryAppeal', memoryAppealLists);
      return memoryAppealLists;
    }
  },
  method: {
    produceOrSupport(index) {
      return index < 4 ? "サポート" : "プロデュース";
    }
  },
  data() {
    return {
      visiblePerfect: true,
      visibleGood: true,
      visibleNormal: true
    }
  },
  methods: {
  }
}
</script>

<style scoped lang="scss">
.output-part {
  font-size: 15px;
}
.one-part {
  border-bottom: solid 1px;
}
.self-dense {
  padding: 3px;
  text-align: right;
}
.vocal-part {
  color: #ff80d6;
}
.dance-part {
  color: #80c8ff;
}
.visual-part {
  color: #ffc850;
}
</style>