<template>
  <v-dialog v-model="isVisibleDialog"
            max-width="500">
    <template v-slot:activator="{on, attrs}">
      <v-btn  color="primary"
              @click="openDialog"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on">
        追加
      </v-btn>
    </template>
    <v-card>
      <v-card-title>
        <span class="headline">{{formTitle}}</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="4" md="4">
              <v-text-field v-model="editedIdol.name"
                            label="名前"></v-text-field>
            </v-col>
            <v-col cols="12" sm="4" md="4">
              <v-select :items="idolNameLists"
                        label="アイドル名"
                        v-model="editedIdol.idolName"
                        outlined></v-select>
            </v-col>
            <v-col cols="12" sm="4" md="4"></v-col>
            <v-col cols="12" sm="4" md="4">
              <v-text-field v-model="editedIdol.vocalStatus"
                            label="Voステ"></v-text-field>
            </v-col>
            <v-col cols="12" sm="4" md="4">
              <v-text-field v-model="editedIdol.danceStatus"
                            label="Daステ"></v-text-field>
            </v-col>
            <v-col cols="12" sm="4" md="4">
              <v-text-field v-model="editedIdol.visualStatus"
                            label="Viステ"></v-text-field>
            </v-col>
            <v-col cols="12" sm="4" md="4">
              <v-text-field v-model="editedIdol.vocalMagnification"
                            label="Vo倍率"></v-text-field>
            </v-col>
            <v-col cols="12" sm="4" md="4">
              <v-text-field v-model="editedIdol.danceMagnification"
                            label="Da倍率"></v-text-field>
            </v-col>
            <v-col cols="12" sm="4" md="4">
              <v-text-field v-model="editedIdol.visualMagnification"
                            label="Vi倍率"></v-text-field>
            </v-col>
            <v-col cols="12" sm="4" md="4">
              <v-select :items="skillTypeLists"
                        label="スキルのタイプ"
                        v-model="editedIdol.skillType"
                        outlined></v-select>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" text @click="close">キャンセル</v-btn>
        <v-btn color="blue darken-1" text @click="save">追加</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  components: {},
  computed: {
    formTitle() {
      return "アイドルを追加する";
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
  // mounted() {},
  data() {
    return {
      dialog: false,
      defaultIdol: {
        name: '',
        idolName: 0,
        vocalStatus: 0,
        danceStatus: 0,
        visualStatus: 0,
        vocalMagnification: 0,
        danceMagnification: 0,
        visualMagnification: 0,
        skillType: "Normal"
      },
      skillTypeLists: ["Normal","Excellent"],
      idolNameLists: ["さくらぎまの","かざのひおり","はちみやめぐる"],
      on: false
    }
  },
  methods: {
    openDialog() {
      this.dialog = true;
    },
    close() {
      this.$emit('closeDialog');
      this.dialog = false;
    },
    save() {
      // ここに、アイドル追加の処理を書く
      if(this.editedIndex > -1) {
        this.$emit('editSupportIdol');
      } else {
        this.$emit('addSupportIdol');
      }
      this.$emit('closeDialog');
      this.dialog = false;
    }
  }
}
</script>

<style scoped>

</style>