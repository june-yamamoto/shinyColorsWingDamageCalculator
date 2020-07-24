<template>
  <v-app-bar>
    <v-btn @click="natsuha()">Wing計算機</v-btn>
    <v-spacer></v-spacer>
    ver 0.1.1
  </v-app-bar>
</template>

<script>
export default {

  methods: {
    natsuha() {
      alert('いい？目指すならトップだけよ！！');
    }
  }
};
</script>