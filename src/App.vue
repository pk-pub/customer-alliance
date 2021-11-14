<template>
  <div id="app">
    <Questionaire />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Questionaire from "@/components/Questionaire.vue";

@Component({
  components: {
    Questionaire
  },
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
