<template>
  <section class="toy-filter">
    <input v-focus v-model="filterBy.name" @input="setFilter" type="text" class="form-input"
      placeholder="Search name..." />

    <label>
      <label-filter @labels="labels" />
    </label>

    <!-- Note: this code is correct,i don't use it because label-filter cmp -->
    <!-- <select @change="setFilter" v-model="filterBy.label">

      <option value="All">All</option>
      <option value="Doll">Doll</option>
      <option value="Battery Powered">Battery Powered</option>
      <option value="Baby">Baby</option>
    </select> -->


    <label>
      Show only toys in stock
      <input name="inStock" @change="setFilter" checked="true" type="checkbox" />
      <!-- <input name="inStock" @change="setFilter" type="checkbox" /> -->
    </label>

    <!-- <toggle-btn name="inStock"  @change="setFilter" checked="true" v-model="inStock" /> -->



  </section>
  {{ filterBy }}
</template>

<script>
import toggleBtn from './toggle-btn-filter.vue'
import labelFilter from './label-filter.vue'

export default {
  name: 'toy-filter',
  data() {
    return {
      filterBy: {
        name: '',
        label: 'All',
        inStock: true,
        // isOn: true,
      },
    }
  },
  created() {
    this.$emit('setFilter', this.filterBy)
  },

  methods: {
    setFilter({ target }) {
      if (target.name === 'inStock') {
        this.filterBy.inStock = !this.filterBy.inStock
      }
      this.$emit('setFilter', this.filterBy)
    },
    labels(value) {
      console.log(value)
      this.filterBy.label = value
      this.setFilter({ target: { name: '' } })
    }
  },
  components: {
    labelFilter,
    toggleBtn
  },
}
</script>
