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
                <div class="modal-dialog modal-lg">
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
                        <div class="col-lg-6">
                            <div class="mb-3">
                            <label for="" class="form-label">Form Date</label>
                            <input
                                type="date"
                                class="form-control"
                                v-model="start_date"
                            />
                            </div>
                        </div>
                        <div class="col-lg-6">
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
                        
                        <!-- Cust, Prod, AC -->
                        <div class="row">
                        <div class="col-lg-4">
                            <div class="mb-3">
                            <label for="" class="form-label">Customer</label>
                            <select v-model="customer" class="form-select">
                                <option :value="null" disabled>Select Customer</option>
                                <option 
                                v-for="customer_options in customer_option" 
                                :value="customer_options.id" 
                                >
                                {{ customer_options.name }}
                                </option>
                            </select>
                            </div>
                        </div>
                        <div class="col-lg-4">
                            <div class="mb-3">
                            <label for="" class="form-label">Product</label>
                            <select v-model="product" class="form-select">
                                <option :value="null" disabled>Select Product</option>
                                <option 
                                v-for="product_options in product_option" 
                                :value="product_options.id" 
                                >
                                {{ product_options.name }}
                                </option>
                            </select>
                            </div>
                        </div>
                        <div class="col-lg-4">
                            <div class="mb-3">
                            <label for="" class="form-label">AC/ENG/APU/COMP</label>
                            <select v-model="registration" class="form-select">
                                <option :value="null" disabled>Select AC/ENG/APU/COMP</option>
                                <!-- <option 
                                v-for="product_options in product_option" 
                                :value="product_options.id" 
                                >
                                {{ product_options.name }}
                                </option> -->
                            </select>
                            </div>
                        </div>
                        </div>

                        <!-- Reg, Sales Type, Type -->
                        <div class="row">
                        <div class="col-lg-4">
                            <div class="mb-3">
                            <label for="" class="form-label">Registration</label>
                            <select v-model="acReg" class="form-select">
                                <option :value="null" disabled>Select Registration</option>
                                <!-- <option 
                                v-for="product_options in product_option" 
                                :value="product_options.id" 
                                >
                                {{ product_options.name }}
                                </option> -->
                            </select>
                            </div>
                        </div>
                        <div class="col-lg-4">
                            <div class="mb-3">
                            <label for="" class="form-label">Sales Type</label>
                            <select v-model="other" class="form-select">
                                <option :value="null" disabled>Select Sales Type</option>
                                <option value="1">RKAP</option>
                                <option value="2">Additional</option>
                            </select>
                            </div>
                        </div>
                        <div class="col-lg-4">
                            <div class="mb-3">
                            <label for="" class="form-label">Type</label>
                            <select v-model="type" class="form-select">
                                <option :value="null" disabled>Select Type</option>
                                <option value="1">TMB Retail</option>
                                <option value="2">TMB Project</option>
                                <option value="3">PBTH</option>
                            </select>
                            </div>
                        </div>
                        </div>

                        <div class="row">
                        <div class="col-lg-4">
                            <div class="mb-3">
                            <label for="" class="form-label">Level</label>
                            <select v-model="level" class="form-select">
                                <option :value="null" disabled>Select Level</option>
                                <option value="1">Level 1</option>
                                <option value="2">Level 2</option>
                                <option value="3">Level 3</option>
                                <option value="4">Level 4</option>
                            </select>
                            </div>
                        </div>
                        <div class="col-lg-4">
                            <div class="mb-3">
                            <label for="" class="form-label">Progress</label>
                            <select v-model="progress" class="form-select">
                                <option :value="null" disabled>Select Progress</option>
                                <option value="1">10 %</option>
                                <option value="2">20 %</option>
                                <option value="3">30 %</option>
                                <option value="4">40 %</option>
                                <option value="5">50 %</option>
                                <option value="6">60 %</option>
                                <option value="7">70 %</option>
                                <option value="8">80 %</option>
                                <option value="9">90 %</option>
                                <option value="10">100 %</option>
                            </select>
                            </div>
                        </div>
                        <div class="col-lg-4">
                            <div class="mb-3">
                            <label for="" class="form-label">Status</label>
                            <select v-model="status" class="form-select">
                                <option :value="null" disabled>Select Status</option>
                                <option value="1">Open</option>
                                <option value="2">Closed</option>
                                <option value="3">Close In</option>
                                <option value="4">Cancel</option>
                            </select>
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
                            <input type="hidden" v-model="is_rkap" value="0" />
                            <label class="form-label fw-bold">Customer</label>
                            <select v-model="customer_id" class="form-select" :class="{ 'is-invalid': errors.customer_id }">
                                <option :value="null" disabled>Select Customer</option>
                                <option 
                                v-for="customer_options in customer_option" 
                                :value="customer_options.id" 
                                :class="{
                                    'is-invalid': errors.customer_id,
                                }"
                                >
                                {{ customer_options.name }}
                                </option>
                            </select>
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
                            <select v-model="product_id" class="form-select" :class="{ 'is-invalid': errors.product_id }">
                                <option :value="null" disabled>Select Product</option>
                                <option 
                                v-for="product_options in product_option" 
                                :value="product_options.id" 
                                :class="{
                                    'is-invalid': errors.product_id,
                                }"
                                >
                                {{ product_options.name }}
                                </option>
                            </select>
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
                            <select v-model="maintenance_id" class="form-select" :class="{ 'is-invalid': errors.maintenance_id }">
                            <option :value="null" disabled>Select maintenance</option>
                            <option 
                                v-for="maintenance_options in maintenance_option" 
                                :value="maintenance_options.id" 
                                :class="{
                                'is-invalid': errors.maintenance_id,
                                }"
                            >
                                {{ maintenance_options.name }}
                            </option>
                            </select>
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
                            <select v-model="hangar_id" class="form-select" :class="{ 'is-invalid': errors.hangar_id }">
                            <option :value="null" disabled>Select Hangar</option>
                            <option 
                                v-for="hangar_options in hangar_option" 
                                :value="hangar_options.id" 
                                :class="{
                                'is-invalid': errors.hangar_id,
                                }"
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
                    </div>

                    <div class="row">
                        <div class="col-lg-6">
                        <div class="form-group mb-3">
                            <label class="form-label fw-bold">Aircraft Type</label>
                            <select v-model="ac_type_id" class="form-select" :class="{ 'is-invalid': errors.ac_type_id }">
                                <option :value="null" disabled>Select Aircraft Type</option>
                                <option 
                                v-for="ac_type_options in ac_type_option" 
                                :value="ac_type_options.id" 
                                :class="{
                                    'is-invalid': errors.ac_type_id,
                                }"
                                >
                                {{ ac_type_options.name }}
                                </option>
                            </select>
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
                            <select v-model="transaction_type_id" class="form-select" :class="{ 'is-invalid': errors.transaction_type_id }">
                            <option :value="null" disabled>Select Type</option>
                            <option value="1">TMB Retail</option>
                            <option value="2">TMB Project</option>
                            <option value="3">PBTH</option>
                            </select>
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
                            type="submit"
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
                    <div class="position-relative me-md-2">
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
                    <!-- Table -->
                    <div class="table-responsive">
                    <table class="table table-row-bordered table-row-gray-200 gy-4">
                        <thead>
                        <tr class="fw-bold fs-6 text-gray-800">
                            <th class="text-center"><p>No</p></th>
                            <!-- Start customer sorting -->
                            <th
                            v-if="order == 'customer' && by == 'asc'"
                            @click="sort('customer', 'desc')"
                            class="text-center"
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
                            style="width: 100%;"
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
                            style="width: 100%;"
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
                            style="width: 100%;"
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
                            >
                            <p class="d-flex justify-content-center">
                                Type
                                <i
                                class="fa-solid fa-sort-down ms-2"
                                style="color: black"
                                ></i>
                            </p>
                            </th>
                            <th v-else @click="sort('type', 'asc')" class="text-center">
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
                            >
                            <p class="d-flex justify-content-center">
                                STATUS
                                <i class="fa-solid fa-sort ms-2"></i>
                            </p>
                            </th>
                            <!-- End progress sorting -->
                            <th class="text-center"><p>ACTION</p></th>
                        </tr>
                        </thead>
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
                                <span class="badge badge-info">{{
                                p_sales.other
                                }}</span>
                            </div>
                            <div v-if="p_sales.other === 'Additional'">
                                <span class="badge badge-primary">{{
                                p_sales.other
                                }}</span>
                            </div>
                            </td>
                            <!-- Type -->
                            <td class="text-center">
                            <div v-if="p_sales.type === 'TMB Retail'">
                                <span class="badge badge-danger">{{
                                p_sales.type
                                }}</span>
                            </div>
                            <div v-if="p_sales.type === 'TMB Project'">
                                <span class="badge badge-primary">{{
                                p_sales.type
                                }}</span>
                            </div>
                            <div v-if="p_sales.type === 'PBTH'">
                                <span class="badge badge-warning">{{
                                p_sales.type
                                }}</span>
                            </div>
                            </td>
                            <!-- Sales Level -->
                            <td class="text-center">
                            <div v-if="p_sales.level === 1">
                                <span class="badge badge-success">Level 1</span>
                            </div>
                            <div v-if="p_sales.level === 2">
                                <span class="badge badge-primary">Level 2</span>
                            </div>
                            <div v-if="p_sales.level === 3">
                                <span class="badge badge-warning">Level 3</span>
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
                                <span class="badge badge-warning"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 50">
                                <span class="badge badge-warning"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 60">
                                <span class="badge badge-warning"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 70">
                                <span class="badge badge-primary"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 80">
                                <span class="badge badge-primary"
                                >{{ p_sales.progress }}%</span
                                >
                            </div>
                            <div v-if="p_sales.progress === 90">
                                <span class="badge badge-success"
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
                                <span class="badge badge-success">{{
                                p_sales.status
                                }}</span>
                            </div>
                            <div v-if="p_sales.status === 'Close in'">
                                <span class="badge badge-warning">{{
                                p_sales.status
                                }}</span>
                            </div>
                            <div v-if="p_sales.status === 'Closed'">
                                <span class="badge badge-primary">{{
                                p_sales.status
                                }}</span>
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

#btnDefault {
  cursor: default;
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