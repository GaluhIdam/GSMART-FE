<template>
  <div>
    <div id="kt_app_toolbar" class="app-toolbar py-3 py-lg-6 bg-white">
      <!--begin::Toolbar container-->
      <div
        id="kt_app_toolbar_container"
        class="app-container container-fluid d-flex flex-stack"
      >
        <!--begin::Page title-->
        <div class=" page-title d-flex flex-column justify-content-center flex-wrap me-3">
          <!--begin::Title-->
          <p class=" page-heading d-flex text-dark fs-6 flex-column justify-content-center my-0">
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
          <li class="breadcrumb-item text-muted">View Prospect TMB</li>
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
              <img :src=customer_image alt="logo" class="img-fluid" width="25" height="25">
            </span>
            <span class="badge text-muted text-bg-light d-block text-start mt-2">TMB</span>
            <h2 class="mt-1">Airframe</h2>
            <div class="text-muted fw-semibold fs-5">Project for {{ registration }}</div>
            <div class="text-muted fs-6">Remark for this project..</div>
            <div class="row mt-3">
              <div class="col-6">
                <div class="border-dashed rounded p-4">
                  <h1 class="fw-bolder mb-0 fs-5">${{ formatNumber(market_share) }}</h1>
                  <p class="mb-0 fw-bold text-gray-500">Market Share</p>
                </div>
              </div>
              <div class="col-6">
                <div class="border-dashed rounded p-4" v-if="sales_plan">
                  <h1 class="fw-bolder mb-0 fs-5">${{ formatNumber(sales_plan) }}</h1>
                  <p class="mb-0 fw-bold text-gray-500">Sales Plan</p>
                </div>
                <div class="border-dashed rounded p-4" v-else>
                  <h1 class="fw-bolder mb-0 fs-5">$0</h1>
                  <p class="mb-0 fw-bold text-gray-500">Sales Plan</p>
                </div>
              </div>
            </div>
            <div class="row mt-1">
              <div class="col-6">
                <div class="border-dashed rounded p-4" v-if="sales_plan">
                  <h1 class="fw-bolder mb-0 fs-5">${{ formatNumber(deviation) }}</h1>
                  <p class="mb-0 fw-bold text-gray-500">Deviation</p>
                </div>
                <div class="border-dashed rounded p-4" v-else>
                  <h1 class="fw-bolder mb-0 fs-5">$0</h1>
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
                    data-bs-toggle="modal"
                    data-bs-target="#contactPersonModal"
                    @click="clearForm()"
                    style="background-color: #1BC5BD">
                    <i class="fa-solid fa-user-plus text-light"></i>
                    Add Contact Person</div>
              </div>
              <div class="modal fade" tabindex="-1" id="contactPersonModal" data-bs-backdrop="static">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h3 class="modal-title">Add Contact Person</h3>

            <!--begin::Close-->
            <div class="btn btn-icon btn-sm btn-active-light-primary ms-2" data-bs-dismiss="modal" aria-label="Close" id="close_modal_contact_person">
              <span class="svg-icon svg-icon-1">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"> 
                <rect opacity="0.5" x="6" y="17.3137" width="16" height="2" rx="1" transform="rotate(-45 6 17.3137)" fill="currentColor"></rect>
                  <rect x="7.41422" y="6" width="16" height="2" rx="1" transform="rotate(45 7.41422 6)" fill="currentColor"></rect>
                </svg>
              </span>
            </div>
            <!--end::Close-->
          </div>
          <div class="modal-body">
            <form @submit.prevent="submit">
              <div class="form-group mb-3">
                <label class="form-label fw-bold">Name</label>
                <input type="text" v-model="contact_person.name" class="form-control" :class="{'is-invalid': errors.name}">
                      <span v-if="errors.name" class="error invalid-feedback">{{errors.name[0]}}</span>
              </div>

              <div class="form-group mb-3">
                <label class="form-label fw-bold">Email</label>
                <input type="text" class="form-control" v-model="contact_person.email" :class="{
                    'is-invalid': errors.email,
                  }"
                />
                <span v-if="errors.email" class="error invalid-feedback">{{
                  errors.email[0]
                }}</span>
              </div>
              <div class="form-group mb-3">
                <label class="form-label fw-bold">Phone</label>
                <input type="text" class="form-control" v-model="contact_person.phone" :class="{
                    'is-invalid': errors.phone,
                  }"
                />
                <span v-if="errors.phone" class="error invalid-feedback">{{
                  errors.phone[0]
                }}</span>
              </div>
              <div class="form-group mb-3">
                <label class="form-label fw-bold">Address</label>
                <input type="text" class="form-control" v-model="contact_person.address" :class="{
                    'is-invalid': errors.address,
                  }"
                />
                <span v-if="errors.address" class="error invalid-feedback">{{
                  errors.address[0]
                }}</span>
              </div>
              <div class="form-group mb-3">
                <label class="form-label fw-bold">Customer</label>
                <multiselect v-model="contact_person.customer_id" :options="customer_options" :searchable="true" :class="{'is-invalid': errors.customer_id,}" label="name"></multiselect>
                <span v-if="errors.customer_id" class="error invalid-feedback">{{
                  errors.customer_id[0]
                }}</span>
              </div>
              <div class="form-group mb-3">
                <label class="form-label fw-bold">Title</label>
                <input type="text" class="form-control" v-model="contact_person.title" :class="{
                    'is-invalid': errors.title,
                  }"
                />
                <span v-if="errors.title" class="error invalid-feedback">{{
                  errors.title[0]
                }}</span>
              </div>
              <div class="row mt-10">
                <div class="col">
                  <button type="button" class="btn btn-light" @click="closeModal()">
                    Back
                  </button>
                </div>
                <div class="col d-flex justify-content-end">
                  <button type="button" class="btn btn-primary" @click="createContactPerson()">Save</button>
                </div>
              </div>
            </form>
          </div>
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
                  <tr v-for="(data, contact_person_index) in contact_persons" :key="contact_person_index">
                    <td class="text-start">
                      <div class="row mx-auto">
                      <span class="btn bg-primary btn-sm text-light col-4">{{ data.firstalphabet }}</span>
                      <span class="col-8">{{ data.name }}</span>
                      </div>
                    </td>
                    <td class="text-start">{{ data.email }}</td>
                    <td class="text-start">{{ data.phone }}</td>
                    <td class="text-start">{{ data.address }}</td>
                    <td class="text-start">
                      <button class="btn btn-sm btn-light" v-on:click="removeContactPerson(data.id)">
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
          <h3 class="card-title fw-bold">Data Prospect</h3>
            <div class="card-toolbar">
              <form>
              <div class="col mx-5">
                <div class="position-relative me-md-2">
              <!--begin::Svg Icon | path: icons/duotune/general/gen021.svg-->
              <span class="svg-icon svg-icon-3 svg-icon-gray-500 position-absolute top-50 translate-middle ms-6">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect opacity="0.5" x="17.0365" y="15.1223" width="8.15546" height="2" rx="1" transform="rotate(45 17.0365 15.1223)" fill="currentColor"></rect>
                  <path d="M11 19C6.55556 19 3 15.4444 3 11C3 6.55556 6.55556 3 11 3C15.4444 3 19 6.55556 19 11C19 15.4444 15.4444 19 11 19ZM11 5C7.53333 5 5 7.53333 5 11C5 14.4667 7.53333 17 11 17C14.4667 17 17 14.4667 17 11C17 7.53333 14.4667 5 11 5Z"
                  fill="currentColor"></path>
                </svg>
              </span>
              <!--end::Svg Icon-->
              <input
                type="text"
                class="form-control form-control-solid ps-10"
                name="search"
                v-model="search"
                placeholder="Search"
              />
            </div>
              </div>
              </form>
              <div class="col">
                <button type="button" class="btn btn-sm btn-primary mx-3" data-bs-toggle="modal" data-bs-target="#modal" @click="add()">
                  Add Registration
                </button>
              </div>
            </div>
        </div>
    <div class="modal fade" tabindex="-1" id="modal" data-bs-backdrop="static">
      <div class="modal-dialog modal-xl modal-dialog-centered">
        <div class="modal-content py-5">
          <div class="modal-header">
            <h3 class="modal-title" v-if="modal_create">Add Registration</h3>
            <h3 class="modal-title" v-if="modal_update">Edit Registration</h3>
            <div type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" id="close_modal_sales">
            </div>
          </div>
          <div class="modal-body">
            <form @submit.prevent="submit">
              <div class="row">
                <div class="col-md-6">
                    <div class="mb-3">
                      <label for="Maintenance" class="form-label">Maintenance</label>
                      <multiselect v-model="tmbSale.maintenance_id" :options="maintenance_option" label="name" 
                      :class="{'is-invalid': errors.maintenance_id}"></multiselect>
                      <span v-if="errors.maintenance_id" class="error invalid-feedback">{{errors.maintenance_id[0]}}</span>
                    </div>
                    <div class="mb-3">
                      <label for="Registration" class="form-label">Registration</label>
                      <input type="text" v-model="tmbSale.ac_reg" class="form-control" open-direction="bottom" :class="{'is-invalid': errors.ac_reg}">
                      <span v-if="errors.ac_reg" class="error invalid-feedback">{{errors.ac_reg[0]}}</span>
                    </div>
                    <div class="mb-3">
                      <label for="TAT" class="form-label">TAT</label>
                      <input type="text" v-model="tmbSale.tat" class="form-control" :class="{'is-invalid': errors.tat}">
                      <span v-if="errors.tat" class="error invalid-feedback">{{errors.tat[0]}}</span>
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="mb-3">
                      <label for="Hangar" class="form-label">Hangar</label>
                      <multiselect v-model="tmbSale.hangar_id" :options="hangar_option" label="name" 
                      :class="{'is-invalid': errors.hangar_id}"></multiselect>
                      <span v-if="errors.hangar_id" class="error invalid-feedback">{{errors.hangar_id[0]}}</span>
                    </div>
                    <div class="mb-3">
                      <label for="Sales Plan" class="form-label">Sales Plan</label>
                      <input type="text" v-model="tmbSale.value" class="form-control" :class="{'is-invalid': errors.value}">
                      <span v-if="errors.value" class="error invalid-feedback">{{errors.value[0]}}</span>
                    </div>
                    <div class="mb-3">
                      <label for="Start Date" class="form-label">Start Date</label>
                      <input type="date" v-model="tmbSale.start_date" class="form-control" :class="{'is-invalid': errors.start_date}">
                      <span v-if="errors.start_date" class="error invalid-feedback">{{errors.start_date[0]}}</span>
                    </div>
                </div>
                <div class="col-md-12 justify-content-between d-flex">
                  <div class="btn btn-secondary mt-3" data-bs-dismiss="modal">Back</div>
                    <button type="submit" v-if="modal_create" class="btn btn-primary mt-3">Submit</button>
                    <button type="submit" v-else class="btn btn-primary mt-3">Update</button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
        <div class="card-body">
          <div class="row d-flex align-items-center">
          </div>
          <div class="py-5">
            <div class="table-responsive">
              <table class="table table-row-bordered table-row-gray-200 gy-4">
                <thead>
                  <tr class="fw-bold fs-6 text-gray-800">
                    <th class="text-center">No</th>
                    <th class="text-center">ID</th>
                    <th class="text-center">Registration</th>
                    <th class="text-center">Maintenance</th>
                    <th class="text-center">Location</th>
                    <th class="text-center">Sales Plan</th>
                    <th class="text-center">TAT</th>
                    <th class="text-center">Start Date</th>
                    <th class="text-center">End Date</th>
                    <th class="text-center">Level</th>
                    <th class="text-center">Status</th>
                    <th class="text-center">Action</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(tmbSale, tmbSales_index) in tmbSales" :key="tmbSales_index">
                    <td class="text-center">{{ paginate_tmbSales.from + tmbSales_index }}</td>
                    <td class="text-center">{{ tmbSale.customer_id}}</td>
                    <td class="text-center">{{ tmbSale.ac_reg }}</td>
                    <td class="text-center">{{ tmbSale.maintenance_id }}</td>
                    <td class="text-center">{{ tmbSale.hangar.name }}</td>
                    <td class="text-center">{{ tmbSale.value }}</td>
                    <td class="text-center">{{ tmbSale.tat }}</td>
                    <td class="text-center">{{ tmbSale.start_date }}</td>
                    <td class="text-center">{{ tmbSale.end_date }}</td>
                    <td class="text-center">{{ tmbSale.level }}</td>
                    <td class="text-center badge text-light bg-primary" style="color: #FFA800" v-if="tmbSale.level == 1">Done</td>
                    <td class="text-center badge" style="color: #FFA800; background-color: #FFF4DE" v-else>In Progress</td>
                    <td class="text-center">
                      <button class="btn btn-sm btn-light">
                        <i class="bi bi-toggles text-primary"></i>
                      </button>
                      <button class="btn btn-sm btn-light" data-bs-toggle="modal" data-bs-target="#modal" @click="edit(tmbSale, tmbSales)">
                        <i class="bi bi-pencil-square text-primary"></i>
                      </button>
                      <button class="btn btn-sm btn-light" v-on:click="removeTmbSales(tmbSale.id)">
                        <i class="bi bi-trash-fill text-primary"></i>
                      </button>
                    </td>
                    <td class="d-flex justify-content-center">
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
        <div class="card-footer">
            <div class="row">
              <div class="col d-flex justify-content-start align-items-center">
                <nav aria-label="Page navigation example">
                  <ul class="pagination">
                    <li class="page-item align-self-center">Rows per page:</li>
                    <li class="page-item">
                      <select
                        class="form-control form-control-sm"
                        v-model="paginate"
                        @change="listSalesTmb()"
                      >
                        <option value="10">10</option>
                        <option value="25">25</option>
                        <option value="50">50</option>
                        <option value="100">100</option>
                      </select>
                    </li>
                  </ul>
                </nav>
              </div>
              <div class="col d-flex justify-content-end align-items-center">
                <nav aria-label="Page navigation example">
                  <ul class="pagination">
                  <li class="page-item">
                    <button type="button" class="page-link" :class="{
                        disabled: !paginate_tmbSales.prev_page_url,
                      }" @click="paginate_tmbSales.prev_page_url && listSalesTmb(paginate_tmbSales.prev_page_url)">
                      Previous
                    </button>
                  </li>
                  <li class="page-item" style="margin-left: 15px; margin-right: 15px">
                    <input type="text" class="form-control form-control-sm text-center" v-model="current_page" @keypress="directPage" style="width: 60px"/>
                  </li>
                  <li class="page-item">
                    <button type="button" class="page-link" :class="{
                        disabled: !paginate_tmbSales.next_page_url,
                      }" @click="paginate_tmbSales.next_page_url && listSalesTmb(paginate_tmbSales.next_page_url)">
                      Next
                    </button>
                  </li>
                </ul>
                </nav>
              </div>
            </div>
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
      selected_customer: null,
      customer: [],
      maintenance_option: [],
      hangar_option: [],
      contact_persons: [],
      tmbSale: {
        ac_reg: null,
        tat: null,
        value: null,
        start_date: null,
        maintenance_id: [],
        hangar_id: [],
      },
      contact_person: {
        name: null,
        email: null,
        address : null,
        phone: null,
        customer_id: null,
        title: null
      },
      tmb: [],
      sales_plan: [],
      registration: [],
      customer_image: [],
      market_share: [],
      deviation: [],
      tmbSales: [],
      errors: {
        maintenance_id: null,
        ac_reg: null,
        tat: null,
        hangar_id: null,
        value: null,
        start_date: null,
        name: null,
        email: null,
        address: null,
        phone: null,
        customer_id: null,
      },
      paginate: '10',
      search: null,
      current_page: null,
      modal_create: false,
      modal_update: false,
      paginate_tmbSales: [],
      value: [],
      customer_options: [],
      }
    },
  created() {
    this.listContactPersons()
    this.listTMB()
    this.listSalesTmb()
    this.listMaintenance()
    this.listHangar()
    this.listCustomer()
    },
    watch: {
    search: debounce(function () {
      this.listSalesTmb()
    }, 500),
  },
  methods: {
    formatNumber(value) {
      let val = (value/1).toFixed(2).replace(',', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
    },
    closeModal() {
      document.getElementById('close_modal_contact_person').click()
      document.getElementById('close_modal_sales').click()
      this.clearForm()
    },
    listCustomer() {
      this.$axios
        .get('api/customer', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.customer_options = response.data.data.data
        })
    },
    listContactPersons() {
      this.$axios
        .get('api/contact-person')
        .then((response) => {
          this.contact_persons = response.data.data
        })
    },
    listTMB() {
      this.$axios
        .get(`api/prospect-tmb/${this.$route.query.id}`)
        .then((response) => {
          // Data TMB
          this.tmb = response.data.data.prospect
          // Data Customer
          this.customer_image = response.data.data.customer.full_path
          // Registration Format
          this.registration = response.data.data.registration
          // Sales Plan Value
          this.sales_plan = response.data.data.sales_plan
          // Market Share Value
          this.market_share = response.data.data.market_share
          // Deviation Value
          this.deviation = response.data.data.deviation
        })
    },
    listMaintenance() {
      this.$axios
        .get('api/maintenance', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.maintenance_option = response.data.data.data
        })
    },
    listHangar() {
      this.$axios
        .get('api/hangar', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.hangar_option = response.data.data
        })
    },
    listSalesTmb(paginate) {
      this.loading()
      paginate = paginate || `/api/sales-show-tmb/${this.$route.query.id}`
      this.$axios
        .get(paginate, {
          params: {
            search: this.search,
            paginate: this.paginate,
          },
        })
        .then((response) => {
          this.tmbSales = response.data.sales.data
          console.log(this.tmbSales)
          this.paginate_tmbSales = response.data.sales
          this.current_page = response.data.sales.current_page
          this.value = response.data
        })
    },
    submit() {
      if (this.modal_create){
        this.clearForm()
        this.create()
      } else if(this.modal_update) {
        this.update()
      } else {
        this.clearForm()
        this.createContactPerson()
      }
    },
    create() {
      this.loading()
      this.$axios
        .post('/api/sales-create-tmb', {
          prospect_id: this.$route.query.id,
          maintenance_id: this.tmbSale.maintenance_id.id,
          ac_reg: this.tmbSale.ac_reg,
          tat: this.tmbSale.tat,
          hangar_id: this.tmbSale.hangar_id.id,
          value: this.tmbSale.value,
          start_date: this.tmbSale.start_date,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.closeModal()
          this.listSalesTmb()
          this.clearForm()
        })
        .catch((error) => {
          if (error.response.status) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          }
        })
    },
    update() {
      this.loading()
      this.$axios
        .put('/api/sales-update/' + this.tmbSale.id, {
          prospect_id: this.$route.query.id,
          maintenance_id: this.tmbSale.maintenance_id.id,
          ac_reg: this.tmbSale.ac_reg,
          tat: this.tmbSale.tat,
          hangar_id: this.tmbSale.hangar_id.id,
          value: this.tmbSale.value,
          start_date: this.tmbSale.start_date,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.listSalesTmb()
          this.clearForm()
          this.closeModal()
        })
        .catch((error) => {
          if (error.response.status) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          }
        })
    },
    createContactPerson() {
      this.loading()
      this.$axios
        .post('/api/contact-person-create', {
          name : this.contact_person.name,
          phone : this.contact_person.phone,
          email : this.contact_person.email,
          address : this.contact_person.address,
          customer_id : this.contact_person.customer_id.id,
          title : this.contact_person.title,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.listContactPersons()
          this.closeModal()
        })
        .catch((error) => {
          if (error.response.status) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          }
        })
    },
    edit(tmbSale) {
      this.modal_create = false
      this.modal_update = true
      this.tmbSale.id = tmbSale.id
      this.tmbSale.maintenance_id = tmbSale.maintenance
      this.tmbSale.ac_reg = tmbSale.ac_reg
      this.tmbSale.tat = tmbSale.tat
      this.tmbSale.hangar_id = tmbSale.hangar
      this.tmbSale.value = tmbSale.value
      this.tmbSale.start_date = tmbSale.start_date
    },
    add() {
      // this.clearForm()
      this.modal_create = true
      this.modal_update = false
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
    clearForm(){
      // this.tmbSale.ac_reg = null
      // this.tmbSale.tat = null
      // this.tmbSale.value = null
      // this.tmbSale.start_date = null
      // this.tmbSale.maintenance_id = null
      // this.tmbSale.hangar_id = null
      this.contact_person.name = null
      this.contact_person.email = null
      this.contact_person.address = null
      this.contact_person.phone = null
      this.contact_person.customer_id = null
      this.contact_person.title = null
    },
    directPage: debounce(function () {
      alert(this.paginate_tmbSales.current_page)
      if (this.current_page < 1) {
        this.paginate_tmbSales.current_page = 1
      } else if (this.paginate_tmbSales.current_page > this.paginate_tmbSales.last_page) {
        this.paginate_tmbSales.current_page = this.paginate_tmbSales.last_page
      }
      let url = new URL(this.paginate_tmbSales.first_page_url)
      let filter_params = url.filterParams
      filter_params.set('page', this.paginate_tmbSales.current_page)
      url.filter = filter_params.toString()
      let new_url = url.toString()
      this.listSalesTmb(new_url)
    }, 500),
    removeTmbSales(id) {
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
            this.$axios.delete('/api/sales-delete-tmb/' + id).then((response) => {
              toastr.success(response.data.message)
              this.listSalesTmb()
            })
          }
        })
        .catch((error) => {
          console.log(error)
        })
    },
    removeContactPerson(id) {
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
            this.$axios.delete('/api/contact-person-delete/' + id).then((response) => {
              toastr.success(response.data.message)
              this.listContactPersons()
            })
          }
        })
        .catch((error) => {
          console.log(error)
        })
    },
    },
  }
</script>

<style>
</style>