<template>
  <div class="home">
    <h1>Adopt a new best friend</h1>
    {{ animalsCount }}
    <button class="btn btn-primary" @click="togglePetForm">Add New Pet</button>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group id="pet-name-group" label="Pet's Name:" label-for="pet-name">
        <b-form-input id="pet-name" v-model="form.name" required placeholder="Enter name"></b-form-input>
      </b-form-group>

      <b-form-group id="species-group" label="Species:" label-for="species">
        <b-form-select id="species" v-model="form.species" :options="['cats', 'dogs']" required></b-form-select>
      </b-form-group>

      <b-form-group id="age-group" label="Pet's Age:" label-for="age">
        <b-form-input id="age" v-model="form.age" required placeholder="Enter age" type="number"></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex"
export default {
  name: "Home",
  data() {
    return {
      showPetForm: false,
      form: {
        name: "",
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters(["animalsCount"])
  },
  methods: {
    ...mapActions(["addPet"]),
    togglePetForm() {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit() {
      const { species, age, name } = this.form
      const payload = {
        species,
        pet: { name, age }
      }
      this.addPet(payload)
      this.form = { name: "", age: 0, species: null }
    }
  }
}
</script>
