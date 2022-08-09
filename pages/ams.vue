<template>
    <div>
        <div id="kt_app_toolbar" class="app-toolbar py-3 py-lg-6 bg-white">
            <!--begin::Toolbar container-->
            <div id="kt_app_toolbar_container" class="app-container container-fluid d-flex flex-stack">
                <!--begin::Page title-->
                <div class="page-title d-flex flex-column justify-content-center flex-wrap me-3">
                    <!--begin::Title-->
                    <p class="page-heading d-flex text-dark fs-6 flex-column justify-content-center my-0 fw-bold">AMS</p>
                    <!--end::Title-->
                </div>
                <ul class="breadcrumb breadcrumb-separatorless fw-semibold fs-7 my-0 pt-1">
                    <!--begin::Item-->
                    <li class="breadcrumb-item text-muted">
                        <nuxt-link to="/" class="text-muted text-hover-primary">Dashboard</nuxt-link>
                    </li>
                    <li class="breadcrumb-item">
                        <span class="bullet bg-gray-400 w-5px h-2px"></span>
                    </li>
                    <li class="breadcrumb-item text-muted">AMS</li>
                    <!--end::Item-->
                </ul>
                <!--end::Page title-->
            </div>
            <!--end::Toolbar container-->
        </div>
        <div class="container mb-10">
            <div class="card shadow-sm mt-5">
                <div class="card-header">
                    <h3 class="card-title fw-bold">List of AMS</h3>
                    <div class="card-toolbar">
                        <button type="button" class="btn btn-sm btn-primary" data-bs-toggle="modal" data-bs-target="#modal" @click="add()">Add AMS</button>
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
                            <input type="text" class="form-control form-control-solid ps-10" initial="search" v-model="search" placeholder="Search" />
                        </div>
                        <!--end::Input group-->
                    </div>
                    <div class="py-5">
                        <div class="table-responsive">
                            <table class="table table-row-bordered table-row-gray-200 gy-4">
                                <thead>
                                    <tr class="fw-bold fs-6 text-gray-800">
                                        <th class="text-center">No</th>
                                        <th class="text-center">Initial</th>
                                        <th class="text-center">User</th>
                                        <th class="text-center">Action</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="(p_ams, p_ams_index) in ams.data" :key="p_ams_index">
                                        <td class="text-center">{{ ams.from + p_ams_index }}</td>
                                        <td class="text-center">{{ p_ams.initial }}</td>
                                        <td class="text-center">{{ p_ams.user.name }}</td>
                                        <td class="d-flex justify-content-center">
                                            <button class="btn btn-sm btn-light">
                                                <i class="bi bi-toggles text-primary"></i>
                                            </button>
                                            <button class="btn btn-sm btn-light" data-bs-toggle="modal" data-bs-target="#modal" @click="edit(p_ams)">
                                                <i class="bi bi-pencil-square text-primary"></i>
                                            </button>
                                            <button class="btn btn-sm btn-light" v-on:click="remove(p_ams.id)">
                                                <i class="bi bi-trash-fill text-primary"></i>
                                            </button>
                                        </td>
                                    </tr>
                                    <tr v-if="ams.data.length < 1">
                                        <td colspan="8">
                                            <div class="text-muted text-center">Data not found</div>
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
                                        <select class="form-control form-control-sm" v-model="paginate" @change="list()">
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
                                        <button
                                            type="button"
                                            class="page-link"
                                            :class="{
                                                disabled: !ams.prev_page_url,
                                            }"
                                            @click="ams.prev_page_url && list(ams.prev_page_url)"
                                        >
                                            Previous
                                        </button>
                                    </li>
                                    <li class="page-item" style="margin-left: 15px; margin-right: 15px">
                                        <input type="text" class="form-control form-control-sm text-center" v-model="current_page" @keypress="directPage" style="width: 60px" />
                                    </li>
                                    <li class="page-item">
                                        <button
                                            type="button"
                                            class="page-link"
                                            :class="{
                                                disabled: !ams.next_page_url,
                                            }"
                                            @click="ams.next_page_url && list(ams.next_page_url)"
                                        >
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

        <div class="modal fade" tabindex="-1" id="modal" data-bs-backdrop="static">
            <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content">
                    <div class="modal-header">
                        <h3 v-if="modal_create" class="modal-title">Add AMS</h3>
                        <h3 v-else class="modal-title">Edit AMS</h3>

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
                            <div class="form-group mb-3">
                                <label class="form-label fw-bold">Initial</label>
                                <input
                                    type="text"
                                    class="form-control"
                                    v-model="p_ams.initial"
                                    :class="{
                                        'is-invalid': errors.initial,
                                    }"
                                />
                                <span v-if="errors.initial" class="error invalid-feedback">{{ errors.initial[0] }}</span>
                            </div>
                            <div class="form-group mb-3">
                                <label class="form-label fw-bold">User</label>
                                <select
                                    class="form-select"
                                    v-model="p_ams.user_id"
                                    :class="{
                                        'is-invalid': errors.user_id,
                                    }"
                                >
                                    <option selected disabled>Select User</option>
                                    <option v-for="user in users" v-bind:value="user.id">{{ user.name }}</option>
                                </select>
                                <span v-if="errors.user_id" class="error invalid-feedback">{{ errors.user_id[0] }}</span>
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
    layout: "template",
    data() {
        return {
            ams: {
                data: [],
                link: [],
            },
            users: null,
            p_ams: {
                id: null,
                initial: null,
                user_id: null,
            },
            modal_create: false,
            selection_user: null,
            isLoading: false,
            search: null,
            order: "id",
            by: "desc",
            paginate: "10",
            current_page: null,
            errors: {
                initial: null,
                user_id: null,
            },
        };
    },
    created() {
        this.list();
        this.user();
    },
    watch: {
        search: debounce(function () {
            this.list();
        }, 500),
    },
    methods: {
        list(paginate) {
            this.loading();
            paginate = paginate || `/api/ams`;
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
                    this.ams = response.data.data;
                    this.current_page = this.ams.current_page;
                    Swal.close();
                })
                .catch((error) => console.log(error));
        },
        directPage: debounce(function () {
            if (this.current_page < 1) {
                this.current_page = 1;
            } else if (this.current_page > this.ams.last_page) {
                this.current_page = this.ams.last_page;
            }
            let url = new URL(this.ams.first_page_url);
            let search_params = url.searchParams;
            search_params.set("page", this.current_page);
            url.search = search_params.toString();
            let new_url = url.toString();
            this.list(new_url);
        }, 500),
        submit() {
            if (this.modal_create) {
                this.create();
            } else {
                this.update();
            }
        },
        add() {
            this.modal_create = true;
        },
        create() {
            this.loading();
            this.$axios
                .post("/api/ams-create", {
                    initial: this.p_ams.initial,
                    user_id: this.p_ams.user_id,
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
        edit(p_ams) {
            this.modal_create = false;
            this.p_ams.id = p_ams.id;
            this.p_ams.initial = p_ams.initial;
            this.p_ams.user_id = p_ams.user_id;
        },
        update() {
            this.loading();

            this.$axios
                .put("/api/ams-update/" + this.p_ams.id, {
                    initial: this.p_ams.initial,
                    user_id: this.p_ams.user_id,
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
        remove(id) {
            Swal.fire({
                title: "Are you sure?",
                text: "You won't be able to revert this!",
                icon: "warning",
                showCancelButton: true,
                confirmButtonColor: "#3085d6",
                cancelButtonColor: "#d33",
                confirmButtonText: "Yes, delete it!",
            })
                .then((result) => {
                    if (result.isConfirmed) {
                        this.$axios.delete("/api/ams-delete/" + id).then((response) => {
                            toastr.success(response.data.message);
                            this.list();
                        });
                    }
                })
                .catch((error) => {
                    console.log(error);
                });
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
        clearForm() {
            this.p_ams.id = null;
            this.p_ams.initial = null;
            this.p_ams.user_id = null;
            this.errors.initial = null;
            this.errors.user_id = null;
        },
        closeModal() {
            document.getElementById("close_modal").click();
            this.clearForm();
        },
        user() {
            this.$axios
                .get("/api/users")
                .then((response) => {
                    this.users = response.data.data.data;
                })
                .catch((error) => console.log(error));
        },
        userMutation() {
            this.isLoading = true;

            this.$axios.get("/api/users").then((response) => {
                this.users = response.data;
                this.isLoading = false;
            });
        },
        user(keyword) {
            this.isLoading = true;

            this.$axios
                .get("/api/users", {
                    params: {
                        search: keyword,
                    },
                })
                .then((response) => {
                    this.users = response.data;
                    this.isLoading = false;
                });
        },
        userLabel({ user_id }) {
            return `${user_id}`;
        },
        selectedUser({ initial, user_id }) {
            this.initial = initial;
            this.user_id = user_id;
        },
    },
};
</script>
<style scoped>
.multiselect__placeholder {
    display: inline-block !important;
    margin-bottom: 0px !important;
    padding-top: 0px !important;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.multiselect.invalid .multiselect__tags {
    border: 1px solid #f86c6b !important;
}

.multiselect__option--highlight {
    background: #428bca !important;
}

.multiselect__option--highlight:after {
    background: #428bca !important;
}

.multiselect__tags {
    padding: 5px !important;
    min-height: 10px;
}

.multiselect__placeholder {
    margin-left: 10px;
    margin-top: 2px;
}

.multiselect__tag {
    background: #f0f0f0 !important;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
    color: black !important;
    margin-bottom: 0px !important;
    margin-right: 5px !important;
}

.multiselect__tag-icon:after {
    color: rgba(60, 60, 60, 0.5) !important;
}

.multiselect__tag-icon:focus,
.multiselect__tag-icon:hover {
    background: #f0f0f0 !important;
}

.multiselect__tag-icon:focus:after,
.multiselect__tag-icon:hover:after {
    color: red !important;
}

.form-control {
    display: block;
    width: 100%;
    height: calc(1.5em + 0.75rem + 2px);
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.mt-20 {
    margin-top: 20px;
}

.mb-20 {
    margin-bottom: 20px;
}

.mb-10 {
    margin-bottom: 10px;
}
</style>
