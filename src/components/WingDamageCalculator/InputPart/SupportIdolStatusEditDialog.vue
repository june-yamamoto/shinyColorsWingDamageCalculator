<template>
  <v-dialog v-model="isVisibleDialog" max-width="500">
    <template v-slot:activator="{on, attrs}">
      <v-btn color="primary" @click="openDialog" dark class="mb-2 add-button" v-bind="attrs" v-on="on">追加</v-btn>
    </template>
    <v-card>
      <v-card-title>
        <span class="headline">{{formTitle}}</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-form ref="form" v-model="valid">
            <v-row>
              <v-col cols="12" sm="4" md="4">
                <v-text-field v-model="editedIdol.name" label="名前" :rules="nameRules"></v-text-field>
              </v-col>
              <v-col cols="12" sm="4" md="4">
                <v-select
                  :items="idolNameLists"
                  label="アイドル名"
                  v-model="editedIdol.idolName"
                  outlined
                  :rules="selectRules"
                ></v-select>
              </v-col>
              <v-col cols="12" sm="4" md="4"></v-col>
              <v-col cols="12" sm="4" md="4">
                <v-text-field v-model.number="editedIdol.vocalStatus" label="Voステ" :rules="statusRules"></v-text-field>
              </v-col>
              <v-col cols="12" sm="4" md="4">
                <v-text-field v-model.number="editedIdol.danceStatus" label="Daステ" :rules="statusRules"></v-text-field>
              </v-col>
              <v-col cols="12" sm="4" md="4">
                <v-text-field v-model.number="editedIdol.visualStatus" label="Viステ" :rules="statusRules"></v-text-field>
              </v-col>
              <v-col cols="12" sm="4" md="4">
                <v-text-field
                  v-model.number="editedIdol.vocalMagnification"
                  label="Vo倍率"
                  :rules="skillRules"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="4" md="4">
                <v-text-field
                  v-model.number="editedIdol.danceMagnification"
                  label="Da倍率"
                  :rules="skillRules"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="4" md="4">
                <v-text-field
                  v-model.number="editedIdol.visualMagnification"
                  label="Vi倍率"
                  :rules="skillRules"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="6" class="skill-dropdown">
                <v-select
                  :items="skillTypeLists"
                  label="スキルのタイプ"
                  v-model="editedIdol.skillType"
                  outlined
                  :rules="selectRules"
                ></v-select>
              </v-col>
            </v-row>
          </v-form>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" text @click="close">キャンセル</v-btn>
        <v-btn color="blue darken-1" text @click="save" :disabled="!valid">追加</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  components: {},
  computed: {
    formTitle() {
      return this.editedIndex === -1
        ? "アイドルを追加する"
        : "アイドルを編集する";
    },
    isVisibleDialog() {
      const editedFlag = this.editedIndex !== -1;
      return this.dialog || editedFlag;
    }
  },
  props: {
    editedIndex: Number,
    editedIdol: {
      name: String,
      idolName: String,
      vocalStatus: Number,
      danceStatus: Number,
      visualStatus: Number,
      vocalMagnification: Number,
      danceMagnification: Number,
      visualMagnification: Number,
      skillType: String
    }
  },
  mounted() {
    this.mounted = true;
  },
  data() {
    return {
      valid: false,
      mounted: false,
      dialog: false,
      defaultIdol: {
        name: "",
        idolName: "櫻木真乃",
        vocalStatus: 0,
        danceStatus: 0,
        visualStatus: 0,
        vocalMagnification: 0,
        danceMagnification: 0,
        visualMagnification: 0,
        skillType: "Normal"
      },
      skillTypeLists: ["Normal", "Excellent"],
      idolNameLists: ["櫻木 真乃", "風野 灯織", "八宮 めぐる",
                      "月岡 恋鐘","幽谷 霧子","田中 摩美々","白瀬 咲耶", "三峰 結華",
                      "桑山 千雪","大崎 甜花", "大崎 甘奈",
                      "小宮 果穂","園田 智代子","杜野 凛世","西城 樹里","有栖川 夏葉",
                      "芹沢 あさひ","黛 冬優子","和泉 愛依",
                      "浅倉 透","樋口 円香","福丸 小糸","市川 雛菜"],
      on: false,
      statusRules: [v => /^([1-9]\d*|0)$/.test(v) || "正の整数値"],
      skillRules: [v => (v >= 0 && !isNaN(v)) || "正の数"],
      nameRules: [v => (v && v.length > 0) || "何か入力してください"],
      selectRules: [v => (v && v.length > 0) || "何か選択してください"]
    };
  },
  methods: {
    openDialog() {
      this.dialog = true;
    },
    close() {
      this.$emit("closeDialog");
      this.dialog = false;
    },
    save() {
      // ここに、アイドル追加の処理を書く
      if (this.editedIndex > -1) {
        this.$emit("editSupportIdol");
      } else {
        this.$emit("addSupportIdol");
      }
      this.$emit("closeDialog");
      this.dialog = false;
    }
  }
};
</script>

<style scoped>
.v-select .skill-dropdown {
  font-size: 1.2em;
}
.add-button {
  margin-left: 10px;
}
</style>