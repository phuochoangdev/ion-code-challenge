<template>
  <el-date-picker
    v-model="date"
    :value="date"
    v-on:click="onChange($event)"
    v-on:change="onChange($event)"
    type="date"
    placeholder="Pick a day"
    class="date-time"
    :disabled="disabled">
  </el-date-picker>
</template>
<script>
export default {
  name: 'date-picker',
  props: {
    value: [String, Number, Date],
    disabled: Boolean,
    required: Boolean
  },
  data () {
    return {
      date: this.value
    }
  },
  watch: {
    value () {
      this.date = typeof this.value === 'string' ? parseInt(this.value) : this.value
    }
  },
  methods: {
    onChange (e) {
      this.$emit('pick', new Date(e))
      this.$emit('input', e)
    }
  }
}
</script>
<style scoped>
  .date-time {
    width: 100%;
  }
</style>
