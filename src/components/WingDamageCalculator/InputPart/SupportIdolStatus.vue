<template>
  <div>
    <v-card flat class="elevation-2">
      <v-card-title style="padding:8px;">
        Sアイドル
        <v-spacer></v-spacer>
        <v-checkbox v-model="visibleTable" label="Sアイドルを表示する"></v-checkbox>
        <SupportIdolStatusEditDialog
          :editedIdol="editedIdol"
          :editedIndex="editedIndex"
          :supportIdol="supportIdol"
          @addSupportIdol="addSupportIdol"
          @editSupportIdol="editSupportIdol"
          @closeDialog="closeDialog"
        ></SupportIdolStatusEditDialog>
      </v-card-title>
      <v-data-table :headers="supportIdolHeader" :items="supportIdol" class="support-idol-input" dense v-show="visibleTable">
        <template v-slot:item.actions="{ item }">
          <v-btn
            class="mr-2 blue lighten-5 selection-button"
            small
            @click="toggleSelected(item)"
            v-if="selected(item)"
          >使う</v-btn>
          <v-btn
            class="mr-2 selection-button"
            small
            @click="toggleSelected(item)"
            v-if="!selected(item)"
          >使わない</v-btn>
          <v-icon small class="mr-2" @click="throwEditSupportIdol(item)">mdi-pencil</v-icon>
          <v-icon small class="mr-2" @click="deleteIdol(item)">mdi-delete</v-icon>
        </template>
      </v-data-table>
    </v-card>
  </div>
</template>

<script>
import SupportIdolStatusEditDialog from "./SupportIdolStatusEditDialog";

export default {
  components: {
    SupportIdolStatusEditDialog
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
  computed: {},
  data() {
    return {
      visibleTable: true,
      selectedSupportIdol: [],
      supportIdolHeader: [
        {
          text: "名前",
          value: "name"
        },
        {
          text: "アイドル名",
          value: "idolName"
        },
        {
          text: "Voステ",
          value: "vocalStatus"
        },
        {
          text: "Daステ",
          value: "danceStatus"
        },
        {
          text: "Viステ",
          value: "visualStatus"
        },
        {
          text: "Vo倍率",
          value: "vocalMagnification"
        },
        {
          text: "Da倍率",
          value: "danceMagnification"
        },
        {
          text: "Vi倍率",
          value: "visualMagnification"
        },
        {
          text: "種類",
          value: "skillType"
        },
        {
          text: "",
          value: "actions",
          sortable: false
        }
      ],
      editedIdol: {},
      editedIndex: -1,
      defaultIdol: {
        name: "",
        idolName: 0,
        vocalStatus: 0,
        danceStatus: 0,
        visualStatus: 0,
        vocalMagnification: 0,
        danceMagnification: 0,
        visualMagnification: 0,
        skillType: ""
      }
    };
  },
  methods: {
    addSupportIdol() {
      this.$emit("addSupportIdol", this.editedIdol);
      this.editedIdol = {};
      this.editedIndex = -1;
    },
    editSupportIdol() {
      this.$emit("editSupportIdol", this.editedIdol, this.editedIndex);
      this.editedIdol = {};
      this.editedIndex = -1;
    },
    throwEditSupportIdol(item) {
      this.editedIndex = this.supportIdol.indexOf(item);
      this.editedIdol = Object.assign({}, item);
    },
    deleteIdol(item) {
      const deleteIdolIndex = this.supportIdol.indexOf(item);
      this.$emit("deleteSupportIdol", deleteIdolIndex);
    },
    closeDialog() {
      this.editedIndex = -1;
      this.editedIdol = Object.assign({}, this.defaultIdol);
    },
    toggleSelected(item) {
      const selectedIndex = this.supportIdol.indexOf(item);
      if (!this.selectedSupportIdol.includes(selectedIndex)) {
        if (this.selectedSupportIdol.length >= 4) {
          alert("4人以上選択できません");
        } else {
          this.selectedSupportIdol.push(selectedIndex);
          this.$emit('updateSelectedSupportIdol', this.selectedSupportIdol);
        }
      } else {
        const index = this.selectedSupportIdol.indexOf(selectedIndex);
        this.selectedSupportIdol.splice(index, 1);
        this.$emit('updateSelectedSupportIdol', this.selectedSupportIdol);
      }
      // console.log(this.selectedSupportIdol);
    },
    selected(item) {
      const selectedIndex = this.supportIdol.indexOf(item);
      return this.selectedSupportIdol.includes(selectedIndex);
    }
  }
};
</script>

<style scoped>
.selection-button {
  width: 60px;
  height: 30px;
}
</style>
