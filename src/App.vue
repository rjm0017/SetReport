<template>
  <div id="app">
    <navbar></navbar>
    <match-record></match-record>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import MatchRecord from "./components/MatchRecord.vue";
export default {
  name: "app",
  components: {
    Navbar,
    MatchRecord
  }
};
</script>

<style lang="scss">
//style guide:
$primary-color-dark: #455a64;
$primary-color: #607d8b;
$primary-color-light: #cfd8dc;
$primary-color-text: #ffffff;
$accent-color: #ff5252;
$primary-text-color: #212121;
$secondary-text-color: #757575;
$divider-color: #bdbdbd;

.app {
  width: 100%;
  display: flex;
  flex-direction: column;
}
</style>
