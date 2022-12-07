<template>
    <div>
        <div class="container-fluid mt-10 mb-20">
            <div class="row">
                <div class="col-lg-6">
                    <Nuxt-link class="menu-link" to="/my-salesplan" active-class="active">
                        <i class="fa-solid fa-angle-left"></i>
                        <span
                        class="menu-title"
                        v-if="role == 'TPR' || role == 'CBO' || role == 'Administrator'"
                        >Sales Plan</span
                        >
                        <span class="menu-title" v-if="role == 'AMS'">Sales Plan</span>
                    </Nuxt-link>
                </div>
            </div>
            <!-- Head Salesplan Table -->
            <div class="row">
                <div class="col-lg-6 col-sm-12">
                    <h3 class="mt-5">Sales Plan Table</h3>
                </div>
                <div class="col-lg-6 col-sm-12 d-flex justify-content-end">
                <button
                    type="button"
                    class="btn btn-info btn-sm my-3 me-2"
                    data-bs-toggle="modal"
                    data-bs-target="#filterdate"
                >
                    Filter Data <i class="fa-solid fa-chevron-down"></i>
                </button>
                <button
                    class="btn btn-primary btn-sm my-3"
                    data-bs-toggle="modal"
                    data-bs-target="#addSales"
                    v-if="role == 'AMS' || role == 'Administrator'"
                >
                    <i class="fas fa-plus"></i> Additional Sales Plan
                </button>
                </div>
            </div>

            <!-- Modal filter data  -->
            <div
                class="modal fade"
                id="filterdate"
                tabindex="-1"
                aria-labelledby="filterdateLabel"
                aria-hidden="true"
            >
                <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header text-center">
                    <h1 class="modal-title w-100" id="filterdateLabel">
                        Filter Data
                    </h1>
                    <button
                        type="button"
                        class="btn-close"
                        data-bs-dismiss="modal"
                        aria-label="Close"
                        @click="closeModal()"
                    ></button>
                    </div>
                    <form>
                    <div class="modal-body">
                        <div class="row">
                          <div class="col-lg-12">
                              <div class="mb-3">
                              <label for="" class="form-label">Form Date</label>
                              <input
                                  type="date"
                                  class="form-control"
                                  v-model="start_date"
                              />
                              </div>
                          </div>
                        </div>
                        <div class="row">
                          <div class="col-lg-12">
                            <div class="mb-3">
                            <label for="" class="form-label">To Date</label>
                            <input
                                type="date"
                                class="form-control"
                                v-model="end_date"
                            />
                            </div>
                          </div>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <div class="col-md-12 text-center">
                        <button
                            type="button"
                            class="btn btn-light mx-3"
                            data-bs-dismiss="modal"
                            @click="closeModal()"
                        >
                            Reset
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary"
                            data-bs-dismiss="modal"
                            @click="listTable()"
                        >
                            Filter
                        </button>
                        </div>
                    </div>
                    </form>
                </div>
                </div>
            </div>

            <!-- Modal addSales  -->
            <div
                class="modal fade"
                id="addSales"
                tabindex="-1"
                aria-labelledby="addSalesLabel"
                aria-hidden="true"
            >
                <div class="modal-dialog modal-lg">
                  <div class="modal-content">
                      <div class="modal-header">
                      <h1 class="modal-title" id="addSalesLabel">
                          Additional Sales Plan
                      </h1>
                      <!--begin::Close-->
                      <div
                          class="btn btn-icon btn-sm btn-active-light-primary ms-2"
                          data-bs-dismiss="modal"
                          aria-label="Close"
                      >
                          <span class="svg-icon svg-icon-1" @click="closeAddSales()">
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
                          <div class="row">
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">Customer</label>
                                  <multiselect v-model="customer_id" :options="customer_option" placeholder="Select Customer" label="name"></multiselect>
                                  <span
                                  v-if="errors.customer_id"
                                  class="error invalid-feedback"
                                  >{{ errors.customer_id[0] }}</span
                                  >
                              </div>
                            </div>
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">Product</label>
                                  <multiselect v-model="product_id" :options="product_option" placeholder="Select Product" label="name"></multiselect>
                                  <span
                                  v-if="errors.product_id"
                                  class="error invalid-feedback"
                                  >{{ errors.product_id[0] }}</span
                                  >
                              </div>
                            </div>
                          </div>

                          <div class="row">
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">Maintenance</label>
                                  <multiselect v-model="maintenance_id" :options="maintenance_option" placeholder="Select Maintenance" label="name"></multiselect>
                                  <span
                                  v-if="errors.maintenance_id"
                                  class="error invalid-feedback"
                                  >{{ errors.maintenance_id[0] }}</span
                                  >
                              </div>
                            </div>
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">Hangar</label>
                                  <multiselect v-model="hangar_id" :options="hangar_option" placeholder="Select Hangar" label="name"></multiselect>
                                  <span
                                  v-if="errors.hangar_id"
                                  class="error invalid-feedback"
                                  >{{ errors.hangar_id[0] }}</span
                                  >
                              </div>
                            </div>
                          </div>

                          <!-- Input ketika pilih N/A -->
                          <div class="row" v-if="maintenance_id">
                            <div class="col-lg-6" v-if="maintenance_id.id == 1">
                              <div class="mb-3">
                                <label class="form-label fw-bold">Remarks</label>
                                <input type="text" v-model="remarks" class="form-control">
                                <span
                                  v-if="errors.remarks"
                                  class="error invalid-feedback"
                                  >{{ errors.remarks[0] }}</span
                                  >
                              </div>
                            </div>
                          </div>

                          <div class="row">
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">Aircraft Type</label>
                                  <multiselect v-model="ac_type_id" :options="ac_type_option" placeholder="Select Aircraft Type" label="name"></multiselect>
                                  <span
                                  v-if="errors.ac_type_id"
                                  class="error invalid-feedback"
                                  >{{ errors.ac_type_id[0] }}</span
                                  >
                              </div>
                            </div>
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">Aircraft Registration</label>
                                  <input
                                    required
                                    type="text"
                                    v-model="ac_reg"
                                    class="form-control"
                                    :class="{ 'is-invalid': errors.ac_reg }"
                                  />
                                  <span v-if="errors.ac_reg" class="error invalid-feedback">{{
                                  errors.ac_reg[0]
                                  }}</span>
                              </div>
                            </div>
                          </div>

                          <div class="row">
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">Sales Plan</label>
                                  <input
                                    required
                                    type="number"
                                    v-model="value"
                                    class="form-control"
                                    :class="{ 'is-invalid': errors.value }"
                                  />
                                  <span v-if="errors.value" class="error invalid-feedback">{{
                                  errors.value[0]
                                  }}</span>
                              </div>
                            </div>
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">Start Date</label>
                                  <input
                                    required
                                    type="date"
                                    v-model="start_date"
                                    class="form-control"
                                    :class="{ 'is-invalid': errors.start_date }"
                                  />
                                  <span
                                  v-if="errors.start_date"
                                  class="error invalid-feedback"
                                  >{{ errors.start_date[0] }}</span
                                  >
                              </div>
                            </div>
                          </div>

                          <div class="row">
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">TAT</label>
                                  <input
                                  required
                                  type="number"
                                  v-model="tat"
                                  class="form-control"
                                  :class="{ 'is-invalid': errors.tat }"
                                  />
                                  <span v-if="errors.tat" class="error invalid-feedback">{{
                                  errors.tat[0]
                                  }}</span>
                              </div>
                            </div>
                            <div class="col-lg-6">
                              <div class="form-group mb-3">
                                  <label class="form-label fw-bold">Type</label>
                                  <multiselect v-model="transaction_type_id" :options="transaction_type_option" placeholder="Select Type" label="name"></multiselect>
                                  <span v-if="errors.transaction_type_id" class="error invalid-feedback">{{
                                  errors.transaction_type_id[0]
                                  }}</span>
                              </div>
                            </div>
                          </div>

                          <div class="row mt-10">
                              <div class="col">
                                <button
                                    type="button"
                                    class="btn btn-light"
                                    data-bs-dismiss="modal"
                                    @click="closeAddSales()"
                                    id="close_modal"
                                >
                                    Back
                                </button>
                              </div>
                              <div class="col d-flex justify-content-end">
                                <button
                                    type="button"
                                    @click="addSales()"
                                    class="btn btn-primary"
                                >
                                    Save
                                </button>
                              </div>
                          </div>
                      </div>
                  </div>
                </div>
            </div>

            <!-- Row Table -->
            <div class="row mt-3">
                <div class="card">
                <div class="card-body">
                    <!-- Search -->
                    <div class="row d-flex align-items-center mb-5">
                        <div class="col-11">
                          <div class="row">
                            <span
                          class="
                              svg-icon svg-icon-3 svg-icon-gray-500
                              position-absolute
                              top-50
                              translate-middle
                              ms-6
                          "
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
                              x="17.0365"
                              y="15.1223"
                              width="8.15546"
                              height="2"
                              rx="1"
                              transform="rotate(45 17.0365 15.1223)"
                              fill="currentColor"
                              ></rect>
                              <path
                              d="M11 19C6.55556 19 3 15.4444 3 11C3 6.55556 6.55556 3 11 3C15.4444 3 19 6.55556 19 11C19 15.4444 15.4444 19 11 19ZM11 5C7.53333 5 5 7.53333 5 11C5 14.4667 7.53333 17 11 17C14.4667 17 17 14.4667 17 11C17 7.53333 14.4667 5 11 5Z"
                              fill="currentColor"
                              ></path>
                          </svg>
                          </span>
                          <input
                          type="text"
                          class="form-control form-control-solid ps-10"
                          name="search"
                          v-model="search"
                          placeholder="Search"
                          />
                          </div>
                        </div>
                        <div class="col">
                          <button class="btn btn-danger btn-sm" @click="removeSearch()">Clear</button>
                        </div>
                    </div>
                    <!-- Table -->
                    <div class="table-responsive">
                    <table class="table table-row-bordered table-row-gray-200 gy-4">
                        <thead>
                        <tr class="fw-bold fs-6 text-gray-800 table-secondary">
                            <th class="text-center"><p>No</p></th>
                            <!-- Start customer sorting -->
                            <th
                            v-if="order == 'customer' && by == 'asc'"
                            @click="sort('customer', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                CUSTOMER
                                <i
                                class="fa-solid fa-sort-up ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else-if="order == 'customer' && by == 'desc'"
                            @click="sort('id', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                CUSTOMER
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else
                            @click="sort('customer', 'asc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                CUSTOMER
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End customer sorting -->

                            <!-- Start product sorting -->
                            <th
                            v-if="order == 'product' && by == 'asc'"
                            @click="sort('product', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                PRODUCT
                                <i
                                class="fa-solid fa-sort-up ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else-if="order == 'product' && by == 'desc'"
                            @click="sort('id', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                PRODUCT
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else
                            @click="sort('product', 'asc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                PRODUCT
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End product sorting -->

                            <!-- Start registration sorting -->
                            <th
                            v-if="order == 'registration' && by == 'asc'"
                            @click="sort('registration', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                AC/ENG/APU/COMP
                                <i
                                class="fa-solid fa-sort-up ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else-if="order == 'registration' && by == 'desc'"
                            @click="sort('id', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                AC/ENG/APU/COMP
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else
                            @click="sort('registration', 'asc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                AC/ENG/APU/COMP
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End registration sorting -->

                            <!-- Start acReg sorting -->
                            <th
                            v-if="order == 'acReg' && by == 'asc'"
                            @click="sort('acReg', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                REGISTRATION
                                <i
                                class="fa-solid fa-sort-up ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else-if="order == 'acReg' && by == 'desc'"
                            @click="sort('id', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                REGISTRATION
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else
                            @click="sort('acReg', 'asc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                REGISTRATION
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End acReg sorting -->

                            <!-- Start other sorting -->
                            <th
                            v-if="order == 'other' && by == 'asc'"
                            @click="sort('other', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Sales Type
                                <i
                                class="fa-solid fa-sort-up ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else-if="order == 'other' && by == 'desc'"
                            @click="sort('id', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Sales Type
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else
                            @click="sort('other', 'asc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Sales Type
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End other sorting -->

                            <!-- Start type sorting -->
                            <th
                            v-if="order == 'type' && by == 'asc'"
                            @click="sort('type', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Type
                                <i
                                class="fa-solid fa-sort-up ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else-if="order == 'type' && by == 'desc'"
                            @click="sort('id', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Type
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th v-else @click="sort('type', 'asc')" class="text-center" 
                            style="white-space: nowrap;">
                            <p class="d-flex justify-content-center">
                                Type
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End type sorting -->

                            <!-- Start level sorting -->
                            <th
                            v-if="order == 'level' && by == 'asc'"
                            @click="sort('level', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Level
                                <i
                                class="fa-solid fa-sort-up ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else-if="order == 'level' && by == 'desc'"
                            @click="sort('id', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Level
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else
                            @click="sort('level', 'asc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Level
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End level sorting -->

                            <!-- Start progress sorting -->
                            <th
                            v-if="order == 'progress' && by == 'asc'"
                            @click="sort('progress', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Progress
                                <i
                                class="fa-solid fa-sort-up ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else-if="order == 'progress' && by == 'desc'"
                            @click="sort('id', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Progress
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else
                            @click="sort('progress', 'asc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                Progress
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End progress sorting -->

                            <!-- Start status sorting -->
                            <th
                            v-if="order == 'status' && by == 'asc'"
                            @click="sort('status', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                STATUS
                                <i
                                class="fa-solid fa-sort-up ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else-if="order == 'status' && by == 'desc'"
                            @click="sort('id', 'desc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                STATUS
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th
                            v-else
                            @click="sort('status', 'asc')"
                            class="text-center"
                            style="white-space: nowrap;"
                            >
                            <p class="d-flex justify-content-center">
                                STATUS
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End progress sorting -->
                            <th class="text-center" style="white-space: nowrap;"><p>ACTION</p></th>
                        </tr>
                        </thead>
                          <tr class="text-center">
                            <td></td>
                            <td>
                              <select v-model="customer" class="form-select">
                                <option v-for="customer_options in customer_option" :value="customer_options.id">
                                  {{ customer_options.name }} 
                                </option>
                              </select>
                            </td>
                            <td>
                              <select v-model="product" class="form-select">
                                <option v-for="product_options in product_option" :value="product_options.id">
                                  {{ product_options.name }} 
                                </option>
                              </select>
                            </td>
                            <td>
                              <div class="row">
                                <div class="col-lg">
                                  <select v-model="ac_type_id" class="form-select">
                                    <option :value="null" disabled>AC</option>
                                    <option v-for="ac_type_options in ac_type_option" :value="ac_type_options.id">
                                      {{ ac_type_options.name }} 
                                    </option>
                                  </select>
                                </div>
                                <div class="col-lg">
                                  <select v-model="engine_id" class="form-select">
                                    <option :value="null" disabled>ENG</option>
                                    <option v-for="engine_options in engine_option" :value="engine_options.id">
                                      {{ engine_options.name }} 
                                    </option>
                                  </select>
                                </div>
                                <div class="col-lg">
                                  <select v-model="apu_id" class="form-select">
                                    <option :value="null" disabled>APU</option>
                                    <option v-for="apu_options in apu_option" :value="apu_options.id">
                                      {{ apu_options.name }} 
                                    </option>
                                  </select>
                                </div>
                                <div class="col-lg">
                                  <select v-model="component_id" class="form-select">
                                    <option :value="null" disabled>COMP</option>
                                    <option v-for="component_options in component_option" :value="component_options.id">
                                      {{ component_options.name }} 
                                    </option>
                                  </select>
                                </div>
                              </div>
                            </td>
                            <td>
                              <select v-model="acReg" class="form-select">
                                <option v-for="registration_options in registration_option" :value="registration_options">
                                  {{ registration_options }} 
                                </option>
                              </select>
                            </td>
                            <td>
                              <select v-model="other" class="form-select">
                                <option :value="1">RKAP</option>
                                <option :value="0">Additional</option>
                              </select>
                            </td>
                            <td>
                              <select v-model="type" class="form-select">
                                <option :value="1">TMB Retail</option>
                                <option :value="2">TMB Project</option>
                                <option :value="3">PBTH</option>
                              </select>
                            </td>
                            <td>
                              <select v-model="level" class="form-select">
                                <option :value="1">Level 1</option>
                                <option :value="2">Level 2</option>
                                <option :value="3">Level 3</option>
                                <option :value="4">Level 4</option>
                              </select>
                            </td>
                            <td>
                              <select v-model="progress" class="form-select">
                                <option :value="1">10 %</option>
                                <option :value="2">20 %</option>
                                <option :value="3">30 %</option>
                                <option :value="4">40 %</option>
                                <option :value="5">50 %</option>
                                <option :value="6">60 %</option>
                                <option :value="7">70 %</option>
                                <option :value="8">80 %</option>
                                <option :value="9">90 %</option>
                                <option :value="10">100 %</option>
                              </select>
                            </td>
                            <td>
                              <select v-model="status" class="form-select">
                                <option :value="1">Open</option>
                                <option :value="3">Close In</option>
                                <option :value="2">Closed</option>
                                <option :value="4">Cancel</option>
                              </select>
                            </td>
                            <td>
                              <button
                                  type="button"
                                  class="btn btn-light mx-3"
                                  @click="closeModal()"
                                  data-bs-toggle="tooltip" data-bs-placement="top" title="Reset Filter"
                              >
                                  <i class="fa-solid fa-rotate-left"></i>
                              </button>
                              <button
                                  type="button"
                                  class="btn btn-primary"
                                  @click="listTable()"
                                  data-bs-toggle="tooltip" data-bs-placement="top" title="Filter Data"
                              >
                                  <i class="fa-solid fa-magnifying-glass"></i>
                              </button>
                            </td>
                          </tr>
                        <tbody>
                        <tr
                            v-for="(p_sales, p_sales_index) in sales_table.data"
                            :key="p_sales_index"
                        >
                            <td class="text-center">
                            {{ sales_paginate.from + p_sales_index }}.
                            </td>
                            <!-- Customer -->
                            <td class="text-center">
                            {{ p_sales.customer }}
                            </td>
                            <!-- Product -->
                            <td class="text-center" v-if="p_sales.type == 'PBTH'">
                            {{ p_sales.product }} - {{ p_sales.month }}
                            </td>
                            <td class="text-center" v-else>
                            {{ p_sales.product }}
                            </td>
                            <!-- AC/ENG/APU/COMP -->
                            <td class="text-center">
                            {{ p_sales.registration }}
                            </td>
                            <!-- REGISTRATION -->
                            <td class="text-center">
                            {{ p_sales.acReg }}
                            </td>
                            <!-- Other -->
                            <td class="text-center">
                              <div v-if="p_sales.other === 'RKAP'">
                                  <b>{{
                                  p_sales.other
                                  }}</b>
                              </div>
                              <div v-if="p_sales.other === 'Additional'">
                                  <b>{{
                                  p_sales.other
                                  }}</b>
                              </div>
                            </td>
                            <!-- Type -->
                            <td class="text-center">
                              <div v-if="p_sales.type === 'TMB Retail'">
                                  <b style="white-space: nowrap;">{{
                                  p_sales.type
                                  }}</b>
                              </div>
                              <div v-if="p_sales.type === 'TMB Project'">
                                  <b style="white-space: nowrap;">{{
                                  p_sales.type
                                  }}</b>
                              </div>
                              <div v-if="p_sales.type === 'PBTH'">
                                  <b>{{
                                  p_sales.type
                                  }}</b>
                              </div>
                            </td>
                            <!-- Sales Level -->
                            <td class="text-center">
                            <div v-if="p_sales.level === 1">
                                <span class="badge badge-success">Level 1</span>
                            </div>
                            <div v-if="p_sales.level === 2">
                                <span class="badge badge-warning">Level 2</span>
                            </div>
                            <div v-if="p_sales.level === 3">
                                <span class="badge badge-primary">Level 3</span>
                            </div>
                            <div v-if="p_sales.level === 4">
                                <span class="badge badge-danger">Level 4</span>
                            </div>
                            </td>
                            <!-- Progress -->
                            <td class="text-center">
                            <div v-if="p_sales.progress === 10">
                                <span class="badge badge-danger"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 20">
                                <span class="badge badge-danger"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 30">
                                <span class="badge badge-danger"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 40">
                                <span class="badge badge-primary"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 50">
                                <span class="badge badge-primary"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 60">
                                <span class="badge badge-primary"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 70">
                                <span class="badge badge-warning"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 80">
                                <span class="badge badge-warning"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 90">
                                <span class="badge badge-warning"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 100">
                                <span class="badge badge-success"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            </td>
                            <!-- Status -->
                            <td class="text-center">
                            <div v-if="p_sales.status === 'Cancel'">
                                <span class="badge badge-danger">{{
                                p_sales.status
                                }}</span>
                            </div>
                            <div v-if="p_sales.status === 'Open'">
                                <span class="badge badge-gmf">{{
                                p_sales.status
                                }}</span>
                            </div>
                            <div v-if="p_sales.status === 'Close in'">
                                <span class="badge badge-success">{{
                                p_sales.status
                                }}</span>
                            </div>
                            <div v-if="p_sales.status === 'Closed'">
                                <span class="badge badge-green">
                                Closed Sales
                                </span>
                            </div>
                            </td>
                            <td class="text-center">
                            <nuxt-link
                                v-if="p_sales"
                                :to="{
                                path: '/my-salesplan-detail',
                                query: { id: p_sales.id },
                                }"
                            >
                                <span class="menu-title">Detail</span>
                            </nuxt-link>
                            </td>
                        </tr>
                        <!-- Jika data kosong -->
                        <tr v-if="sales_table.data.length < 1">
                            <td colspan="12">
                            <div class="text-muted text-center">Data not found</div>
                            </td>
                        </tr>
                        </tbody>
                    </table>
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
                                @change="listTable()"
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
                    <div
                        class="
                        col col-lg-8
                        d-flex
                        justify-content-end
                        align-items-center
                        "
                    >
                        <nav aria-label="Page navigation example">
                        <ul class="pagination">
                            <!-- Start pagination -->
                            <li
                            v-for="(link, link_index) in sales_table.links"
                            :key="link_index"
                            class="page-item"
                            :class="{ disabled: !link.url, active: link.active }"
                            >
                            <a
                                href="javascript:void(0)"
                                @click="listTable(link.url)"
                                class="page-link"
                            >
                                <span v-if="link.label == '&laquo; Previous'">
                                <i class="fa-solid fa-caret-left"></i>
                                </span>
                                <span v-else-if="link.label == 'Next &raquo;'">
                                <i class="fa-solid fa-caret-right"></i>
                                </span>
                                <span v-else>
                                {{ link.label }}
                                </span>
                            </a>
                            </li>
                            <!-- End pagination -->
                        </ul>
                        </nav>
                    </div>
                    </div>
                </div>
                </div>
            </div>
            <!-- End Table -->
        </div>
    </div>
