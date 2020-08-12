<template>
  <div>
    <v-container>
      <v-row justify="center" align="center">
        <v-col sm="10" md="8" lg="6" class="text-center">
          <h2>Enter login details</h2>
          <form>
            <v-text-field
              v-model="name"
              :error-messages="nameErrors"
              :counter="10"
              label="Username"
              required
              @input="$v.name.$touch()"
              @blur="$v.name.$touch()"
            ></v-text-field>
            <v-text-field
              v-model="email"
              :error-messages="emailErrors"
              label="E-mail"
              required
              @input="$v.email.$touch()"
              @blur="$v.email.$touch()"
            ></v-text-field>
            <v-btn class="mr-4" @click="submit">submit</v-btn>
            <v-btn @click="clear">clear</v-btn>
          </form>
          <h3 v-if="success" class="mt-12">
            Login successful, redirecting you to the Feed...
          </h3>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength, maxLength, email } from 'vuelidate/lib/validators'

export default {
  mixins: [validationMixin],

  validations: {
    name: { required, minLength: minLength(3), maxLength: maxLength(10) },
    email: { required, email },
  },

  data: () => ({
    name: '',
    email: '',
    success: false,
  }),

  computed: {
    nameErrors() {
      const errors = []
      if (!this.$v.name.$dirty) return errors
      !this.$v.name.maxLength &&
        errors.push('Name must be at most 10 characters long')
      !this.$v.name.minLength &&
        errors.push('Name must be at least 3 characters long')
      !this.$v.name.required && errors.push('Name is required.')
      return errors
    },
    emailErrors() {
      const errors = []
      if (!this.$v.email.$dirty) return errors
      !this.$v.email.email && errors.push('Must be valid e-mail')
      !this.$v.email.required && errors.push('E-mail is required')
      return errors
    },
  },

  methods: {
    submit() {
      this.$v.$touch()
      this.success = true
      setTimeout(() => this.$router.push('feed'), 3000)
    },
    clear() {
      this.$v.$reset()
      this.name = ''
      this.email = ''
    },
  },
}
</script>

<style></style>
