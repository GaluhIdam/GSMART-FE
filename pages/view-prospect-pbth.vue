<template>
  <div>
    <div id="kt_app_toolbar" class="app-toolbar py-3 py-lg-6 bg-white">
      <!--begin::Toolbar container-->
      <div
        id="kt_app_toolbar_container"
        class="app-container container-fluid d-flex flex-stack"
      >
        <!--begin::Page title-->
        <div
          class="
            page-title
            d-flex
            flex-column
            justify-content-center
            flex-wrap
            me-3
          "
        >
          <!--begin::Title-->
          <p
            class="
              page-heading
              d-flex
              text-dark
              fs-6
              flex-column
              justify-content-center
              my-0
            "
          >
            View Prospect
          </p>
          <!--end::Title-->
        </div>
        <ul
          class="breadcrumb breadcrumb-separatorless fw-semibold fs-7 my-0 pt-1"
        >
          <!--begin::Item-->
          <li class="breadcrumb-item text-muted">
            <nuxt-link to="/my-prospect" class="text-muted text-hover-primary"
              >My Prospect</nuxt-link
            >
          </li>
          <li class="breadcrumb-item">
            <span class="bullet bg-gray-400 w-5px h-2px"></span>
          </li>
          <li class="breadcrumb-item text-muted">View Prospect PBTH</li>
          <!--end::Item-->
        </ul>
        <!--end::Page title-->
      </div>
      <!--end::Toolbar container-->
    </div>
    <div class="container mb-10">
      <div class="card shadow-sm mt-5">
        <div class="row">
          <div class="col-md-5 p-16">
            <span class="btn btn-light btn-sm p-5">
              <img src="~/assets/media/logos/logo-gai.png" alt="logo" class="img-fluid" width="25" height="25">
            </span>
            <span class="badge text-muted text-bg-light d-block text-start mt-2">PBTH</span>
            <h2 class="mt-1">Airframe</h2>
            <div class="text-muted fw-semibold fs-5">Project for B737-800 MAX</div>
            <div class="text-muted fs-6">Remark for this project..</div>
            <div class="row mt-3">
              <div class="col-6">
                <div class="border-dashed rounded p-4">
                  <h1 class="fw-bolder mb-0 fs-5">$1,500,000.00</h1>
                  <p class="mb-0 fw-bold text-gray-500">Market Share</p>
                </div>
              </div>
              <div class="col-6">
                <div class="border-dashed rounded p-4">
                  <h1 class="fw-bolder mb-0 fs-5">$5,850,000.00</h1>
                  <p class="mb-0 fw-bold text-gray-500">Sales Plan</p>
                </div>
              </div>
            </div>
            <div class="row mt-1">
              <div class="col-6">
                <div class="border-dashed rounded p-4">
                  <h1 class="fw-bolder mb-0 fs-5">$650,000.00</h1>
                  <p class="mb-0 fw-bold text-gray-500">Deviation</p>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md-7 container">
            <div class="row mt-15 mb-2">
              <div class="col-6">
                  <div class="fs-3">Contact Person</div>
              </div>
              <div class="col-6 text-end">
                  <div type="button"
                    class="btn btn-sm text-light"
                    style="background-color: #1BC5BD"
                    data-bs-toggle="modal"
                    data-bs-target="#modal"
                    @click="add()">
                    <i class="fa-solid fa-user-plus text-light"></i>
                    Add Contact Person</div>
              </div>
            </div>

            <div class="modal fade" tabindex="-1" id="modal" data-bs-backdrop="static">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h3 class="modal-title">Add Contact Person</h3>

            <!--begin::Close-->
            <div
              class="btn btn-icon btn-sm btn-active-light-primary ms-2"
              data-bs-dismiss="modal"
              aria-label="Close"
            >
              <span class="svg-icon svg-icon-1" @click="closeModal()">
                <svg
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <rect
                    opacity="0.5"
                    x="6"
                    y="17.3137"
                    width="16"
                    height="2"
                    rx="1"
                    transform="rotate(-45 6 17.3137)"
                    fill="currentColor"
                  ></rect>
                  <rect
                    x="7.41422"
                    y="6"
                    width="16"
                    height="2"
                    rx="1"
                    transform="rotate(45 7.41422 6)"
                    fill="currentColor"
                  ></rect>
                </svg>
              </span>
            </div>
            <!--end::Close-->
          </div>
          <div class="modal-body">
            <form @submit.prevent="submit">
              <div class="form-group mb-3">
                <label class="form-label fw-bold">Name</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="contact_persons.name"
                  :class="{
                    'is-invalid': errors.name,
                  }"
                />
                <span v-if="errors.name" class="error invalid-feedback">{{
                  errors.name[0]
                }}</span>
              </div>

              <div class="form-group mb-3">
                <label class="form-label fw-bold">Email</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="contact_persons.email"
                  :class="{
                    'is-invalid': errors.email,
                  }"
                />
                <span v-if="errors.email" class="error invalid-feedback">{{
                  errors.email[0]
                }}</span>
              </div>
              <div class="form-group mb-3">
                <label class="form-label fw-bold">Phone</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="contact_persons.phone"
                  :class="{
                    'is-invalid': errors.phone,
                  }"
                />
                <span v-if="errors.phone" class="error invalid-feedback">{{
                  errors.phone[0]
                }}</span>
              </div>
              <div class="form-group mb-3">
                <label class="form-label fw-bold">Address</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="contact_persons.address"
                  :class="{
                    'is-invalid': errors.address,
                  }"
                />
                <span v-if="errors.address" class="error invalid-feedback">{{
                  errors.address[0]
                }}</span>
              </div>
              <div class="form-group mb-3">
                <label class="form-label fw-bold">Customer</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="contact_persons.customer_id"
                  :class="{
                    'is-invalid': errors.customer_id,
                  }"
                />
                <span v-if="errors.customer_id" class="error invalid-feedback">{{
                  errors.customer_id[0]
                }}</span>
              </div>
              <div class="row mt-10">
                <div class="col">
                  <button
                    type="button"
                    class="btn btn-light"
                    data-bs-dismiss="modal"
                    id="close_modal"
                    @click="closeModal()"
                  >
                    Back
                  </button>
                </div>
                <div class="col d-flex justify-content-end">
                  <button type="submit" class="btn btn-primary">Save</button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>

            <div class="table-responsive">
              <table class="table table-row-bordered table-row-gray-200 gy-4">
                <thead>
                  <tr class="fw-bold fs-6 text-gray-800">
                    <th class="text-start text-uppercase text-muted">Name</th>
                    <th class="text-start text-uppercase text-muted">Email</th>
                    <th class="text-start text-uppercase text-muted">Phone</th>
                    <th class="text-start text-uppercase text-muted">Address</th>
                    <th class="text-start"></th>
                  </tr>
                </thead>
                <tbody>
                  <tr
                      v-for="(
                      contact_person, contact_persons_index
                      ) in contact_person.data"
                      :key="contact_persons_index"
                  >
                    <td class="text-start">{{ contact_person.name }}</td>
                    <td class="text-start">{{ contact_person.email }}</td>
                    <td class="text-start">{{ contact_person.phone }}</td>
                    <td class="text-start">{{ contact_person.address }}</td>

                    <td class="text-start">
                      <button
                        class="btn btn-sm btn-light"
                        v-on:click="remove(contact_person.id)"
                      >
                        <i class="bi bi-trash-fill text-primary"></i>
                      </button>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
      <div class="mb-10">
      <div class="card shadow-sm mt-5">
        <div class="card-header">
          <h3 class="card-title fw-bold">Convidence Level</h3>
        </div>
        <div class="card-body">
          <div class="row">
            <div class="col-md-4">
            <input
                type="text"
                class="form-control form-control-solid"
                name="search"
                v-model="search"
              />
              </div>
              <div class="col-md-4">
              <button class="btn btn-primary">Calculate</button>
              <button class="btn btn-primary">Save</button>
              </div>
            </div>
        </div>
      </div>

        <div class="card shadow-sm mt-5">
          <div class="card-header">
            <h3 class="card-title fw-bold">Flights Hour Target</h3>
          </div>
            <div class="table-responsive container">
              <table class="table table-row-bordered table-row-gray-200 gy-4">
                <thead>
                  <tr class="fw-bold fs-6 text-gray-800">
                    <th class="text-center">Month</th>
                    <th class="text-center">Target FH</th>
                    <th class="text-center">Target Rate</th>
                    <th class="text-center">Plan FH</th>
                    <th class="text-center">Sales Plan</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <!-- v-for="(pbth, pbth_index) in pbth.data" :key="pbth_index" -->
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                  </tr>
                </tbody>
              </table>
            </div>
        </div>
      </div>
    </div>
    </div>
