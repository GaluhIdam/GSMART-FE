<template>
  <div>
    <div class="container-fluid mt-10 mb-20">
      <div class="row mb-5">
        <div class="col-lg-6 col-sm-12">
          <h3 class="mt-3">Dashboard Sales Plan</h3>
        </div>
        <div class="col-lg-6 col-sm-12 d-flex justify-content-end">
          <NuxtLink class="btn btn-sm btn-primary" to="/my-salesplan-table" exact-active-class="active">
            <i class="fa-solid fa-table-list"></i>
            <span>Sales Plan Table</span>
          </NuxtLink>
        </div>
      </div>

      <!-- Row Total -->
      <div class="card shadow-sm mb-5">
        <div class="card-body">
          <div class="row" v-if="sales">
            <div class="col-lg my-1">
              <div class="border-dashed p-4">
                <p class="text-muted" id="fontSm">Total Target</p>
                <h4>
                  USD {{ formatPrice(sales.totalTarget) }}
                </h4>
              </div>
            </div>
            <div class="col-lg my-1">
              <div class="border-dashed p-4">
                <p class="text-muted" id="fontSm">Total Open</p>
                <h4>
                  USD {{ formatPrice(sales.totalOpen) }}
                </h4>
              </div>
            </div>
            <div class="col-lg my-1">
              <div class="border-dashed p-4">
                <p class="text-muted" id="fontSm">Total Closed</p>
                <h4>
                  USD {{ formatPrice(sales.totalClosed) }}
                </h4>
              </div>
            </div>
            <div class="col-lg my-1">
              <div class="border-dashed p-4">
                <p class="text-muted" id="fontSm">Total Close In</p>
                <h4>
                  USD {{ formatPrice(sales.totalCloseIn) }}
                </h4>
              </div>
            </div>
            <div class="col-lg my-1">
              <div class="border-dashed p-4">
                <p class="text-muted" id="fontSm">Total Cancel</p>
                <h4>
                  USD {{ formatPrice(sales.totalCancel) }}
                </h4>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- End row total -->

      <!-- Row 2 -->
      <div class="row mt-10">
        <!-- Level 4 -->
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div
              class="
                position-absolute
                top-0
                start-50
                translate-middle
                d-flex
                justify-content-center
                rounded
              "
              id="bgGreen2"
            >
              <h1 class="mt-5" id="textGreen">4</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 id="textGreen" v-if="sales">
                  USD {{ formatPrice(sales.level4.total) }}
                </h2>
                <p class="text-muted">Awareness</p>
              </div>
              <div class="d-grid gap-2" id="cardStyle">
                <a
                  @click="level4Open()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-success
                    d-flex
                    justify-content-start
                    btn-active-light-success
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span
                      id="btnGreen"
                      style="margin-left: -10px"
                      v-if="sales"
                      >{{ formatPrice(sales.level4.countOpen) }}</span
                    >
                    <span id="textGreen" v-if="sales"
                      >USD {{ formatPrice(sales.level4.open) }}</span
                    >
                  </div>
                  <div
                    class="d-flex align-items-center justify-content-end"
                    style="margin-left: -15px"
                  >
                    <span
                      class="text-muted ms-10"
                      id="fontSm"
                      style="margin-left: -15px"
                      >Open</span
                    >
                  </div>
                </a>
                <a
                  @click="level4Cancel()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-danger
                    d-flex
                    justify-content-start
                    btn-active-light-danger
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span id="btnRed" style="margin-left: -10px" v-if="sales">{{
                      formatPrice(sales.level4.countCancel)
                    }}</span>
                    <span id="textRed" v-if="sales"
                      >USD {{ formatPrice(sales.level4.cancel) }}</span
                    >
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span
                      class="text-muted ms-10"
                      id="fontSm"
                      style="margin-left: -15px"
                      >Cancel</span
                    >
                  </div>
                </a>
              </div>
            </div>
            <div class="card-footer border-0" id="cardFooter"></div>
          </div>
        </div>

        <!-- Level 3 -->
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div
              class="
                position-absolute
                top-0
                start-50
                translate-middle
                d-flex
                justify-content-center
                rounded
              "
              id="bgBlue2"
            >
              <h1 class="mt-5" id="textBlue">3</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 id="textBlue" v-if="sales">
                  USD {{ formatPrice(sales.level3.total) }}
                </h2>
                <p class="text-muted">Opportunity</p>
              </div>
              <div class="d-grid gap-2" id="cardStyle">
                <a
                  @click="level3Open()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-success
                    d-flex
                    justify-content-start
                    btn-active-light-success
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span
                      id="btnGreen"
                      style="margin-left: -10px"
                      v-if="sales"
                      >{{ formatPrice(sales.level3.countOpen) }}</span
                    >
                    <span id="textGreen" v-if="sales"
                      >USD {{ formatPrice(sales.level3.open) }}</span
                    >
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span
                      class="text-muted ms-10"
                      id="fontSm"
                      style="margin-left: -15px"
                      >Open</span
                    >
                  </div>
                </a>
                <a
                  @click="level3Cancel()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-danger
                    d-flex
                    justify-content-start
                    btn-active-light-danger
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span id="btnRed" style="margin-left: -10px" v-if="sales">{{
                      formatPrice(sales.level3.countCancel)
                    }}</span>
                    <span id="textRed" v-if="sales"
                      >USD {{ formatPrice(sales.level3.cancel) }}</span
                    >
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span
                      class="text-muted ms-10"
                      id="fontSm"
                      style="margin-left: -15px"
                      >Cancel</span
                    >
                  </div>
                </a>
              </div>
            </div>
            <div class="card-footer border-0" id="cardFooter"></div>
          </div>
        </div>

        <!-- Level 2 -->
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div
              class="
                position-absolute
                top-0
                start-50
                translate-middle
                d-flex
                justify-content-center
                rounded
              "
              id="bgPurple2"
            >
              <h1 class="mt-5" id="textPurple">2</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 id="textPurple" v-if="sales">
                  USD {{ formatPrice(sales.level2.total) }}
                </h2>
                <p class="text-muted">Attractive Proposal</p>
              </div>
              <div class="d-grid gap-2" id="cardStyle">
                <a
                  @click="level2Open()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-success
                    d-flex
                    justify-content-start
                    btn-active-light-success
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span
                      id="btnGreen"
                      style="margin-left: -10px"
                      v-if="sales"
                      >{{ formatPrice(sales.level2.countOpen) }}</span
                    >
                    <span id="textGreen" v-if="sales"
                      >USD {{ formatPrice(sales.level2.open) }}</span
                    >
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span
                      class="text-muted ms-10"
                      id="fontSm"
                      style="margin-left: -15px"
                      >Open</span
                    >
                  </div>
                </a>
                <a
                  @click="level2Open()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-danger
                    d-flex
                    justify-content-start
                    btn-active-light-danger
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span id="btnRed" style="margin-left: -10px" v-if="sales">{{
                      formatPrice(sales.level2.countCancel)
                    }}</span>
                    <span id="textRed" v-if="sales"
                      >USD {{ formatPrice(sales.level2.cancel) }}</span
                    >
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span
                      class="text-muted ms-10"
                      id="fontSm"
                      style="margin-left: -15px"
                      >Cancel</span
                    >
                  </div>
                </a>
              </div>
            </div>
            <div class="card-footer border-0" id="cardFooter"></div>
          </div>
        </div>

        <!-- Level 1 -->
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div
              class="
                position-absolute
                top-0
                start-50
                translate-middle
                d-flex
                justify-content-center
                rounded
              "
              id="bgGold2"
            >
              <h1 class="mt-5" id="textGold">1</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 id="textGold" v-if="sales">
                  USD {{ formatPrice(sales.level1.total) }}
                </h2>
                <p class="text-muted">Contract Signing</p>
              </div>
              <div class="d-grid gap-2" id="cardStyle">
                <a
                  @click="level1Open()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-success
                    d-flex
                    justify-content-start
                    btn-active-light-success
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span
                      id="btnGreen"
                      style="margin-left: -10px"
                      v-if="sales"
                      >{{ formatPrice(sales.level1.countOpen) }}</span
                    >
                    <span
                      id="textGreen"
                    
                      v-if="sales"
                      >USD {{ formatPrice(sales.level1.open) }}</span
                    >
                  </div>
                  <div
                    class="d-flex align-items-center justify-content-end"
                  >
                    <span
                      class="text-muted ms-10"
                      id="fontSm"
                      style="margin-left: -15px"
                      >Open</span
                    >
                  </div>
                </a>
                <a
                  @click="level1Open()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-danger
                    d-flex
                    justify-content-start
                    btn-active-light-danger
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span
                      id="btnRed"
                      style="margin-left: -10px"
                      v-if="sales"
                      >{{ formatPrice(sales.level1.countCancel) }}</span
                    >
                    <span
                      id="textRed"
                    
                      v-if="sales"
                      >USD {{ formatPrice(sales.level1.cancel) }}</span
                    >
                  </div>
                  <div
                    class="d-flex align-items-center justify-content-end"
                  >
                    <span
                      class="text-muted ms-10"
                      id="fontSm"
                      style="margin-left: -15px"
                      >Cancel</span
                    >
                  </div>
                </a>
                <a
                  @click="level1Closed()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-info
                    d-flex
                    justify-content-start
                    btn-active-light-info
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span
                      id="btnPurple"
                      style="margin-left: -10px"
                      v-if="sales"
                      >{{ formatPrice(sales.level1.countClosed) }}</span
                    >
                    <span
                      id="textPurple"
                    
                      v-if="sales"
                      >USD {{ formatPrice(sales.level1.closed) }}</span
                    >
                  </div>
                  <div
                    class="d-flex align-items-center justify-content-end"
                  >
                    <span
                      class="text-muted ms-10"
                      id="fontSm"
                      style="margin-left: -15px"
                      >Closed</span
                    >
                  </div>
                </a>
                <a
                  @click="level1ClosedIn()"
                  class="
                    btn btn-outline btn-outline-dashed btn-outline-warning
                    d-flex
                    justify-content-start
                    btn-active-light-warning
                    me-2
                    mb-2
                  "
                >
                  <div class="d-flex align-items-center gap-2">
                    <span
                      id="btnGold"
                      style="margin-left: -10px"
                      v-if="sales"
                      >{{ formatPrice(sales.level1.countCloseIn) }}</span
                    >
                    <span
                      id="textGold"
                    
                      v-if="sales"
                      >USD {{ formatPrice(sales.level1.closeIn) }}</span
                    >
                  </div>
                  <div
                    class="d-flex align-items-center justify-content-end"
                  >
                    <span
                      class="text-muted ms-10"
                      style="margin-left: -15px"
                      id="fontSm"
                    >
                      Close in
                    </span>
                  </div>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- End row 2 -->      
    </div>
  </div>
