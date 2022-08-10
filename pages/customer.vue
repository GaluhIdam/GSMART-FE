<template>
    <div>
        <div id="kt_app_toolbar" class="app-toolbar py-3 py-lg-6 bg-white">
            <!--begin::Toolbar container-->
            <div id="kt_app_toolbar_container" class="app-container container-fluid d-flex flex-stack">
                <!--begin::Page title-->
                <div class="page-title d-flex flex-column justify-content-center flex-wrap me-3">
                    <!--begin::Title-->
                    <p class="page-heading d-flex text-dark fs-6 flex-column justify-content-center my-0">Customers</p>
                    <!--end::Title-->
                </div>
                <!--end::Page title-->
            </div>
            <!--end::Toolbar container-->
        </div>
        <div class="container mt-20 mb-20">
            <div class="card shadow-sm">
                <div class="card-header">
                    <h3 class="card-title">List of Customers</h3>
                    <div class="card-toolbar">
                        <button type="button" class="btn btn-sm btn-primary" data-bs-toggle="modal" data-bs-target="#modal" @click="add()">Add Customer</button>
                    </div>
                </div>
                <div class="card-body">
                    <div class="row d-flex align-items-center">
                        <!--begin::Input group-->
                        <div class="position-relative me-md-2">
                            <!--begin::Svg Icon | path: icons/duotune/general/gen021.svg-->
                            <span class="svg-icon svg-icon-3 svg-icon-gray-500 position-absolute top-50 translate-middle ms-6">
                                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <rect opacity="0.5" x="17.0365" y="15.1223" width="8.15546" height="2" rx="1" transform="rotate(45 17.0365 15.1223)" fill="currentColor"></rect>
                                    <path d="M11 19C6.55556 19 3 15.4444 3 11C3 6.55556 6.55556 3 11 3C15.4444 3 19 6.55556 19 11C19 15.4444 15.4444 19 11 19ZM11 5C7.53333 5 5 7.53333 5 11C5 14.4667 7.53333 17 11 17C14.4667 17 17 14.4667 17 11C17 7.53333 14.4667 5 11 5Z" fill="currentColor"></path>
                                </svg>
                            </span>
                            <!--end::Svg Icon-->
                            <input type="text" class="form-control form-control-solid ps-10" name="search" v-model="search" placeholder="Search" />
                        </div>
                        <!--end::Input group-->
                    </div>
                    <div class="py-5">
                        <div class="table-responsive">
                            <table class="table table-row-bordered table-row-gray-200 gy-4">
                                <thead>
                                    <tr class="fw-bold fs-6 text-gray-800">
                                        <th class="text-center">No</th>
                                        <th class="text-center">Code</th>
                                        <th class="text-center">Name</th>
                                        <th class="text-center">Country</th>
                                        <th class="text-center">Area</th>
                                        <th class="text-center">Region</th>
                                        <th class="text-center">Action</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
                <div class="card-footer">Footer</div>
            </div>
        </div>
        <div class="modal fade" tabindex="-1" id="modal" data-bs-backdrop="static">
            <div class="modal-dialog modal-lg">
                <div class="modal-content">
                    <div class="modal-header">
                        <h3 v-if="modal_create" class="modal-title">Add Customer</h3>
                        <h3 v-else class="modal-title">Edit Customer</h3>

                        <!--begin::Close-->
                        <div class="btn btn-icon btn-sm btn-active-light-primary ms-2" data-bs-dismiss="modal" aria-label="Close">
                            <span class="svg-icon svg-icon-1" @click="closeModal()">
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
                            <div class="row">
                                <div class="col-6">
                                    <div class="form-group mb-4">
                                        <label class="form-label fw-bold">Customer Name</label>
                                        <input type="text" v-model="customer.name" :class="{ 'is-invalid': errors.name }" class="form-control" />
                                        <span v-if="errors.name" class="error invalid-feedback">{{ errors.name[0] }}</span>
                                    </div>
                                    <div class="form-group mb-4">
                                        <label class="form-label fw-bold">Region</label>
                                        <multiselect v-model="region_value" :options="region" placeholder="" label="name" :searchable="true" :class="{ 'is-invalid': errors.region_id }"></multiselect>
                                        <span v-if="errors.region_id" class="error invalid-feedback">{{ errors.region_id[0] }}</span>
                                    </div>
                                </div>
                                <div class="col-6">
                                    <div class="form-group mb-4">
                                        <label class="form-label fw-bold">Customer Code</label>
                                        <input type="text" v-model="customer.code" :class="{ 'is-invalid': errors.code }" class="form-control" />
                                        <span v-if="errors.code" class="error invalid-feedback">{{ errors.code[0] }}</span>
                                    </div>
                                    <div class="form-group mb-4">
                                        <label class="form-label fw-bold">Country</label>
                                        <multiselect v-model="country_value" :options="country" :disabled="isDisabled" :searchable="true" placeholder="" label="name" :class="{ 'is-invalid': errors.country_id }"></multiselect>
                                        <span v-if="errors.country_id" class="error invalid-feedback">{{ errors.country_id[0] }}</span>
                                    </div>
                                </div>
                            </div>
                            <hr />
                            <div id="kt_docs_repeater_basic">
                                <!--begin::Form group-->
                                <h3 class="mb-5 mt-5">Area & AMS</h3>
                                <!--begin::Form group-->
                                <div class="form-group mt-5">
                                    <a type="button" @click="addAreaAms()" class="btn btn-primary btn-sm"> Add </a>
                                </div>
                                <!--end::Form group-->
                                <div class="form-group">
                                    <div data-repeater-list="kt_docs_repeater_basic">
                                        <div data-repeater-item v-for="(data, index) in area_ams" :key="index">
                                            <div class="form-group row mb-5">
                                                <div class="col px-1 d-flex justify-content-center align-items-end">
                                                    <h3 class="mb-4">{{ index + 1 }}.</h3>
                                                </div>
                                                <div class="col-md-5 text-center">
                                                    <label class="form-label">Area</label>
                                                    <multiselect v-model="data.area" placeholder="Search and select Area" label="name" :searchable="true" :options="area"></multiselect>
                                                </div>
                                                <div class="col-md-5 text-center">
                                                    <label class="form-label">AMS</label>
                                                    <multiselect v-model="data.ams" placeholder="Search and select AMS" label="initial" :searchable="true" :options="ams"></multiselect>
                                                </div>
                                                <div class="col-md-1">
                                                    <a type="button" @click="remove(index)" class="btn btn-light-danger mt-3 mt-md-8">
                                                        <i class="la la-trash-o"></i>
                                                    </a>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <!--end::Form group-->
                            </div>
                            <div class="row mt-10">
                                <div class="col">
                                    <button type="button" class="btn btn-light" data-bs-dismiss="modal" id="close_modal" @click="closeModal()">Back</button>
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
    </div>
