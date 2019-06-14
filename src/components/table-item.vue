<template>
  <div class="table-item">
    <table></table>
  </div>
</template>
<script>
export default {
  props: {
    prop: String,
    label: String
  },
  data() {
    return {}
  }
}
</script>
<style scoped>
.table-item{
  box-sizing: border-box;
}
.table-item *{
  box-sizing: inherit;
}
</style>
