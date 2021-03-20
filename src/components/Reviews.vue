<template>
  <div>
    <p>Top reviews</p>
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
