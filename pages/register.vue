<template>
  <div>
    <!-- Registration -->
    <form v-if="step === steps.register" @submit.prevent="register">
      <input
        v-model="registerForm.email"
        type="email"
        placeholder="Email"
        class="form-control"
      />
      <input
        v-model="registerForm.password"
        type="password"
        placeholder="Password"
        class="form-control"
      />
      <button type="submit" class="bg-blue-400">Register</button>
    </form>
    <!-- Confirmation -->
    <form v-else @submit.prevent="confirm">
      <input
        v-model="confirmForm.email"
        type="email"
        placeholder="Email"
        class="form-control"
      />
      <input
        v-model="confirmForm.code"
        type="code"
        placeholder="Code"
        class="form-control"
      />
      <button type="submit" class="bg-blue-400">Confirm</button>
    </form>
  </div>
</template>

<script>
const steps = {
  register: 'REGISTER',
  confirm: 'CONFIRM',
}
export default {
  data: () => ({
    steps: { ...steps },
    step: steps.register,
    registerForm: {
      email: '',
      password: '',
    },
    confirmForm: {
      email: '',
      code: '',
    },
  }),
  methods: {
    async register() {
      try {
        await this.$store.dispatch('auth/register', this.registerForm)
        this.confirmForm.email = this.registerForm.email
        this.step = this.steps.confirm
      } catch (error) {
        console.log({ error })
      }
    },
    async confirm() {
      try {
        await this.$store.dispatch('auth/confirmRegistration', this.confirmForm)
        await this.$store.dispatch('auth/login', this.registerForm)
        this.$router.push('/')
      } catch (error) {
        console.log({ error })
      }
    },
  },
}
</script>
