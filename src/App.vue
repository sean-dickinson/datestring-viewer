<template>
  <div id="app">
    <section class="hero is-fullheight">
      <div class="hero-body">
        <div class="container">
          <div class="box level">
            <current-time class="level-item" :selectedDate="combinedDate"></current-time>
          </div>
          <div class="level">
            <div class="level-item">
              <b-datepicker v-model="date" inline></b-datepicker>
            </div>
            <div class="level-item">
              <b-clockpicker v-model="time" class="is-primary" inline></b-clockpicker>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import CurrentTime from './components/CurrentTime.vue';

@Component({
  components: {
    CurrentTime,
  },
})
export default class App extends Vue {
  public date: Date = new Date();
  public time: Date = new Date();
  get combinedDate(): Date {
    const d = new Date(this.date);
    d.setHours(this.time.getHours(), this.time.getMinutes());
    return new Date(d);
  }

  public mounted() {
    setInterval(() => {
      this.time = new Date();
    }, 20 * 1000);
  }
}
</script>

<style lang="scss">
@import "~bulma/sass/utilities/_all";

// Set your colors
$primary: #cba4f7;
$primary-invert: findColorInvert($primary);
$info: #59eabb;
$info-invert: findColorInvert($info);

// Setup $colors to use as bulma classes (e.g. 'is-twitter')
$colors: (
  "white": (
    $white,
    $black
  ),
  "black": (
    $black,
    $white
  ),
  "light": (
    $light,
    $light-invert
  ),
  "dark": (
    $dark,
    $dark-invert
  ),
  "primary": (
    $primary,
    $primary-invert
  ),
  "info": (
    $info,
    $info-invert
  ),
  "success": (
    $success,
    $success-invert
  ),
  "warning": (
    $warning,
    $warning-invert
  ),
  "danger": (
    $danger,
    $danger-invert
  )
);

// Links
$link: $primary;
$link-invert: $primary-invert;
$link-focus-border: $primary;

// Import Bulma and Buefy styles
@import "~bulma";
@import "~buefy/src/scss/buefy";

#app {
  height: 100vh;
  width: 100vw;
}

html,
body {
  margin: 0;
  background: $info;
}

.b-clockpicker{
  .card {
        border-radius: $radius;
    }

    .card-header {
        border-top-left-radius: $radius;
        border-top-right-radius: $radius;
    }
}
</style>
