<template>
  <v-app>
    <BakeryBox/>
  </v-app>
</template>

<script>
import BakeryBox from "./components/BakeryBox";

export default {
  name: 'App',
  components: {
    BakeryBox
  },
  data: () => ({
    //
  }),
};
</script>
