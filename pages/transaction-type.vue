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
              fw-bold
            "
          >
            Transaction Type
          </p>
          <!--end::Title-->
        </div>
        <ul
          class="breadcrumb breadcrumb-separatorless fw-semibold fs-7 my-0 pt-1"
        >
          <!--begin::Item-->
          <li class="breadcrumb-item text-muted">
            <nuxt-link to="/" class="text-muted text-hover-primary"
              >Dashboard</nuxt-link
            >
          </li>
          <li class="breadcrumb-item">
            <span class="bullet bg-gray-400 w-5px h-2px"></span>
          </li>
          <li class="breadcrumb-item text-muted">Transaction Type</li>
          <!--end::Item-->
        </ul>
        <!--end::Page title-->
      </div>
      <!--end::Toolbar container-->
    </div>
    <div class="container mb-10">
      <div class="card shadow-sm mt-5">
        <div class="card-header">
          <h3 class="card-title fw-bold">List of Transaction Type</h3>
          <div class="card-toolbar">
            <button
              type="button"
              class="btn btn-sm btn-primary"
              data-bs-toggle="modal"
              data-bs-target="#modal_create"
            >
              Add Transaction Type
            </button>
            <div
              class="modal fade"
              tabindex="-1"
              id="modal_create"
              data-bs-backdrop="static"
            >
              <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content">
                  <div class="modal-header">
                    <h3 class="modal-title">Add Transaction Type</h3>

                    <!--begin::Close-->
                    <div
                      class="btn btn-icon btn-sm btn-active-light-primary ms-2"
                      data-bs-dismiss="modal"
                      aria-label="Close"
                    >
                      <span class="svg-icon svg-icon-1"></span>
                    </div>
                    <!--end::Close-->
                  </div>
                  <div class="modal-body">
                    <form v-on:submit.prevent="add">
                      <div class="form-group mb-3">
                        <label for="name" class="form-label fw-bold"
                          >Name</label
                        >
                        <input
                          type="text"
                          class="form-control"
                          v-model="name"
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
                        <label for="description" class="form-label fw-bold"
                          >Description</label
                        >
                        <input
                          type="text"
                          class="form-control"
                          v-model="description"
                          :class="{
                            'is-invalid': errors.description,
                          }"
                        />
                        <span
                          v-if="errors.description"
                          class="error invalid-feedback"
                          >{{ errors.description[0] }}</span
                        >
                      </div>
                      <div class="row mt-10">
                        <div class="col">
                          <button
                            type="button"
                            class="btn btn-light"
                            data-bs-dismiss="modal"
                          >
                            Back
                          </button>
                        </div>
                        <div class="col d-flex justify-content-end">
                          <button type="submit" class="btn btn-primary">
                            Save
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
        <div class="card-body">
          <div class="row d-flex align-items-center">
            <!--begin::Input group-->
            <div class="position-relative me-md-2">
              <!--begin::Svg Icon | path: icons/duotune/general/gen021.svg-->
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
              <!--end::Svg Icon-->
              <input
                type="text"
                class="form-control form-control-solid ps-10"
                name="search"
                v-model="search"
                placeholder="Search"
              />
            </div>
            <!--end::Input group-->
          </div>
          <div class="py-5">
            <div class="table-responsive">
              <table class="table table-row-bordered table-row-gray-200 gy-4">
                <thead>
                  <tr class="fw-bold fs-6 text-gray-800">
                    <th class="text-center">No</th>
                    <th class="text-center">Name</th>
                    <th class="text-center">Description</th>
                    <th class="text-center">Action</th>
                  </tr>
                </thead>
                <tbody>
                  <tr
                    v-for="(
                      transaction, transaction_index
                    ) in transaction_type.data"
                    :key="transaction_index"
                  >
                    <td class="text-center">{{ transaction_index + 1 }}</td>
                    <td class="text-center">{{ transaction.name }}</td>
                    <td class="text-center">{{ transaction.description }}</td>
                    <td class="d-flex justify-content-center">
                      <button class="btn btn-sm btn-light">
                        <i class="bi bi-toggles text-primary"></i>
                      </button>
                      <button
                        class="btn btn-sm btn-light"
                        data-bs-toggle="modal"
                        data-bs-target="#modal_edit"
                        @click="edit(transaction)"
                      >
                        <i class="bi bi-pencil-square text-primary"></i>
                      </button>
                      <button
                        class="btn btn-sm btn-light"
                        v-on:click="remove(transaction.id)"
                      >
                        <i class="bi bi-trash-fill text-primary"></i>
                      </button>
                    </td>
                  </tr>
                  <tr v-if="transaction_type.data.length < 1">
                    <td colspan="8">
                      <div class="text-muted text-center">Data not found</div>
                    </td>
                  </tr>
                </tbody>
              </table>
              <div
                class="modal fade"
                tabindex="-1"
                id="modal_edit"
                @close="open = false"
              >
                <div class="modal-dialog modal-dialog-centered">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h3 class="modal-title">Edit Transaction Type</h3>

                      <!--begin::Close-->
                      <div
                        class="
                          btn btn-icon btn-sm btn-active-light-primary
                          ms-2
                        "
                        data-bs-dismiss="modal"
                        aria-label="Close"
                      >
                        <span class="svg-icon svg-icon-1"></span>
                      </div>
                      <!--end::Close-->
                    </div>

                    <div class="modal-body">
                      <form v-on:submit.prevent="update()">
                        <div class="form-group mb-3">
                          <label for="name" class="form-label fw-bold"
                            >Name</label
                          >
                          <input
                            type="text"
                            class="form-control"
                            v-model="transaction.name"
                            name="name"
                          />
                        </div>
                        <div class="form-group mb-3">
                          <label for="description" class="form-label fw-bold"
                            >Description</label
                          >
                          <input
                            type="text"
                            class="form-control"
                            v-model="transaction.description"
                            name="description"
                          />
                        </div>
                        <div class="row mt-10">
                          <div class="col">
                            <button
                              type="button"
                              class="btn btn-light"
                              data-bs-dismiss="modal"
                            >
                              Back
                            </button>
                          </div>
                          <div class="col d-flex justify-content-end">
                            <button type="submit" class="btn btn-primary">
                              Save Changes
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
                      v-on:change="list()"
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
                    <button
                      type="button"
                      class="page-link"
                      :class="{
                        disabled: !transaction_type.prev_page_url,
                      }"
                      @click="
                        transaction_type.prev_page_url &&
                          list(transaction_type.prev_page_url)
                      "
                    >
                      Previous
                    </button>
                  </li>
                  <li
                    class="page-item"
                    style="margin-left: 15px; margin-right: 15px"
                  >
                    <input
                      type="text"
                      class="form-control form-control-sm text-center"
                      v-model="current_page"
                      @keypress="directPage"
                      style="width: 60px"
                    />
                  </li>
                  <li class="page-item">
                    <button
                      type="button"
                      class="page-link"
                      :class="{
                        disabled: !transaction_type.next_page_url,
                      }"
                      @click="
                        transaction_type.next_page_url &&
                          list(transaction_type.next_page_url)
                      "
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
  </div>
