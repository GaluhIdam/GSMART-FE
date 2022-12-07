<template>
  <div>
    <!-- Content -->
    <div class="container-fluid mt-5 mb-5">
      <!-- Breadcrumb -->
      <div class="row mb-5">
        <div class="col-lg-6">
          <Nuxt-link class="menu-link" to="/my-salesplan-table" active-class="active">
            <i class="fa-solid fa-angle-left"></i>
            <span class="menu-title">Sales Plan Table</span>
          </Nuxt-link>
        </div>
        <div class="col-lg-6">
          <div class="position-relative">
            <div class="position-absolute top-0 end-0">
              <nav aria-label="breadcrumb">
                <ol class="breadcrumb">
                  <li class="breadcrumb-item">
                    <Nuxt-link
                      class="menu-link"
                      to="/my-salesplan-table"
                      active-class="active"
                    >
                      <span class="menu-title">Sales Plan Table</span>
                      &nbsp;
                    </Nuxt-link>
                  </li>
                  <li class="breadcrumb-item active" aria-current="page">
                    Detail
                  </li>
                </ol>
              </nav>
            </div>
          </div>
        </div>
      </div>
      <!-- End Breadcrumb -->

      <!-- Detail -->
      <div class="row mt-4">
        <div class="card">
          <div class="card-body">
            <!-- header -->
            <div class="row">
              <div class="col-lg-6">
                <h3>Detail Sales Plan</h3>
              </div>
              <div class="col-lg-6">
                <div class="text-right">
                  <div
                    class="position-absolute top-0 end-0 mx-15 mt-4"
                    v-if="sales_detail"
                  >
                    <button
                      class="btn btn-info btn-sm me-2"
                      data-bs-toggle="modal"
                      data-bs-target="#switchAMS"
                      v-if="
                        sales_detail.status === 'Open' && role == 'Administrator' ||  role == 'TPR'
                      "
                    >
                    <i class="fa-solid fa-repeat"></i> 
                      Switch AMS
                    </button>
                    <button
                      class="btn btn-primary btn-sm"
                      data-bs-toggle="modal"
                      data-bs-target="#editSales"
                      v-if="
                        sales_detail.type === 'TMB Project' || sales_detail.type === 'TMB Retail' &&
                        sales_detail.status === 'Open' && role == 'Administrator' ||  role == 'TPR'
                      "
                    >
                      <i class="fa-solid fa-pen"></i> Edit Sales Plan
                    </button>
                  </div>
                </div>
              </div>
            </div>
            <!-- End header -->

            <!-- Modal switchAMS -->
            <div
              class="modal fade"
              id="switchAMS"
              tabindex="-1"
              aria-labelledby="switchAMSLabel"
              aria-hidden="true"
            >
              <div class="modal-dialog">
                <div class="modal-content">
                  <div class="modal-header">
                    <h5 class="modal-title w-100" id="switchAMSLabel">
                      Switch AMS
                    </h5>
                    <button
                      type="button"
                      class="btn-close"
                      data-bs-dismiss="modal"
                      aria-label="Close"
                    ></button>
                  </div>
                  <form>
                    <div class="modal-body">
                      <form action="">
                        <div class="mb-3">
                          <label class="form-label">To</label>
                          <select
                            v-model="ams_id"
                            class="form-select"
                            :class="{ 'is-invalid': errors.ams_id }"
                          >
                            <option :value="null" disabled>Select AMS</option>
                            <option v-for="(amss, ams_index) in ams" :value="amss.id" :key="ams_index">
                              {{ amss.initial }} - {{ amss.user.name }}
                            </option>
                          </select>
                          <span
                            v-if="errors.ams_id"
                            class="error invalid-feedback"
                            >{{ errors.ams_id[0] }}</span
                          >
                        </div>
                        <div class="mb-3">
                          <label class="form-label">Description</label> <br />
                          <div id="bodyAMS" v-if="sales_detail">
                            Level: <b>{{ sales_detail.level }}</b> Status:
                            <b>{{ sales_detail.status }}</b> Sales Type:
                            <b>{{ sales_detail.other }}</b> Type:
                            <b>{{ sales_detail.type }}</b> Month Sales:
                            <b>{{ sales_detail.monthSales }}</b> Years:
                            <b>{{ sales_detail.year }}</b> Start Date Project:
                            <b>{{ sales_detail.startDate }}</b> End Date
                            Project: <b>{{ sales_detail.endDate }}</b> TAT:
                            <b>{{ sales_detail.tat }} Days</b> Progress:
                            <b>{{ sales_detail.progress }}%</b> Product:
                            <b>{{ sales_detail.product.name }}</b>
                            Location:
                            <b v-if="sales_detail.location == '-' || null">-</b>
                            <b v-else>{{ sales_detail.location }}</b>
                            Maintenance:
                            <b>{{ sales_detail.maintenance }}</b>
                          </div>
                        </div>
                      </form>
                    </div>
                    <div class="modal-footer">
                      <button
                        type="button"
                        class="btn btn-secondary"
                        data-bs-dismiss="modal"
                        id="close_modal_ams"
                        @click="closeModalAMS()"
                      >
                        Close
                      </button>
                      <button
                        type="button"
                        class="btn btn-primary"
                        @click="swtichAMS()"
                        v-permission="['switch_ams']"
                      >
                        Send
                      </button>
                    </div>
                  </form>
                </div>
              </div>
            </div>

            <!-- Modal edit Sales -->
            <div
              class="modal fade"
              tabindex="-1"
              id="editSales"
              data-bs-backdrop="static"
            >
              <div class="modal-dialog modal-dialog-centered modal-lg">
                <div class="modal-content">
                  <div class="modal-header">
                    <h3 class="modal-title">Edit Sales Plan</h3>

                  <!--begin::Close-->
                  <div
                    class="btn btn-icon btn-sm btn-active-light-primary ms-2"
                    data-bs-dismiss="modal"
                    aria-label="Close"
                  >
                    <span
                      class="svg-icon svg-icon-1"
                      @click="closeModalContact()"
                    >
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
                    <form @submit.prevent="salesUpdate" v-if="sales_detail">
                      <input type="hidden" v-model="sales_detail.id" />
                      <div class="row">
                        <div class="col-lg-6">
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold"
                              >Maintenance</label
                            >
                            <select
                              v-model="maintenance_id"
                              class="form-select"
                              :class="{ 'is-invalid': errors.maintenance_id }"
                            >
                              <option :value="null" disabled>Select Maintenance</option>
                              <!-- <option :value="sales_detail.maintenance" >{{ sales_detail.maintenance }}</option> -->
                              <option
                                v-for="(maintenance_options, maintenance_index) in maintenance_option"
                                :value="maintenance_options.id"
                                :key="maintenance_index"
                              >
                                {{ maintenance_options.name }}
                              </option>
                            </select>
                            <span
                              v-if="errors.maintenance_id"
                              class="error invalid-feedback"
                            >
                              {{ errors.maintenance_id[0] }}
                            </span>
                          </div>
                        </div>
                        <div class="col-lg-6">
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold"
                              >Registration</label
                            >
                            <input
                              type="text"
                              class="form-control"
                              v-model="sales_detail.acReg"
                              :class="{
                                'is-invalid': errors.ac_reg,
                              }"
                            />
                            <span
                              v-if="errors.ac_reg"
                              class="error invalid-feedback"
                              >{{ errors.ac_reg[0] }}</span
                            >
                          </div>
                        </div>
                      </div>
                      <div class="row my-3">
                        <div class="col-lg-6">
                          <div class="mb-3">
                            <label class="form-label fw-bold">Location</label>
                            <select v-model="hangar_id" class="form-select" :class="{ 'is-invalid': errors.hangar_id }">
                              <option :value="null" disabled>
                                Select Hangar
                              </option>
                              <option
                                v-for="(hangar_options, hangar_index) in hangar_option"
                                :value="hangar_options.id"
                                :key="hangar_index"
                              >
                                {{ hangar_options.name }}
                              </option>
                            </select>
                            <span
                              v-if="errors.hangar_id"
                              class="error invalid-feedback"
                              >{{ errors.hangar_id[0] }}</span
                            >
                          </div>
                        </div>
                        <div class="col-lg-6">
                          <div class="mb-3">
                            <label class="form-label fw-bold">Line</label>
                            <select v-model="line_id" class="form-select" :class="{ 'is-invalid': errors.line_id }">
                              <option :value="null" disabled>
                                Select Line
                              </option>
                              <option
                                v-for="(lines, line_index) in line"
                                v-if="lines.hangar_id === hangar_id"
                                :value="lines.id"
                                :key="line_index"
                              >
                                {{ lines.name }}
                              </option>
                            </select>
                            <span
                              v-if="errors.line_id"
                              class="error invalid-feedback"
                              >{{ errors.line_id[0] }}</span
                            >
                          </div>
                        </div>
                      </div>
                      <div class="row">
                        <div class="col-lg-4">
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">Sales Plan</label>
                            <input
                              type="number"
                              class="form-control"
                              v-model="sales_detail.totalSales"
                              :class="{
                                'is-invalid': errors.value,
                              }"
                            />
                            <span
                              v-if="errors.value"
                              class="error invalid-feedback"
                              >{{ errors.value[0] }}</span
                            >
                          </div>
                        </div>
                        <div class="col-lg-4">
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">Start Date</label>
                            <input
                              type="date"
                              class="form-control"
                              v-model="sales_detail.startDate"
                              :class="{
                                'is-invalid': errors.start_date,
                              }"
                            />
                            <span
                              v-if="errors.start_date"
                              class="error invalid-feedback"
                              >{{ errors.start_date[0] }}</span
                            >
                          </div>
                        </div>
                        <div class="col-lg-4">
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">TAT</label>
                            <input
                              type="number"
                              class="form-control"
                              v-model="sales_detail.tat"
                              :class="{
                                'is-invalid': errors.tat,
                              }"
                            />
                            <span
                              v-if="errors.tat"
                              class="error invalid-feedback"
                              >{{ errors.tat[0] }}</span
                            >
                          </div>
                        </div>
                      </div>
                      <div class="row mt-10">
                        <div class="col d-flex justify-content-end">
                          <button
                            type="button"
                            class="btn btn-light mx-2"
                            data-bs-dismiss="modal"
                            id="close_modal_edit_sales"
                            @click="closeModalEditSales()"
                          >
                            Close
                          </button>
                          <button
                            type="submit"
                            class="btn btn-primary"
                            v-permission="['update_sales']"
                          >
                            Save
                          </button>
                        </div>
                      </div>
                    </form>
                    <form class="mt-5" @submit.prevent="pbthUpdate" v-if="sales_detail && transactionType == 'PBTH'">
                    <h3 class="fs-2 fw-fold">Edit Rate & Flight Hour</h3>
                      <div class="row">
                        <div class="col-lg-6">
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">
                              Rate
                            </label>
                            <input type="number" class="form-control" v-model="data_pbth_rate">
                            <span
                              v-if="errors.maintenance_id"
                              class="error invalid-feedback"
                            >
                              {{ errors.maintenance_id[0] }}
                            </span>
                          </div>
                        </div>
                        <div class="col-lg-6">
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">
                              Flight Hour
                            </label>
                            <input type="number" class="form-control" v-model="data_pbth_flighthour">
                            <span
                              v-if="errors.hangar_id"
                              class="error invalid-feedback"
                            >
                              {{ errors.hangar_id[0] }}
                            </span>
                          </div>
                        </div>
                      </div>
                      <div class="row mt-10">
                        <div class="col d-flex justify-content-end">
                          <button
                            type="button"
                            class="btn btn-light mx-2"
                            data-bs-dismiss="modal"
                            id="close_modal_edit_sales"
                          >
                            Close
                          </button>
                          <button
                            type="submit"
                            class="btn btn-primary"
                          >
                            Save
                          </button>
                        </div>
                      </div>
                    </form>
                  </div>
                </div>
              </div>
            </div>

            <!-- Card -->
            <div class="row mt-3">
              <div class="col-lg-4 col-md-12 col-sm-12">
                <div class="card mb-3" style="max-width: 540px">
                  <div class="row no-gutters">
                    <div
                      class="col-md"
                      style="margin-top: -20px; margin-left: -30px"
                    >
                      <div class="card-body">
                        <h5 class="card-title" v-if="sales_detail">
                          {{ sales_detail.registration }}
                        </h5>
                        <p class="card-text" v-if="sales_detail">
                          <small class="text-muted"
                            ><i class="fa-solid fa-plane-up"></i>
                            {{ sales_detail.acReg }}</small
                          >
                        </p>
                        <p class="card-text" v-if="sales_detail">
                          <small class="text-muted"
                            ><i class="fa-solid fa-spa"></i>
                            {{ sales_detail.customer.name }}</small
                          >
                        </p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-lg">
                <div class="text-center d-grid gap-2">
                  <span class="me-2 mb-2" id="cardMarketShare">
                    <h3 class="mt-2" id="textMarketShare" v-if="sales_detail">
                      USD {{ formatPrice(sales_detail.marketShare) }}
                    </h3>
                    <p><small class="text-muted">Sales RKAP</small></p>
                  </span>
                </div>
              </div>
              <div class="col-lg">
                <div class="text-center d-grid gap-2">
                  <span class="me-2 mb-2" id="cardSalesPlan">
                    <h3 class="mt-2" id="textSalesPlan" v-if="sales_detail">
                      USD {{ formatPrice(sales_detail.totalSales) }}
                    </h3>
                    <p><small class="text-muted">Total Sales Plan</small></p>
                  </span>
                </div>
              </div>
              <div class="col-lg">
                <div class="text-center d-grid gap-2">
                  <span class="me-2 mb-2" id="cardDevisiasi">
                    <h3 class="mt-2" id="textDevisiasi" v-if="sales_detail">
                      USD {{ formatPrice(sales_detail.deviasi) }}
                    </h3>
                    <p><small class="text-muted">Deviation</small></p>
                  </span>
                </div>
              </div>
            </div>
            <!-- End Card -->

            <!-- Detail -->
            <div class="row" v-if="sales_detail">
              <div class="col-lg-1 col-s">
                <p class="text-muted mt-5">Level</p>
                <div v-if="sales_detail.level === 1">
                  <span class="badge badge-success"><b>Level 1</b></span>
                </div>
                <div v-if="sales_detail.level === 2">
                  <span class="badge badge-warning"><b>Level 2</b></span>
                </div>
                <div v-if="sales_detail.level === 3">
                  <span class="badge badge-primary"><b>Level 3</b></span>
                </div>
                <div v-if="sales_detail.level === 4">
                  <span class="badge badge-danger"><b>Level 4</b></span>
                </div>
                <p class="text-muted mt-5">Status</p>
                <div v-if="sales_detail.status === 'Cancel'">
                  <span class="badge badge-danger"><b>Cancel</b></span>
                </div>
                <div v-if="sales_detail.status === 'Open'">
                  <span class="badge badge-gmf"><b>Open</b></span>
                </div>
                <div v-if="sales_detail.status === 'Close in'">
                  <span class="badge badge-success"><b>Close in</b></span>
                </div>
                <div v-if="sales_detail.status === 'Closed'">
                  <span class="badge badge-green"><b>Closed Sales</b></span>
                </div>
              </div>
              <div class="col-lg-1">
                <p class="text-muted mt-5">Sales Type</p>
                <div v-if="sales_detail.other === 'RKAP'">
                  <b>RKAP</b>
                </div>
                <div v-else-if="sales_detail.other === 'Additional'">
                  <b>Additional</b>
                </div>
                <p class="text-muted mt-5">Type</p>
                <div v-if="sales_detail.type === 'TMB Retail'">
                  <b>{{
                  sales_detail.type
                  }}</b>
                </div>
                <div v-if="sales_detail.type === 'TMB Project'">
                  <b>{{
                  sales_detail.type
                  }}</b>
                </div>
                <div v-if="sales_detail.type === 'PBTH'">
                  <b>{{
                  sales_detail.type
                  }}</b>
                </div>
              </div>
              <div class="col-lg-2">
                <p class="text-muted mt-5">Progress</p>
                <div v-if="sales_detail.progress === 10">
                  <span class="badge badge-danger">10 %</span>
                </div>
                <div v-if="sales_detail.progress === 20">
                  <span class="badge badge-danger">20 %</span>
                </div>
                <div v-if="sales_detail.progress === 30">
                  <span class="badge badge-danger">30 %</span>
                </div>
                <div v-if="sales_detail.progress === 40">
                  <span class="badge badge-primary">40 %</span>
                </div>
                <div v-if="sales_detail.progress === 50">
                  <span class="badge badge-primary">50 %</span>
                </div>
                <div v-if="sales_detail.progress === 60">
                  <span class="badge badge-primary">60 %</span>
                </div>
                <div v-if="sales_detail.progress === 70">
                  <span class="badge badge-warning">70 %</span>
                </div>
                <div v-if="sales_detail.progress === 80">
                  <span class="badge badge-warning">80 %</span>
                </div>
                <div v-if="sales_detail.progress === 90">
                  <span class="badge badge-warning">90 %</span>
                </div>
                <div v-if="sales_detail.progress === 100">
                  <span class="badge badge-success">100 %</span>
                </div>
                <p class="text-muted mt-5">Month Sales</p>
                <p>
                  <b>{{ sales_detail.monthSales }}</b>
                </p>
              </div>
              <div class="col-lg-1">
                <p class="text-muted mt-5">TAT</p>
                <p>
                  <b>{{ sales_detail.tat }} Days</b>
                </p>
                <p class="text-muted mt-5">Years</p>
                <p>
                  <b>{{ sales_detail.year }}</b>
                </p>
              </div>
              <div class="col-lg-2">
                <p class="text-muted mt-5">Start Date Project</p>
                <p>
                  <b>{{ sales_detail.startDate }}</b>
                </p>
                <p class="text-muted mt-5">End Date Project</p>
                <p>
                  <b>{{ sales_detail.endDate }}</b>
                </p>
              </div>
              <div class="col-lg-2">
                <p class="text-muted mt-5">Location</p>
                <p>
                  <b v-if="sales_detail.location == '-' || null">-</b>
                  <b v-else>{{ sales_detail.location }}</b>
                </p>
                <p class="text-muted mt-5">Product</p>
                <p>
                  <b>{{ sales_detail.product.name }}</b>
                </p>
              </div>
              <div class="col-lg-3">
                <p class="text-muted mt-5">Maintenance</p>
                <p>
                  <b>{{ sales_detail.maintenance }}</b>
                </p>
              </div>
            </div>
            <!-- End Detail -->
            <hr>
            <!-- Tab -->
            <div class="row mt-5">
              <ul class="nav nav-pills" id="pills-tab" role="tablist">
                <li class="nav-item" role="presentation">
                  <button
                    class="nav-link active"
                    id="upgrade-level-tab"
                    data-bs-toggle="tab"
                    data-bs-target="#upgrade-level-tab-pane"
                    type="button"
                    role="tab"
                    aria-controls="upgrade-level-tab-pane"
                    aria-selected="true"
                  >
                    Upgrade Level
                  </button>
                </li>
                <li class="nav-item" role="presentation">
                  <button
                    class="nav-link"
                    id="history-tab"
                    data-bs-toggle="tab"
                    data-bs-target="#history-tab-pane"
                    type="button"
                    role="tab"
                    aria-controls="history-tab-pane"
                    aria-selected="false"
                  >
                    History
                  </button>
                </li>
                <li class="nav-item" role="presentation">
                  <button
                    class="nav-link"
                    id="contact-tab"
                    data-bs-toggle="tab"
                    data-bs-target="#contact-tab-pane"
                    type="button"
                    role="tab"
                    aria-controls="contact-tab-pane"
                    aria-selected="false"
                  >
                    Contact Person
                  </button>
                </li>
                <li
                  class="nav-item"
                  role="presentation"
                  v-if="
                    role == 'AMS' || role == 'Administrator' || role == 'TPR'
                  "
                >
                  <button
                    class="nav-link"
                    id="reschedule-tab"
                    data-bs-toggle="tab"
                    data-bs-target="#reschedule-tab-pane"
                    type="button"
                    role="tab"
                    aria-controls="reschedule-tab-pane"
                    aria-selected="false"
                  >
                    Reschedule
                  </button>
                </li>
                <li
                  class="nav-item"
                  role="presentation"
                  v-if="
                    role == 'AMS' || role == 'Administrator' || role == 'TPR'
                  "
                >
                  <button
                    class="nav-link"
                    id="cancel-tab"
                    data-bs-toggle="tab"
                    data-bs-target="#cancel-tab-pane"
                    type="button"
                    role="tab"
                    aria-controls="cancel-tab-pane"
                    aria-selected="false"
                  >
                    Cancel
                  </button>
                </li>
              </ul>

              <div class="tab-content" id="pills-tabContent">
                <!-- Tab Upgrade Level -->
                <div
                  class="tab-pane fade show active"
                  id="upgrade-level-tab-pane"
                  role="tabpanel"
                  aria-labelledby="upgrade-level-tab"
                  tabindex="0"
                >
                  <!--begin::Stepper-->
                  <div
                    class="stepper stepper-pills mt-5"
                    id="kt_stepper_example_basic"
                  >
                  <div v-if="sales_detail">
                    <!--begin::Nav-->
                    <div v-if="sales_detail.level == 4">
                      <div class="stepper-nav flex-center flex-wrap mb-10">
                        <!--begin::Step 1-->
                          <div
                            class="stepper-item mx-8 my-4 current"
                            data-kt-stepper-element="nav"
                          >
                            <!--begin::Wrapper-->
                            <div class="stepper-wrapper d-flex align-items-center">
                              <!--begin::Icon-->
                              <div class="stepper-icon w-40px h-40px">
                                <i class="stepper-check fas fa-check"></i>
                                <span class="stepper-number">4</span>
                              </div>
                              <!--end::Icon-->

                              <!--begin::Label-->
                              <div class="stepper-label">
                                <div class="stepper-desc">Awareness</div>
                              </div>
                              <!--end::Label-->
                            </div>
                            <!--end::Wrapper-->

                            <!--begin::Line-->
                            <div class="stepper-line h-40px"></div>
                            <!--end::Line-->
                          </div>
                        <!--end::Step 1-->
                        <!--begin::Step 2-->
                        <div
                          class="stepper-item mx-8 my-4"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">3</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Opportunity</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 2-->

                        <!--begin::Step 3-->
                        <div
                          class="stepper-item mx-8 my-4"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">2</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Attractive Proposal</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 3-->

                        <!--begin::Step 4-->
                        <div
                          class="stepper-item mx-8 my-4"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">1</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Contract Signing</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 4-->
                      </div>
                    </div>
                    <div v-else-if="sales_detail.level == 3">
                      <div class="stepper-nav flex-center flex-wrap mb-10">
                        <!--begin::Step 1-->
                          <div
                            class="stepper-item mx-8 my-4 completed"
                            data-kt-stepper-element="nav"
                          >
                            <!--begin::Wrapper-->
                            <div class="stepper-wrapper d-flex align-items-center">
                              <!--begin::Icon-->
                              <div class="stepper-icon w-40px h-40px">
                                <i class="stepper-check fas fa-check"></i>
                                <span class="stepper-number">4</span>
                              </div>
                              <!--end::Icon-->

                              <!--begin::Label-->
                              <div class="stepper-label">
                                <div class="stepper-desc">Awareness</div>
                              </div>
                              <!--end::Label-->
                            </div>
                            <!--end::Wrapper-->

                            <!--begin::Line-->
                            <div class="stepper-line h-40px"></div>
                            <!--end::Line-->
                          </div>
                        <!--end::Step 1-->
                        <!--begin::Step 2-->
                        <div
                          class="stepper-item mx-8 my-4 current"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">3</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Opportunity</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 2-->

                        <!--begin::Step 3-->
                        <div
                          class="stepper-item mx-8 my-4"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">2</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Attractive Proposal</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 3-->

                        <!--begin::Step 4-->
                        <div
                          class="stepper-item mx-8 my-4"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">1</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Contract Signing</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 4-->
                      </div>
                    </div>
                    <div v-else-if="sales_detail.level == 2">
                      <div class="stepper-nav flex-center flex-wrap mb-10">
                        <!--begin::Step 1-->
                          <div
                            class="stepper-item mx-8 my-4 completed"
                            data-kt-stepper-element="nav"
                          >
                            <!--begin::Wrapper-->
                            <div class="stepper-wrapper d-flex align-items-center">
                              <!--begin::Icon-->
                              <div class="stepper-icon w-40px h-40px">
                                <i class="stepper-check fas fa-check"></i>
                                <span class="stepper-number">4</span>
                              </div>
                              <!--end::Icon-->

                              <!--begin::Label-->
                              <div class="stepper-label">
                                <div class="stepper-desc">Awareness</div>
                              </div>
                              <!--end::Label-->
                            </div>
                            <!--end::Wrapper-->

                            <!--begin::Line-->
                            <div class="stepper-line h-40px"></div>
                            <!--end::Line-->
                          </div>
                        <!--end::Step 1-->
                        <!--begin::Step 2-->
                        <div
                          class="stepper-item mx-8 my-4 completed"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">3</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Opportunity</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 2-->

                        <!--begin::Step 3-->
                        <div
                          class="stepper-item mx-8 my-4 current"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">2</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Attractive Proposal</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 3-->

                        <!--begin::Step 4-->
                        <div
                          class="stepper-item mx-8 my-4"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">1</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Contract Signing</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 4-->
                      </div>
                    </div>
                    <div v-else-if="sales_detail.level == 1 && sales_detail.status != 'Closed'">
                      <div class="stepper-nav flex-center flex-wrap mb-10">
                        <!--begin::Step 1-->
                          <div
                            class="stepper-item mx-8 my-4 completed"
                            data-kt-stepper-element="nav"
                          >
                            <!--begin::Wrapper-->
                            <div class="stepper-wrapper d-flex align-items-center">
                              <!--begin::Icon-->
                              <div class="stepper-icon w-40px h-40px">
                                <i class="stepper-check fas fa-check"></i>
                                <span class="stepper-number">4</span>
                              </div>
                              <!--end::Icon-->

                              <!--begin::Label-->
                              <div class="stepper-label">
                                <div class="stepper-desc">Awareness</div>
                              </div>
                              <!--end::Label-->
                            </div>
                            <!--end::Wrapper-->

                            <!--begin::Line-->
                            <div class="stepper-line h-40px"></div>
                            <!--end::Line-->
                          </div>
                        <!--end::Step 1-->
                        <!--begin::Step 2-->
                        <div
                          class="stepper-item mx-8 my-4 completed"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">3</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Opportunity</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 2-->

                        <!--begin::Step 3-->
                        <div
                          class="stepper-item mx-8 my-4 completed"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">2</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Attractive Proposal</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 3-->

                        <!--begin::Step 4-->
                        <div
                          class="stepper-item mx-8 my-4 current"
                          data-kt-stepper-element="nav"
                        >
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                            <!--begin::Icon-->
                            <div class="stepper-icon w-40px h-40px">
                              <i class="stepper-check fas fa-check"></i>
                              <span class="stepper-number">1</span>
                            </div>
                            <!--begin::Icon-->

                            <!--begin::Label-->
                            <div class="stepper-label">
                              <div class="stepper-desc">Contract Signing</div>
                            </div>
                            <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                        </div>
                        <!--end::Step 4-->
                      </div>
                    </div>
                    <!--end::Nav-->
                  </div>

                    <!--begin::Form-->
                    <div
                      class="form mx-auto"
                      novalidate="novalidate"
                      id="kt_stepper_example_basic_div"
                    >
                      <!--begin::Group-->
                      <div class="mb-5" v-if="sales_detail">
                        <!--begin::Step 4-->
                        <div v-if="sales_detail.level == 4">
                          <div
                            class="flex-column current"
                            data-kt-stepper-element="content"
                          >
                            <form>
                              <div class="row">
                                <!-- Fill in Contact Person of Customer -->
                                <div class="col-lg-6">
                                  <h3>Fill in Contact Person of Customer</h3>
                                  <p class="text-muted">
                                    <small
                                      >by <a href="#">{{ user }}</a></small
                                    >
                                  </p>
                                </div>
                                <div class="col-lg-6 mb-20">
                                  <div
                                    class="position-relative"
                                    v-if="sales_detail"
                                  >
                                    <div
                                      class="position-absolute top-0 end-0"
                                      v-if="
                                        sales_detail.level == 4 &&
                                        sales_detail.status === 'Open'
                                      "
                                    >
                                      <button
                                        type="button"
                                        class="btn btn-primary btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#addContact"
                                        @click="addContact()"
                                        v-if="
                                          role == 'AMS' ||
                                          role == 'Administrator'
                                        "
                                      >
                                        Add Contact Person
                                      </button>
                                    </div>
                                  </div>
                                </div>
                                <div class="rounded box-d" id="myBorder">
                                  <div class="mt-3 table-responsive">
                                    <table class="table" v-if="contact">
                                      <tr
                                        v-for="contact in level4[0].data"
                                        :key="contact.id"
                                        id="heightContact"
                                      >
                                        <td>
                                          <strong>{{ contact.name }}</strong>
                                        </td>
                                        <td>
                                          <strong>{{ contact.phone }}</strong>
                                        </td>
                                        <td>
                                          <strong>{{ contact.email }}</strong>
                                        </td>
                                      </tr>
                                    </table>
                                  </div>
                                </div>

                                <!-- Upload Attachment RFQ or Email Request -->
                                <div class="col-lg-6 mt-3">
                                  <h3>
                                    Upload Attachment RFQ or Email Request
                                  </h3>
                                  <p class="text-danger">
                                    <small>* File size max 5MB</small>
                                  </p>
                                </div>
                                <div class="col-lg-6 mt-3 mb-20">
                                  <div
                                    class="position-relative"
                                    v-if="sales_detail"
                                  >
                                    <div
                                      class="position-absolute top-0 end-0"
                                      v-if="
                                        sales_detail.level == 4 &&
                                        sales_detail.status === 'Open'
                                      "
                                    >
                                      <button
                                        type="button"
                                        class="btn btn-primary btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#addFile"
                                        @click="addFile1()"
                                        v-if="
                                          role == 'AMS' ||
                                          role == 'Administrator'
                                        "
                                        v-permission="['upload_files']"
                                      >
                                        Upload Document
                                      </button>
                                    </div>
                                  </div>
                                </div>
                                <div class="rounded box-d" id="myBorder">
                                  <div class="mt-3 table-responsive">
                                    <table class="table" v-if="files">
                                      <tr
                                        v-for="files in level4[1].data"
                                        :key="files.id"
                                      >
                                        <td>
                                          <a
                                            :href="files.full_path"
                                            class="
                                              btn
                                              btn-outline-primary
                                              btn-outline
                                              btn-sm
                                              mb-2
                                            "
                                            target="_blank"
                                          >
                                            <strong>{{
                                              files.file_name
                                            }}</strong>
                                          </a>
                                        </td>
                                        <td
                                          class="d-flex justify-content-end"
                                          v-if="
                                            sales_detail.level == 4 &&
                                            sales_detail.status === 'Open'
                                          "
                                        >
                                          <button
                                            type="button"
                                            class="btn btn-danger btn-sm"
                                            @click="removeFile(files.id)"
                                            v-permission="['delete_files']"
                                            v-if="
                                              role == 'AMS' ||
                                              role == 'Administrator'
                                            "
                                          >
                                            <span class="fas fa-trash"></span>
                                          </button>
                                        </td>
                                      </tr>
                                    </table>
                                  </div>
                                </div>

                                <!-- Upload Attachment Workscope -->
                                <div class="col-lg-6 mt-3">
                                  <h3>Upload Attachment Workscope</h3>
                                  <p class="text-danger">
                                    <small>* File size max 5MB</small>
                                  </p>
                                </div>
                                <div class="col-lg-6 mt-3 mb-20">
                                  <div
                                    class="position-relative"
                                    v-if="sales_detail"
                                  >
                                    <div
                                      class="position-absolute top-0 end-0"
                                      v-if="
                                        sales_detail.level == 4 &&
                                        sales_detail.status === 'Open'
                                      "
                                    >
                                      <button
                                        type="button"
                                        class="btn btn-primary btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#addFile"
                                        @click="addFile2()"
                                        v-if="
                                          role == 'AMS' ||
                                          role == 'Administrator'
                                        "
                                        v-permission="['upload_files']"
                                      >
                                        Upload Document
                                      </button>
                                    </div>
                                  </div>
                                </div>
                                <div class="rounded box-d" id="myBorder">
                                  <div class="mt-3">
                                    <table class="table" v-if="files">
                                      <tr
                                        v-for="files in level4[2].data"
                                        :key="files.id"
                                      >
                                        <td>
                                          <a
                                            :href="files.full_path"
                                            class="
                                              btn
                                              btn-outline-primary
                                              btn-outline
                                              btn-sm
                                              mb-2
                                            "
                                            target="_blank"
                                          >
                                            <strong>{{
                                              files.file_name
                                            }}</strong>
                                          </a>
                                        </td>
                                        <td
                                          class="d-flex justify-content-end"
                                          v-if="
                                            sales_detail.level == 4 &&
                                            sales_detail.status === 'Open'
                                          "
                                        >
                                          <button
                                            type="button"
                                            class="btn btn-danger btn-sm"
                                            @click="removeFile(files.id)"
                                            v-permission="['delete_files']"
                                            v-if="
                                              role == 'AMS' ||
                                              role == 'Administrator'
                                            "
                                          >
                                            <span class="fas fa-trash"></span>
                                          </button>
                                        </td>
                                      </tr>
                                    </table>
                                  </div>
                                </div>

                                <div class="row mt-5" v-if="role == 'AMS'">
                                  <div class="alert alert-info" role="alert" v-if="(level4[3].status == 0)">
                                    Waiting for Approval Hangar Slot
                                  </div>
                                  <div class="alert alert-success" role="alert" v-if="(level4[3].status == 1)">
                                    Approved
                                  </div>
                                </div>
                                <!-- Slot Request -->
                                <div class="col-lg-6 mt-5">
                                  <h3>Slot Request</h3>
                                  <p class="text-muted">
                                    <small
                                      >by <a href="#">{{ user }}</a></small
                                    >
                                  </p>
                                </div>
                                <div class="col-lg-6 mt-5 mb-20">
                                  <div class="position-relative">
                                    <div
                                      class="position-absolute top-0 end-0"
                                      v-if="sales_detail.status == 'Open'"
                                    >
                                      <button
                                        v-if="
                                        level4[3].data != null &&
                                        level4[3].status == 0 &&
                                        role == 'Administrator' || role == 'CBO'" 
                                        type="button"
                                        @click="slotReject()"
                                        class="btn btn-danger btn-sm"
                                      >
                                        Reject
                                      </button>
                                      <button
                                        v-if="
                                        level4[3].data != null &&
                                        level4[3].status == 0 &&
                                        role == 'Administrator' || role == 'CBO'
                                        "
                                        type="button"
                                        class="btn btn-success btn-sm"
                                        @click="slotApprove()"
                                      >
                                        Approve
                                      </button>
                                      <button
                                        v-if="
                                        level4[3].data == null &&
                                        level4[3].status == 0 &&
                                        sales_detail.level == 4 &&
                                        role == 'AMS' || role == 'Administrator'"
                                        type="button"
                                        class="btn btn-info btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#slotRequest"
                                      >
                                        Request to CBO
                                      </button>
                                    </div>
                                  </div>
                                </div>
                                <div class="row">
                                  <div class="col-lg-6">
                                    <div class="mb-3">
                                      <label>Hangar</label>
                                      <div v-if="level4[3].data != null">
                                        <input
                                          type="text"
                                          class="form-control form-control-solid"
                                          v-model="level4[3].data.hangar"
                                          readonly
                                        />
                                      </div>
                                      <div v-else>
                                        <input
                                          type="text"
                                          class="form-control form-control-solid"
                                          value = "-"
                                          readonly
                                        />
                                      </div>
                                    </div>
                                  </div>
                                  <div class="col-lg-6">
                                    <div class="mb-3">
                                      <label>Line Hangar Request</label>
                                      <div class="row">
                                        <div v-if="level4[3].data != null">
                                          <input
                                            type="text"
                                            class=" form-control form-control-solid"
                                            v-model="level4[3].data.line"
                                            readonly
                                          />
                                        </div>
                                        <div v-else>
                                          <input
                                            type="text"
                                            value = "-"
                                            class=" form-control form-control-solid"
                                            readonly
                                          />
                                        </div>
                                      </div>
                                    </div>
                                  </div>
                                </div>

                                <div
                                  class="text-center mt-5"
                                  v-if="
                                    role == 'TPR' || role == 'Administrator'
                                  "
                                >
                                  <form>
                                    <input
                                      type="hidden"
                                      v-model="upgrade"
                                      value="1"
                                    />
                                    <button
                                      type="button"
                                      class="btn btn-info btn-sm"
                                      @click="upgradeLevel()"
                                      v-if="
                                        sales_detail.status === 'Open' &&
                                        sales_detail.level == 4 &&
                                        sales_detail.upgrade == true
                                      "
                                      v-permission="['upgrade_level']"
                                    >
                                      Upgrade Level
                                    </button>
                                  </form>
                                </div>
                                <div
                                  class="text-center mt-5"
                                  v-if="role == 'AMS'"
                                >
                                  <form>
                                    <button
                                      type="button"
                                      class="btn btn-info btn-sm"
                                      data-bs-toggle="modal"
                                      data-bs-target="#notifyUpgrade"
                                      v-if="
                                        sales_detail.status === 'Open' &&
                                        sales_detail.level == 4 &&
                                        sales_detail.upgrade == true
                                      "
                                    >
                                      Request to Upgrade
                                    </button>
                                  </form>
                                </div>
                              </div>
                            </form>
                          </div>
                        </div>
                        <!--begin::Step 4-->

                        <!--begin::Step 3-->
                        <div v-else-if="sales_detail.level == 3">
                          <div
                            class="flex-column current"
                            data-kt-stepper-element="content"
                          >
                            <form>
                              <div class="row">

                                <!-- Attachment of Maintenance Proposal for Customer -->
                                <div class="col-lg-6 mt-3">
                                  <h3>
                                    Attachment of Maintenance Proposal for
                                    Customer
                                  </h3>
                                  <p class="text-danger">
                                    <small>* File size max 5MB</small>
                                  </p>
                                </div>
                                <div class="col-lg-6 mt-3 mb-20">
                                  <div
                                    class="position-relative"
                                    v-if="sales_detail"
                                  >
                                    <div
                                      class="position-absolute top-0 end-0"
                                      v-if="
                                        sales_detail.level == 3 &&
                                        sales_detail.status === 'Open'
                                      "
                                    >
                                      <button
                                        type="button"
                                        class="btn btn-success btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#notifyCOGS"
                                        v-if="
                                          role == 'TPR' ||
                                          role == 'Administrator'
                                        "
                                      >
                                        Notify COGS
                                      </button>
                                      <button
                                        type="button"
                                        class="btn btn-primary btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#addFile"
                                        @click="addFile4()"
                                        v-if="
                                          role == 'CBO' ||
                                          role == 'Administrator'
                                        "
                                        v-permission="['upload_files']"
                                      >
                                        Upload Document
                                      </button>
                                    </div>
                                  </div>
                                </div>
                                <div class="rounded box-d" id="myBorder">
                                  <div class="mt-3">
                                    <table class="table" v-if="files">
                                      <tr
                                        v-for="files in level3[1].data"
                                        :key="files.id"
                                      >
                                        <td>
                                          <a
                                            :href="files.full_path"
                                            class="
                                              btn
                                              btn-outline-primary
                                              btn-outline
                                              btn-sm
                                              mb-2
                                            "
                                            target="_blank"
                                          >
                                            <strong>{{
                                              files.file_name
                                            }}</strong>
                                          </a>
                                        </td>
                                        <td
                                          class="d-flex justify-content-end"
                                          v-if="
                                            sales_detail.level == 3 &&
                                            sales_detail.status === 'Open'
                                          "
                                        >
                                          <button
                                            type="button"
                                            class="btn btn-danger btn-sm"
                                            @click="removeFile(files.id)"
                                            v-permission="['delete_files']"
                                            v-if="
                                              role == 'CBO' ||
                                              role == 'Administrator'
                                            "
                                          >
                                            <span class="fas fa-trash"></span>
                                          </button>
                                        </td>
                                      </tr>
                                    </table>
                                  </div>
                                </div>

                                <!-- Attachment of Profitability Analysis Form Signed -->
                                <div class="col-lg-6 mt-3">
                                  <h3>
                                    Attachment of Profitability Analysis Form
                                    Signed
                                  </h3>
                                  <p class="text-danger">
                                    <small>* File size max 5MB</small>
                                  </p>
                                </div>
                                <div class="col-lg-6 mt-3 mb-20">
                                  <div
                                    class="position-relative"
                                    v-if="sales_detail"
                                  >
                                    <div
                                      class="position-absolute top-0 end-0"
                                      v-if="
                                        sales_detail.level == 3 &&
                                        sales_detail.status === 'Open'
                                      "
                                    >
                                      <button
                                        type="button"
                                        class="btn btn-primary btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#addFile"
                                        @click="addFile5()"
                                        v-if="
                                          role == 'AMS' ||
                                          role == 'Administrator'
                                        "
                                        v-permission="['upload_files']"
                                      >
                                        Upload Document
                                      </button>
                                    </div>
                                  </div>
                                </div>
                                <div class="rounded box-d" id="myBorder">
                                  <div class="mt-3">
                                    <table class="table" v-if="files">
                                      <tr
                                        v-for="files in level3[2].data"
                                        :key="files.id"
                                      >
                                        <td>
                                          <a
                                            :href="files.full_path"
                                            class="
                                              btn
                                              btn-outline-primary
                                              btn-outline
                                              btn-sm
                                              mb-2
                                            "
                                            target="_blank"
                                          >
                                            <strong>{{
                                              files.file_name
                                            }}</strong>
                                          </a>
                                        </td>
                                        <td
                                          class="d-flex justify-content-end"
                                          v-if="
                                            sales_detail.level == 3 &&
                                            sales_detail.status === 'Open'
                                          "
                                        >
                                          <button
                                            type="button"
                                            class="btn btn-danger btn-sm"
                                            @click="removeFile(files.id)"
                                            v-permission="['delete_files']"
                                            v-if="
                                              role == 'AMS' ||
                                              role == 'Administrator'
                                            "
                                          >
                                            <span class="fas fa-trash"></span>
                                          </button>
                                        </td>
                                      </tr>
                                    </table>
                                  </div>
                                </div>

                                <!-- Attachment of Financial Assesment Form (optional) -->
                                <div class="col-lg-6 mt-3">
                                  <h3>
                                    Attachment of Financial Assesment Form
                                    (optional)
                                  </h3>
                                  <p class="text-danger">
                                    <small>* File size max 5MB</small>
                                  </p>
                                </div>
                                <div class="col-lg-6 mt-3 mb-20">
                                  <div
                                    class="position-relative"
                                    v-if="sales_detail"
                                  >
                                    <div
                                      class="position-absolute top-0 end-0"
                                      v-if="
                                        sales_detail.level == 3 &&
                                        sales_detail.status === 'Open'
                                      "
                                    >
                                      <button
                                        type="button"
                                        class="btn btn-primary btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#addFile"
                                        @click="addFile3()"
                                        v-if="
                                          role == 'AMS' ||
                                          role == 'Administrator'
                                        "
                                        v-permission="['upload_files']"
                                      >
                                        Upload Document
                                      </button>
                                    </div>
                                  </div>
                                </div>
                                <div class="rounded box-d" id="myBorder">
                                  <div class="mt-3">
                                    <table class="table" v-if="files">
                                      <tr
                                        v-for="files in level3[0].data"
                                        :key="files.id"
                                      >
                                        <td>
                                          <a
                                            :href="files.full_path"
                                            class="
                                              btn
                                              btn-outline-primary
                                              btn-outline
                                              btn-sm
                                              mb-2
                                            "
                                            target="_blank"
                                          >
                                            <strong>{{
                                              files.file_name
                                            }}</strong>
                                          </a>
                                        </td>
                                        <td
                                          class="d-flex justify-content-end"
                                          v-if="
                                            sales_detail.level == 3 &&
                                            sales_detail.status === 'Open'
                                          "
                                        >
                                          <button
                                            type="button"
                                            class="btn btn-danger btn-sm"
                                            @click="removeFile(files.id)"
                                            v-permission="['delete_files']"
                                            v-if="
                                              role == 'AMS' ||
                                              role == 'Administrator'
                                            "
                                          >
                                            <span class="fas fa-trash"></span>
                                          </button>
                                        </td>
                                      </tr>
                                    </table>
                                  </div>
                                </div>

                                <div
                                  class="text-center mt-5"
                                  v-if="
                                    role == 'TPR' || role == 'Administrator'
                                  "
                                >
                                  <form>
                                    <input
                                      type="hidden"
                                      v-model="upgrade"
                                      value="1"
                                    />
                                    <button
                                      type="button"
                                      class="btn btn-info btn-sm"
                                      @click="upgradeLevel()"
                                      v-if="
                                        sales_detail.status === 'Open' &&
                                        sales_detail.level == 3 &&
                                        sales_detail.upgrade == true
                                      "
                                      v-permission="['upgrade_level']"
                                    >
                                      Upgrade Level
                                    </button>
                                  </form>
                                </div>
                                <div
                                  class="text-center mt-5"
                                  v-if="role == 'AMS'"
                                >
                                  <form>
                                    <button
                                      type="button"
                                      class="btn btn-info btn-sm"
                                      data-bs-toggle="modal"
                                      data-bs-target="#notifyUpgrade"
                                      v-if="
                                        sales_detail.status === 'Open' &&
                                        sales_detail.level == 3 &&
                                        sales_detail.upgrade == true
                                      "
                                    >
                                      Request to Upgrade
                                    </button>
                                  </form>
                                </div>
                              </div>
                            </form>
                          </div>
                        </div>
                        <!--begin::Step 3-->

                        <!--begin::Step 2-->
                        <div v-else-if="sales_detail.level == 2">
                          <div
                            class="flex-column current"
                            data-kt-stepper-element="content"
                          >
                            <form>
                              <div class="row">
                                <!-- Attachment of Customer Approval (SOW Signed / Proposal Approved) -->
                                <div class="col-lg-6 mt-3">
                                  <h3>
                                    Attachment of Customer Approval (SOW Signed
                                    / Proposal Approved)
                                  </h3>
                                  <p class="text-danger">
                                    <small>* File size max 5MB</small>
                                  </p>
                                </div>
                                <div class="col-lg-6 mt-3 mb-20">
                                  <div
                                    class="position-relative"
                                    v-if="sales_detail"
                                  >
                                    <div
                                      class="position-absolute top-0 end-0"
                                      v-if="
                                        sales_detail.level == 2 &&
                                        sales_detail.status === 'Open'
                                      "
                                    >
                                      <button
                                        type="button"
                                        class="btn btn-primary btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#addFile"
                                        @click="addFile6()"
                                        v-if="
                                          role == 'AMS' ||
                                          role == 'Administrator'
                                        "
                                        v-permission="['upload_files']"
                                      >
                                        Upload Document
                                      </button>
                                    </div>
                                  </div>
                                </div>
                                <div class="rounded box-d" id="myBorder">
                                  <div class="mt-3">
                                    <table class="table" v-if="files">
                                      <tr
                                        v-for="files in level2[0].data"
                                        :key="files.id"
                                      >
                                        <td>
                                          <a
                                            :href="files.full_path"
                                            class="
                                              btn
                                              btn-outline-primary
                                              btn-outline
                                              btn-sm
                                              mb-2
                                            "
                                            target="_blank"
                                          >
                                            <strong>{{
                                              files.file_name
                                            }}</strong>
                                          </a>
                                        </td>
                                        <td
                                          class="d-flex justify-content-end"
                                          v-if="
                                            sales_detail.level == 2 &&
                                            sales_detail.status === 'Open'
                                          "
                                        >
                                          <button
                                            type="button"
                                            class="btn btn-danger btn-sm"
                                            @click="removeFile(files.id)"
                                            v-permission="['delete_files']"
                                            v-if="
                                              role == 'AMS' ||
                                              role == 'Administrator'
                                            "
                                          >
                                            <span class="fas fa-trash"></span>
                                          </button>
                                        </td>
                                      </tr>
                                    </table>
                                  </div>
                                </div>

                                <div
                                  class="text-center mt-5"
                                  v-if="
                                    role == 'TPR' || role == 'Administrator'
                                  "
                                >
                                  <form>
                                    <input
                                      type="hidden"
                                      v-model="upgrade"
                                      value="1"
                                    />
                                    <button
                                      type="button"
                                      class="btn btn-info btn-sm"
                                      @click="upgradeLevel()"
                                      v-if="
                                        sales_detail.status === 'Open' &&
                                        sales_detail.level == 2 &&
                                        sales_detail.upgrade == true
                                      "
                                      v-permission="['upgrade_level']"
                                    >
                                      Upgrade Level
                                    </button>
                                  </form>
                                </div>
                                <div
                                  class="text-center mt-5"
                                  v-if="role == 'AMS'"
                                >
                                  <form>
                                    <button
                                      type="button"
                                      class="btn btn-info btn-sm"
                                      data-bs-toggle="modal"
                                      data-bs-target="#notifyUpgrade"
                                      v-if="
                                        sales_detail.status === 'Open' &&
                                        sales_detail.level == 2 &&
                                        sales_detail.upgrade == true
                                      "
                                    >
                                      Request to Upgrade
                                    </button>
                                  </form>
                                </div>
                              </div>
                            </form>
                          </div>
                        </div>
                        <!--begin::Step 2-->

                        <!--begin::Step 1-->
                        <div v-else-if="sales_detail.level == 1">
                          <div
                            class="flex-column current"
                            data-kt-stepper-element="content"
                          >
                              <div class="row">
                                <!-- Attachment of WO/PO number customer document -->
                                <div class="col-lg-6 mt-3">
                                  <h3>
                                    Attachment of WO/PO number customer document
                                  </h3>
                                  <p class="text-muted">
                                    <small
                                      >by <a href="#">{{ user }}</a></small
                                    >
                                  </p>
                                </div>
                                <div class="col-lg-6 mt-3 mb-20">
                                  <div
                                    class="position-relative"
                                    v-if="sales_detail"
                                  >
                                    <div
                                      class="position-absolute top-0 end-0"
                                      v-if="
                                        sales_detail.level == 1 &&
                                        sales_detail.status === 'Open' || sales_detail.status === 'Closed'
                                      "
                                    >
                                      <input
                                        type="hidden"
                                        v-model="status"
                                        value="2"
                                      />
                                      <button
                                        type="button"
                                        class="btn btn-primary btn-sm"
                                        data-bs-toggle="modal"
                                        data-bs-target="#addFile"
                                        @click="addFile7()"
                                        v-if="
                                          role == 'AMS' ||
                                          role == 'Administrator'
                                        "
                                        v-permission="['upload_files']"
                                      >
                                        Upload Document
                                      </button>
                                    </div>
                                  </div>
                                </div>
                                <div class="rounded box-d" id="myBorder">
                                  <div class="mt-3">
                                    <table class="table" v-if="files">
                                      <tr
                                        v-for="files in level1[0].data"
                                        :key="files.id"
                                      >
                                        <td>
                                          <a
                                            :href="files.full_path"
                                            class="
                                              btn
                                              btn-outline-primary
                                              btn-outline
                                              btn-sm
                                              mb-2
                                            "
                                            target="_blank"
                                          >
                                            <strong>{{
                                              files.file_name
                                            }}</strong>
                                          </a>
                                        </td>
                                        <td
                                          class="d-flex justify-content-end"
                                          v-if="
                                            sales_detail.level == 1 &&
                                            sales_detail.status === 'Closed'
                                          "
                                        >
                                          <button
                                            type="button"
                                            class="btn btn-danger btn-sm"
                                            @click="removeFile(files.id)"
                                            v-permission="['delete_files']"
                                            v-if="
                                              role == 'AMS' ||
                                              role == 'Administrator'
                                            "
                                          >
                                            <span class="fas fa-trash"></span>
                                          </button>
                                        </td>
                                      </tr>
                                    </table>
                                  </div>
                                </div>

                                <!-- Input SO Number -->
                                <div class="col-lg-6 mt-5">
                                  <h3>Input SO Number</h3>
                                </div>
                                  <div class="row">
                                    <div
                                      class="input-group mb-3"
                                    >
                                      <input
                                        type="text"
                                        class="form-control"
                                        id="readOnly"
                                        v-if="
                                          level1[0].data == ''
                                        "
                                        v-model="level1[1].data"
                                        readonly
                                      />
                                      <input
                                        type="text"
                                        class="form-control"
                                        v-else
                                        v-model="level1[1].data"
                                        :class="{
                                          'is-invalid': errors.so_number,
                                        }"
                                      />
                                      <button
                                        class="btn btn-sm"
                                        type="button"
                                        id="textSync"
                                        v-if="
                                          sales_detail.status === 'Closed' &&
                                          level1[0].data != '' &&
                                          role == 'Administrator' || role == 'CBO'
                                        "
                                        @click="updateSO()"
                                        v-permission="['input_so_number']"
                                      >
                                        Submit
                                      </button>
                                      <span
                                        v-if="errors.so_number"
                                        class="error invalid-feedback"
                                        >{{ errors.so_number[0] }}</span
                                      >
                                    </div>
                                  </div>
                              </div>
                          </div>
                        </div>
                        <!--begin::Step 1-->
                      </div>
                      <!--end::Group-->
                    </div>
                    <!--end::Form-->
                  </div>
                  <!--end::Stepper-->
                </div>

                <!-- Tab History -->
                <div
                  class="tab-pane fade"
                  id="history-tab-pane"
                  role="tabpanel"
                  aria-labelledby="history-tab"
                  tabindex="0"
                >
                  <div class="mt-5">
                    <!-- Filter -->
                    <div class="row">
                      <div class="col-lg-8"></div>
                      <div
                        class="
                          col-lg-4 col-sm-12
                          d-flex
                          justify-content-end
                          align-items-center
                        "
                      >
                        <select class="form-select" v-model="filter">
                          <option :value="null" disabled>Select Month</option>
                          <option value="1">January</option>
                          <option value="2">February</option>
                          <option value="3">March</option>
                          <option value="4">April</option>
                          <option value="5">May</option>
                          <option value="6">June</option>
                          <option value="7">July</option>
                          <option value="8">August</option>
                          <option value="9">September</option>
                          <option value="10">October</option>
                          <option value="11">November</option>
                          <option value="12">December</option>
                        </select>
                        <button
                          type="button"
                          class="btn btn-info btn-sm ms-3"
                          @click="
                            listFileHistory()
                            clearFormHistory()
                          "
                        >
                          Filter
                        </button>
                      </div>
                    </div>

                    <div v-for="(file_history, file_index) in file_histories" :key="file_index">
                      <div class="row">
                        <div class="col-lg-6 col-sm-12" v-if="file_history">
                          <h3 class="mt-3">
                            <span class="fas fa-calendar-days"></span>
                            {{ file_history.uploadedAt }}
                          </h3>
                        </div>
                      </div>

                      <!-- Isi -->
                      <div class="row mt-4" v-if="file_history">
                        <h3>{{ file_history.totalFiles }} File Uploaded</h3>
                        <p class="text-muted">
                          <small
                            >by <a href="#">{{ user }}</a></small
                          >
                        </p>
                        <div class="rounded box-d mb-5" id="myBorder">
                          <div class="mt-3">
                            <table class="table">
                              <tr
                                v-for="file in file_history.files"
                                :key="file.id"
                              >
                                <td>
                                  <form>
                                    <a
                                      :href="file.full_path"
                                      class="
                                        btn
                                        btn-outline-primary
                                        btn-outline
                                        btn-sm
                                      "
                                      target="_blank"
                                    >
                                      <strong>{{ file.file_name }}</strong>
                                    </a>
                                  </form>
                                </td>
                              </tr>
                            </table>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Tab Contact -->
                <div
                  class="tab-pane fade"
                  id="contact-tab-pane"
                  role="tabpanel"
                  aria-labelledby="contact-tab"
                  tabindex="0"
                >
                  <div class="mt-5" v-if="sales_detail">
                    <div class="table-responsive">
                      <table
                        class="table table-row-bordered table-row-gray-200 gy-4"
                        v-if="contact"
                      >
                        <thead>
                          <tr class="fw-bold fs-6 text-gray-800">
                            <th class="text-center">No</th>
                            <th class="text-center">Name</th>
                            <th class="text-center">Phone</th>
                            <th class="text-center">Email</th>
                            <th class="text-center">Title</th>
                            <th
                              class="text-center"
                              v-if="
                                role == 'AMS' ||
                                role == 'Administrator' ||
                                role == 'TPR'
                              "
                            >
                              Action
                            </th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr
                            v-for="(contact, contact_index) in level4[0].data"
                            @dblclick="getItem(contact_index)"
                            :key="contact_index"
                          >
                            <td class="text-center">
                              {{ contact_index + 1 }}
                            </td>
                            <td>
                              {{ contact.name }}
                            </td>
                            <td>
                              {{ contact.phone }}
                            </td>
                            <td>
                              {{ contact.email }}
                            </td>
                            <td>
                              {{ contact.title }}
                            </td>
                            <td
                              class="d-flex justify-content-center"
                              v-if="
                                role == 'AMS' ||
                                role == 'Administrator' ||
                                role == 'TPR'
                              "
                            >
                              <button
                                class="btn btn-sm btn-light"
                                @click="removeContact(contact.id)"
                                v-permission="['delete_contacts']"
                              >
                                <i class="bi bi-trash-fill text-primary"></i>
                              </button>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </div>

                    <div
                      class="text-center mt-20"
                      v-if="sales_detail.status === 'Open'"
                    >
                      <button
                        type="button"
                        class="btn btn-primary"
                        data-bs-toggle="modal"
                        v-permission="['create_contacts']"
                        data-bs-target="#addContact"
                        @click="addContact()"
                      >
                        Add Contact Person
                      </button>
                    </div>
                  </div>
                </div>

                <!-- Tab Reschedule -->
                <div
                  class="tab-pane fade"
                  id="reschedule-tab-pane"
                  role="tabpanel"
                  aria-labelledby="reschedule-tab"
                  tabindex="0"
                >
                  <div class="mt-5" v-if="sales_detail">
                      <form>
                        <input
                          type="hidden"
                          disabled
                          class="form-control"
                          v-model="current_date_reschedule"
                        />
                        <input
                          type="hidden"
                          class="form-control"
                          v-model="sales_detail.monthSales"
                        />
                        <input
                          type="hidden"
                          class="form-control"
                          v-model="sales_detail.acReg"
                          readonly
                          id="readOnly"
                        />
                        <div class="mb-3">
                          <label>To </label>
                          <select v-model="user_id" class="form-select" :class="{ 'is-invalid': errors.user_id }">
                            <option :value="null" disabled>
                              Select User
                            </option>
                            <option
                              v-for="(user_options, user_index) in user_option"
                              v-if="user_options.role_id === 4"
                              :value="user_options.id"
                              :key="user_index"
                            >
                              {{ user_options.name }} -
                              {{ user_options.email }}
                            </option>
                          </select>
                          <span
                            v-if="errors.user_id"
                            class="error invalid-feedback"
                            >{{ errors.user_id[0] }}</span
                          >
                        </div>
                        
                        <!-- Hangar & Line -->
                        <div class="row">
                          <div class="col-lg-6">
                            <div class="mb-3">
                              <label>Hangar</label>
                              <select v-model="hangar_id" class="form-select" :class="{ 'is-invalid': errors.hangar_id }">
                                <option :value="null" disabled>
                                  Select Hangar
                                </option>
                                <option
                                  v-for="(hangar_options, hangar_index) in hangar_option"
                                  :value="hangar_options.id"
                                  :key="hangar_index"
                                >
                                  {{ hangar_options.name }}
                                </option>
                              </select>
                              <span
                                v-if="errors.hangar_id"
                                class="error invalid-feedback"
                                >{{ errors.hangar_id[0] }}</span
                              >
                            </div>
                          </div>
                          <div class="col-lg-6">
                            <div class="mb-3">
                              <label>Line</label>
                              <select v-model="line_id" class="form-select" :class="{ 'is-invalid': errors.line_id }">
                                <option :value="null" disabled>
                                  Select Line
                                </option>
                                <option
                                  v-for="(lines, line_index) in line"
                                  v-if="lines.hangar_id === hangar_id"
                                  :value="lines.id"
                                  :key="line_index"
                                >
                                  {{ lines.name }}
                                </option>
                              </select>
                              <span
                                v-if="errors.line_id"
                                class="error invalid-feedback"
                                >{{ errors.line_id[0] }}</span
                              >
                            </div>
                          </div>
                        </div>

                        <!-- Start Date & TAT -->
                        <div class="row">
                          <div class="col-lg-6">
                            <div class="mb-3">
                              <label class="form-label">Start Date</label>
                              <input
                                type="text"
                                class="form-control"
                                v-model="sales_detail.startDate"
                                readonly
                                id="readOnly"
                              />
                            </div>
                          </div>
                          <div class="col-lg-6">
                            <div class="mb-3">
                              <label class="form-label">TAT</label>
                              <input
                                type="number"
                                class="form-control"
                                v-model="tat"
                              />
                            </div>
                          </div>
                        </div>
                          
                        <!-- Reschedule -->
                        <div class="row">
                          <div class="col-lg-6">
                            <div class="mb-3">
                              <label class="form-label">Reschedule</label>
                              <input
                                type="date"
                                class="form-control"
                                v-model="reschedule"
                                :class="{
                                  'is-invalid': errors.reschedule,
                                }"
                              />
                              <span
                                v-if="errors.reschedule"
                                class="error invalid-feedback"
                                >{{ errors.reschedule[0] }}</span
                              >
                            </div>
                          </div>
                        </div>

                        <div
                          class="text-center mt-5"
                          v-if="sales_detail.status === 'Open'"
                        >
                          <button
                            type="button"
                            @click="salesRescheduleReject()"
                            class="btn btn-danger btn-sm"
                            v-if="
                              role == 'CBO' || role == 'Administrator'
                            "
                            >
                            Reject
                            </button>
                            <button
                              type="button"
                              class="btn btn-success btn-sm mx-2"
                              @click="salesRescheduleApprove()"
                              v-if="
                                role == 'CBO' || role == 'Administrator'
                              "
                            >
                              Approve
                            </button>
                            <button
                              type="button"
                              class="btn btn-info btn-sm"
                              @click="salesReschedule()"
                              v-permission="['reschedule_sales']"
                              v-if="
                                role == 'AMS' || role == 'Administrator'
                              "
                            >
                            Request to CBO
                          </button>
                        </div>
                      </form>
                  </div>
                </div>

                <!-- Cancel Form -->
                <div
                  class="tab-pane fade"
                  id="cancel-tab-pane"
                  role="tabpanel"
                >
                  <form>
                    <div class="mb-3 mt-5">
                      <label>To </label>
                      <select v-model="user_id" class="form-select" :class="{ 'is-invalid': errors.user_id }">
                        <option :value="null" disabled>
                          Select User
                        </option>
                        <option
                          v-for="(user_options, user_index) in user_option"
                          v-if="user_options.role_id === 4"
                          :value="user_options.id"
                          :key="user_index"
                        >
                          {{ user_options.name }} -
                          {{ user_options.email }}
                        </option>
                      </select>
                      <span
                        v-if="errors.user_id"
                        class="error invalid-feedback"
                        >{{ errors.user_id[0] }}</span
                      >
                    </div>
                    <div class="mb-3">
                      <label class="form-label">Category</label>
                      <div class="row mb-5">
                        <div class="col">
                          <div class="input-group mb-3">
                            <select v-model="category_id" class="form-select" :class="{ 'is-invalid': errors.category_id }">
                              <option :value="null" disabled>Select Category</option>
                              <option
                                v-for="(category_options, category_index) in category_option"
                                :value="category_options.id"
                                :class="{
                                  'is-invalid': errors.category_id,
                                }"
                                :key="category_index"
                              >
                                {{ category_options.name }}
                              </option>
                            </select>
                            <span
                              v-if="errors.category_id"
                              class="error invalid-feedback"
                            >
                              {{ errors.category_id[0] }}
                            </span>
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="mb-3">
                      <label class="form-label">Reason of Cancel</label>
                      <textarea
                        class="form-control"
                        cols="30"
                        rows="10"
                        v-model="reason"
                        :class="{ 'is-invalid': errors.reason }"
                      ></textarea>
                      <span
                        v-if="errors.reason"
                        class="error invalid-feedback"
                      >
                        {{ errors.reason[0] }}
                      </span>
                    </div>
                    <div
                      class="text-center mt-5"
                      v-if="sales_detail_status == 'Open'"
                    >
                    <button
                      type="button"
                      @click="salesCancelReject()"
                      class="btn btn-danger btn-sm"
                      v-if="
                        role == 'CBO' || role == 'Administrator'
                      "
                    >
                    Reject
                    </button>
                    <button
                      type="button"
                      class="btn btn-success btn-sm mx-2"
                      @click="salesCancelApprove()"
                      v-if="
                        role == 'CBO' || role == 'Administrator'
                      "
                    >
                      Approve
                    </button>
                      <button
                        type="button"
                        class="btn btn-info btn-sm"
                        @click="salesCancel()"
                        v-permission="['reject_sales']"
                        v-if="
                          role == 'AMS' || role == 'Administrator'
                        "
                      >
                        Request to CBO
                      </button>
                    </div>
                  </form>
                </div>

                <!-- Modal Contact -->
                <div
                  class="modal fade"
                  tabindex="-1"
                  id="addContact"
                  data-bs-backdrop="static"
                >
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 v-if="modal_contact" class="modal-title">
                          Add Contact Person
                        </h3>
                        <h3 v-else class="modal-title">Edit Contact Person</h3>

                        <!--begin::Close-->
                        <div
                          class="
                            btn btn-icon btn-sm btn-active-light-primary
                            ms-2
                          "
                          data-bs-dismiss="modal"
                          aria-label="Close"
                        >
                          <span
                            class="svg-icon svg-icon-1"
                            @click="closeModalContact()"
                          >
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
                        <form @submit.prevent="submitContact">
                          <input
                            type="hidden"
                            v-if="sales_detail"
                            v-model="sales_detail.id"
                          />
                          <div class="row">
                            <div class="form-group mb-3">
                              <label class="form-label fw-bold">Name</label>
                              <input
                                type="text"
                                class="form-control"
                                v-model="p_contact.name"
                                :class="{
                                  'is-invalid': errors.name,
                                }"
                              />
                              <span
                                v-if="errors.name"
                                class="error invalid-feedback"
                                >{{ errors.name[0] }}</span
                              >
                            </div>
                            <div class="form-group mb-3">
                              <label class="form-label fw-bold">Phone</label>
                              <input
                                type="number"
                                class="form-control"
                                v-model="p_contact.phone"
                                :class="{
                                  'is-invalid': errors.phone,
                                }"
                              />
                              <span
                                v-if="errors.phone"
                                class="error invalid-feedback"
                                >{{ errors.phone[0] }}</span
                              >
                            </div>
                            <div class="form-group mb-3">
                              <label class="form-label fw-bold">Email</label>
                              <input
                                type="email"
                                class="form-control"
                                v-model="p_contact.email"
                                :class="{
                                  'is-invalid': errors.email,
                                }"
                              />
                              <span
                                v-if="errors.email"
                                class="error invalid-feedback"
                                >{{ errors.email[0] }}</span
                              >
                            </div>
                            <div class="form-group mb-3">
                              <label class="form-label fw-bold">Address</label>
                              <input
                                type="text"
                                class="form-control"
                                v-model="p_contact.address"
                                :class="{
                                  'is-invalid': errors.address,
                                }"
                              />
                              <span
                                v-if="errors.address"
                                class="error invalid-feedback"
                                >{{ errors.address[0] }}</span
                              >
                            </div>
                            <div class="form-group mb-3">
                              <label class="form-label fw-bold">Title</label>
                              <input
                                type="text"
                                class="form-control"
                                v-model="p_contact.title"
                                :class="{
                                  'is-invalid': errors.title,
                                }"
                              />
                              <span
                                v-if="errors.title"
                                class="error invalid-feedback"
                                >{{ errors.title[0] }}</span
                              >
                            </div>
                          </div>
                          <div class="row mt-10">
                            <div class="col d-flex justify-content-end">
                              <button
                                type="button"
                                class="btn btn-light mx-2"
                                data-bs-dismiss="modal"
                                id="close_modal_contact"
                                @click="closeModalContact()"
                              >
                                Close
                              </button>
                              <button
                                type="submit"
                                class="btn btn-primary"
                                v-permission="['create_contacts']"
                              >
                                Save
                              </button>
                            </div>
                          </div>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Modal Upload -->
                <div
                  class="modal fade"
                  tabindex="-1"
                  id="addFile"
                  data-bs-backdrop="static"
                >
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 v-if="modal_upload == 1" class="modal-title">
                          Upload Attachment RFQ or Email Request
                        </h3>
                        <h3 v-if="modal_upload == 2" class="modal-title">
                          Upload Attachment Workscope
                        </h3>
                        <h3 v-if="modal_upload == 3" class="modal-title">
                          Attachment of Financial Assesment Form (optional)
                        </h3>
                        <h3 v-if="modal_upload == 4" class="modal-title">
                          Attachment of Maintenance Proposal for Customer
                        </h3>
                        <h3 v-if="modal_upload == 5" class="modal-title">
                          Attachment of Profitability Analysis Form Signed
                        </h3>
                        <h3 v-if="modal_upload == 6" class="modal-title">
                          Attachment of Customer Approval (SOW Signed / Proposal
                          Approved)
                        </h3>
                        <h3 v-if="modal_upload == 7" class="modal-title">
                          Attachment of WO/PO number customer document
                        </h3>

                        <!--begin::Close-->
                        <div
                          class="
                            btn btn-icon btn-sm btn-active-light-primary
                            ms-2
                          "
                          data-bs-dismiss="modal"
                          aria-label="Close"
                        >
                          <span
                            class="svg-icon svg-icon-1"
                            @click="closeModalFile()"
                          >
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
                        <form>
                          <div class="form-group mb-3">
                            <input
                              type="file"
                              @change="attachFile()"
                              id="files"
                              ref="files"
                              class="form-control"
                              multiple
                              :class="{
                                'is-invalid': errors.files,
                              }"
                            />
                            <div
                              v-for="(file_error, key) in file_errors"
                              :key="key"
                            >
                              <ul class="list-group mt-3">
                                <li
                                  class="list-group-item text-danger border-0"
                                  v-for="(errorItem, innerKey) in file_error"
                                  :key="innerKey"
                                >
                                  {{ errorItem }}
                                </li>
                              </ul>
                            </div>
                          </div>
                          <div class="row mt-10">
                            <div class="col d-flex justify-content-end">
                              <button
                                type="button"
                                class="btn btn-light mx-2"
                                data-bs-dismiss="modal"
                                id="close_modal_file"
                                @click="closeModalFile()"
                              >
                                Close
                              </button>
                              <button
                                type="button"
                                @click="submitFile()"
                                v-permission="['upload_files']"
                                class="btn btn-primary"
                              >
                                Save
                              </button>
                            </div>
                          </div>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Modal slotRequest -->
                <div
                  class="modal fade"
                  tabindex="-1"
                  id="slotRequest"
                  data-bs-backdrop="static"
                >
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 class="modal-title">Request Hangar Slot to CBO</h3>
                        <!--begin::Close-->
                        <div
                          class="
                            btn btn-icon btn-sm btn-active-light-primary
                            ms-2
                          "
                          data-bs-dismiss="modal"
                          aria-label="Close"
                        >
                          <span
                            class="svg-icon svg-icon-1"
                            @click="closeRequestSlot()"
                          >
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
                        <form v-if="sales_detail">
                          <div class="mb-3">
                            <label>To <span class="text-danger">*</span></label>
                            <select v-model="user_id" class="form-select" :class="{ 'is-invalid': errors.user_id }">
                              <option :value="null" disabled>
                                Select User
                              </option>
                              <option
                                v-for="(user_options, user_index) in user_option"
                                v-if="user_options.role_id === 4"
                                :value="user_options.id"
                                :key="user_index"
                              >
                                {{ user_options.name }} -
                                {{ user_options.email }}
                              </option>
                            </select>
                            <span
                              v-if="errors.user_id"
                              class="error invalid-feedback"
                              >{{ errors.user_id[0] }}</span
                            >
                          </div>
                          <div class="mb-3">
                            <label
                              >Hangar <span class="text-danger">*</span></label
                            >
                            <select v-model="hangar_id" class="form-select" :class="{ 'is-invalid': errors.hangar_id }">
                              <option :value="null" disabled>
                                Select Hangar
                              </option>
                              <option
                                v-for="(hangar_options, hangar_index) in hangar_option"
                                :value="hangar_options.id"
                                :key="hangar_index"
                              >
                                {{ hangar_options.name }}
                              </option>
                            </select>
                            <span
                              v-if="errors.hangar_id"
                              class="error invalid-feedback"
                              >{{ errors.hangar_id[0] }}</span
                            >
                          </div>
                          <div class="form-group mb-3">
                            <label for=""
                              >Line <span class="text-danger">*</span></label
                            >
                            <select v-model="line_id" class="form-select" :class="{ 'is-invalid': errors.line_id }">
                              <option :value="null" disabled>
                                Select Line
                              </option>
                              <option
                                v-for="(lines, line_index) in line"
                                v-if="lines.hangar_id === hangar_id"
                                :value="lines.id"
                                :key="line_index"
                              >
                                {{ lines.name }}
                              </option>
                            </select>
                            <span
                              v-if="errors.line_id"
                              class="error invalid-feedback"
                              >{{ errors.line_id[0] }}</span
                            >
                          </div>
                          <div class="row mt-10">
                            <div class="col d-flex justify-content-end">
                              <button
                                type="button"
                                class="btn btn-danger btn-sm mx-2"
                                data-bs-dismiss="modal"
                                id="close_modal_slot"
                                @click="closeRequestSlot()"
                              >
                                Discard
                              </button>
                              <button
                                type="button"
                                @click="slotRequest()"
                                class="btn btn-primary btn-sm"
                              >
                                Send
                              </button>
                            </div>
                          </div>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Modal notifyUpgrade -->
                <div
                  class="modal fade"
                  tabindex="-1"
                  id="notifyUpgrade"
                  data-bs-backdrop="static"
                >
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 class="modal-title">Notify Request to Upgrade</h3>
                        <!--begin::Close-->
                        <div
                          class="
                            btn btn-icon btn-sm btn-active-light-primary
                            ms-2
                          "
                          data-bs-dismiss="modal"
                          aria-label="Close"
                        >
                          <span
                            class="svg-icon svg-icon-1"
                            @click="closeNotifyLevel()"
                          >
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
                        <form>
                          <div class="mb-3">
                            <label>To <span class="text-danger">*</span></label>
                            <select
                              v-model="user_id"
                              class="form-select"
                              :class="{ 'is-invalid': errors.user_id }"
                            >
                              <option :value="null" disabled>
                                Select User
                              </option>
                              <option
                                v-for="(user_options, user_index) in user_option"
                                v-if="user_options.role_id === 3"
                                :value="user_options.id"
                                :key="user_index"
                              >
                                {{ user_options.name }} -
                                {{ user_options.email }}
                              </option>
                            </select>
                            <span
                              v-if="errors.user_id"
                              class="error invalid-feedback"
                              >{{ errors.user_id[0] }}</span
                            >
                            <small class="text-muted"
                              >Send notification to selected employee</small
                            >
                          </div>
                          <div class="row mt-10">
                            <div class="col d-flex justify-content-end">
                              <button
                                type="button"
                                class="btn btn-danger btn-sm mx-2"
                                data-bs-dismiss="modal"
                                id="close_modal_notify"
                                @click="closeNotifyLevel()"
                              >
                                Discard
                              </button>
                              <button
                                type="button"
                                @click="notifyUpgrade()"
                                class="btn btn-primary btn-sm"
                              >
                                Send
                              </button>
                            </div>
                          </div>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Modal notifyCOGS -->
                <div
                  class="modal fade"
                  tabindex="-1"
                  id="notifyCOGS"
                  data-bs-backdrop="static"
                >
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 class="modal-title">Notify to COGS</h3>
                        <!--begin::Close-->
                        <div
                          class="
                            btn btn-icon btn-sm btn-active-light-primary
                            ms-2
                          "
                          data-bs-dismiss="modal"
                          aria-label="Close"
                        >
                          <span
                            class="svg-icon svg-icon-1"
                            @click="closeNotifyCOGS()"
                          >
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
                        <form v-if="sales_detail">
                          <div class="mb-3">
                            <label>To <span class="text-danger">*</span></label>
                            <select v-model="user_id" class="form-select">
                              <option :value="null" disabled>
                                Select User
                              </option>
                              <option
                                v-for="(user_options, user_index) in user_option"
                                v-if="user_options.role_id === 4"
                                :value="user_options.id"
                                :key="user_index"
                              >
                                {{ user_options.name }} -
                                {{ user_options.email }}
                              </option>
                            </select>
                            <small class="text-muted"
                              >Send notification to selected employee</small
                            >
                          </div>
                          <div class="row mt-10">
                            <div class="col d-flex justify-content-end">
                              <button
                                type="button"
                                class="btn btn-danger btn-sm mx-2"
                                data-bs-dismiss="modal"
                                id="close_modal_cogs"
                                @click="closeNotifyCOGS()"
                              >
                                Discard
                              </button>
                              <button
                                type="button"
                                @click="notifyCOGS()"
                                class="btn btn-primary btn-sm"
                              >
                                Send
                              </button>
                            </div>
                          </div>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <!-- End Tab -->
          </div>
        </div>
      </div>
      <!-- End Detail -->
    </div>
    <!-- End Content -->
  </div>
