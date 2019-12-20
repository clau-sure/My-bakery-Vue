<template>
  <span>
    <v-icon large color="red lighten-1">fastfood</v-icon>
    <p class="font-weight-light headline" color="blue-grey darken-3">Discover our daily menu!</p>
    <p
      class="font-weight-light"
      color="blue-grey lighten-5"
    >Please, click the following button for discovering our today's menu.</p>
    <v-btn rounded depressed @click="bakeryRequest" :disabled="this.button">
      Go!
      <v-icon small class="ml-3">restaurant_menu</v-icon>
    </v-btn>
    <p v-show="loader">
      <v-progress-circular class="mt-4" :size="25" color="red lighten-1" indeterminate></v-progress-circular>
    </p>
    <p class="mt-4">{{info}}</p>
    <p class="mt-4" v-show="message">Wait {{countDown | formatDate}} for knowing tomorrow's menu.</p>
  </span>
</template>

<script>
import filters from "../filters/filters";

export default {
  name: "BakeryBoxContent",
  data() {
    return {
      info: null,
      url:
        "https://xz94zfs6u8.execute-api.eu-west-1.amazonaws.com/default/myBakery",
      api_url: "https://cors-anywhere.herokuapp.com/",
      loader: false,
      countDown: 86400,
      message: false,
      button: false
    };
  },
  methods: {
    bakeryRequest() {
      this.loader = true;
      fetch(this.api_url + this.url)
        .then(response => {
          if (response.status >= 200 && response.status <= 299) {
            return response.json();
          } else {
            throw Error(response.statusText);
          }
        })
        .then(jsonResponse => {
          this.loader = false;
          this.countDownTimer();
          this.info = jsonResponse;
        })
        .catch(error => {
          console.log(error);
        });
    },
    countDownTimer() {
      if (this.countDown > 0) {
        setTimeout(() => {
          this.countDown -= 1;
          this.countDownTimer();
        }, 1000);
      }
      if (this.countDown != 0) {
        this.message = true;
        this.button = true;
      }
      if (this.countDown == 0) {
        this.message = false;
        this.button = false;
      }
    }
  }
};
</script>

<style>
</style>