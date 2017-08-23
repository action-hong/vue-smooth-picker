<template>
  <div>
    <smooth-picker :data="data" :change="change" ref="timePicker"></smooth-picker>
    <p>{{ value }}</p>
  </div>
</template>

<script>
export default {
  props: ['value'],
  data () {
    return {
      data: [
        {
          currentIndex: 0,
          flex: 1,
          list: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
        },
        {
          currentIndex: 1,
          flex: 1,
          list: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
        }
      ]
    }
  },
  methods: {
    change (gIndex, iIndex) {
      this.data[gIndex].currentIndex = iIndex
      this.$emit('input', this.data[0].currentIndex * 10 + this.data[1].currentIndex)
    }
  },
  watch: {
    value: function (val) {
      console.log(val)
      let min = Math.floor(Number(val) / 10)
      let sec = Number(val) % 10
      //ugly, need fix source code
      this.$refs.timePicker.setGroupData(0, Object.assign({}, this.data[0], {currentIndex: min}))
      this.$refs.timePicker.setGroupData(1, Object.assign({}, this.data[1], {currentIndex: sec}))
      this.$refs.timePicker.correctionCurrentIndex(null, 0)
      this.$refs.timePicker.correctionCurrentIndex(null, 1)
    }
  }
}
</script>

<style>

</style>
