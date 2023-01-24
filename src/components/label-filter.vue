<template>
  <div style="display: inline-block">
    <p style="margin-left: 10px">Choose Tags</p>
    <el-select v-model="value" multiple placeholder="All" style="width: 240px">

      <el-option 
      v-for="item in options" 
      :key="item.value" 
      :label="item.label" 
      :value="item.value" 
      @click="labels" />

    </el-select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: [],
      options: [
        {
          value: 'All',
          label: 'All',
        },
        {
          value: 'Doll',
          label: 'Doll',
        },
        {
          value: 'Battery Powered',
          label: 'Battery Powered',
        },
        {
          value: 'Baby',
          label: 'Baby',
        },
      ]

    }
  },
  methods: {
    labels() {
      this.$emit('labels', this.value)
    }
  }
}
</script>
