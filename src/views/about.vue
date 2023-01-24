<template>
  <h1 class="chart-subtitle">Our branches</h1>
  <awesome-map />
</template>


<script>
import awesomeMap from '../components/awesome-map.vue'

export default {
  name: 'about',
  data() {
    return {
      msg: 'console.log',
    }
  },
  methods: {},
  components: {
    awesomeMap
  },
}
</script>