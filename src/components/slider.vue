<template>
  <div class="slider">
    <div class="line" ref="line" @mousedown="dragStart" :style="{width: width + 'px'}">
      <div class="complete" :style="{width: value + '%', backgroundColor: color}"></div>
      <div class="btn" :style="{left: percent}"></div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    color: String,
    value: {
      type: Number,
      default: 50
    },
    width: String
  },
  computed: {
    percent() {
      return 'calc(' + this.value + '% - 10px)'
    }
  },
  data() {
    return {
      beforeX: '',
      afterX: '',
      drag: false,
      lineWidth: ''
    }
  },
  mounted() {
    window.onmousemove = (event) => {
      this.dragBtn(event);
    }
    window.onmouseup = (event) => {
      this.dragEnd(event);
    }
  },
  methods: {
    dragStart(){
      this.drag = true;
      this.lineWidth = this.$refs.line.offsetWidth
    },
    dragBtn(event) {
      if(this.drag){
        let e = event || window.event;
        this.afterX = e.pageX;
        let lineX = this.$refs.line.offsetLeft;
        let minus = this.afterX - lineX;
        let after = minus / this.lineWidth * 100
        if(after > 100){
          after = 100
        } else if(after < 0){
          after = 0
        }
        this.$emit('input', after)
      }
    },
    dragEnd() {
      this.drag = false
    }
  },
}
</script>
<style scoped>
.slider{
  box-sizing: border-box;
}
.slider *{
  box-sizing: inherit;
}
.line,.complete{
  height: 5px;
  border-radius: 5px;
  position: relative;
}
.line{
  display: inline-block;
  background-color: #e1e1e1;
}
.btn{
  height: 20px;
  width: 20px;
  border-radius: 10px;
  border: 1px solid #d7d7d7;
  background-color: #fff;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
}
</style>
