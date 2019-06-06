<template>
  <div class="imageBlock">
    <div class="block" v-for="(item, index) in data" :key="index" :style="{width: itemWidth+'%'}">
      <a :href="item.link" class="links">
        <div class="img">
          <img :src="item.img" :alt="item.alt">
        </div>
        <p>{{item.text}}</p>
      </a>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    column: String | Number,
    data: Array
  },
  computed: {
    itemWidth() {
      return 100 / this.column - 2
    }
  },
  data() {
    return {}
  }
}
</script>
<style scoped>
.imageBlock{
  box-sizing: border-box;
}
.imageBlock::after{
  content: '';
  display: block;
  clear: both;
}
.imageBlock *{
  box-sizing: inherit;
}
.block{
  float: left;
  box-shadow: 4px 4px 8px #e1e1e1;
  margin: 0 1%;
}
.block:hover{
  transform: scale(1.01);
  box-shadow: 8px 8px 16px #d7d7d7;
}
.links{
  display: inline-block;
  text-decoration: none;
  color: #333;
}
.img img{
  width: 100%;
}
</style>
