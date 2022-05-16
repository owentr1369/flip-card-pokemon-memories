<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <InteractScreen
    v-if="statusMatch === 'match'"
    :cardContext="settings.cardContext"
    @onFinish="onGetResult"
  />
  <ResultScreen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  />
  <CopyrightScreen />
</template>

<script>
import MainScreen from "@/components/MainScreen.vue";
import InteractScreen from "@/components/InteractScreen.vue";
import ResultScreen from "@/components/ResultScreen.vue";
import CopyrightScreen from "@/components/CopyrightSceen.vue";
import { shuffled } from "@/utils/array";
// import ResultScreen from "@/components/ResultScreen.vue";
// import CopyrightScreen from "@/components/CopyrightScreen.vue";
export default {
  name: "App",
  components: { MainScreen, InteractScreen, ResultScreen, CopyrightScreen },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
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
    onGetResult() {
      // get timer
      this.timer = new Date().getTime() - this.settings.startedAt;

      // switch to result component
      this.statusMatch = "result";
    },
  },
};
</script>

<style>
</style>
