<template>
  <section v-if="toyToEdit" class="toy-edit py-2">
    <!-- {{  toyToEdit }} -->
    <form @submit.prevent="saveToy" class="form">
      <div class="form-control">
        <label for="txt" class="form-label">Toy Name</label>
        <input required v-model="toyToEdit.name" id="txt" type="text" class="form-input"
          placeholder="Enter your toy name here..." />
      </div>
      <div class="form-control">
        <label for="price" class="form-label">Toy Price</label>
        <input required v-model.number="toyToEdit.price" id="price" type="number" class="form-input" />
      </div>
      <div class="btn-group">
        <button @click="saveToy" class="btn btn-info">save</button>
        <button @click="goBack" class="btn btn-danger-text">go back</button>
      </div>
    </form>
  </section>

  <pre>{{ toyToEdit }}</pre>
  <h1 v-if="filterBy"> Page:{{ filterBy.page }}</h1>
</template>

<script>

import { httpService } from '../services/http.service'
import { toyService } from '../services/toy-service'

export default {
  name: 'toy-edit',
  data() {
    return {
      toyToEdit: null,
      filterBy: {
        name: null,
        page: null,
      }
    }
  },

  created() {
    this.filterBy.page = this.$store.getters.page || 0

    const { id } = this.$route.params
    if (id) {
      httpService.get(`toy/${id}`)
        .then((toy) => {
          this.toyToEdit = toy
        })
    }
    else this.toyToEdit = toyService.getEmptyToy()

  },
  methods: {
    goBack() {
      this.$router.push('/toy')
    },
    saveToy() {
      this.$store.dispatch({ type: 'saveToy', toy: this.toyToEdit })
        .then(() => {
          this.$store.dispatch({ type: 'loadToys', filterBy: this.filterBy })
          this.$router.push('/toy')

        })
    },
  },
}
</script>
