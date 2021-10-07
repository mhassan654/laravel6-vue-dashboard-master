<template>
  <div class="row">

    <div class="col-md-6 m-auto">
  <div class="authincation-content">
      <div class="row no-gutters">
          <div class="col-xl-12">
              <div class="auth-form">
                  <h4 class="text-center mb-4">Sign in your account</h4>
                  <form action="{!! url('/index'); !!}">
                      <div class="form-group">
                          <label class="mb-1"><strong>Email</strong></label>
                          <input type="email" class="form-control" value="hello@example.com">
                      </div>
                      <div class="form-group">
                          <label class="mb-1"><strong>Password</strong></label>
                          <input type="password" class="form-control" value="Password">
                      </div>
                      <div class="form-row d-flex justify-content-between mt-4 mb-2">
                        <div class="form-group">
                           <div class="custom-control custom-checkbox ml-1">
                              <input type="checkbox" class="custom-control-input" id="basic_checkbox_1">
                              <label class="custom-control-label" for="basic_checkbox_1">Remember my preference</label>
                            </div>
                        </div>
                        <div class="form-group">
                            <a href="{!! url('/page-forgot-password'); !!}">Forgot Password?</a>
                        </div>
                      </div>
                      <div class="text-center">
                          <button type="submit" class="btn btn-primary btn-block">Sign Me In</button>
                      </div>
                  </form>
                  <div class="new-account mt-3">
                      <p>Don't have an account? <a class="text-primary" href="{!! url('/page-register'); !!}" >Sign up</a></p>
                  </div>
              </div>
          </div>
      </div>
  </div>
</div>
    <!-- <div class="col-lg-7 m-auto">
      <card :title="$t('login')">
        <form @submit.prevent="login" @keydown="form.onKeydown($event)">

          <div class="mb-3 row">
            <label class="col-md-3 col-form-label text-md-end">{{ $t('email') }}</label>
            <div class="col-md-7">
              <input v-model="form.email" :class="{ 'is-invalid': form.errors.has('email') }" class="form-control" type="email" name="email">
              <has-error :form="form" field="email" />
            </div>
          </div>


          <div class="mb-3 row">
            <label class="col-md-3 col-form-label text-md-end">{{ $t('password') }}</label>
            <div class="col-md-7">
              <input v-model="form.password" :class="{ 'is-invalid': form.errors.has('password') }" class="form-control" type="password" name="password">
              <has-error :form="form" field="password" />
            </div>
          </div>


          <div class="mb-3 row">
            <div class="col-md-3" />
            <div class="col-md-7 d-flex">
              <checkbox v-model="remember" name="remember">
                {{ $t('remember_me') }}
              </checkbox>

              <router-link :to="{ name: 'password.request' }" class="small ms-auto my-auto">
                {{ $t('forgot_password') }}
              </router-link>
            </div>
          </div>

          <div class="mb-3 row">
            <div class="col-md-7 offset-md-3 d-flex">

              <v-button :loading="form.busy">
                {{ $t('login') }}
              </v-button>

              <login-with-github />
            </div>
          </div>
        </form>
      </card>
    </div> -->
  </div>
</template>

<script>
import Form from 'vform'
import Cookies from 'js-cookie'
import LoginWithGithub from '~/components/LoginWithGithub'

export default {
  components: {
    LoginWithGithub
  },

  middleware: 'guest',

  metaInfo () {
    return { title: this.$t('login') }
  },

  data: () => ({
    form: new Form({
      email: '',
      password: ''
    }),
    remember: false
  }),

  methods: {
    async login () {
      // Submit the form.
      const { data } = await this.form.post('/api/login')

      // Save the token.
      this.$store.dispatch('auth/saveToken', {
        token: data.token,
        remember: this.remember
      })

      // Fetch the user.
      await this.$store.dispatch('auth/fetchUser')

      // Redirect home.
      this.redirect()
    },

    redirect () {
      const intendedUrl = Cookies.get('intended_url')

      if (intendedUrl) {
        Cookies.remove('intended_url')
        this.$router.push({ path: intendedUrl })
      } else {
        this.$router.push({ name: 'home' })
      }
    }
  }
}
</script>