</template>

<script>
import debounce from 'lodash/debounce'
export default {
  layout: 'template',
  data() {
    return {
      open: false,
      transaction_type: {
        data: [],
        link: [],
      },
      transaction: {
        id: null,
        name: null,
        description: null,
      },
      name: null,
      description: null,
      search: null,
      order: 'id',
      by: 'desc',
      paginate: '10',
      current_page: null,
      errors: {
        name: null,
        description: null,
      },
    }
  },
  created() {
    this.list()
  },
  watch: {
    search: debounce(function () {
      this.list()
    }, 500),
  },
  methods: {
    list(paginate) {
      this.loading()
      paginate = paginate || `/api/transaction-type`
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
          this.transaction_type = response.data.data
          this.current_page = this.transaction_type.current_page
          Swal.close()
        })
        .catch((error) => console.log(error))
    },
    directPage: debounce(function () {
      if (this.current_page < 1) {
        this.current_page = 1
      } else if (this.current_page > this.transaction_type.last_page) {
        this.current_page = this.transaction_type.last_page
      }
      let url = new URL(this.transaction_type.first_page_url)
      let search_params = url.searchParams
      search_params.set('page', this.current_page)
      url.search = search_params.toString()
      let new_url = url.toString()
      this.list(new_url)
    }, 500),
    add() {
      this.loading()
      this.$axios
        .post('/api/transaction-type-create', {
          name: this.name,
          description: this.description,
        })
        .then((result) => {
          Swal.fire({
            title: 'Data save successfully!',
            icon: 'success',
            confirmButtonText: 'OK',
          }).then((result) => {
            this.clearForm()
            this.list()
            this.closeModal()
          })
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data
            Swal.fire('Data save failed!', '', 'error')
          }
        })
    },
    edit(transaction) {
      this.transaction.id = transaction.id
      this.transaction.name = transaction.name
      this.transaction.description = transaction.description
    },
    update() {
      this.loading()

      this.$axios
        .put('/api/transaction-type-update/' + this.transaction.id, {
          name: this.transaction.name,
          description: this.transaction.description,
        })
        .then((result) => {
          Swal.fire({
            title: 'Data update successfully!',
            icon: 'success',
            confirmButtonText: 'OK',
          }).then((result) => {
            this.open = false
            this.list()
            this.closeModal()
          })
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data
            Swal.fire('Data update failed!', '', 'error')
          }
        })
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
            this.$axios
              .delete('/api/transaction-type-delete/' + id)
              .then((response) => {
                Swal.fire({
                  title: 'Deleted!',
                  icon: 'success',
                  text: 'Your data has been deleted.',
                  confirmButtonText: 'Ok',
                }).then((result) => {
                  this.list()
                })
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
    clearForm() {
      this.name = ''
      this.description = ''
      this.errors.name = null
      this.errors.description = null
    },
    closeModal() {
      document.getElementById('modal_edit').click()
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
.mb-10 {
  margin-bottom: 10px;
}
</style>

