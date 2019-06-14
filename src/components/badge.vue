<template>
  <div class="badge">
    <slot></slot>
    <sup class="badge-box" :style="{backgroundColor: color}">{{value}}</sup>
  </div>
</template>
<script>
export default {
  props: {
    value: {
      type: String | Number,
      default: "0"
    },
    color: {
      type: String,
      default: "#f00"
    }
  },
  data() {
    return {};
  }
};
</script>
<style scoped>
.badge {
  box-sizing: border-box;
  position: relative;
  display: inline-block;
}
.badge * {
  box-sizing: inherit;
}
.badge-box {
  position: absolute;
  top: 0;
  right: 10px;
  transform: translateY(-50%) translateX(100%);
  border-radius: 10px;
  color: #fff;
  display: inline-block;
  font-size: 12px;
  height: 18px;
  line-height: 18px;
  padding: 0 6px;
  text-align: center;
  white-space: nowrap;
  border: 1px solid #fff;
}
</style>