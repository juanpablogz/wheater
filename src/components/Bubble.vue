<template>
<div>
  <div class="position">
      <div class="bubble">
        <img :src="`http://openweathermap.org/img/w/${forecast[0]['wheater'].icon}.png`" alt="">
      </div>
      <div class="bubble-2">
        {{forecast[0].tem_max}}
      </div>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    image: {
      type: String,
      required: false
    },
    width: {
      type: [Number, String],
      default: "64"
    },
    height: {
      type: [Number, String],
      default: "64"
    },
    forecast: {
      type: [Array],
      default: "sin datos"
    }
  },
  computed: {

  }
};
</script>

<style scoped>
  .position {
    position: absolute;
  }
</style>
