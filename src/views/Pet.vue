<template>
  <div>
    <h1>{{ animal.name }} ({{ $route.params.species }})</h1>
    <h4>Age: {{ animal.age }} years old</h4>
    <h4>Breed: {{ animal.breed }}</h4>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data () {
    return {
      animal: {}
    }
  },
  computed: {
    ...mapState([
      'cats',
      'dogs'
    ])
  },
  mounted () {
    const animal = this[this.$route.params.species][this.$route.params.id]
    this.animal = animal
  }
}
</script>