</template>

<script>
import debounce from 'lodash/debounce'
export default {
  layout: 'template',
  name: 'MySalesPlanPage',
  data() {
    return {
      prospect_option_salesplan: [],
      aircraft_name_value: null,
      aircraft_id_value: null,
      product_id_value: null,
      prospect_value_salesplan: null,
      product_name_value: null,
      maintenance_name_value: null,
      maintenance_id_value: null,
      user: this.$auth.user.name,
      role: this.$auth.user.role.name,
      sales_table: {
        data: [],
        links: [],
      },
      p_sales: {
        id: null,
        customer: null,
        prospect: null,
        acReg: null,
        registration: null,
        other: null,
        type: null,
        level: null,
        progress: null,
        status: null,
      },
      search: null,

      maintenance_option: [],
      product_option: [],
      customer_option: [],
      hangar_option: [],
      ac_type_option: [],
      prospect_option: [],

      ac_reg: null,
      is_rkap: null,
      value: null,
      tat: null,
      customer: null,
      product: null,
      acReg: null,
      other: null,
      registration: null,
      transaction_type_id: null,
      type: null,
      level: null,
      progress: null,
      status: null,
      start_date: null,
      end_date: null,

      ac_type_id: null,
      ac_type_value: null,

      prospect_id: null,
      prospect_value: null,

      customer_id: null,
      customer_value: null,

      product_id: null,
      product_value: null,

      maintenance_id: null,
      maintenance_value: null,

      hangar_id: null,
      hangar_value: null,

      order: 'id',
      by: 'desc',
      paginate: '10',
      current_page: null,

      sales: null,
      sales_paginate: [],
      isDisabled: true,
      errors: {
        customer: null,
        prospect: null,
        acReg: null,
        registration: null,
        other: null,
        type: null,
        level: null,
        progress: null,
        status: null,
        customer_id: null,
        product_id: null,
        maintenance_id: null,
        transaction_type_id: null,
        hangar_id: null,
        ac_reg: null,
        value: null,
        tat: null,
        ac_type_id: null,
        prospect_id: null,
        start_date: null,
      },
    }
  },
  watch: {
    search: debounce(function () {
      this.listTable()
    }, 500),
  },
  created() {
    this.list()
    this.listTable()
    this.listCustomer()
    this.listProduct()
    this.listMaintenance()
    this.listHangar()
    this.listACType()
  },
  methods: {
    directPage: debounce(function () {
      if (this.current_page < 1) {
        this.current_page = 1
      } else if (this.current_page > this.sales_paginate.last_page) {
        this.current_page = this.sales_paginate.last_page
      }
      let url = new URL(this.sales_paginate.first_page_url)
      let search_params = url.searchParams
      search_params.set('page', this.current_page)
      url.search = search_params.toString()
      let new_url = url.toString()
      this.listTable(new_url)
    }, 500),
    sort(order, by) {
      this.order = order
      this.by = by
      this.listTable()
    },
    formatPrice(value) {
      let val = (value / 1).toFixed(0).replace(',', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
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
    list() {
      this.loading()
      this.$axios
        .get('/api/sales-dashboard')
        .then((response) => {
          this.sales = response.data.data
        })
        .catch((error) => console.log(error))
    },
    listTable(paginate) {
      this.loading()
      paginate = paginate || `/api/sales-table`
      this.$axios
        .get(paginate, {
          params: {
            search: this.search,
            order: this.order,
            by: this.by,
            paginate: this.paginate,
            start_date: this.start_date,
            end_date: this.end_date,
            customer: this.customer,
            product: this.product,
            acReg: this.acReg,
            registration: this.registration,
            other: this.other,
            type: this.type,
            progress: this.progress,
            status: this.status,
            level: this.level,
          },
        })
        .then((response) => {
          this.sales_table.data = response.data.data.data
          this.sales_table.links = response.data.data.links
          this.sales_paginate = response.data.data
          this.current_page = this.sales_paginate.current_page
          Swal.close()
        })
        .catch((error) => console.log(error))
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
          this.customer_option = response.data.data.data
        })
        .catch((error) => console.log(error))
    },
    listProduct() {
      this.$axios
        .get('api/product', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.product_option = response.data.data.data
        })
        .catch((error) => console.log(error))
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
        .catch((error) => console.log(error))
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
    listACType() {
      this.$axios
        .get('/api/aircraft-type', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.ac_type_option = response.data.data.data
        })
        .catch((error) => {
          console.log(error)
        })
    },

    level4Open() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=1&level=4')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },
    level4Cancel() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=4&level=4')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },
    level3Open() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=1&level=3')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },
    level3Cancel() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=4&level=3')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },
    level2Open() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=1&level=2')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },
    level2Cancel() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=4&level=2')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },
    level1Open() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=1&level=1')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },
    level1Cancel() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=4&level=1')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },
    level1Closed() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=2&level=1')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },
    level1ClosedIn() {
      this.$axios
        .get('api/sales-table?order=id&by=desc&paginate=10&status=3&level=1')
        .then((response) => {
          this.$router.push({
            name: 'my-salesplan-table',
          })
        })
    },

    addSales() {
      this.loading()
      this.$axios
        .post(`api/sales-create-tmb`, {
          is_rkap: this.is_rkap,
          transaction_type_id: this.transaction_type_id,
          customer_id: this.customer_id,
          product_id: this.product_id,
          maintenance_id: this.maintenance_id,
          hangar_id: this.hangar_id,
          ac_type_id: this.ac_type_id,
          ac_reg: this.ac_reg,
          value: this.value,
          start_date: this.start_date,
          tat: this.tat,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.list()
          this.listTable()
          Swal.close()
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
            this.errors = error.response.data.errors
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },

    closeModal() {
      this.clearForm()
    },
    clearForm() {
      this.start_date = null
      this.end_date = null
      this.type = null
      this.customer = null
      this.product = null
      this.acReg = null
      this.registration = null
      this.level = null
      this.other = null
      this.progress = null
      this.status = null
      this.listTable()
    },

    closeAddSales() {
      document.getElementById('close_modal').click()
      this.clearFormAddSales()
    },
    clearFormAddSales() {
      this.customer_id = null
      this.product_id = null
      this.maintenance_id = null
      this.hangar_id = null
      this.ac_reg = null
      this.transaction_type_id = null
      this.salesPlan = null
      this.tat = null
      this.start_date = null

      this.maintenance_value = null
      this.product_value = null
      this.ac_type_value = null

      this.customer_value = null
      this.product_name_value = null
      this.maintenance_name_value = null
      this.prospect_value_salesplan = null
      this.ac_reg = null
      this.hangar_value = null
      this.aircraft_name_value = null
      this.value = null
      // this.errors.prospect_id = null
      this.errors.customer_id = null
      this.errors.product_id = null
      this.errors.hangar_id = null
      this.errors.maintenance_id = null
      this.errors.ac_type_id = null
      this.errors.ac_reg = null
      this.errors.transaction_type_id = null
      this.errors.value = null
      this.errors.start_date = null
      this.errors.tat = null

      this.listTable()
    },
  },
}
</script>

<style>
@media (min-width:320px)  {
  #cardStyle{
    width: auto;
  }
}

