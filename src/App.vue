<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="setting.cardsContext"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
//import { shuffleArray } from "./utils/array.js";
export default {
  name: "App",
  data() {
    return {
      setting: {
        totalOfBlock: 0,
        cardsContext: null,
        startedAt: null,
      },
      statusMatch: "default",
    };
  },
  components: {
    MainScreen,
    InteractScreen,
  },
  methods: {
    onHandleBeforeStart(config) {
      const firstArray = Array.from(
        { length: config.totalOfBlock / 2 },
        (_, index) => 1 + index * 1
      );
      const secondArray = [...firstArray];
      const lastArray = firstArray.concat(secondArray);
      this.setting.cardsContext = lastArray.sort(() => {
        return Math.random() - 0.5;
      });
      this.setting.totalOfBlock = config.totalOfBlock;
      this.setting.startedAt = new Date().getTime();
      // before start
      this.statusMatch = "match";
    },
  },
};
</script>