</template>
<script>
import debounce from 'lodash/debounce'
export default {
  layout: 'template',
  name: 'MySalesPlanDetailPage',
  data() {
    return {
      user: this.$auth.user.name,
      role: this.$auth.user.role.name,
      sales: {
        data: [],
        link: [],
      },
      p_contact: {
        id: null,
        name: null,
        phone: null,
        email: null,
        address: null,
        title: null,
        status: null,
      },
      initial: null,
      search: null,
      so_number: null,
      type: null,
      order: 'id',
      by: 'desc',
      paginate: '10',
      files: [],
      ams: null,
      value: [],
      hangar_id: null,
      upgrade: null,
      maintenance_id: null,
      line_id: null,
      end_date: null,
      current_date: null,
      maintenance_option: [],
      hangar_option: [],
      line: null,
      status: null,
      contact_person: [],
      user_option: null,
      modal_contact: false,
      modal_upload: null,
      current_page: null,
      sales_detail: null,
      user_id: null,
      contact: null,
      requirement_id: null,
      sales_id: null,
      files: '',
      filter: null,
      contacts: null,
      level4: null,
      level3: null,
      level2: null,
      level1: null,
      ams_id: null,
      category: null,
      category_option: null,
      category_id: null,
      reason: null,
      file_histories: [],
      file_errors: [],
      flight_hour: null,
      tat: null,
      reschedule: null,
      errors: {
        ams_id: null,
        name: null,
        phone: null,
        email: null,
        address: null,
        title: null,
        hangar_id: null,
        line_id: null,
        status: null,
        files: null,
        so_number: null,
        maintenance_id: null,
        ac_reg: null,
        tat: null,
        location: null,
        value: null,
        category: null,
        reason: null,
        user_id: null,
        category_id: null,
        start_date: null,
      },
      sales_detail_status: null,
      current_date_reschedule: null,
      transactionType: null,
      data_pbth_rate: null,
      data_pbth_flighthour: null,
      prospect_id: null,
    }
  },
  mounted() {
    KTStepper.getInstance()
    KTFormRepeaterBasic.init()
    // this.step()
  },
  watch: {
    search: debounce(function () {
      this.listDetail()
      this.listContact()
      this.listFile()
      this.listFileHistory()
    }, 500),
  },
  created() {
    this.listDetail()
    this.listContact()
    this.listFile()
    this.listFileHistory()
    this.listAMS()
    this.listHangar()
    this.listLine()
    this.listMaintenance()
    this.listUser()
    this.listCategory()
  },
  methods: {
    directPage: debounce(function () {
      if (this.current_page < 1) {
        this.current_page = 1
      } else if (this.current_page > this.contact.last_page) {
        this.current_page = this.contact.last_page
      }
      let url = new URL(this.contact.first_page_url)
      let search_params = url.searchParams
      search_params.set('page', this.current_page)
      url.search = search_params.toString()
      let new_url = url.toString()
      this.listContact(new_url)
    }, 500),
    formatPrice(value) {
      let val = (value / 1).toFixed(0).replace(',', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
    },
    step() {
      var element = document.querySelector('#kt_stepper_example_basic')
      var stepper = new KTStepper(element)
      stepper.on('kt.stepper.next', function (stepper) {
        stepper.goNext()
      })
      stepper.on('kt.stepper.previous', function (stepper) {
        stepper.goPrevious()
      })
    },
    attachFile() {
      this.files = this.$refs.files.files
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
    loading2() {
      Swal.fire({
        timer: 5000,
        didOpen: () => {
          Swal.showLoading()
        },
        background: 'transparent',
        allowOutsideClick: false,
      })
    },
    listDetail() {
      this.loading2()
      this.$axios
        .get(`api/sales-show/${this.$route.query.id}`)
        .then((response) => {
          this.sales_detail = response.data.data.salesDetail
          this.transactionType = response.data.data.salesDetail.type
          this.prospect_id = response.data.data.salesDetail.prospect_id
          this.current_date_reschedule = this.sales_detail.startDate
          this.sales_detail_status = this.sales_detail.status
          this.customer_name = response.data.data.salesDetail.customer.name
          this.level4 = response.data.data.level4
          this.level3 = response.data.data.level3
          this.level2 = response.data.data.level2
          this.level1 = response.data.data.level1
          this.listPBTH()
          Swal.close()
        })
        .catch((error) => {
          if (error.response.status == 404) {
            toastr.error(error.response.data.message)
            this.$router.push({
              name: 'my-salesplan-table',
            })
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
            this.$router.push({
              name: 'my-salesplan-table',
            })
          }
        })
    },
    listPBTH() {
      this.$axios
        .get(`api/prospect-pbth/` + this.prospect_id)
        .then((response) => {
          this.data_pbth_flighthour = response.data.data.prospect[0].flight_hour
          this.data_pbth_rate = response.data.data.prospect[0].rate
        })
    },
    listContact(paginate) {
      this.loading()
      paginate = paginate || `/api/contact-person`
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
          this.contact = response.data.data.data
          this.current_page = this.contact.current_page
          Swal.close()
        })
        .catch((error) => console.log(error))
    },
    listFile() {
      this.loading()
      this.$axios
        .get(`api/file`)
        .then((response) => {
          this.files = response.data.data
          Swal.close()
        })
        .catch((error) => console.log(error))
    },
    listFileHistory() {
      this.loading()
      this.$axios
        .get(`api/file-history/${this.$route.query.id}`, {
          params: {
            filter: this.filter,
          },
        })
        .then((response) => {
          this.file_histories = response.data.data.history
          Swal.close()
        })
        .catch((error) => console.log(error))
    },
    listAMS() {
      this.loading()
      this.$axios
        .get(`api/ams`)
        .then((response) => {
          this.ams = response.data.data.data
          Swal.close()
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
    },
    listLine() {
      this.loading()
      this.$axios
        .get(`api/line`)
        .then((response) => {
          this.line = response.data.data
          Swal.close()
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
    listUser() {
      this.loading()
      this.$axios
        .get(`api/users`)
        .then((response) => {
          this.user_option = response.data.data.data
          Swal.close()
        })
        .catch((error) => console.log(error))
    },
    listCategory() {
      this.loading()
      this.$axios
        .get(`api/cancel-category`)
        .then((response) => {
          this.category_option = response.data.data
          Swal.close()
        })
        .catch((error) => console.log(error))
    },

    swtichAMS() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, switch sales!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-switch-ams/${this.$route.query.id}`, {
                ams_id: this.ams_id,
              })
              .then((response) => {
                this.closeModalAMS()
                toastr.success(response.data.message)
                this.$router.push({
                  name: 'my-salesplan',
                })
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    updateSO() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, Input SO Number!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`/api/sales-so-number/${this.$route.query.id}`, {
                sales_id: this.$route.query.id,
                so_number: this.level1[1].data,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
                // this.$router.push({
                //   name: 'my-salesplan',
                // })
              })
              .catch((error) => {
                if (error.response.status == 422) {
                  // Ini yang bikin error
                  // Minusnya ngga ada notif required kalo inputan SO Number kosong
                  // this.errors = error.response.data.errors
                  toastr.error(error.response.data.message)
                }
              })
          }
        })
    },
    slotRequest() {
      this.loading()
      this.$axios
        .post(`api/sales-request-hangar`, {
          sales_id: this.$route.query.id,
          hangar_id: this.hangar_id,
          line_id: this.line_id,
          user_id: this.user_id,
          target_url: this.$route.fullPath,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.listDetail()
          this.closeRequestSlot()
          Swal.close()
        })
        .catch((error) => {
          if (error.response.status == 422) {
            // this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    slotApprove() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, Approve it!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-approve-hangar/${this.$route.query.id}`, {
                is_approved: 1,
                target_url: this.$route.fullPath,
                // sales_id: this.$route.query.id,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
                Swal.close()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    slotReject() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, Reject it!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-approve-hangar/${this.$route.query.id}`, {
                is_approved: 0,
                target_url: this.$route.fullPath,
                // sales_id: this.$route.query.id,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
                Swal.close()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    salesUpdate() {
      this.loading()
      this.$axios
        .put(`/api/sales-update-tmb/${this.$route.query.id}`, {
          sales_id: this.$route.query.id,
          maintenance_id: this.maintenance_id,
          hangar_id: this.hangar_id,
          line_id: this.line_id,
          ac_reg: this.sales_detail.acReg,
          tat: this.sales_detail.tat,
          value: this.sales_detail.totalSales,
          start_date: this.sales_detail.startDate,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.listDetail()
          this.clearFormEditSales()
          this.closeModalEditSales()
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          }
        })
    },
    pbthUpdate() {
      this.loading()
      this.$axios
      .put(`/api/sales-update-pbth/` + this.prospect_id, {
          rate: this.data_pbth_rate,
          flight_hour: this.data_pbth_flighthour,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.closeModalEditSales()
          this.listPBTH()
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
          }
        })
    },
    salesReschedule() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, reschedule sales!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .post(`api/sales-request-reschedule`, {
                sales_id: this.$route.query.id,
                user_id: this.user_id,
                hangar_id: this.hangar_id,
                line_id: this.line_id,
                target_url: this.$route.fullPath,
                current_date: this.sales_detail.startDate,
                tat: this.tat,
                start_date: this.reschedule,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    salesRescheduleApprove() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, Approve it!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-approve-reschedule/${this.$route.query.id}`, {
                is_approved: 1,
                target_url: this.$route.fullPath,
                // sales_id: this.$route.query.id,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
                Swal.close()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    salesRescheduleReject() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, Reject it!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-request-reschedule`, {
                is_approved: 0,
                target_url: this.$route.fullPath,
                // sales_id: this.$route.query.id,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
                Swal.close()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    salesCancel() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, cancel sales!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .post(`api/sales-request-cancel`, {
                sales_id: this.$route.query.id,
                user_id: this.user_id,
                category_id: this.category_id,
                target_url: this.$route.fullPath,
                reason: this.reason,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.$router.push({
                  name: 'my-salesplan',
                })
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    salesCancelApprove() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, Approve it!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-approve-cancel/${this.$route.query.id}`, {
                is_approved: 1,
                target_url: this.$route.fullPath,
                // sales_id: this.$route.query.id,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
                Swal.close()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    salesCancelReject() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, Reject it!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-request-cancel`, {
                is_approved: 0,
                target_url: this.$route.fullPath,
                // sales_id: this.$route.query.id,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
                Swal.close()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    upgradeLevel() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, upgrade level!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-upgrade-level/${this.$route.query.id}`, {
                sales_id: this.$route.query.id,
                upgrade: this.upgrade,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    notifyCOGS() {
      this.loading()
      this.$axios
        .post(`api/sales-request-cogs`, {
          sales_id: this.$route.query.id,
          user_id: this.user_id,
          target_url: this.$route.fullPath,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.listDetail()
          this.closeNotifyCOGS()
        })
        .catch((error) => {
          if (error.response.status == 422) {
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    notifyUpgrade() {
      this.loading()
      this.$axios
        .post(`api/sales-request-upgrade`, {
          sales_id: this.$route.query.id,
          user_id: this.user_id,
          target_url: this.$route.fullPath,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.listDetail()
          this.closenotifyUpgrade()
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
    closeSales() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, closed it!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-upgrade-level/${this.$route.query.id}`, {
                status: this.status,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listDetail()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    requestClosed() {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'question',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, request to closed it!',
      })
        .then((result) => {
          if (result.isConfirmed) {
            this.$axios
              .put(`api/sales-close/${this.$route.query.id}`, {
                status: this.status,
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.$router.push({
                  name: 'my-salesplan',
                })
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },

    submitFile() {
      this.loading()
      let formData = new FormData()
      for (var i = 0; i < this.files.length; i++) {
        let file = this.files[i]
        formData.append('files[' + i + ']', file)
      }
      formData.append('sales_id', this.sales_detail.id)
      formData.append('requirement_id', this.sequence)
      this.$axios
        .post('/api/file-create', formData, {
          headers: {
            'Content-Type': 'multipart/form-data',
          },
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.listFile()
          this.listDetail()
          this.listFileHistory()
          this.closeModalFile()
          this.clearFormFile()
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.file_errors = error.response.data.errors
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    removeFile(id) {
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
            this.$axios.delete('/api/file-delete/' + id).then((response) => {
              toastr.success(response.data.message)
              this.listFile()
              this.listDetail()
              this.listFileHistory()
            })
          }
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    // Upload Attachment RFQ or Email Request
    addFile1() {
      this.sequence = 2
      this.modal_upload = 1
    },
    // Upload Attachment Workscope
    addFile2() {
      this.sequence = 3
      this.modal_upload = 2
    },
    // Attachment of Financial Assesment Form (optional)
    addFile3() {
      this.sequence = 5
      this.modal_upload = 3
    },
    // Attachment of Maintenance Proposal for Customer
    addFile4() {
      this.sequence = 6
      this.modal_upload = 4
    },
    // Attachment of Profitability Analysis Form Signed
    addFile5() {
      this.sequence = 7
      this.modal_upload = 5
    },
    // Attachment of Customer Approval (SOW Signed / Proposal Approved)
    addFile6() {
      this.sequence = 8
      this.modal_upload = 6
    },
    // Attachment of WO/PO number Customer Document
    addFile7() {
      this.sequence = 9
      this.modal_upload = 7
    },

    submitContact() {
      if (this.modal_contact) {
        this.createContact()
      } else {
        this.updateContact()
      }
    },
    addContact() {
      this.modal_contact = true
    },
    createContact() {
      this.loading()
      this.$axios
        .post('/api/contact-person-create', {
          id: this.p_contact.id,
          customer_id: this.sales_detail.customer.id,
          sales_id: this.sales_detail.id,
          name: this.p_contact.name,
          phone: this.p_contact.phone,
          email: this.p_contact.email,
          address: this.p_contact.address,
          title: this.p_contact.title,
          status: this.p_contact.status,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.listContact()
          this.listDetail()
          this.closeModalContact()
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors
            toastr.error(error.response.data.message)
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    removeContact(id) {
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
            this.$axios
              .delete('/api/contact-person-delete/' + id, {
                params: {
                  sales_id: this.sales_detail.id,
                },
              })
              .then((response) => {
                toastr.success(response.data.message)
                this.listContact()
                this.listDetail()
              })
          }
        })
        .catch((error) => {
          if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },

    closeModalFile() {
      document.getElementById('close_modal_file').click()
      this.listFile()
      this.listDetail()
      this.listFileHistory()
      this.clearFormFile()
    },
    clearFormFile() {
      this.files = null
      this.$refs.files.value = null
      this.errors.files = null
      this.file_errors = null
      this.errors.sales_detail = null
      this.errors.requirement_id = null
    },

    closeModalContact() {
      document.getElementById('close_modal_contact').click()
      this.clearFormContact()
    },
    clearFormContact() {
      this.p_contact.id = null
      this.p_contact.name = null
      this.p_contact.phone = null
      this.p_contact.email = null
      this.p_contact.address = null
      this.p_contact.title = null
      this.p_contact.status = null
      this.errors.name = null
      this.errors.phone = null
      this.errors.email = null
      this.errors.address = null
      this.errors.title = null
      this.errors.status = null
    },

    closeModalAMS() {
      document.getElementById('close_modal_ams').click()
      this.clearFormAMS()
    },
    clearFormAMS() {
      this.files = null
      this.initial = null
      this.name = null
      this.errors.sales_detail = null
      this.errors.requirement_id = null
    },

    clearFormEditSales() {
      this.maintenance_id = null
      this.hangar_id = null
      this.line_id = null
      // this.sales_detail.acReg = null
      // this.sales_detail.tat = null
      // this.sales_detail.totalSales = null
      // this.sales_detail.startDate = null

      this.errors.maintenance_id = null
      this.errors.ac_reg = null
      this.errors.hangar_id = null
      this.errors.line_id = null
      this.errors.value = null
      this.errors.start_date = null
      this.errors.tat = null
    },
    closeModalEditSales() {
      document.getElementById('close_modal_edit_sales').click()
      this.clearFormEditSales()
    },

    clearFormRequestSlot() {
      this.user_id = null
      this.line_id = null
      this.hangar_id = null
      this.errors.user_id = null
      this.errors.line_id = null
      this.errors.hangar_id = null
    },
    closeRequestSlot() {
      document.getElementById('close_modal_slot').click()
      this.clearFormRequestSlot()
    },

    clearFormNotifyLevel() {
      this.user_id = null
      this.line_id = null
    },
    closeNotifyLevel() {
      document.getElementById('close_modal_notify').click()
      this.clearFormNotifyLevel()
    },

    clearFormnotifyUpgrade() {
      this.user_id = null
      this.line_id = null
    },
    closenotifyUpgrade() {
      document.getElementById('close_modal_notify').click()
      this.clearFormnotifyUpgrade()
    },

    clearFormNotifyCOGS() {
      this.user_id = null
    },
    closeNotifyCOGS() {
      document.getElementById('close_modal_cogs').click()
      this.clearFormNotifyCOGS()
    },

    clearFormHistory() {
      this.filter = null
    },
  },
}
</script>
<style>
.mt-20 {
  margin-top: 20px;
}
.mb-20 {
  margin-bottom: 20px;
}

.badge-gmf {
  background-color: #003399;
}

.badge-green {
  background-color: #ADE792;
}

#readOnly {
  background-color: #f0f0f5;
}

#heightContact {
  height: 35px;
}

#cardMarketShare {
  border: dotted #04c8c8;
  border-radius: 10px;
  padding-top: 10px;
}

#cardSalesPlan {
  border: dotted #50cd89;
  border-radius: 10px;
  padding-top: 10px;
}

#cardDevisiasi {
  border: dotted #f1416c;
  border-radius: 10px;
  padding-top: 10px;
}

#textMarketShare {
  color: #04c8c8;
}

#textSalesPlan {
  color: #50cd89;
}

#textDevisiasi {
  color: #f1416c;
}

#textSync {
  background-color: #f1e0d0;
  color: #955f2d;
  margin-left: 10px;
}

#textWaiting {
  background-color: #f1e0d0;
  color: #955f2d;
}

#textApproved {
  background-color: #2146c7;
  color: #fff;
}

#bodyAMS {
  background: #f1f5f9;
  padding: 10px;
  border-radius: 8px;
}

#myBorder {
  border: dashed #cde7fe;
}
</style>
