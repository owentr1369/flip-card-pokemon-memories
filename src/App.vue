<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <InteractScreen
    v-if="statusMatch === 'match'"
    :cardContext="settings.cardContext"
  />
</template>

<script>
import MainScreen from "@/components/MainScreen.vue";
import InteractScreen from "@/components/InteractScreen.vue";
import { shuffled } from "@/utils/array";
// import ResultScreen from "@/components/ResultScreen.vue";
// import CopyrightScreen from "@/components/CopyrightScreen.vue";
export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardContext: [],
        startedAt: null,
      },
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log("running handle before start", config);
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCard = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCard = [...firstCard];
      const cards = [...firstCard, ...secondCard];

      this.settings.cardContext = shuffled(shuffled(shuffled(cards)));
      this.settings.startedAt = new Date().getTime();

      this.statusMatch = "match";
    },
  },
  components: { MainScreen, InteractScreen },
};
</script>

<style>
</style>
