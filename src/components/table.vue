<template>
  <div class="table">
    <table>
      <thead>
        <tr>
          <th v-for="(item, index) in config" :key="index">{{item.title}}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in data" :key="index">
          <td v-for="(items, indexs) in config" :key="indexs" v-if="item[items.key]">{{item[items.key]}}</td>
          <td v-else>
            <slot></slot>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  props: {
    data: Array,
    config: Array
  },
  data() {
    return {}
  },
  computed: {
    button() {
      if(this.$slots.default){
        return this.$slots.default
      } else {
        return 0
      }
    }
  },
}
</script>
<style scoped>
.table{
  box-sizing: border-box;
}
.table *{
  box-sizing: inherit;
}
table{
  width: 100%;
  border-collapse: collapse;
  border-spacing: 0;
  empty-cells: show;
  border: 1px solid #e9e9e9;
}
table th{
  background: #f7f7f7;
  color: #5c6b77;
  font-weight: 600;
  white-space: nowrap;
}
table td, table th{
  padding: 8px 16px;
  border: 1px solid #e9e9e9;
  text-align: left;
}
</style>
