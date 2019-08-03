<template>
  <div>
    <h4>Render a datatable using test4.json</h4>
    <p>Note: Calculate Average value, Total value </p>
    <br />
    <br />
    <line-chart :data="data"></line-chart>
  </div>
</template>

<script>
import data from './JsonFiles/test4'

export default {
  name: 'Test4',
  component: {
  },
  data () {
    return {
      data: data
    }
  },
  created () {
    this.data = data.map((item) => {
      const { data } = item
      const { Teamwork, Benefit, Career } = data

      data.Total = Teamwork + Benefit + Career
      data.Average = data.Total / 3
      item.data = data

      return item
    })
  }
}
</script>

<style scoped>

</style>