@media (min-width:1281px)  {
  #cardStyle{
    margin-left: -15px; 
    width: 258px;
  }

  #cardFooter{
    height: 134px
  }
}

.mt-20 {
  margin-top: 20px;
}

.mb-20 {
  margin-bottom: 20px;
}

.carousel-indicators [data-bs-target] {
  box-sizing: content-box;
  flex: 0 1 auto;
  width: 10px;
  height: 10px;
  padding: 0;
  margin-right: 3px;
  margin-left: 3px;
  text-indent: -999px;
  cursor: pointer;
  background-color: #000;
  background-clip: padding-box;
  border: 0;
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent;
  opacity: 0.5;
  transition: opacity 0.6s ease;
  border-radius: 100%;
}

.carousel-indicators .active {
  background-color: #188af8;
}

#btnGreen {
  background-color: #dff0d0;
  color: #5e932f;
  border-radius: 100%;
  padding: 5px 13px 5px 13px;
}

#btnRed {
  background-color: #f8e8e8;
  color: #952d2d;
  border-radius: 100%;
  padding: 5px 13px 5px 13px;
}

#btnPurple {
  background-color: #f8e8f6;
  color: #952d88;
  border-radius: 100%;
  padding: 5px 13px 5px 13px;
}

#btnGold {
  background-color: #f8f7e8;
  color: #958e2d;
  border-radius: 100%;
  padding: 5px 13px 5px 13px;
}

#bgGreen {
  background: #dff0d0;
}

#bgBlue {
  background: #e8e9f8;
}

#bgRed {
  background: #f8e8e8;
}

#bgPurple {
  background: #f8e8f6;
}

#bgGold {
  background: #f8f7e8;
}

#bgGreen2 {
  background-color: #dff0d0;
  width: 60px;
  height: 60px;
}

#bgBlue2 {
  background-color: #d0d3f1;
  width: 60px;
  height: 60px;
}

#bgPurple2 {
  background-color: #f1d0ee;
  width: 60px;
  height: 60px;
}

#bgGold2 {
  background-color: #f1efd0;
  width: 60px;
  height: 60px;
}

#textGreen {
  color: #5e932f;
}

#textRed {
  color: #952d2d;
}

#textBlue {
  color: #2d3495;
}

#textPurple {
  color: #952d88;
}

#textGold {
  color: #958e2d;
}

#fontSm {
  font-size: 12px;
}
</style>