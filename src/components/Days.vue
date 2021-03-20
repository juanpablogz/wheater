<template>
  <q-page>
  <div>
    <p>3 Days Forecast</p>
    <div v-for="wheater in forecast" :key="wheater.id">
      <div class="elevate" :style="size">
        <div class="description">
          <div>
            <img :src="`http://openweathermap.org/img/w/${wheater['wheater'].icon}.png`" alt="">
            
          </div>
          <div class="days">
            <div>{{wheater['date']}}</div>
            <div>{{wheater['wheater'].main}}</div>
          </div>
          <div class="temperature">
            {{wheater['tem_max']}} / {{wheater['tem_min']}}
          </div>
        </div>
      </div>
    </div>
  </div>
  </q-page>
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
    size() {
      return {
        width: this.width + "px",
        height: this.height + "px"
      };
    },
  }
};
</script>

<style></style>
