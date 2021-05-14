<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">simple-todo</h1>
      <!-- Unauthenticated view -->
      <div v-if="!$auth.isAuthenticated">
        <nuxt-link to="/login">Login</nuxt-link>
        <nuxt-link to="/register">Register</nuxt-link>
      </div>
      <!-- authenticated view -->
      <div v-else>
        <p>You're logged in as {{ $auth.email }}</p>
        <button @click="$store.dispatch('auth/logout')" class="button--grey">
          Logout
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