</template>

<script>
import debounce from 'lodash/debounce'
export default {
  layout: 'template',
  data() {
    return {
      contact_person: {
        data: [],
        },
        contact_persons: {
        id: null,
        name: null,
        email: null,
        phone: null,
        address: null,
        customer_id: null,
      },
      modal_create: false,
      errors: {
        name: null,
        nopeg: null,
        email: null,
        unit: null,
      },
      }
    },
    created() {
    this.list()
    this.listContactPersons()
  },
  methods: {
    list(paginate) {
      this.loading()
      paginate = paginate || `/api/contact-persons`
      this.$axios
        .get(paginate, {
          params: {
            search: this.search,
            order: this.order,
            by: this.by,
            paginate: this.paginate,
          },
        })
        .then((response) => {
          this.contact_person = response.data.data
          this.current_page = this.contact_person.current_page
          Swal.close()
        })
        .catch((error) => console.log(error))
    },
    listContactPersons() {
      this.$axios
        .get('api/contact-persons', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.contact_person = response.data
          console.log(response.data.data)
        })
    },
    listPBTH() {
      this.$axios
        .get('api/pbth', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.pbth = response.data
          console.log(response.data)
        })
    },
    add() {
      this.modal_create = true
    },
    clearForm() {
      this.contact_persons.id = null
      this.contact_persons.name = null
      this.contact_persons.email = null
      this.contact_persons.phone = null
      this.contact_persons.address = null
      this.contact_persons.customer_id = null
      this.errors.name = null
      this.errors.email = null
      this.errors.phone = null
      this.errors.address = null
      this.errors.customer_id = null
    },
    closeModal() {
      document.getElementById('close_modal').click()
      this.clearForm()
    },
    remove(id) {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios.delete('/api/contact-persons-delete/' + id).then((response) => {
              toastr.success(response.data.message)
              this.list()
            })
          }
        })
        .catch((error) => {
          console.log(error)
        })
    },
    loading() {
      Swal.fire({
        timer: 500,
        didOpen: () => {
          Swal.showLoading()
        },
        background: 'transparent',
        allowOutsideClick: false,
      })
    },
    }
  }
</script>

<style>
</style>