<template>
  <v-container fluid mt-5>
    <v-row align="center" justify="center">
      <v-col cols="7">
        <v-hover>
          <template v-slot="{ hover }">
            <v-card :elevation="hover ? 6 : 3" class="text-center pa-8">
            <BakeryBoxContent/>
            </v-card>
          </template>
        </v-hover>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import BakeryBoxContent from "./BakeryBoxContent";

export default {
  name: "BakeryBox",
  components: {
    BakeryBoxContent
  }
};
</script>

<style>
</style>