</template>

<script>
import debounce from "lodash/debounce";
export default {
    name: "CustomerPage",
    layout: "template",
    data() {
        return {
            area_ams: [],
            country_value: [],
            region_value: [],
            region: [],
            country: [],
            ams: [],
            area: [],
            multiselectList: [],
            modal_create: false,
            customer: {
                name: null,
                code: null,
            },
            search: null,
            search_country: null,
            isDisabled: true,
            errors: {
                name: null,
                code: null,
                country_id: null,
                region_id: null,
            },
        };
    },
    mounted() {
        KTFormRepeaterBasic.init();
    },
    watch: {
        region_value: debounce(function () {
            this.listCountry();
            this.clear();
        }, 100),
    },
    methods: {
        addAreaAms() {
            this.area_ams.push({
                area: null,
                ams: null,
            });
        },
        remove(index) {
            this.area_ams.splice(index, 1);
        },
        listRegion() {
            this.$axios
                .get("api/region", {
                    params: {
                        paginate: 1000,
                    },
                })
                .then((response) => {
                    this.region = response.data.data.data;
                })
                .catch((error) => console.log(error));
        },
        listCountry() {
            if (this.region_value) {
                this.$axios
                    .get(`/api/countries`, {
                        params: {
                            search: this.region_value.id,
                            paginate: 1000,
                        },
                    })
                    .then((response) => {
                        this.country = response.data.data.data;
                    })
                    .catch((error) => console.log(error));
            }
        },
        listArea() {
            this.$axios
                .get("api/area", {
                    params: {
                        paginate: 1000,
                    },
                })
                .then((response) => {
                    this.area = response.data.data.data;
                })
                .catch((error) => console.log(error));
        },
        listAMS() {
            this.$axios
                .get("api/ams", {
                    params: {
                        paginate: 1000,
                    },
                })
                .then((response) => {
                    this.ams = response.data.data.data;
                })
                .catch((error) => console.log(error));
        },
        create() {
            this.loading();
            this.$axios
                .post("api/customer-create", {
                    name: this.customer.name,
                    code: this.customer.code,
                    country_id: this.country_value.id,
                    region_id: this.region_value.id,
                    area_id: this.area_value,
                    ams_id: this.ams_value,
                })
                .then((response) => {
                    toastr.success(response.data.message);
                    this.list();
                    this.closeModal();
                })
                .catch((error) => {
                    if (error.response.status == 422) {
                        this.errors = error.response.data.errors;

                        toastr.error(error.response.data.message);
                    }
                });
        },
        submit() {
            if (this.modal_create) {
                this.create();
            } else {
                this.update();
            }
        },
        add() {
            this.modal_create = true;
            this.listRegion();
            this.listAMS();
            this.listArea();
        },
        loading() {
            Swal.fire({
                timer: 500,
                didOpen: () => {
                    Swal.showLoading();
                },
                background: "transparent",
                allowOutsideClick: false,
            });
        },
        closeModal() {
            document.getElementById("close_modal").click();
            this.clearForm();
        },
        clear() {
            this.country = [];
            this.country_value = [];
            if (this.region_value == null) {
                this.isDisabled = true;
                this.country = [];
                this.country_value = [];
            } else {
                this.isDisabled = false;
            }
        },
        clearForm() {
            this.region = [];
            this.region_value = [];
            this.country = [];
            this.country_value = [];
            this.ams = [];
            this.ams_value = [];
            this.area = [];
            this.area_value = [];
            if (this.region_value == null) {
                this.isDisabled = true;
            } else {
                this.isDisabled = false;
            }
            this.customer.name = null;
            this.customer.code = null;
        },
    },
};
</script>
<style>
.mt-20 {
    margin-top: 20px;
}
.mb-20 {
    margin-bottom: 20px;
}
</style>
