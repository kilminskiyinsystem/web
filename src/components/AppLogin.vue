<template>
    <v-container>
        <v-form @submit.prevent="submit">
            <v-text-field
            label="E-mail"
            v-model="email"
            required
            ></v-text-field>

            <v-text-field
            label="Password"
            v-model="password"
            type="password"
            required
            ></v-text-field>

            <v-btn color="green" type="submit">Submit</v-btn>
        </v-form>
    </v-container>
</template>

<script>
export default {
  data () {
    return {
      email: null,
      password: null
    }
  },
  methods: {
    submit () {
      console.log(`Email is ${this.email} and Password is ${this.password}`)
    }
  }
}
</script>
