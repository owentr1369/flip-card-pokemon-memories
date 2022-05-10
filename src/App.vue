<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <InteractScreen v-if="statusMatch === 'match'" />
</template>

<script>
import MainScreen from "@/components/MainScreen.vue";
import InteractScreen from "@/components/InteractScreen.vue";
// import ResultScreen from "@/components/ResultScreen.vue";
// import CopyrightScreen from "@/components/CopyrightScreen.vue";
export default {
  name: "App",
  data() {
    return {
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log("running handle before start", config);
      this.statusMatch = "match";
    },
  },
  components: { MainScreen, InteractScreen },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
