<template>
  <div class="mr-navbar">
    <div class="nav-icon">
      <i class="fas fa-anchor fa-3x"></i>
    </div>
    <div class="mr-name">Match Report</div>
    <div class="left-bar">
      <a class="lb-icon" href="https://www.twitter.com/loki_ssb" target="_blank">
        <i class="fab fa-twitter fa-2x"></i>
      </a>
      <a class="lb-icon" href="https://www.github.com/rjm0017" target="_blank">
        <i class="fab fa-github fa-2x"></i>
      </a>
    </div>
  </div>
</template>

<style lang="scss" >
@import "../../node_modules/bulma/bulma.sass";

$primary-color-dark: #455a64;
$primary-color: #607d8b;
$primary-color-light: #cfd8dc;
$primary-color-text: #ffffff;
$accent-color: #ff5252;
$primary-text-color: #212121;
$secondary-text-color: #757575;
$divider-color: #bdbdbd;

.mr-navbar {
  color: $accent-color;
  background-color: #455a64;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
  a {
    color: $accent-color;
  }
  .nav-icon {
    margin: 0.5rem;
    color: $accent-color;
  }
  .mr-name {
    margin: 0.5em;
    font-size: 150%;
    font-weight: 500;
    justify-content: center;
    align-content: center;
    color: $accent-color;
    @include mobile {
      display: none;
    }
  }
  .left-bar {
    display: flex;
    justify-content: space-between;
    margin-left: auto;
    margin-right: 0.5em;
    .lb-icon {
      margin-left: 0.5em;
    }
  }
}
</style>
