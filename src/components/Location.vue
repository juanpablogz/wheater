<template>
  <div>
<div>
    <div class="elevate" :style="size">
      <div class="description">
        <div>
          <img src="http://openweathermap.org/img/w/10n.png" alt="">
        </div>
        <div class="days">
          <div>Friday</div>
          <div>Rain</div>
        </div>
        <div class="temperature">
          32 / 23
        </div>
      </div>
    </div>
    <div class="elevate" :style="size">
      <div class="description">
        <div>
          <img src="http://openweathermap.org/img/w/10n.png" alt="">
        </div>
        <div class="days">
          <div>Friday</div>
          <div>Rain</div>
        </div>
        <div class="temperature">
          32 / 23
        </div>
      </div>
    </div>
</div>
    <div class="elevate elevate-custom">
        <h5>add location</h5>
        <div style="display: flex; justify-content:center">
            <img src="https://res.cloudinary.com/dutj1bbos/image/upload/c_scale,w_130/v1616196909/cherry-584_tmw938.png" alt="">
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
    temperature: {
      type: String,
      default: "temperature"
    }
  },
  computed: {
    size() {
      return {
        width: this.width + "px",
        height: this.height + "px"
      };
    }
  }
};
</script>

<style></style>
