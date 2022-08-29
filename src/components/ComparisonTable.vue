<template>
    <b-table  class="compare-table" show-empty striped hover :fields="fields" :items="items" caption-top  responsive>
      <template #table-caption>
        <b-col class="mt-5 comp-title">
          <h5 class="text-center">Comparison Table</h5>
        </b-col>
      </template>
      <template #empty>
        <h6 class="text-center no-data">No comparison data found.</h6>
      </template>
      <template v-slot:cell(thumbnailUrl)="row" >
        <b-avatar rounded="lg" :src="row.item.thumbnailUrl"></b-avatar>
      </template>
    </b-table>
</template>

<script>

export default {
  name: 'ComparisonTable',
  props: {
    fields: Array,
    items: Array,
  },
}
</script>
<style :scoped>
.no-data{margin-bottom:0; padding:12px 0;}
.comp-title{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px 5px;
  background-color: #111046;
  color: #fff;
  text-transform: uppercase;
}
.compare-table{
  margin-bottom:35px;
}
</style>
