<template>
  <el-color-picker :value="internalValue" v-on:change="onChange($event)"></el-color-picker>
</template>
<script>
export default {
  name: 'color-picker',
  props: {
    value: String
  },
  data () {
    return {
      internalValue: this.value
    }
  },
  watch: {
    value () {
      this.internalValue = this.value
    }
  },
  methods: {
    onChange (e) {
      this.$emit('input', e)
    }
  }
}
</script>
