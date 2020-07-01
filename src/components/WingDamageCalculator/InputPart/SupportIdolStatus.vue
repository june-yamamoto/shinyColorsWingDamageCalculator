<template>
  <div>
    <v-data-table :headers="supportIdolHeader"
                  :items="supportIdol"
                  show-select
                  class="support-idol-input">
      <template v-slot:top>
        <v-toolbar>
          <v-toolbar-title>
            Sアイドル
          </v-toolbar-title>
          <v-spacer></v-spacer>
          <SupportIdolStatusEditDialog></SupportIdolStatusEditDialog>
        </v-toolbar>
      </template>
      <template v-slot:item.actions="{ item }">
        <v-icon small
                class="mr-2"
                @click="editIdol(item)">mdi-pencil</v-icon>
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
      supportIdol: [{
        name: "駅真乃",
        idolName: 0,
        vocalStatus: 150,
        danceStatus: 260,
        visualStatus: 260,
        vocalMagnification: 0,
        danceMagnification: 2,
        visualMagnification: 2,
        skillType: "normal"
      }]
    }
  },
  methods: {
      editIdol() {
        console.log('editIdol');
      },
      deleteIdol() {
        console.log('deleteIdol');
      }
    }
};
</script>

<style scoped></style>
