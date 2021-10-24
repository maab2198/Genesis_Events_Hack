<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-4 is-offset-4">
          <h2 class="title has-text-centered">Register!</h2>

          <Notification :message="error" v-if="error" />

          <form method="post" @submit.prevent="register">
            <div class="field">
              <label class="label">Email</label>
              <div class="control">
                <input
                  type="email"
                  class="input"
                  name="email"
                  v-model="data.email"
                  required
                />
              </div>
            </div>
            <div class="field">
              <label class="label">Password</label>
              <div class="control">
                <input
                  type="password"
                  class="input"
                  name="password"
                  v-model="data.password"
                  required
                />
              </div>
            </div>
            <div class="control">
              <button type="submit" class="button is-dark is-fullwidth">
                Register
              </button>
            </div>
          </form>

          <div class="has-text-centered" style="margin-top: 20px">
            Already got an account? <nuxt-link to="/login">Login</nuxt-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from '~/components/Notification'

export default {
  components: {
    Notification,
  },

  data() {
    return {
       data: {
        email: '',
        password: '',
        returnSecureToken: true,
      },
    }
  },

  methods: {
    async register() {
      try {
        const response = await fetch(
          'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyC_ryyBF1moAH7aDEl0E4bNzf8tvAMrJqQ',
          {
            method: 'POST', 
            headers: {
              'Content-Type': 'application/json',
              
            },
            body: JSON.stringify(this.data), // body data type must match "Content-Type" header
          }
        )
        this.$router.push('/singin')
        console.log(response)
      } catch (err) {
        console.log(err)
      }
    },
    }
  }

</script>

<style scoped lang="scss">
@import '@/assets/scss/_vars.scss';

  input{
    background-color:$text
  }

</style>