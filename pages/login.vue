<template>
  <div class="row justify-content-center ms-0 me-0">
    <div class="col-md-9 px-0">
      <div class="container">
        <img
          src="~/assets/media/logos/gmf-logo.png"
          class="mt-30 logo-size"
          alt="logo"
        />
        <div class="text-white mt-vh">
          <h1 class="text-white fs-large">G-SMART</h1>
          <div class="blok mb-5" />
          <p class="fs-3 mb-1">For Sales & Marketing</p>
          <p class="mb-10">
            if you have any trouble using this application, please contact us at
            spoc@gmf-aeroasia.co.id
          </p>
        </div>
      </div>
    </div>
    <div
      class="
        col-md-3
        px-0
        bg-color
        d-flex
        align-items-center
        justify-content-center
      "
    >
      <div class="card">
        <div class="card-body px-30">
          <h1 class="fw-bold mb-50 text-center top-margin">
            Login to your account.
          </h1>
          <div class="text-center mx-c">
            <p class="text-danger mb-0 mt-0">
              {{ errors }}
            </p>
          </div>
          <form method="post" v-on:submit.prevent="loginUser">
            <div class="form-group mt-5">
              <input
                type="text"
                class="form-control rounded-pill"
                placeholder="Employee Number"
                v-model="login.username"
              />
            </div>
            <div class="form-group mt-10">
              <input
                type="password"
                class="form-control rounded-pill"
                placeholder="Password"
                v-model="login.password"
              />
            </div>
            <div class="mt-10 d-flex justify-content-center mb-85">
              <button
                type="submit"
                class="btn btn-success rounded-pill w-200px"
              >
                Login
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoginPage',
  head() {
    return {
      bodyAttrs: {
        class: 'bg-background',
      },
    }
  },
  data() {
    return {
      login: {
        username: '',
        password: '',
      },
      errors: '',
    }
  },

  created() {},

  methods: {
    async loginUser() {
      await this.$auth
        .loginWith('local', {
          data: this.login,
        }, this.loading())
        .then((result) => {
          this.$router.push('/')
          this.successMessage()
        })
        .catch((error) => {
          if (error.response.status == 401) {
            this.errors = 'Username or Password is invalid!'
            this.failMessage()
          } else if (error.response.status == 422) {
            this.errors = 'Please insert Username or Password!'
            this.failMessage()
          }
        })
    },
    loading() {
      Swal.fire({
        timer: 3000,
        didOpen: () => {
          Swal.showLoading()
        },
        background: 'transparent',
        allowOutsideClick: false,
      })
    },
    successMessage() {
      toastr.options = {
        closeButton: false,
        debug: false,
        newestOnTop: false,
        progressBar: false,
        positionClass: 'toastr-top-right',
        preventDuplicates: false,
        onclick: null,
        showDuration: '300',
        hideDuration: '1000',
        timeOut: '5000',
        extendedTimeOut: '1000',
        showEasing: 'swing',
        hideEasing: 'linear',
        showMethod: 'fadeIn',
        hideMethod: 'fadeOut',
      }
      toastr.success('Login Successfully!')
    },
    failMessage() {
      toastr.options = {
        closeButton: false,
        debug: false,
        newestOnTop: false,
        progressBar: false,
        positionClass: 'toastr-top-right',
        preventDuplicates: false,
        onclick: null,
        showDuration: '300',
        hideDuration: '1000',
        timeOut: '5000',
        extendedTimeOut: '1000',
        showEasing: 'swing',
        hideEasing: 'linear',
        showMethod: 'fadeIn',
        hideMethod: 'fadeOut',
      }
      toastr.error('Login failed, please try again!')
    },
  },
}
</script>
