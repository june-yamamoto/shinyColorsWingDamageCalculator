<template>
  <div>
    <v-data-table :headers="supportIdolHeader"
                  :items="supportIdol"
                  show-select
                  class="support-idol-input">
      <template v-slot:top>
        <v-toolbar flat class="elevation-1">
          <v-toolbar-title>
            Sアイドル
          </v-toolbar-title>
          <v-spacer></v-spacer>
          <SupportIdolStatusEditDialog
            :editedIdol="editedIdol"
            :editedIndex="editedIndex"
            :supportIdol="supportIdol"
            @addSupportIdol="addSupportIdol"
            @editSupportIdol="editSupportIdol"
            @closeDialog="closeDialog"></SupportIdolStatusEditDialog>
        </v-toolbar>
      </template>
      <template v-slot:item.actions="{ item }">
        <v-icon small
                class="mr-2"
                @click="throwEditSupportIdol(item)">mdi-pencil</v-icon>
        <v-icon small
                class="mr-2"
                @click="deleteIdol(item)">mdi-delete</v-icon>
      </template>
    </v-data-table>
  </div>
</template>

<script>
import SupportIdolStatusEditDialog from "./SupportIdolStatusEditDialog"

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
  data() {
    return {
      supportIdolHeader: [
        {
          text: "名前",
          value: "name"
        },{
          text: "アイドル名",
          value: "idolName"
        },{
          text: "Voステ",
          value: "vocalStatus"
        },{
          text: "Daステ",
          value: "danceStatus"
        },{
          text: "Viステ",
          value: "visualStatus"
        },{
          text: "Vo倍率",
          value: "vocalMagnification"
        },{
          text: "Da倍率",
          value: "danceMagnification"
        },{
          text: "Vi倍率",
          value: "visualMagnification"
        },{
          text: "種類",
          value: "skillType"
        },{
          text: "",
          value: "actions",
          sortable: false
        }
      ],
      editedIdol: {},
      editedIndex: -1,
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
    }
  },
  methods: {
    addSupportIdol() {
      this.$emit('addSupportIdol', this.editedIdol);
    },
    editSupportIdol() {
      this.$emit('editSupportIdol', this.editedIdol, this.editedIndex);
      console.log('editIdol');
    },
    throwEditSupportIdol(item) {
      this.editedIndex = this.supportIdol.indexOf(item);
      this.editedIdol = Object.assign({}, item);
    },
    deleteIdol(item) {
      const deleteIdolIndex = this.supportIdol.indexOf(item);
      this.$emit('deleteSupportIdol', deleteIdolIndex);
    },
    closeDialog() {
      this.editedIndex = -1;
      this.editedIdol = this.defaultIdol;
    }
  }
};
</script>

<style scoped></style>
