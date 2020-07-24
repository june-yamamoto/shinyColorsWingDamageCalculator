<template>
  <div class="root-card">
    <v-row justify="center">
      <v-col cols="12" lg="10" md="11" sm="12">
        <v-card class="second-card">
          <InputStatusPart
            :supportIdol="supportIdol"
            @addSupportIdol="addSupportIdol"
            @editSupportIdol="editSupportIdol"
            @deleteSupportIdol="deleteSupportIdol"
            @updateProduceIdolStatus="updateProduceIdolStatus"
            @updateSelectedSupportIdol="updateSelectedSupportIdol"
            @saveLocalStorage="saveLocalStorage"></InputStatusPart>
        </v-card>
        <v-card class="second-card">
          <SettingPart @updateSettings="updateSettings"></SettingPart>
        </v-card>
        <v-card class="second-card">
          <OutputPart :supportIdol="selectedSupportIdol"
                      :produceIdolStatus="produceIdolStatus"
                      :produceIdolSkills="produceIdolSkills"
                      :week="week"
                      :buff="buffPercentage"
                      v-if="this.selectedSupportIdol.length === 4"></OutputPart>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import InputStatusPart from "./WingDamageCalculator/InputStatusPart"
import SettingPart from "./WingDamageCalculator/SettingPart"
import OutputPart from "./WingDamageCalculator/OutputPart"

export default {
  components: {
    InputStatusPart,
    OutputPart,
    SettingPart
  },
  mounted() {
    this.initializeIdols();
  },
  data() {
    return {
      supportIdol : [],
      selectedIdol: [],
      produceIdolStatus : {
        name: "",
        vocalStatus: 50,
        danceStatus: 50,
        visualStatus: 50
      },
      produceIdolSkills : [],
      week: 1,
      buff: {
        vocal: 0,
        dance: 0,
        visual: 0
      }
    }
  },
  computed: {
    selectedSupportIdol() {
      const selectedIdolLists = [];
      this.selectedIdol.forEach(value => {
        selectedIdolLists.push(this.supportIdol[value]);
      });
      return selectedIdolLists;
    },
    buffPercentage() {
      const buff = {};
      buff.vocal = (this.buff.vocal + 100)/100;
      buff.dance = (this.buff.dance + 100)/100;
      buff.visual = (this.buff.visual + 100)/100;
      return buff
    }
  },
  methods: {
    initializeIdols() {
      const test = false;
      // console.log('initialize');
      if(test) {
        const defaultSupportIdol = {
          name: "駅真乃",
          idolName: "櫻木真乃",
          vocalStatus: 150,
          danceStatus: 240,
          visualStatus: 300,
          vocalMagnification: 0,
          danceMagnification: 2,
          visualMagnification: 2,
          skillType: "Normal"
        };
        const defaultSupportIdol2 = {
          name: "釣りみ",
          idolName: "田中摩美々",
          vocalStatus: 263,
          danceStatus: 233,
          visualStatus: 238,
          vocalMagnification: 3.5,
          danceMagnification: 0,
          visualMagnification: 0,
          skillType: "Excellent"
        };
        const defaultSupportIdol3 = {
          name: "ハッピー甘奈",
          idolName: "大崎甘奈",
          vocalStatus: 170,
          danceStatus: 195,
          visualStatus: 255,
          vocalMagnification: 0,
          danceMagnification: 0,
          visualMagnification: 3,
          skillType: "Normal"
        };
        const defaultSupportIdol4 = {
          name: "夜明け凛世",
          idolName: "杜野凛世",
          vocalStatus: 150,
          danceStatus: 360,
          visualStatus: 190,
          vocalMagnification: 0,
          danceMagnification: 2.5,
          visualMagnification: 0,
          skillType: "Normal"
        };
        this.addSupportIdol(defaultSupportIdol);
        this.addSupportIdol(defaultSupportIdol2);
        this.addSupportIdol(defaultSupportIdol3);
        this.addSupportIdol(defaultSupportIdol4);
      } else {
        // console.log('localStorage', JSON.parse(localStorage.getItem('supportIdolLists')));
        const savedSupportIdolLists = JSON.parse(localStorage.getItem('supportIdolLists'));
        const savedProduceIdolStatus = JSON.parse(localStorage.getItem('produceIdolStatus'));
        const savedProduceIdolSkills = JSON.parse(localStorage.getItem('produceIdolSkills'));
        if(savedSupportIdolLists) {
          for(let i = 0; i < savedSupportIdolLists.length ; i++) {
            this.addSupportIdol(savedSupportIdolLists[i]);
          };
        }

      }
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
    },
    updateSettings(week, buff) {
      this.week = Number(week);
      this.buff.vocal = Number(buff.vocal);
      this.buff.dance = Number(buff.dance);
      this.buff.visual = Number(buff.visual);
    },
    updateSelectedSupportIdol(selectedIdol) {
      this.selectedIdol = selectedIdol;
    },
    saveLocalStorage() {
      localStorage.setItem('supportIdolLists', JSON.stringify(this.supportIdol));
      localStorage.setItem('produceIdolStatus', JSON.stringify(this.produceIdolStatus));
      localStorage.setItem('produceIdolSkills', JSON.stringify(this.produceIdolSkills));
      alert('アイドル情報を保存しました');
    }
  }
}
</script>

<style scoped lang="scss">
.root-card {
  margin: 10px;
}
.second-card {
  margin: 10px;
}
</style>