<template>
  <div class="home-view-container">
    <h1>Adopt a new best friend.</h1>
    {{ getAllCats.length }} cats
    <br>
    &
    <br>
    {{ getAllDogs.length }} dogs
    <br>
    {{ animalsCount }} total animals
    <br>
    <br>
    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          type="text"
          v-model="formData.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Breed:" label-for="input-2">
        <b-form-input
          id="input-2"
          type="text"
          v-model="formData.breed"
          required
          placeholder="Enter Breed"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-3" label="Gender:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="formData.gender"
          :options="['male', 'female']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-2">
        <b-form-input
          id="input-2"
          type="number"
          v-model="formData.age"
          required
          placeholder="Enter age"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>

  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        breed: '',
        species: null,
        gender: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats',
      'getAllDogs'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name, breed, gender } = this.formData
      const payload = {
        species,
        pet: {
          name,
          breed,
          species,
          age,
          gender
        }
      }
      this.addPet(payload)

      // reset form after submit
      this.formData = {
        name: '',
        age: 0,
        breed: '',
        species: null,
        gender: null
      }
    }
  }
}
</script>
