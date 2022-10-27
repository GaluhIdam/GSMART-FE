<template>
  <div>
    <!-- Content -->
    <div class="container-fluid mt-5 mb-5">
      <!-- Breadcrumb -->
      <div class="row mb-5">
        <div class="col-lg-6">
          <Nuxt-link
            class="menu-link"
            to="/my-salesplan"
            active-class="active"
            >
            <i class="fa-solid fa-angle-left"></i>
              <span class="menu-title"  v-if="role == 'TPR' || role == 'CBO' || role == 'Administrator'">All Sales Plan</span>
              <span class="menu-title"  v-if="role == 'AMS'">My Sales Plan</span>
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
                      to="/my-salesplan"
                      active-class="active"
                      >
                      <span class="menu-title"  v-if="role == 'TPR' || role == 'CBO' || role == 'Administrator'">All Sales Plan</span>
                      <span class="menu-title"  v-if="role == 'AMS'">My Sales Plan</span> &nbsp;
                    </Nuxt-link>
                  </li>
                  <li class="breadcrumb-item active" aria-current="page">Detail </li>
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
                <h3>Detail</h3>
              </div>
              <div class="col-lg-6">
                <div class="text-right">
                  <div class="position-absolute top-0 end-0 mx-15 mt-4" v-if="sales_detail">
                    <button class="btn btn-outline btn-outline-info btn-sm" data-bs-toggle="modal" data-bs-target="#switchAMS" v-if="sales_detail.status === 'Open'">Switch AMS</button>
                    <button class="btn btn-primary btn-sm" data-bs-toggle="modal" data-bs-target="#editSales" v-if="sales_detail.type === 'TMB' && sales_detail.status === 'Open'"><i class="fa-solid fa-pen"></i> Edit Sales Plan</button>
                  </div>
                </div>
              </div>
            </div>
            <!-- End header -->

            <!-- Modal switchAMS -->
            <div class="modal fade" id="switchAMS" tabindex="-1" aria-labelledby="switchAMSLabel" aria-hidden="true">
              <div class="modal-dialog">
                <div class="modal-content">
                  <div class="modal-header">
                    <h5 class="modal-title w-100" id="switchAMSLabel">Switch AMS</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                  </div>
                  <form>
                    <div class="modal-body">
                      <form action="">
                        <div class="mb-3">
                          <label class="form-label">To</label>
                          <select v-model="ams_id" class="form-select">
                            <option v-for="amss in ams" :value="amss.id">
                              {{ amss.initial }} - {{ amss.user.name }}
                            </option>
                          </select>
                        </div>
                        <div class="mb-3">
                          <label class="form-label">Description</label> <br>
                          <div id="bodyAMS" v-if="sales_detail">
                            Level: <b>{{ sales_detail.level }}</b> Status: <b>{{ sales_detail.status }}</b> Other: <b>{{ sales_detail.other }}</b> Type: <b>{{ sales_detail.type }}</b> Month Sales: <b>{{ sales_detail.monthSales }}</b>
                            Years: <b>{{ sales_detail.year }}</b> Start Date Project: <b>{{ sales_detail.start_date }}</b> End Date Project: <b>{{ sales_detail.endDate }}</b>
                            TAT: <b>{{ sales_detail.tat }} Days</b> Progress: <b>{{ sales_detail.progress }}%</b> Product: <b>{{ sales_detail.product.name }}</b> Location: <b>{{ sales_detail.location.name }}</b>
                            Maintenance: <b>{{ sales_detail.maintenance.name }}</b>
                          </div>
                        </div>
                      </form>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" id="close_modal_ams" @click="closeModalAMS()">Close</button>
                      <button type="button" class="btn btn-primary" @click="swtichAMS()" v-permission="['switch_ams']">Send</button>
                    </div>
                  </form>
                </div>
              </div>
            </div>

            <!-- Modal edit Sales -->
            <div class="modal fade" tabindex="-1" id="editSales" data-bs-backdrop="static">
              <div class="modal-dialog modal-dialog-centered modal-lg">
                <div class="modal-content">
                  <div class="modal-header">
                    <h3 class="modal-title">Edit Sales Plan</h3>

                    <!--begin::Close-->
                    <div class="btn btn-icon btn-sm btn-active-light-primary ms-2" data-bs-dismiss="modal" aria-label="Close"
                    >
                      <span class="svg-icon svg-icon-1" @click="closeModalContact()">
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
                      <input type="hidden" v-model="sales_detail.id">
                      <div class="row">
                        <div class="col-lg-6">
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">Maintenance</label>
                            <select v-model="maintenance_id" class="form-select">
                              <option 
                                v-for="maintenance_options in maintenance_option" 
                                :value="maintenance_options.id" 
                              >
                              <!-- <option 
                                v-for="maintenance_options in maintenance_option" 
                                :value="maintenance_options.id" 
                                :selected="maintenance_options.id = maintenance_id"
                              > -->
                                {{ maintenance_options.name }}
                              </option>
                            </select>
                            <span v-if="errors.maintenance_id" class="error invalid-feedback">
                              {{ errors.maintenance_id[0] }}
                            </span>
                          </div>
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">Registration</label>
                            <input
                              type="text"
                              class="form-control"
                              v-model="sales_detail.acReg"
                              :class="{
                                'is-invalid': errors.acReg,
                              }"
                            />
                            <span v-if="errors.acReg" class="error invalid-feedback">{{
                              errors.acReg[0]
                            }}</span>
                          </div>
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
                        <div class="col-lg-6">
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">Location</label>
                            <select v-model="hangar_id" class="form-select">
                              <option 
                                v-for="hangar_options in hangar_option" 
                                :value="hangar_options.id" 
                              >
                              <!-- <option 
                                v-for="hangar_options in hangar_option" 
                                :value="hangar_options.id" 
                                :selected="hangar_options.id = hangar_id"
                              > -->
                                {{ hangar_options.name }}
                              </option>
                            </select>
                            <span v-if="errors.hangar_id" class="error invalid-feedback">
                              {{ errors.hangar_id[0] }}
                            </span>
                          </div>
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">Sales Plan</label>
                            <input
                              type="number"
                              class="form-control"
                              v-model="sales_detail.totalSales"
                              :class="{
                                'is-invalid': errors.totalSales,
                              }"
                            />
                            <span
                              v-if="errors.totalSales"
                              class="error invalid-feedback"
                              >{{ errors.totalSales[0] }}</span
                            >
                          </div>
                          <div class="form-group mb-3">
                            <label class="form-label fw-bold">Start Date</label>
                            <input
                              type="date"
                              class="form-control"
                              v-model="sales_detail.start_date"
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
                      </div>
                      <div class="row mt-10">
                        <div class="col d-flex justify-content-end">
                          <button type="button" class="btn btn-light mx-2" data-bs-dismiss="modal" id="close_modal_edit_sales">
                            Close
                          </button>
                          <button type="submit" class="btn btn-primary" v-permission="['update_sales']">Save</button>
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
                <div class="card mb-3" style="max-width: 540px;">
                  <div class="row no-gutters">
                    <div class="col-md-2 mt-2" v-if="sales_detail">
                      <img :src="sales_detail.customer.full_path" class="rounded" alt="No Image" style="width: 70px;">
                      <!-- <img src="https://dummyimage.com/70x70/000/fff" class="rounded" style="width: 70px;"> -->
                    </div>
                    <div class="col-md-10" style="margin-top: -20px;">
                      <div class="card-body">
                        <h5 class="card-title" v-if="sales_detail">{{ sales_detail.registration }}</h5>
                        <p class="card-text" v-if="sales_detail"><small class="text-muted"><i class="fa-solid fa-plane-up"></i> {{ sales_detail.acReg }}</small></p>
                        <p class="card-text" v-if="sales_detail"><small class="text-muted"><i class="fa-solid fa-spa"></i> {{ sales_detail.customer.name }}</small></p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-lg-2 col-md-12 col-sm-12" id="cardTop">
                <div class="text-center d-grid gap-2">
                  <span class="me-2 mb-2" id="cardMarketShare">
                    <h3 class="mt-2" id="textMarketShare" v-if="sales_detail">${{ formatPrice(sales_detail.marketShare) }}</h3>
                    <p><small class="text-muted">Market Share</small></p>
                  </span>
                </div>
              </div>
              <div class="col-lg-2 col-md-12 col-sm-12" id="cardTop">
                <div class="text-center d-grid gap-2">
                  <span class="me-2 mb-2" id="cardSalesPlan">
                    <h3 class="mt-2" id="textSalesPlan" v-if="sales_detail">${{ formatPrice(sales_detail.totalSales) }}</h3>
                    <p><small class="text-muted">Total Sales Plan</small></p>
                  </span>
                </div>
              </div>
              <div class="col-lg-2 col-md-12 col-sm-12" id="cardTop">
                <div class="text-center d-grid gap-2">
                  <span class="me-2 mb-2" id="cardDevisiasi">
                    <h3 class="mt-2" id="textDevisiasi" v-if="sales_detail">${{ formatPrice(sales_detail.deviasi) }}</h3>
                    <p><small class="text-muted">Devisiasi</small></p>
                  </span>
                </div>
              </div>
            </div>
            <!-- End Card -->

            <!-- Detail -->
            <div class="row mt-3">
              <div class="col-lg-1" v-if="sales_detail">
                <p class="text-muted">Level</p>
                <div v-if="sales_detail.level === 1">
                  <span class="badge badge-success"><b>Level 1</b></span>
                </div>
                <div v-if="sales_detail.level === 2">
                  <span class="badge badge-primary"><b>Level 2</b></span>
                </div>
                <div v-if="sales_detail.level === 3">
                  <span class="badge badge-warning"><b>Level 3</b></span>
                </div>
                <div v-if="sales_detail.level === 4">
                  <span class="badge badge-danger"><b>Level 4</b></span>
                </div>
                <p class="text-muted mt-5">Status</p>
                <div v-if="sales_detail.status === 'Cancel'">
                  <span class="badge badge-danger"><b>Cancel</b></span>
                </div>
                <div v-if="sales_detail.status === 'Open'">
                  <span class="badge badge-success"><b>Open</b></span>
                </div>
                <div v-if="sales_detail.status === 'Close in'">
                  <span class="badge badge-warning"><b>Close in</b></span>
                </div>
                <div v-if="sales_detail.status === 'Closed'">
                  <span class="badge badge-primary"><b>Closed</b></span>
                </div>
              </div>
              <div class="col-lg-1" v-if="sales_detail">
                <p class="text-muted mx-2">Other</p>
                <div v-if="sales_detail.other === 'RKAP'">
                  <span class="badge badge-info mx-2"><b>RKAP</b></span>
                </div>
                <div v-else="sales_detail.other === 'Additional'">
                  <span class="badge badge-primary mx-2"><b>Additional</b></span>
                </div>
                <p class="text-muted mt-5 mx-2">Type</p>
                <div v-if="sales_detail.type === 'TMB'">
                  <span class="badge badge-danger mx-2">TMB</span>
                </div>
                <div v-if="sales_detail.type === 'PBTH'">
                  <span class="badge badge-warning mx-2">PBTH</span>
                </div>
              </div>
              <div class="col-lg-2" v-if="sales_detail">
                <p class="text-muted mx-10">Progress</p>
                <div v-if="sales_detail.progress === 10">
                  <span class="badge badge-danger mx-10">10 %</span>
                </div>
                <div v-if="sales_detail.progress === 20">
                  <span class="badge badge-danger mx-10">20 %</span>
                </div>
                <div v-if="sales_detail.progress === 30">
                  <span class="badge badge-danger mx-10">30 %</span>
                </div>
                <div v-if="sales_detail.progress === 40">
                  <span class="badge badge-warning mx-10">40 %</span>
                </div>
                <div v-if="sales_detail.progress === 50">
                  <span class="badge badge-warning mx-10">50 %</span>
                </div>
                <div v-if="sales_detail.progress === 60">
                  <span class="badge badge-warning mx-10">60 %</span>
                </div>
                <div v-if="sales_detail.progress === 70">
                  <span class="badge badge-primary mx-10">70 %</span>
                </div>
                <div v-if="sales_detail.progress === 80">
                  <span class="badge badge-primary mx-10">80 %</span>
                </div>
                <div v-if="sales_detail.progress === 90">
                  <span class="badge badge-success mx-10">90 %</span>
                </div>
                <div v-if="sales_detail.progress === 100">
                  <span class="badge badge-success mx-10">100 %</span>
                </div>
                <p class="text-muted mt-5 mx-10">Month Sales</p>
                <p class="mx-10" v-if="sales_detail"><b>{{ sales_detail.monthSales }}</b></p>
              </div>
              <div class="col-lg-1">
                <p class="text-muted">TAT</p>
                <p v-if="sales_detail"><b>{{ sales_detail.tat }} Days</b></p>
                <p class="text-muted mt-5">Years</p>
                <p v-if="sales_detail"><b>{{ sales_detail.year }}</b></p>
              </div>
              <div class="col-lg-2">
                <p class="text-muted">Start Date Project</p>
                <p v-if="sales_detail"><b>{{ sales_detail.startDate }}</b></p>
                <p class="text-muted mt-5">End Date Project</p>
                <p v-if="sales_detail"><b>{{ sales_detail.endDate }}</b></p>
              </div>
              <div class="col-lg-2">
                <p class="text-muted">Location</p>
                <p v-if="sales_detail"><b>{{ sales_detail.location.name }}</b></p>
                <p class="text-muted mt-5">Product</p>
                <p v-if="sales_detail"><b>{{ sales_detail.product.name }}</b></p>
              </div>
              <div class="col-lg-3">
                <p class="text-muted">Maintenance</p>
                <p v-if="sales_detail"><b>{{ sales_detail.maintenance.description }}</b></p>
              </div>
            </div>
            <!-- End Detail -->

            <!-- Tab -->
            <div class="row mt-5">
              <ul class="nav nav-tabs" id="myTab" role="tablist">
                <li class="nav-item" role="presentation">
                  <button class="nav-link active" id="upgrade-level-tab" data-bs-toggle="tab" data-bs-target="#upgrade-level-tab-pane" type="button" role="tab" aria-controls="upgrade-level-tab-pane" aria-selected="true">Upgrade Level</button>
                </li>
                <li class="nav-item" role="presentation">
                  <button class="nav-link" id="history-tab" data-bs-toggle="tab" data-bs-target="#history-tab-pane" type="button" role="tab" aria-controls="history-tab-pane" aria-selected="false">History</button>
                </li>
                <li class="nav-item" role="presentation">
                  <button class="nav-link" id="contact-tab" data-bs-toggle="tab" data-bs-target="#contact-tab-pane" type="button" role="tab" aria-controls="contact-tab-pane" aria-selected="false">Contact Person</button>
                </li>
                <li class="nav-item" role="presentation" v-if="role == 'AMS' || role == 'Administrator' || role == 'TPR'">
                  <button class="nav-link" id="reschedule-tab" data-bs-toggle="tab" data-bs-target="#reschedule-tab-pane" type="button" role="tab" aria-controls="reschedule-tab-pane" aria-selected="false">Reschedule/Cancel</button>
                </li>
              </ul>

              <div class="tab-content" id="myTabContent">
                <!-- Tab Upgrade Level -->
                <div class="tab-pane fade show active" id="upgrade-level-tab-pane" role="tabpanel" aria-labelledby="upgrade-level-tab" tabindex="0">
                  <!--begin::Stepper-->
                  <div class="stepper stepper-pills mt-5" id="kt_stepper_example_basic">
                    <!--begin::Nav-->
                    <div class="stepper-nav flex-center flex-wrap mb-10">
                        <!--begin::Step 1-->
                        <div class="stepper-item mx-8 my-4 current" data-kt-stepper-element="nav">
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
                                    <div class="stepper-desc">
                                      Awareness
                                    </div>
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
                        <div class="stepper-item mx-8 my-4" data-kt-stepper-element="nav">
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
                                    <div class="stepper-desc">
                                      Opportunity
                                    </div>
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
                        <div class="stepper-item mx-8 my-4" data-kt-stepper-element="nav">
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
                                    <div class="stepper-desc">
                                      Attractive Proposal
                                    </div>
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
                        <div class="stepper-item mx-8 my-4" data-kt-stepper-element="nav">
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
                                    <div class="stepper-desc">
                                        Contract Signing
                                    </div>
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
                    <!--end::Nav-->

                    <!--begin::Form-->
                    <div class="form mx-auto" novalidate="novalidate" id="kt_stepper_example_basic_div">
                        <!--begin::Group-->
                        <div class="mb-5" v-if="sales_detail">

                            <!--begin::Step 4-->
                            <div class="flex-column current" data-kt-stepper-element="content" v-if="sales_detail.level === 4 || sales_detail.level === 3 || sales_detail.level === 2 || sales_detail.level === 1">
                              <form>
                                <div class="row">
                                  <!-- Fill in Contact Person of Customer -->
                                  <div class="col-lg-6">
                                    <h3>Fill in Contact Person of Customer</h3>
                                    <p class="text-muted"><small>by <a href="#">{{ user }}</a></small></p>
                                  </div>
                                  <div class="col-lg-6">
                                    <div class="position-relative" v-if="sales_detail">
                                      <div class="position-absolute top-0 end-0" v-if="sales_detail.level == 4 && sales_detail.status === 'Open'">
                                        <button 
                                          type="button" 
                                          class="btn btn-primary btn-sm" 
                                          data-bs-toggle="modal" 
                                          data-bs-target="#addContact" 
                                          @click="addContact()"
                                          v-if = "role == 'AMS' || role == 'Administrator'"
                                          >
                                          Add Contact Person
                                        </button>
                                      </div>
                                    </div>
                                  </div>
                                  <div class="rounded box-d" id="myBorder">
                                    <div class="mt-3 table-responsive">
                                      <table class="table" v-if="contact">
                                        <tr v-for="contact in level4[0].data" :key="contact.id" id="heightContact">
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
                                    <h3>Upload Attachment RFQ or Email Request</h3>
                                    <p class="text-danger"><small>* File size max 5MB</small></p>
                                  </div>
                                  <div class="col-lg-6 mt-3">
                                    <div class="position-relative" v-if="sales_detail">
                                      <div class="position-absolute top-0 end-0" v-if="sales_detail.level == 4 && sales_detail.status === 'Open'">
                                        <button 
                                        type="button" 
                                        class="btn btn-primary btn-sm" 
                                        data-bs-toggle="modal" 
                                        data-bs-target="#addFile" 
                                        @click="addFile1()"
                                        v-if="role == 'AMS' || role == 'Administrator'"
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
                                        <tr v-for="files in level4[1].data" :key="files.id">
                                          <td>
                                              <a :href="files.full_path" class="btn btn-outline-primary btn-outline btn-sm mb-2" target="_blank">
                                                <strong>{{ files.file_name }}</strong>
                                              </a>
                                          </td>
                                          <td class="d-flex justify-content-end" v-if="sales_detail.level == 4 && sales_detail.status === 'Open'">
                                            <button type="button" 
                                              class="btn btn-danger btn-sm" 
                                              @click="removeFile(files.id)" 
                                              v-permission="['delete_files']"
                                              v-if = "role == 'AMS' || role == 'Administrator'"
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
                                    <p class="text-danger"><small>* File size max 5MB</small></p>
                                  </div>
                                  <div class="col-lg-6 mt-3">
                                    <div class="position-relative" v-if="sales_detail">
                                      <div class="position-absolute top-0 end-0" v-if="sales_detail.level == 4 && sales_detail.status === 'Open'">
                                        <button 
                                          type="button" 
                                          class="btn btn-primary btn-sm" 
                                          data-bs-toggle="modal" 
                                          data-bs-target="#addFile" 
                                          @click="addFile2()"
                                          v-if="role == 'AMS' || role == 'Administrator'"
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
                                        <tr v-for="files in level4[2].data" :key="files.id">
                                          <td>
                                              <a :href="files.full_path" class="btn btn-outline-primary btn-outline btn-sm mb-2" target="_blank">
                                                <strong>{{ files.file_name }}</strong>
                                              </a>
                                          </td>
                                          <td class="d-flex justify-content-end" v-if="sales_detail.level == 4 && sales_detail.status === 'Open'">
                                            <button type="button" 
                                              class="btn btn-danger btn-sm" 
                                              @click="removeFile(files.id)" 
                                              v-permission="['delete_files']"
                                              v-if = "role == 'AMS' || role == 'Administrator'"
                                              >
                                              <span class="fas fa-trash"></span>
                                            </button>
                                          </td>
                                        </tr>
                                      </table>
                                    </div>
                                  </div>

                                  <div class="text-center mt-5" v-if="role == 'TPR' || role == 'Administrator'">
                                    <form>
                                      <input type="hidden" v-model="upgrade" value="1">
                                      <button type="button" class="btn btn-info btn-sm" 
                                        @click="upgradeLevel()" 
                                        v-if = "sales_detail.status === 'Open' && sales_detail.level == 4 && sales_detail.upgrade == true"
                                        v-permission="['upgrade_level']"
                                        >
                                        Upgrade Level
                                      </button>
                                    </form>
                                  </div>
                                  <div class="text-center mt-5" v-if="role == 'AMS'">
                                    <form>
                                      <button type="button" 
                                        class="btn btn-info btn-sm" 
                                        data-bs-toggle="modal" 
                                        data-bs-target="#notifyUpgrade" 
                                        v-if = "sales_detail.status === 'Open' && sales_detail.level == 4 && sales_detail.upgrade == true"
                                        >
                                        Request to Upgrade
                                      </button>
                                    </form>
                                  </div>

                                </div>
                              </form>
                            </div>
                            <!--begin::Step 4-->

                            <!--begin::Step 3-->
                            <div class="flex-column" data-kt-stepper-element="content" v-if="sales_detail.level === 3 || sales_detail.level === 2 || sales_detail.level === 1">
                              <form>
                                <div class="row">
                                  <!-- Attachment of Financial Assesment Form (optional) -->
                                  <div class="col-lg-6 mt-3">
                                    <h3>Attachment of Financial Assesment Form (optional)</h3>
                                    <p class="text-danger"><small>* File size max 5MB</small></p>
                                  </div>
                                  <div class="col-lg-6 mt-3">
                                    <div class="position-relative" v-if="sales_detail">
                                      <div class="position-absolute top-0 end-0" v-if="sales_detail.level == 3 && sales_detail.status === 'Open'">
                                        <button 
                                        type="button" 
                                        class="btn btn-primary btn-sm" 
                                        data-bs-toggle="modal" 
                                        data-bs-target="#addFile" 
                                        @click="addFile3()"
                                        v-if="role == 'AMS' || role == 'Administrator'"
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
                                        <tr v-for="files in level3[0].data" :key="files.id">
                                          <td>
                                              <a :href="files.full_path" class="btn btn-outline-primary btn-outline btn-sm mb-2" target="_blank">
                                                <strong>{{ files.file_name }}</strong>
                                              </a>
                                          </td>
                                          <td class="d-flex justify-content-end" v-if="sales_detail.level == 3 && sales_detail.status === 'Open'">
                                            <button type="button" 
                                              class="btn btn-danger btn-sm" 
                                              @click="removeFile(files.id)" 
                                              v-permission="['delete_files']"
                                              v-if = "role == 'AMS' || role == 'Administrator'"
                                              >
                                              <span class="fas fa-trash"></span>
                                            </button>
                                          </td>
                                        </tr>
                                      </table>
                                    </div>
                                  </div>

                                  <!-- Attachment of Maintenance Proposal for Customer -->
                                  <div class="col-lg-6 mt-3">
                                    <h3>Attachment of Maintenance Proposal for Customer</h3>
                                    <p class="text-danger"><small>* File size max 5MB</small></p>
                                  </div>
                                  <div class="col-lg-6 mt-3">
                                    <div class="position-relative" v-if="sales_detail">
                                      <div class="position-absolute top-0 end-0" v-if="sales_detail.level == 3 && sales_detail.status === 'Open'">
                                        <button type="button" class="btn btn-outline-warning btn-outline btn-sm">Sync</button>
                                        <button 
                                          type="button" 
                                          class="btn btn-success btn-sm"
                                          data-bs-toggle="modal" 
                                          data-bs-target="#notifyCOGS" 
                                          v-if="role == 'TPR' || role == 'Administrator'"
                                        >
                                          Notify COGS
                                        </button>
                                        <button 
                                        type="button" 
                                        class="btn btn-primary btn-sm" 
                                        data-bs-toggle="modal" 
                                        data-bs-target="#addFile" 
                                        @click="addFile4()"
                                        v-if="role == 'CBO' || role == 'Administrator'"
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
                                        <tr v-for="files in level3[1].data" :key="files.id">
                                          <td>
                                              <a :href="files.full_path" class="btn btn-outline-primary btn-outline btn-sm mb-2" target="_blank">
                                                <strong>{{ files.file_name }}</strong>
                                              </a>
                                          </td>
                                          <td class="d-flex justify-content-end" v-if="sales_detail.level == 3 && sales_detail.status === 'Open'">
                                            <button type="button" 
                                              class="btn btn-danger btn-sm" 
                                              @click="removeFile(files.id)" 
                                              v-permission="['delete_files']"
                                              v-if = "role == 'CBO' || role == 'Administrator'"
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
                                    <h3>Attachment of Profitability Analysis Form Signed</h3>
                                    <p class="text-danger"><small>* File size max 5MB</small></p>
                                  </div>
                                  <div class="col-lg-6 mt-3">
                                    <div class="position-relative" v-if="sales_detail">
                                      <div class="position-absolute top-0 end-0" v-if="sales_detail.level == 3 && sales_detail.status === 'Open'">
                                        <span class="btn btn-sm" id="textWaiting">Waiting Approve VP TP</span>
                                        <button 
                                        type="button" 
                                        class="btn btn-primary btn-sm" 
                                        data-bs-toggle="modal" 
                                        data-bs-target="#addFile" 
                                        @click="addFile5()"
                                        v-if="role == 'AMS' || role == 'Administrator'"
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
                                        <tr v-for="files in level3[2].data" :key="files.id">
                                          <td>
                                              <a :href="files.full_path" class="btn btn-outline-primary btn-outline btn-sm mb-2" target="_blank">
                                                <strong>{{ files.file_name }}</strong>
                                              </a>
                                          </td>
                                          <td class="d-flex justify-content-end" v-if="sales_detail.level == 3 && sales_detail.status === 'Open'">
                                            <button type="button" 
                                              class="btn btn-danger btn-sm" 
                                              @click="removeFile(files.id)" 
                                              v-permission="['delete_files']"
                                              v-if = "role == 'AMS' || role == 'Administrator'"
                                              >
                                              <span class="fas fa-trash"></span>
                                            </button>
                                          </td>
                                        </tr>
                                      </table>
                                    </div>
                                  </div>

                                  <div class="text-center mt-5" v-if="role == 'TPR' || role == 'Administrator'">
                                    <form>
                                      <input type="hidden" v-model="upgrade" value="1">
                                      <button type="button" class="btn btn-info btn-sm" 
                                        @click="upgradeLevel()" 
                                        v-if = "sales_detail.status === 'Open' && sales_detail.level == 3 && sales_detail.upgrade == true"
                                        v-permission="['upgrade_level']"
                                        >
                                        Upgrade Level
                                      </button>
                                    </form>
                                  </div>
                                  <div class="text-center mt-5" v-if="role == 'AMS'">
                                    <form>
                                      <button 
                                        type="button" 
                                        class="btn btn-info btn-sm" 
                                        data-bs-toggle="modal" 
                                        data-bs-target="#notifyUpgrade" 
                                        v-if = "sales_detail.status === 'Open' && sales_detail.level == 3 && sales_detail.upgrade == true"
                                        >
                                        Request to Upgrade
                                      </button>
                                    </form>
                                  </div>

                                </div>
                              </form>
                            </div>
                            <!--begin::Step 3-->

                            <!--begin::Step 2-->
                            <div class="flex-column" data-kt-stepper-element="content" v-if="sales_detail.level === 2 || sales_detail.level === 1">
                              <form>
                                <div class="row">
                                  <!-- Attachment of Customer Approval (SOW Signed / Proposal Approved) -->
                                  <div class="col-lg-6 mt-3">
                                    <h3>Attachment of Customer Approval (SOW Signed / Proposal Approved)</h3>
                                    <p class="text-danger"><small>* File size max 5MB</small></p>
                                  </div>
                                  <div class="col-lg-6 mt-3">
                                    <div class="position-relative" v-if="sales_detail">
                                      <div class="position-absolute top-0 end-0" v-if="sales_detail.level == 2 && sales_detail.status === 'Open'">
                                        <button 
                                        type="button" 
                                        class="btn btn-primary btn-sm" 
                                        data-bs-toggle="modal" 
                                        data-bs-target="#addFile" 
                                        @click="addFile6()"
                                        v-if="role == 'AMS' || role == 'Administrator'"
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
                                        <tr v-for="files in level2[0].data" :key="files.id">
                                          <td>
                                              <a :href="files.full_path" class="btn btn-outline-primary btn-outline btn-sm mb-2" target="_blank">
                                                <strong>{{ files.file_name }}</strong>
                                              </a>
                                          </td>
                                          <td class="d-flex justify-content-end" v-if="sales_detail.level == 2 && sales_detail.status === 'Open'">
                                            <button type="button" 
                                              class="btn btn-danger btn-sm" 
                                              @click="removeFile(files.id)" 
                                              v-permission="['delete_files']"
                                              v-if = "role == 'AMS' || role == 'Administrator'"
                                              >
                                              <span class="fas fa-trash"></span>
                                            </button>
                                          </td>
                                        </tr>
                                      </table>
                                    </div>
                                  </div>

                                  <!-- Slot Request -->
                                  <div class="col-lg-6 mt-5">
                                    <h3>Slot Request</h3>
                                    <p class="text-muted"><small>by <a href="#">{{ user }}</a></small></p>
                                  </div>
                                  <div class="col-lg-6 mt-5">
                                    <div class="position-relative">
                                      <div class="position-absolute top-0 end-0" v-if="sales_detail">
                                        <button 
                                            type="button" 
                                            class="btn btn-success btn-sm"
                                            @click="slotConfirm()"
                                            v-if = "level2[1].status == 0 && sales_detail.status === 'Open' && sales_detail.level == 2 && sales_detail.upgrade == false && role == 'CBO' || role == 'Administrator'"
                                          >
                                            Approve
                                        </button>
                                        <span class="btn btn-sm" id="textApproved" v-if="level2[1].status == 1 && sales_detail.status === 'Open' && sales_detail.level == 2">
                                          Approved by CBO
                                        </span>
                                        <button 
                                          type="button" 
                                          class="btn btn-info btn-sm"
                                          data-bs-toggle="modal" 
                                          data-bs-target="#slotRequest" 
                                          v-if = "level2[1].status == 0 && sales_detail.status === 'Open' && sales_detail.level == 2 && role == 'AMS' || role == 'Administrator'"
                                        >
                                          Request to CBO
                                        </button>
                                      </div>
                                    </div>
                                  </div>
                                  <div class="row" v-if="sales_detail">
                                    <div class="col-lg-4">
                                      <div class="mb-3">
                                        <label>Hangar</label>
                                        <input type="text" class="form-control form-control-solid" v-model="sales_detail.location.id" readonly/>
                                      </div>
                                      <div class="mb-3">
                                        <label>Line Hangar Request</label>
                                        <div class="row" >
                                          <div class="col-12" v-if="level2[1].data != null">
                                            <input type="text" v-model="level2[1].data.line.name" class="form-control form-control-solid" readonly>
                                          </div>
                                          <div class="col-12" v-else>
                                            <input type="text" class="form-control form-control-solid" readonly>
                                          </div>
                                        </div>
                                      </div>

                                      <!-- Confirm Line Hanggar -->
                                      <!-- 
                                      <div class="row" v-if="role == 'CBO' || role == 'Administrator'">
                                        <div class="col-9">
                                          <div class="mb-3">
                                            <label>Choose Line Hangar</label>
                                            <select v-model="line_id" class="form-select">
                                              <option :value="null" disabled>Select Line</option>
                                              <option 
                                                v-for="lines in line" 
                                                v-if="lines.hangar_id === sales_detail.location.id"
                                                :value="lines.id"
                                              >
                                                {{ lines.name }}
                                              </option>
                                            </select>
                                          </div>
                                        </div>
                                        <div class="col-3">
                                          <button 
                                            class="btn btn-primary btn-sm mt-7" 
                                            type="button" 
                                            @click="updateSlot()"
                                            v-if="sales_detail.status === 'Open'"
                                            v-permission="['slot_request']"
                                          >
                                            Edit
                                          </button>
                                        </div>
                                      </div> 
                                      -->
                                    </div>
                                    <div class="col-lg-4">
                                      <div class="mb-3">
                                        <label>Registration</label>
                                        <input type="text" class="form-control form-control-solid" v-model="sales_detail.registration" readonly/>
                                      </div>
                                      <div class="mb-3">
                                        <label>TAT</label>
                                        <input type="number" class="form-control form-control-solid" v-model="sales_detail.tat" readonly/>
                                      </div>
                                    </div>
                                    <div class="col-lg-4" v-if="sales_detail">
                                      <div class="mb-3">
                                        <lbabel>Start Date</lbabel>
                                        <input type="text" class="form-control form-control-solid" v-model="sales_detail.startDate" readonly/>
                                      </div>
                                      <div class="mb-3">
                                        <label>End Date</label>
                                        <input type="text" class="form-control form-control-solid" v-model="sales_detail.endDate" readonly/>
                                      </div>
                                    </div>
                                  </div>

                                  <div class="text-center mt-5" v-if="role == 'TPR' || role == 'Administrator'">
                                    <form>
                                      <input type="hidden" v-model="upgrade" value="1">
                                      <button type="button" class="btn btn-info btn-sm" 
                                        @click="upgradeLevel()" 
                                        v-if = "sales_detail.status === 'Open' && sales_detail.level == 2 && sales_detail.upgrade == true"
                                        v-permission="['upgrade_level']"
                                        >
                                        Upgrade Level
                                      </button>
                                    </form>
                                  </div>
                                  <div class="text-center mt-5" v-if="role == 'AMS'">
                                    <form>
                                      <button 
                                        type="button" 
                                        class="btn btn-info btn-sm" 
                                        data-bs-toggle="modal" 
                                        data-bs-target="#notifyUpgrade" 
                                        v-if = "sales_detail.status === 'Open' && sales_detail.level == 2 && sales_detail.upgrade == true"
                                        >
                                        Request to Upgrade
                                      </button>
                                    </form>
                                  </div>

                                </div>
                              </form>
                            </div>
                            <!--begin::Step 2-->

                            <!--begin::Step 1-->
                            <div class="flex-column" data-kt-stepper-element="content" v-if="sales_detail.level === 1">
                              <form action="">
                                <div class="row">
                                  <!-- Attachment of WO/PO number customer document -->
                                  <div class="col-lg-6 mt-3">
                                    <h3>Attachment of WO/PO number customer document</h3>
                                    <p class="text-muted"><small>by <a href="#">{{ user }}</a></small></p>
                                  </div>
                                  <div class="col-lg-6 mt-3">
                                    <div class="position-relative" v-if="sales_detail">
                                      <div class="position-absolute top-0 end-0" v-if="sales_detail.level == 1 && sales_detail.status === 'Open'">
                                        <input type="hidden" v-model="status" value="2">
                                        <button type="button" class="btn btn-success btn-sm" 
                                          @click="closeSales()" 
                                          v-if="role == 'Administrator' || role == 'AMS'"
                                          v-permission="['upgrade_level']"
                                          >
                                          Closed Sales
                                        </button>
                                        <button 
                                        type="button" 
                                        class="btn btn-primary btn-sm" 
                                        data-bs-toggle="modal" 
                                        data-bs-target="#addFile" 
                                        @click="addFile7()"
                                        v-if="role == 'AMS' || role == 'Administrator'"
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
                                        <tr v-for="files in level1[0].data" :key="files.id">
                                          <td>
                                              <a :href="files.full_path" class="btn btn-outline-primary btn-outline btn-sm mb-2" target="_blank">
                                                <strong>{{ files.file_name }}</strong>
                                              </a>
                                          </td>
                                          <td class="d-flex justify-content-end" v-if="sales_detail.level == 1 && sales_detail.status === 'Open'">
                                            <button type="button" 
                                              class="btn btn-danger btn-sm" 
                                              @click="removeFile(files.id)" 
                                              v-permission="['delete_files']"
                                              v-if = "role == 'AMS' || role == 'Administrator'"
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
                                  <form>
                                    <div class="row">
                                      <div class="input-group mb-3" v-permission="['input_so_number']" v-if="level1[1].data == ''">
                                          <input 
                                            type="text" 
                                            class="form-control" 
                                            v-model="sales_detail.so_number"
                                            :class="{
                                              'is-invalid': errors.so_number,
                                            }"
                                          />
                                          <button 
                                            class="btn btn-sm" 
                                            type="button" 
                                            id="textSync"
                                            @click="updateSO()" 
                                            v-if="sales_detail.status === 'Open' && role == 'CBO' || role == 'Administrator'"
                                            >
                                            Sync
                                          </button>
                                          <span v-if="errors.so_number" class="error invalid-feedback">{{
                                            errors.so_number[0]
                                          }}</span>
                                      </div>
                                      <div class="input-group mb-3" v-else>
                                        <input 
                                          type="text" 
                                          class="form-control" 
                                          v-model="level1[1].data"
                                          readonly
                                        />
                                      </div>
                                    </div>
                                  </form>

                                  <div class="text-center mt-10" v-if="sales_detail">
                                    <form v-if="sales_detail.status === 'Closed'">
                                      <input type="hidden" v-model="status" value="3">
                                      <button 
                                      type="button" 
                                      class="btn btn-primary btn-sm" 
                                      @click="requestClosed()" 
                                      v-permission="['close_sales']" 
                                      v-if="role == 'Administrator' || role == 'AMS'"
                                      >
                                        Request to Closed
                                      </button>
                                    </form>
                                  </div>

                                </div>
                              </form>
                            </div>
                            <!--begin::Step 1-->
                        </div>
                        <!--end::Group-->

                        <!--begin::Actions-->
                        <div class="d-flex flex-stack">
                            <!--begin::Wrapper-->
                            <div class="me-2">
                                <button type="button" class="btn btn-light btn-active-light-primary" data-kt-stepper-action="previous">
                                    Back
                                </button>
                            </div>
                            <!--end::Wrapper-->

                            <!--begin::Wrapper-->
                            <div>
                                <!-- <button type="button" class="btn btn-primary" data-kt-stepper-action="submit" disabled>
                                    <span class="indicator-label">
                                        Done
                                    </span>
                                    <span class="indicator-progress">
                                        Please wait... <span class="spinner-border spinner-border-sm align-middle ms-2"></span>
                                    </span>
                                </button> -->

                                <button type="button" class="btn btn-primary" data-kt-stepper-action="next">
                                    Continue
                                </button>
                            </div>
                            <!--end::Wrapper-->
                        </div>
                        <!--end::Actions-->
                    </div>
                    <!--end::Form-->
                  </div>
                  <!--end::Stepper-->
                </div>

                <!-- Tab History -->  
                <div class="tab-pane fade" id="history-tab-pane" role="tabpanel" aria-labelledby="history-tab" tabindex="0">
                  <div class="mt-5">
                    <!-- Filter -->
                    <div class="row">
                      <div class="col-lg-8"></div>
                      <div class="col-lg-4 col-sm-12 d-flex justify-content-end align-items-center">
                        <label for="" class="form-label me-3">Select Month</label>
                        <select class="form-select" v-model="filter">
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
                        <button type="button" class="btn btn-info btn-sm ms-3" @click="listFileHistory(); clearFormHistory();">Filter</button>
                      </div>
                    </div>
                    
                    <div v-for="file_history in file_histories">
                      <div class="row">
                        <div class="col-lg-6 col-sm-12" v-if="file_history">
                          <h3 class="mt-3"><span class="fas fa-calendar-days"></span> {{ file_history.uploadedAt }}</h3>
                        </div>
                      </div>

                      <!-- Isi -->
                      <div class="row mt-4" v-if="file_history">
                        <h3>{{ file_history.totalFiles }} File Uploaded</h3>
                        <p class="text-muted"><small>by <a href="#">{{ user }}</a></small></p>
                        <div class="rounded box-d mb-5" id="myBorder">
                          <div class="mt-3">
                            <table class="table">
                              <tr v-for="file in file_history.files" :key="file.id">
                                <td>
                                    <form>
                                      <a :href="file.full_path" 
                                        class="btn btn-outline-primary btn-outline btn-sm" 
                                        target="_blank">
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
                <div class="tab-pane fade" id="contact-tab-pane" role="tabpanel" aria-labelledby="contact-tab" tabindex="0">
                  <div class="mt-5" v-if="sales_detail">
                    <div class="table-responsive">
                      <table class="table table-row-bordered table-row-gray-200 gy-4" v-if="contact">
                        <thead>
                          <tr class="fw-bold fs-6 text-gray-800">
                            <th class="text-center">No</th>
                            <th class="text-center">Name</th>
                            <th class="text-center">Phone</th>
                            <th class="text-center">Email</th>
                            <th class="text-center">Title</th>
                            <th class="text-center" v-if="role == 'AMS' || role == 'Administrator' || role == 'TPR'">Action</th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr v-for="(contact, contact_index) in level4[0].data"  @dblclick="getItem(contact_index)">
                            <td class="text-center">
                              {{ contact_index+1 }}
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
                            <td class="d-flex justify-content-center" v-if="role == 'AMS' || role == 'Administrator' || role == 'TPR'">
                              <button class="btn btn-sm btn-light"  @click="removeContact(contact.id)" v-permission="['delete_contacts']">
                                <i class="bi bi-trash-fill text-primary"></i>
                              </button>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </div>

                    <div class="text-center mt-20" v-if="sales_detail.status === 'Open' && role == 'AMS' || role == 'Administrator' || role == 'TPR'">
                      <button type="button" class="btn btn-primary" data-bs-toggle="modal" v-permission="['create_contacts']" data-bs-target="#addContact" @click="addContact()">
                        Add Contact Person
                      </button>
                    </div>
                  </div>
                </div>

                <!-- Tab Reschedule/Cancel -->
                <div class="tab-pane fade" id="reschedule-tab-pane" role="tabpanel" aria-labelledby="reschedule-tab" tabindex="0">
                  <div class="mt-5" v-if="sales_detail">
                    <ul class="nav nav-tabs nav-line-tabs nav-line-tabs-2x mb-5 fs-6" v-if="role == 'AMS'">
                      <li class="nav-item">
                          <a class="nav-link active" data-bs-toggle="tab" href="#kt_tab_pane_1">Reschedule</a>
                      </li>
                    </ul>
                    <ul class="nav nav-tabs nav-line-tabs nav-line-tabs-2x mb-5 fs-6" v-else-if="role == 'TPR'">
                      <li class="nav-item">
                          <a class="nav-link" data-bs-toggle="tab" href="#kt_tab_pane_2">Cancel</a>
                      </li>
                    </ul>
                    <ul class="nav nav-tabs nav-line-tabs nav-line-tabs-2x mb-5 fs-6" v-else-if="role == 'Administrator'">
                      <li class="nav-item">
                          <a class="nav-link active" data-bs-toggle="tab" href="#kt_tab_pane_1">Reschedule</a>
                      </li>
                      <li class="nav-item">
                          <a class="nav-link" data-bs-toggle="tab" href="#kt_tab_pane_2">Cancel</a>
                      </li>
                    </ul>

                    <div class="tab-content" id="myTabContent">
                      <!-- Reschedule Form -->
                      <div v-if="role == 'AMS' || role == 'Administrator'">
                        <div class="tab-pane fade show active" id="kt_tab_pane_1" role="tabpanel">
                          <form @submit.prevent="salesReschedule" v-if="sales_detail" >
                            <div class="mb-3">
                              <label class="form-label">Hanggar</label>
                              <input type="text" class="form-control" readonly v-model="sales_detail.location.id" id="readOnly">
                            </div>
                            <div class="mb-3">
                              <label class="form-label">Registration</label>
                              <input type="text" class="form-control" v-model="sales_detail.registration" readonly id="readOnly">
                            </div>
                            <div class="mb-3">
                              <label class="form-label">CBO Date</label>
                              <input 
                                type="date" 
                                class="form-control" 
                                v-model="sales_detail.start_date"
                                :class="{
                                  'is-invalid': errors.start_date,
                                }"
                              >
                              <span
                                v-if="errors.start_date"
                                class="error invalid-feedback"
                                >{{ errors.start_date[0] }}</span
                              >
                            </div>
                            <div class="mb-3">
                              <label class="form-label">End Date</label>
                              <input 
                                type="date" 
                                class="form-control" 
                                v-model="end_date" 
                                :class="{
                                  'is-invalid': errors.end_date,
                                }"
                              >
                                <span
                                  v-if="errors.end_date"
                                  class="error invalid-feedback"
                                  >{{ errors.end_date[0] }}</span
                                >
                            </div>
                            <div class="mb-3">
                              <label class="form-label">TAT</label>
                              <input type="number" class="form-control" v-model="sales_detail.tat" readonly id="readOnly">
                            </div>
                            <div class="mb-3">
                              <label class="form-label">Current Date</label>
                              <input 
                                type="date" 
                                class="form-control" 
                                v-model="current_date"
                                :class="{
                                  'is-invalid': errors.current_date,
                                }"
                              >
                              <span
                                v-if="errors.current_date"
                                class="error invalid-feedback"
                                >{{ errors.current_date[0] }}</span
                              >
                            </div>
                            <div class="mb-3">
                              <label class="form-label">Sales Month</label>
                              <input type="text" class="form-control" v-model="sales_detail.monthSales" readonly id="readOnly">
                            </div>
                            <div class="text-center mt-5" v-if="sales_detail.status === 'Open'">
                              <button type="reset" class="btn btn-danger">Reset</button>
                              <button type="submit" class="btn btn-primary" v-permission="['reschedule_sales']">Confirm</button>
                            </div>
                          </form>
                        </div>
                      </div>
                      <!-- Cancel Form -->
                      <div  v-if="role == 'TPR' || role == 'Administrator'">
                        <div class="tab-pane fade show active" id="kt_tab_pane_2" role="tabpanel">
                          <form @submit.prevent="salesCancel">
                            <div class="mb-3">
                              <label class="form-label">Category</label>
                              <div class="row mb-5">
                                <div class="col">
                                  <div class="input-group mb-3">
                                    <!-- <select v-model="category" class="form-select">
                                      <option :value="category">Category 1</option>
                                      <option :value="category">Category 2</option>
                                      <option :value="category">Category 3</option>
                                    </select> -->
                                    <input type="text" v-model="category" class="form-control" :class="{ 'is-invalid': errors.category, }">
                                    <span v-if="errors.category" class="error invalid-feedback">
                                      {{ errors.category[0] }}
                                    </span>
                                  </div>
                                </div>
                              </div>
                            </div>
                            <div class="mb-3">
                              <label class="form-label">Reason of Cancel</label>
                              <textarea class="form-control" cols="30" rows="10" v-model="reason" :class="{ 'is-invalid': errors.reason, }"></textarea>
                              <span v-if="errors.reason" class="error invalid-feedback">
                                {{ errors.reason[0] }}
                              </span>
                            </div>
                            <div class="text-center mt-5" v-if="sales_detail.status === 'Open'">
                              <button type="reset" class="btn btn-danger">Reset</button>
                              <button type="submit" class="btn btn-primary" v-permission="['reject_sales']">Confirm</button>
                            </div>
                          </form>
                        </div>
                      </div>
                    </div>
                    
                  </div>
                </div>

                <!-- Modal Contact -->
                <div class="modal fade" tabindex="-1" id="addContact" data-bs-backdrop="static">
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 v-if="modal_contact" class="modal-title">Add Contact Person</h3>
                        <h3 v-else class="modal-title">Edit Contact Person</h3>

                        <!--begin::Close-->
                        <div class="btn btn-icon btn-sm btn-active-light-primary ms-2" data-bs-dismiss="modal" aria-label="Close"
                        >
                          <span class="svg-icon svg-icon-1" @click="closeModalContact()">
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
                          <input type="hidden" v-if="sales_detail" v-model="sales_detail.id">
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
                              <span v-if="errors.name" class="error invalid-feedback">{{
                                errors.name[0]
                              }}</span>
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
                              <span v-if="errors.phone" class="error invalid-feedback">{{
                                errors.phone[0]
                              }}</span>
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
                              <button type="button" class="btn btn-light mx-2" data-bs-dismiss="modal" id="close_modal_contact" @click="closeModalContact()">
                                Close
                              </button>
                              <button type="submit" class="btn btn-primary" v-permission="['create_contacts']">Save</button>
                            </div>
                          </div>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Modal Upload -->
                <div class="modal fade" tabindex="-1" id="addFile" data-bs-backdrop="static">
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 v-if="modal_upload == 1" class="modal-title">Upload Attachment RFQ or Email Request</h3>
                        <h3 v-if="modal_upload == 2" class="modal-title">Upload Attachment Workscope</h3>
                        <h3 v-if="modal_upload == 3" class="modal-title">Attachment of Financial Assesment Form (optional)</h3>
                        <h3 v-if="modal_upload == 4" class="modal-title">Attachment of Maintenance Proposal for Customer</h3>
                        <h3 v-if="modal_upload == 5" class="modal-title">Attachment of Profitability Analysis Form Signed</h3>
                        <h3 v-if="modal_upload == 6" class="modal-title">Attachment of Customer Approval (SOW Signed / Proposal Approved)</h3>
                        <h3 v-if="modal_upload == 7" class="modal-title">Attachment of WO/PO number customer document</h3>

                        <!--begin::Close-->
                        <div class="btn btn-icon btn-sm btn-active-light-primary ms-2" data-bs-dismiss="modal" aria-label="Close">
                          <span class="svg-icon svg-icon-1" @click="closeModalFile()">
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
                            <input type="file"
                            @change="attachFile()" 
                            id="files" 
                            ref="files" 
                            class="form-control" multiple  
                            style="height: 200px; "
                            :class="{
                              'is-invalid': errors.files,
                            }"
                            />
                            <span v-if="errors.files" class="error invalid-feedback">{{
                              errors.files[0]
                            }}</span>
                          </div>
                          <div class="row mt-10">
                            <div class="col d-flex justify-content-end">
                              <button type="button" class="btn btn-light mx-2" data-bs-dismiss="modal" id="close_modal_file" @click="closeModalFile()">
                                Close
                              </button>
                              <button type="button" @click="submitFile()" v-permission="['upload_files']" class="btn btn-primary">Save</button>
                            </div>
                          </div>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Modal slotRequest -->
                <div class="modal fade" tabindex="-1" id="slotRequest" data-bs-backdrop="static">
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 class="modal-title">Request Hangar Slot to CBO</h3>
                        <!--begin::Close-->
                        <div class="btn btn-icon btn-sm btn-active-light-primary ms-2" data-bs-dismiss="modal" aria-label="Close">
                          <span class="svg-icon svg-icon-1" @click="closeRequestSlot()">
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
                              <option :value="null" disabled>Select User</option>
                              <option 
                              v-for="user_options in user_option" 
                              v-if="user_options.role_id === 4"
                              :value="user_options.id"
                              >
                                {{ user_options.name }} - {{ user_options.email }}
                              </option>
                            </select>
                            <small class="text-muted">Send notification to selected employee</small>
                          </div>
                          <div class="mb-3">
                            <label>Hangar <span class="text-danger">*</span></label>
                            <input type="text" class="form-control form-control-solid" v-model="sales_detail.location.id" readonly/>
                          </div>
                          <div class="form-group mb-3">
                            <label for="">Line <span class="text-danger">*</span></label>
                            <select v-model="line_id" class="form-select">
                              <option :value="null" disabled>Select Line</option>
                              <option 
                              v-for="lines in line" 
                              v-if="lines.hangar_id === sales_detail.location.id"
                              :value="lines.id"
                              >
                                {{ lines.name }}
                              </option>
                            </select>
                            <span v-if="errors.lines" class="error invalid-feedback">{{
                              errors.lines[0]
                            }}</span>
                          </div>
                          <div class="row mt-10">
                            <div class="col d-flex justify-content-end">
                              <button type="button" class="btn btn-danger btn-sm mx-2" data-bs-dismiss="modal" id="close_modal_slot" @click="closeRequestSlot()">
                                Discard
                              </button>
                              <button type="button" @click="slotRequest()" class="btn btn-primary btn-sm">Send</button>
                            </div>
                          </div>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Modal notifyUpgrade -->
                <div class="modal fade" tabindex="-1" id="notifyUpgrade" data-bs-backdrop="static">
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 class="modal-title">Notify Request to Upgrade</h3>
                        <!--begin::Close-->
                        <div class="btn btn-icon btn-sm btn-active-light-primary ms-2" data-bs-dismiss="modal" aria-label="Close">
                          <span class="svg-icon svg-icon-1" @click="closeNotifyLevel()">
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
                            <select v-model="user_id" class="form-select">
                              <option :value="null" disabled>Select User</option>
                              <option 
                              v-for="user_options in user_option" 
                              v-if="user_options.role_id === 3"
                              :value="user_options.id"
                              >
                                {{ user_options.name }} - {{ user_options.email }}
                              </option>
                            </select>
                            <small class="text-muted">Send notification to selected employee</small>
                          </div>
                          <div class="row mt-10">
                            <div class="col d-flex justify-content-end">
                              <button type="button" class="btn btn-danger btn-sm mx-2" data-bs-dismiss="modal" id="close_modal_notify" @click="closeNotifyLevel()">
                                Discard
                              </button>
                              <button type="button" @click="notifyUpgrade()" class="btn btn-primary btn-sm">Send</button>
                            </div>
                          </div>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Modal notifyCOGS -->
                <div class="modal fade" tabindex="-1" id="notifyCOGS" data-bs-backdrop="static">
                  <div class="modal-dialog modal-dialog-centered">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h3 class="modal-title">Notify to COGS</h3>
                        <!--begin::Close-->
                        <div class="btn btn-icon btn-sm btn-active-light-primary ms-2" data-bs-dismiss="modal" aria-label="Close">
                          <span class="svg-icon svg-icon-1" @click="closeNotifyCOGS()">
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
                              <option :value="null" disabled>Select User</option>
                              <option 
                              v-for="user_options in user_option" 
                              v-if="user_options.role_id === 4"
                              :value="user_options.id"
                              >
                                {{ user_options.name }} - {{ user_options.email }}
                              </option>
                            </select>
                            <small class="text-muted">Send notification to selected employee</small>
                          </div>
                          <div class="row mt-10">
                            <div class="col d-flex justify-content-end">
                              <button type="button" class="btn btn-danger btn-sm mx-2" data-bs-dismiss="modal" id="close_modal_cogs" @click="closeNotifyCOGS()">
                                Discard
                              </button>
                              <button type="button" @click="notifyCOGS()" class="btn btn-primary btn-sm">Send</button>
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
      user: this.$auth.user.user.name,
      role: this.$auth.user.user.role.name,
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
      reason: null,
      file_histories: [],
      errors: {
        name: null,
        phone: null,
        email: null,
        address: null,
        title: null,
        status: null,
        files: null,
        so_number: null,
        maintenance_id: null,
        acreg: null,
        tat: null,
        location: null,
        value: null,
        category: null,
        reason: null,
      },
    }
  },
  mounted() {
    KTStepper.getInstance()
    KTFormRepeaterBasic.init()
    this.step()
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
      let val = (value/1).toFixed(0).replace(',', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
    },
    step() {
      var element = document.querySelector("#kt_stepper_example_basic");
      var stepper = new KTStepper(element);
      stepper.on("kt.stepper.next", function (stepper) {
          stepper.goNext(); 
      });
      stepper.on("kt.stepper.previous", function (stepper) {
          stepper.goPrevious(); 
      });
    },
    attachFile() {
      this.files = this.$refs.files.files;
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
    listDetail() {
      this.$axios
      .get(`api/sales-show/${this.$route.query.id}`)
      .then((response) => {
        this.sales_detail = response.data.data.salesDetail
        this.level4 = response.data.data.level4
        this.level3 = response.data.data.level3
        this.level2 = response.data.data.level2
        this.level1 = response.data.data.level1
        Swal.close()
      })
      .catch((error) => {
        if (error.response.status == 404) {
          toastr.error(error.response.data.message)
          this.$router.push({
            name: 'my-salesplan'
          });
        } 
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
      .get(`api/file/`)
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
        }
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
      .get(`api/ams/`)
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
      .get(`api/line/`)
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
      .get(`api/users/`)
      .then((response) => {
        this.user_option = response.data.data.data
        console.log(this.user_option)
        Swal.close()
      })
      .catch((error) => console.log(error))
    },

    swtichAMS() {
      this.loading()
      this.$axios
      .put(`api/sales-switch-ams/${this.$route.query.id}`, {
        ams_id: this.ams_id
      })
      .then((response) => {
        toastr.success(response.data.message)
        this.$router.push({
          name: 'my-salesplan'
        });
      })
      .catch((error) => {
        if (error.response.status == 422) {
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
        confirmButtonText: 'Yes, Update SO Number!',
      })
      .then((result) => {
        if (result.isConfirmed) {
          this.$axios
          .put(`/api/sales-so-number/${this.$route.query.id}`, {
            sales_id: this.$route.query.id,
            so_number: this.sales_detail.so_number,
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
          this.errors = error.response.data.errors
          toastr.error(error.response.data.message)
        } else if (error.response.status == 403) {
          toastr.error(error.response.data.message)
        }
      })
    },
    slotConfirm() {
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
          .put(`api/sales-slot-confirm/${this.$route.query.id}`, {
            sales_id: this.$route.query.id,
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
        .put(`/api/sales-update/${this.$route.query.id}`, {
          sales_id: this.$route.query.id,
          maintenance_id: this.maintenance_id,
          hangar_id: this.hangar_id,
          acReg: this.sales_detail.acReg,
          tat: this.sales_detail.tat,
          totalSales: this.sales_detail.totalSales,
          start_date: this.sales_detail.start_date,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.listDetail()
          this.clearFormEditSales()
          this.closeModalEditSales()
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
        confirmButtonText: 'Yes, upgrade level!',
      })
      .then((result) => {
        if (result.isConfirmed) {
          this.$axios
          .put(`api/sales-reschedule/${this.$route.query.id}`, {
            sales_id: this.$route.query.id,
            hangar_id: this.sales_detail.location.id,
            current_date: this.current_date,
            start_date: this.sales_detail.start_date,
            tat: this.sales_detail.tat,
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
    salesCancel() {
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
          .put(`api/sales-reject/${this.$route.query.id}`, {
            sales_id: this.$route.query.id,
            category: this.category,
            reason: this.reason,
          })
          .then((response) => {
            toastr.success(response.data.message)
            this.$router.push({
              name: 'my-salesplan'
            });
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
        .post(`api/sales-request-cogs/`, {
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
        .post(`api/sales-request-upgrade/`, {
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
          } else if (error.response.status == 403) {
            toastr.error(error.response.data.message)
          }
        })
    },
    slotRequest() {
      this.loading()
      this.$axios
      .post(`api/sales-slot-request/`, {
        sales_id: this.$route.query.id,
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
          toastr.error(error.response.data.message)
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
              name: 'my-salesplan'
            });
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
      let formData = new FormData();
      for( var i = 0; i < this.files.length; i++ ){
        let file = this.files[i];
        formData.append('files[' + i + ']', file);  
      }
      formData.append('sales_id', this.sales_detail.id);
      formData.append('requirement_id', this.sequence);
      this.$axios
        .post('/api/file-create', 
        formData, 
        {
          headers: {
            'Content-Type': 'multipart/form-data'
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
            this.errors = error.response.data.errors
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
          this.$axios.delete('/api/file-delete/' + id)
        .then((response) => {
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
    addFile1() {
      this.sequence = 2
      this.modal_upload = 1
    },
    addFile2() {
      this.sequence = 3
      this.modal_upload = 2
    },
    addFile3() {
      this.sequence = 4
      this.modal_upload = 3 
    }, 
    addFile4() {
      this.sequence = 5
      this.modal_upload = 4 
    },
    addFile5() {
      this.sequence = 6
      this.modal_upload = 5 
    },
    addFile6() {
      this.sequence = 7
      this.modal_upload = 6 
    },
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
              this.$axios.delete('/api/contact-person-delete/' + id, {
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
      this.$refs.files.value = null;
      this.errors.files = null
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

    clearFormEditSales(){
      this.maintenance_id = null
      this.hangar_id = null
      this.sales_detail.acreg = null
      this.sales_detail.tat = null
      this.sales_detail.value = null
      this.sales_detail.start_date = null
      
      this.errors.maintenance_id = null
      this.errors.hangar_id = null
      this.errors.acreg = null
      this.errors.tat = null
      this.errors.value = null
      this.errors.start_date = null
    },
    closeModalEditSales() {
      document.getElementById('close_modal_edit_sales').click()
      this.clearFormEditSales()
    },

    clearFormRequestSlot() {
      this.user_id = null
      this.line_id = null
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
  }
}
</script>
<style>
.mt-20 {
  margin-top: 20px;
}
.mb-20 {
  margin-bottom: 20px;
}
#readOnly {
  background-color:#f0f0f5;
}

#heightContact {
  height: 35px
}

#cardTop {
  width: 218px;
}

#cardMarketShare {
  border: dotted #04C8C8; 
  border-radius: 10px; 
  padding-top: 10px;
}

#cardSalesPlan {
  border: dotted #50CD89; 
  border-radius: 10px; 
  padding-top: 10px;
}

#cardDevisiasi {
  border: dotted #F1416C; 
  border-radius: 10px; 
  padding-top: 10px;
}

#textMarketShare {
  color: #04C8C8;
}

#textSalesPlan {
  color: #50CD89;
}

#textDevisiasi {
  color: #F1416C;
}

#textSync {
  background-color: #F1E0D0; 
  color: #955F2D;
  margin-left: 10px;
}

#textWaiting {
  background-color: #F1E0D0; 
  color: #955F2D;
}

#textApproved {
  background-color: #2146C7; 
  color: #fff;
}

#bodyAMS {
  background: #F1F5F9; 
  padding: 10px;
  border-radius: 8px
}

#myBorder {
  border:dashed #CDE7FE;
}
</style>  