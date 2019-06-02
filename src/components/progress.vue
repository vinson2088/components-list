<template>
  <div class="progress">
    <div class="progress-box">
      <div
        class="progress-bar"
        :style="{width: percent + '%', backgroundColor: color}"
      >{{percent + '%'}}</div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    percent: String | Number,
    color: String
  },
  data() {
    return {};
  }
};
</script>
<style scoped>
.progress {
  display: inline-block;
  max-width: 300px;
  width: 100%;
  box-sizing: border-box;
}
.progress * {
  box-sizing: inherit;
}
.progress-box {
  border: 1px solid #e1e1e1;
  border-radius: 10px;
  height: 20px;
  background-color: #e1e1e1;
}
.progress-bar {
  border-radius: 10px;
  height: 20px;
  transition: all 0.5s;
  color: #fff;
  text-align: right;
  font-size: 15px;
  line-height: 20px;
  padding-right: 5px;
}
</style>
