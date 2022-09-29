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
                    style="background-color: #1BC5BD">
                    <i class="fa-solid fa-user-plus text-light"></i>
                    Add Contact Person</div>
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
                      contact_persons, contact_persons_index
                      ) in contact_persons.data"
                      :key="contact_persons_index"
                  >
                    <td class="text-start">{{ contact_persons.name }}</td>
                    <td class="text-start">{{ contact_persons.email }}</td>
                    <td class="text-start">{{ contact_persons.phone }}</td>
                    <td class="text-start">{{ contact_persons.address }}</td>

                    <td class="text-start">
                      <button
                        class="btn btn-sm btn-light"
                        v-on:click="remove(contact_persons.id)"
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
          <h3 class="card-title fw-bold">Data Prospect</h3>
          <div class="card-toolbar">
            <button
              type="button"
              class="btn btn-sm btn-primary mx-3"
              data-bs-toggle="modal"
              data-bs-target="#modal"
            >
              Add Registration
            </button>
            <div type="button"
              class="btn btn-sm text-light"
              style="background-color: #1BC5BD">
              <i class="fa-solid fa-user-plus text-light"></i>
              Search</div>
          </div>
        </div>
    <div class="modal fade" tabindex="-1" id="modal" data-bs-backdrop="static">
      <div class="modal-dialog modal-xl modal-dialog-centered">
        <div class="modal-content py-5">
          <div class="modal-header">
            <h3 class="modal-title">Add Registration</h3>
            <div type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close">
            </div>
          </div>
          <div class="modal-body">
            <form>
              <div class="row">
                <div class="col-md-6">
                  <div class="mb-3">
                    <label for="Maintenance" class="form-label">Maintenance</label>
                    <input type="email" class="form-control">
                  </div>
                  <div class="mb-3">
                    <label for="Maintenance" class="form-label">Registration</label>
                    <input type="text" class="form-control">
                  </div>
                  <div class="mb-3">
                    <label for="Maintenance" class="form-label">TAT</label>
                    <input type="text" class="form-control">
                  </div>
                  <button class="btn btn-secondary mt-3" data-bs-dismiss="modal" aria-label="Close">Back</button>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label for="Maintenance" class="form-label">Hangar</label>
                    <input type="email" class="form-control">
                  </div>
                  <div class="mb-3">
                    <label for="Maintenance" class="form-label">Sales Plan</label>
                    <input type="text" class="form-control">
                  </div>
                  <div class="mb-3">
                    <label for="Maintenance" class="form-label">Start Date</label>
                    <input type="text" class="form-control">
                  </div>
                  <button type="submit" class="btn btn-primary mt-3">Submit</button>
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
                  <tr>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">a</td>
                    <td class="text-center">
                      <button class="btn btn-sm btn-light">
                        <i class="bi bi-toggles text-primary"></i>
                      </button>
                      <button
                        class="btn btn-sm btn-light"
                        data-bs-toggle="modal"
                        data-bs-target="#modal"
                        @click="edit(users)"
                      >
                        <i class="bi bi-pencil-square text-primary"></i>
                      </button>
                      <button
                        class="btn btn-sm btn-light"
                        v-on:click="remove(users.id)"
                      >
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
      contact_persons: {
        data: [],
        },
      }
    },
  created() {
    this.listContactPersons()
    this.list()
    },
  methods: {
    listContactPersons() {
      this.$axios
        .get('api/contact-persons', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.contact_persons = response.data
          console.log(response.data.data)
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
    },
  }
</script>

<style>
</style>