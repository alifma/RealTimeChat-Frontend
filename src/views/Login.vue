<template>
  <div class="container pt-5">
    <div class="card">
      <div class="card-header text-center">
        <h1>Halaman Login</h1>
      </div>
      <div class="card-body">
        <form @submit.prevent ="onLogin()" action="" class="text-center">
          <label class="font-weight-bold" for="">Username </label>
          <input required v-model="username" type="text" class="form-control my-2">
          <button class="btn btn-warning font-weight-bold">Login</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      username: ''
    }
  },
  methods: {
    onLogin () {
      this.$router.push(`/home?username=${this.username}`)
    }
  }
}
</script>