</template>

<script>
import debounce from 'lodash/debounce'
export default {
  layout: 'template',
  name: 'MySalesPlanTablePage',
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
      search: this.$cookies.get('search'),

      maintenance_option: [],
      product_option: [],
      customer_option: [],
      hangar_option: [],
      ac_type_option: [],
      component_option: [],
      apu_option: [],
      engine_option: [],
      registration_option: [],

      transaction_type_option: [
        {name: 'TMB Retail', value: 1},
        {name: 'TMB Project', value: 2},
      ],

      sales_type_option: [
        {name: 'RKAP', value: 1},
        {name: 'Additional', value: 2},
      ],

      type_multiselect_option: [
        {name: 'TMB Retail', value: 1},
        {name: 'TMB Project', value: 2},
        {name: 'PBTH', value: 3},
      ],

      level_multiselect_option: [
        {name: 'Level 1', value: 1},
        {name: 'Level 2', value: 2},
        {name: 'Level 3', value: 3},
        {name: 'Level 4', value: 4},
      ],

      progress_multiselect_option: [
        {name: '10%', value: 1},
        {name: '20%', value: 2},
        {name: '30%', value: 3},
        {name: '40%', value: 4},
        {name: '50%', value: 5},
        {name: '60%', value: 6},
        {name: '70%', value: 7},
        {name: '80%', value: 8},
        {name: '90%', value: 9},
        {name: '100%', value: 10},
      ],

      status_multiselect_option: [
        {name: 'Open', value: 1},
        {name: 'Close In', value: 3},
        {name: 'Closed', value: 2},
        {name: 'Cancel', value: 4},
      ],

      ac_reg: null,
      is_rkap: null,
      value: null,
      tat: null,
      customer: this.$cookies.get('customer'),
      product: this.$cookies.get('product'),
      acReg: this.$cookies.get('acReg'),
      other: this.$cookies.get('other'),
      registration: null,
      transaction_type_id: null,
      type: this.$cookies.get('type'),
      level: this.$cookies.get('level'),
      progress: this.$cookies.get('progress'),
      status: this.$cookies.get('status'),
      start_date: this.$cookies.get('start_date'),
      end_date: this.$cookies.get('end_date'),

      ac_type_id: this.$cookies.get('ac_type_id'),
      ac_type_id: null,
      ac_type_value: null,
      engine_id: this.$cookies.get('engine_id'),
      component_id: this.$cookies.get('component_id'),
      apu_id: this.$cookies.get('apu_id'),

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
        remarks: null,
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
    }, 800),
  },
  created() {
    this.listTable()
    this.listCustomer()
    this.listProduct()
    this.listMaintenance()
    this.listHangar()
    this.listACType()
    this.listComponent()
    this.listApu()
    this.listEngine()
    this.listRegistration()
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
    listTable(paginate) {
      this.loading()
      this.runCookie()
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
            ac_type_id: this.ac_type_id,
            component_id: this.component_id,
            apu_id: this.apu_id,
            engine_id: this.engine_id,
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
    removeSearch() {
      this.search = null
      this.$cookies.set('search', this.search, {
        path: '/',
        maxAge: 60 * 60 * 24 * 7
      })
    },
    runCookie() {
      //search
      if(this.search) {
          this.$cookies.set('search', this.search, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('search', this.search, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        }
      if(this.$cookies.get('search')) {
          this.search = this.$cookies.get('search')
        }

      //start date
      if(this.start_date) {
          this.$cookies.set('start_date', this.start_date, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('start_date', this.start_date, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        }
      if(this.$cookies.get('start_date')) {
          this.start_date = this.$cookies.get('start_date')
        }

      //end date
      if(this.end_date) {
          this.$cookies.set('end_date', this.end_date, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('end_date', this.end_date, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('end_date')) {
          this.end_date = this.$cookies.get('end_date')
        }

      //customer
      if(this.customer) {
         this.$cookies.set('customer', this.customer, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('customer', this.customer, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        }
      if(this.$cookies.get('customer')) {
          this.customer = this.$cookies.get('customer')
        }

      //product
      if(this.product) {
         this.$cookies.set('product', this.product, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('product', this.product, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('product')) {
          this.product = this.$cookies.get('product')
        }

      //acReg
      if(this.acReg) {
         this.$cookies.set('acReg', this.acReg, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('acReg', this.acReg, {
             path: '/',
             maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('acReg')) {
          this.acReg = this.$cookies.get('acReg')
        }

      //ac_type_id
      if(this.ac_type_id) {
         this.$cookies.set('ac_type_id', this.ac_type_id, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('ac_type_id', this.ac_type_id, {
             path: '/',
             maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('ac_type_id')) {
          this.ac_type_id = this.$cookies.get('ac_type_id')
        }

      //component_id
      if(this.component_id) {
         this.$cookies.set('component_id', this.component_id, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('component_id', this.component_id, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('component_id')) {
          this.component_id = this.$cookies.get('component_id')
        }

      //apu_id
      if(this.apu_id) {
         this.$cookies.set('apu_id', this.apu_id, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('apu_id', this.apu_id, {
             path: '/',
             maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('apu_id')) {
          this.apu_id = this.$cookies.get('apu_id')
        }

      //engine_id
      if(this.engine_id) {
         this.$cookies.set('engine_id', this.engine_id, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('engine_id', this.engine_id, {
             path: '/',
             maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('engine_id')) {
          this.engine_id = this.$cookies.get('engine_id')
        }

      //other
      if(this.other) {
         this.$cookies.set('other', this.other, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('other', this.other, {
             path: '/',
             maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('other')) {
          this.other = this.$cookies.get('other')
        }

      //type
      if(this.type) {
          this.$cookies.set('type', this.type, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('type', this.type, {
             path: '/',
             maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('type')) {
          this.type = this.$cookies.get('type')
        }

      //progress
      if(this.progress) {
         this.$cookies.set('progress', this.progress, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('progress', this.progress, {
             path: '/',
             maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('progress')) {
          this.progress = this.$cookies.get('progress')
        }

      //status
      if(this.status) {
         this.$cookies.set('status', this.status, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('status', this.status, {
             path: '/',
             maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('status')) {
          this.status = this.$cookies.get('status')
        }

      //level
      if(this.level) {
         this.$cookies.set('level', this.level, {
            path: '/',
            maxAge: 60 * 60 * 24 * 7
          })
        } else {
          this.$cookies.set('level', this.level, {
             path: '/',
             maxAge: 60 * 60 * 24 * 7
           })
        }
      if(this.$cookies.get('level')) {
          this.level = this.$cookies.get('level')
        }
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
    listComponent() {
      this.$axios
        .get('/api/component', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.component_option = response.data.data.data
        })
        .catch((error) => {
          console.log(error)
        })
    },
    listApu() {
      this.$axios
        .get('/api/apu', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.apu_option = response.data.data.data
        })
        .catch((error) => {
          console.log(error)
        })
    },
    listEngine() {
      this.$axios
        .get('/api/engine', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.engine_option = response.data.data.data
        })
        .catch((error) => {
          console.log(error)
        })
    },
    listRegistration() {
      this.$axios
        .get('/api/sales-acreg')
        .then((response) => {
          this.registration_option = response.data.data
        })
        .catch((error) => {
          console.log(error)
        })
    },

    addSales() {
      this.loading()
      this.$axios
        .post(`api/sales-create-tmb`, {
          is_rkap: 0,
          transaction_type_id: this.transaction_type_id.value,
          customer_id: this.customer_id != null ? this.customer_id.id : null,
          product_id: this.product_id != null ? this.product_id.id : null,
          maintenance_id: this.maintenance_id != null ? this.maintenance_id.id : null,
          hangar_id: this.hangar_id != null ? this.hangar_id.id : null,
          ac_type_id: this.ac_type_id != null ? this.ac_type_id.id : null,
          ac_reg: this.ac_reg,
          remarks: this.remarks,
          value: this.value,
          start_date: this.start_date,
          tat: this.tat,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.closeAddSales()
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
      this.$cookies.removeAll()
      this.start_date = null
      this.end_date = null
      this.type = null
      this.customer = null
      this.product = null
      this.acReg = null
      this.ac_type_id = null
      this.component_id = null
      this.apu_id = null
      this.engine_id = null
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
      this.ac_type_id = null
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
      this.remarks = null
      this.hangar_value = null
      this.aircraft_name_value = null
      this.value = null
      this.errors.customer_id = null
      this.errors.product_id = null
      this.errors.hangar_id = null
      this.errors.maintenance_id = null
      this.errors.ac_type_id = null
      this.errors.ac_reg = null
      this.errors.remarks = null
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

#btnDefault {
  cursor: default;
}

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

#cardTopDashed {
  border: dashed #fff;
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
