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
            My Prospect
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
          <li class="breadcrumb-item text-muted">My Prospect</li>
          <!--end::Item-->
        </ul>
        <!--end::Page title-->
      </div>
      <!--end::Toolbar container-->
    </div>
    <div class="container mt-10 mb-20">
      <div class="card shadow-sm mb-5">
        <div class="card-header">
          <h1 class="card-title fw-bold">Your Prospect Statistic</h1>
        </div>
        <div class="card-body">
          <div class="row mb-5">
            <div class="col">
              <div class="row">
                <p class="mb-5 fw-bold text-gray-600">
                  This year earnings calculated. Apart from arranging the
                  order of topics.
                </p>
                <div class="col">
                  <div class="border-dashed p-4">
                    <h1 class="fw-bold mb-0">$ {{ prospect2.totalMarketShare }}</h1>
                    <p class="mb-0 fw-bold text-gray-500">Total Market Share</p>
                  </div>
                </div>
                <div class="col">
                  <div class="border-dashed p-4">
                    <h1 class="fw-bold mb-0">$ {{ prospect2.totalSalesPlan }}</h1>
                    <p class="mb-0 fw-bold text-gray-500">Total Salesplan</p>
                  </div>
                </div>
                <div class="col">
                  <div class="border-dashed p-4">
                    <h1 class="fw-bold mb-0">$ {{ prospect2.deviation }}</h1>
                    <p class="mb-0 fw-bold text-gray-500">Deviation</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="card-body">
        <div class="card shadow-sm mt-5">
          <div class="card-header">
            <h3 class="card-title fw-bold">My Prospect</h3>
            <div class="card-toolbar">
              <button
                type="button"
                class="btn btn-sm btn-primary"
                data-bs-toggle="modal"
                data-bs-target="#kt_modal_create_app"
              >
                Add Prospect
              </button>
            </div>
          </div>
          <div class="card-body">
            <div class="row d-flex align-items-center">
            </div>
            <div class="py-5">
              <ul
                class="
                  nav nav-tabs nav-line-tabs
                  mb-5
                  fs-6
                  justify-content-end
                  mt-5
                "
              >
                <li class="nav-item">
                  <a
                    class="nav-link active"
                    exact-active-class="active"
                    data-bs-toggle="tab"
                    href="#kt_tab_pane_1"
                    @click="filterYear(currentYear)"
                    >This Year</a
                  >
                </li>
                <li class="nav-item">
                  <a
                    class="nav-link"
                    active-class="active"
                    data-bs-toggle="tab"
                    href="#kt_tab_pane_2"
                    @click="filterYear(currentYear - 1)"
                    >{{ currentYear - 1 }}</a
                  >
                </li>
                <li class="nav-item">
                  <a
                    class="nav-link"
                    active-class="active"
                    data-bs-toggle="tab"
                    href="#kt_tab_pane_3"
                    @click="filterYear(currentYear - 2)"
                    >{{ currentYear - 2 }}</a
                  >
                </li>
                <li class="nav-item">
                  <a
                    class="nav-link"
                    active-class="active"
                    data-bs-toggle="tab"
                    href="#kt_tab_pane_4"
                    @click="filterYear(currentYear - 3)"
                    >{{ currentYear - 3 }}</a
                  >
                </li>
              </ul>
              <div class="tab-content" id="myTabContent">
                <div
                  class="tab-pane fade show active"
                  id="kt_tab_pane_1"
                  role="tabpanel"
                >
                  <div class="table-responsive">
                    <table
                      class="table table-row-bordered table-row-gray-200 gy-4"
                    >
                      <thead>
                        <tr class="fw-bold fs-6 text-gray-800">
                          <th class="text-center">No</th>
                          <th class="text-center">Year</th>
                          <th class="text-center">Transaction</th>
                          <th class="text-center">Type</th>
                          <th class="text-center">Strategic Initiative</th>
                          <th class="text-center">PM</th>
                          <th class="text-center">Customer Code</th>
                          <th class="text-center">Customer</th>
                          <th class="text-center">AMS</th>
                          <th class="text-center">Market Share</th>
                          <th class="text-center">Sales Plan</th>
                          <th class="text-center">Action</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr
                          v-for="(
                            prospect, prospect_index
                          ) in prospect"
                          :key="prospect_index"
                        >
                          <td class="text-center">
                            {{ prospect3.from + prospect_index }}
                          </td>
                          <td class="text-center">{{ prospect.year }}</td>
                          <td class="text-center">{{ prospect.transaction_type.name }}</td>
                          <td class="text-center">{{ prospect.prospect_type.name }}</td>
                          <td class="text-center">{{ prospect.strategic_initiative.name }}</td>
                          <td class="text-center">{{ prospect.pm.name }}</td>
                          <td class="text-center">{{ prospect.ams_customer.customer.code }}</td>
                          <td class="text-center">{{ prospect.ams_customer.customer.name }}</td>
                          <td class="text-center">{{ prospect.ams_customer.ams.initial }}</td>
                          <td>
                            <div v-if="prospect.market_share" class="text-center" style="color: #50CD89">
                              ${{ prospect.market_share }}
                            </div>
                            <div v-else class="text-center" style="color: #50CD89">
                              $
                            </div>
                          </td>

                            <td v-if="prospect.sales" class="text-center" style="color: #50CD89">
                              ${{ prospect.sales.value }}
                            </td>
                            <td v-else class="text-center" style="color: #50CD89">
                              $
                            </td>
                          
                          <td class="text-center">
                            <nuxt-link
                              v-if="prospect"
                              :to="{ path: 'view-prospect', query: { id: prospect.ams_customer.customer.id }}"
                              class="btn btn-sm btn-light"
                              >View</nuxt-link
                            >
                          </td>
                        </tr>
                        <tr v-if="prospect.length < 1">
                          <td colspan="12">
                            <div class="text-muted text-center">
                              Data not found
                            </div>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </div>
                <div class="tab-pane fade" id="kt_tab_pane_2" role="tabpanel">
                  <div class="table-responsive">
                    <table
                      class="table table-row-bordered table-row-gray-200 gy-4"
                    >
                      <thead>
                        <tr class="fw-bold fs-6 text-gray-800">
                          <th class="text-center">No</th>
                          <th class="text-center">Year</th>
                          <th class="text-center">Transaction</th>
                          <th class="text-center">Type</th>
                          <th class="text-center">Strategic Initiative</th>
                          <th class="text-center">PM</th>
                          <th class="text-center">Customer Code</th>
                          <th class="text-center">Customer</th>
                          <th class="text-center">AMS</th>
                          <th class="text-center">Market Share</th>
                          <th class="text-center">Sales Plan</th>
                          <th class="text-center">Action</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr
                          v-for="(
                            prospect, prospect_index
                          ) in prospect"
                          :key="prospect_index"
                        >
                          <td class="text-center">
                            {{ prospect3.from + prospect_index }}
                          </td>
                          <td class="text-center">{{ prospect.year }}</td>
                          <td class="text-center">{{ prospect.transaction_type.name }}</td>
                          <td class="text-center">{{ prospect.prospect_type.name }}</td>
                          <td class="text-center">{{ prospect.strategic_initiative.name }}</td>
                          <td class="text-center">{{ prospect.pm.name }}</td>
                          <td class="text-center">{{ prospect.ams_customer.customer.code }}</td>
                          <td class="text-center">{{ prospect.ams_customer.customer.name }}</td>
                          <td class="text-center">{{ prospect.ams_customer.ams.initial }}</td>
                          <td>
                            <div v-if="prospect.market_share" class="text-center" style="color: #50CD89">
                              ${{ prospect.market_share }}
                            </div>
                            <div v-else class="text-center" style="color: #50CD89">
                              $
                            </div>
                          </td>

                            <td v-if="prospect.sales" class="text-center" style="color: #50CD89">
                              ${{ prospect.sales.value }}
                            </td>
                            <td v-else class="text-center" style="color: #50CD89">
                              $
                            </td>
                          
                          <td class="text-center">
                            <nuxt-link
                              v-if="prospect"
                              :to="{ path: 'view-prospect', query: { id: prospect.ams_customer.customer.id }}"
                              class="btn btn-sm btn-light"
                              >View</nuxt-link
                            >
                          </td>
                        </tr>
                        <tr v-if="prospect.length < 1">
                          <td colspan="12">
                            <div class="text-muted text-center">
                              Data not found
                            </div>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </div>
                <div class="tab-pane fade" id="kt_tab_pane_3" role="tabpanel">
                  <div class="table-responsive">
                    <table
                      class="table table-row-bordered table-row-gray-200 gy-4"
                    >
                      <thead>
                        <tr class="fw-bold fs-6 text-gray-800">
                          <th class="text-center">No</th>
                          <th class="text-center">Year</th>
                          <th class="text-center">Transaction</th>
                          <th class="text-center">Type</th>
                          <th class="text-center">Strategic Initiative</th>
                          <th class="text-center">PM</th>
                          <th class="text-center">Customer Code</th>
                          <th class="text-center">Customer</th>
                          <th class="text-center">AMS</th>
                          <th class="text-center">Market Share</th>
                          <th class="text-center">Sales Plan</th>
                          <th class="text-center">Action</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr
                          v-for="(
                            prospect, prospect_index
                          ) in prospect"
                          :key="prospect_index"
                        >
                          <td class="text-center">
                            {{ prospect3.from + prospect_index }}
                          </td>
                          <td class="text-center">{{ prospect.year }}</td>
                          <td class="text-center">{{ prospect.transaction_type.name }}</td>
                          <td class="text-center">{{ prospect.prospect_type.name }}</td>
                          <td class="text-center">{{ prospect.strategic_initiative.name }}</td>
                          <td class="text-center">{{ prospect.pm.name }}</td>
                          <td class="text-center">{{ prospect.ams_customer.customer.code }}</td>
                          <td class="text-center">{{ prospect.ams_customer.customer.name }}</td>
                          <td class="text-center">{{ prospect.ams_customer.ams.initial }}</td>
                          <td>
                            <div v-if="prospect.market_share" class="text-center" style="color: #50CD89">
                              ${{ prospect.market_share }}
                            </div>
                            <div v-else class="text-center" style="color: #50CD89">
                              $
                            </div>
                          </td>

                            <td v-if="prospect.sales" class="text-center" style="color: #50CD89">
                              ${{ prospect.sales.value }}
                            </td>
                            <td v-else class="text-center" style="color: #50CD89">
                              $
                            </td>
                          
                          <td class="text-center">
                            <nuxt-link
                              v-if="prospect"
                              :to="{ path: 'view-prospect', query: { id: prospect.ams_customer.customer.id }}"
                              class="btn btn-sm btn-light"
                              >View</nuxt-link
                            >
                          </td>
                        </tr>
                        <tr v-if="prospect.length < 1">
                          <td colspan="12">
                            <div class="text-muted text-center">
                              Data not found
                            </div>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </div>
                <div class="tab-pane fade" id="kt_tab_pane_4" role="tabpanel">
                  <div class="table-responsive">
                    <table
                      class="table table-row-bordered table-row-gray-200 gy-4"
                    >
                      <thead>
                        <tr class="fw-bold fs-6 text-gray-800">
                          <th class="text-center">No</th>
                          <th class="text-center">Year</th>
                          <th class="text-center">Transaction</th>
                          <th class="text-center">Type</th>
                          <th class="text-center">Strategic Initiative</th>
                          <th class="text-center">PM</th>
                          <th class="text-center">Customer Code</th>
                          <th class="text-center">Customer</th>
                          <th class="text-center">AMS</th>
                          <th class="text-center">Market Share</th>
                          <th class="text-center">Sales Plan</th>
                          <th class="text-center">Action</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr
                          v-for="(
                            prospect, prospect_index
                          ) in prospect"
                          :key="prospect_index"
                        >
                          <td class="text-center">
                            {{ prospect3.from + prospect_index }}
                          </td>
                          <td class="text-center">{{ prospect.year }}</td>
                          <td class="text-center">{{ prospect.transaction_type.name }}</td>
                          <td class="text-center">{{ prospect.prospect_type.name }}</td>
                          <td class="text-center">{{ prospect.strategic_initiative.name }}</td>
                          <td class="text-center">{{ prospect.pm.name }}</td>
                          <td class="text-center">{{ prospect.ams_customer.customer.code }}</td>
                          <td class="text-center">{{ prospect.ams_customer.customer.name }}</td>
                          <td class="text-center">{{ prospect.ams_customer.ams.initial }}</td>
                          <td>
                            <div v-if="prospect.market_share" class="text-center" style="color: #50CD89">
                              ${{ prospect.market_share }}
                            </div>
                            <div v-else class="text-center" style="color: #50CD89">
                              $
                            </div>
                          </td>

                            <td v-if="prospect.sales" class="text-center" style="color: #50CD89">
                              ${{ prospect.sales.value }}
                            </td>
                            <td v-else class="text-center" style="color: #50CD89">
                              $
                            </td>
                          
                          <td class="text-center">
                            <nuxt-link
                              v-if="prospect"
                              :to="{ path: 'view-prospect', query: { id: prospect.ams_customer.customer.id }}"
                              class="btn btn-sm btn-light"
                              >View</nuxt-link
                            >
                          </td>
                        </tr>
                        <tr v-if="prospect.length < 1">
                          <td colspan="12">
                            <div class="text-muted text-center">
                              Data not found
                            </div>
                          </td>
                        </tr>
                      </tbody>
                    </table>
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
                        @change="listProspect()"
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
                        disabled: !prospect3.prev_page_url,
                      }"
                      @click="prospect3.prev_page_url && listProspect(prospect3.prev_page_url)"
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
                        disabled: !prospect3.next_page_url,
                      }"
                      @click="prospect3.next_page_url && listProspect(prospect3.next_page_url)"
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
    <div
      class="modal fade"
      id="kt_modal_create_app"
      tabindex="-1"
      aria-hidden="true"
    >
      <!--begin::Modal dialog-->
      <div class="modal-dialog modal-fullscreen">
        <!--begin::Modal content-->
        <div class="modal-content">
          <!--begin::Modal body-->
          <div class="modal-body px-0 py-0">
            <!--begin::Stepper-->
            <div
              class="
                stepper stepper-pills stepper-column
                d-flex
                flex-column flex-lg-row
                h-100
              "
              id="kt_stepper_example_vertical"
            >
              <div class="row h-100 w-100">
                <div
                  class="col-md-3 d-flex align-items-start bg-dark text-white"
                >
                  <!--begin::Aside-->
                  <div class="px-10">
                    <!--begin::Nav-->
                    <div class="stepper-nav mt-10 py-10">
                      <!--begin::Step 1-->
                      <div
                        class="stepper-item me-5 current"
                        data-kt-stepper-element="nav"
                      >
                        <!--begin::Wrapper-->
                        <div class="stepper-wrapper d-flex align-items-center">
                          <!--begin::Icon-->
                          <div class="stepper-icon w-40px h-40px">
                            <i class="stepper-check fas fa-check"></i>
                            <span class="stepper-number">1</span>
                          </div>
                          <!--end::Icon-->

                          <!--begin::Label-->
                          <div class="stepper-label">
                            <h6
                              class="stepper-title fs-6 current"
                              data-kt-stepper-text="text"
                            >
                              Prospect Type
                            </h6>
                            <div class="stepper-desc fs-9">
                              Select Prospect Type
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
                      <div
                        class="stepper-item me-5"
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
                            <h3 class="stepper-title fs-6">
                              Year and Customer
                            </h3>
                            <div class="stepper-desc fs-9">
                              Select Year and Customer
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
                      <div
                        class="stepper-item me-5"
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
                            <h3 class="stepper-title fs-6">
                              Transaction & Project Type
                            </h3>
                            <div class="stepper-desc fs-9">
                              Select Transaction & Project Type
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
                      <div
                        class="stepper-item me-5"
                        data-kt-stepper-element="nav"
                      >
                        <!--begin::Wrapper-->
                        <div class="stepper-wrapper d-flex align-items-center">
                          <!--begin::Icon-->
                          <div class="stepper-icon w-40px h-40px">
                            <i class="stepper-check fas fa-check"></i>
                            <span class="stepper-number">4</span>
                          </div>
                          <!--begin::Icon-->

                          <!--begin::Label-->
                          <div class="stepper-label">
                            <h3 class="stepper-title fs-6">Complete Form</h3>
                            <div class="stepper-desc fs-9">
                              Fill All Required Field
                            </div>
                          </div>
                          <!--end::Label-->
                        </div>
                        <!--end::Wrapper-->
                      </div>
                      <!--end::Step 4-->
                    </div>
                    <!--end::Nav-->
                  </div>
                </div>
                <div class="col-md-9">
                  <form class="w-100 p-3">
                    <div class="row mt-5">
                      <!--begin::Content-->
                      <div class="flex-row-fluid">
                        <!--begin::Form-->
                        <div
                          class="form px-5 py-5 mx-auto"
                          novalidate="novalidate"
                        >
                          <!--begin::Group-->
                          <div class="mb-5 d-flex justify-content-center">
                            <!--begin::Step 1-->
                            <div
                              class="
                                flex-column flex-column
                                w-50
                                p-3
                                w-50
                                p-3
                                current
                              "
                              data-kt-stepper-element="content"
                            >
                              <div class="w-100 p-3">
                                <h3 class="mb-1">Select Prospect Type</h3>
                                <p class="fs-7 mb-5 text-muted">
                                  If you need more info, please check out FAQ
                                  Page
                                </p>
                                <!--begin::Option-->

                                <div
                                  class="mt-10"
                                  v-for="(
                                    prospectType, prospect_type_index
                                  ) in prospect_type.data"
                                  :key="prospect_type_index"
                                >
                                  <input
                                    type="radio"
                                    class="btn-check"
                                    name="prospectType"
                                    v-model="prospect.prospect_type_id"
                                    :value="prospectType.id"
                                    :id="prospectType.name"
                                  />
                                  <label
                                    class="
                                      btn
                                      btn-outline
                                      btn-outline-dashed
                                      btn-active-light-primary
                                      p-7
                                      d-flex
                                      align-items-center
                                      mb-5
                                    "
                                    :for="prospectType.name"
                                  >
                                    <span
                                      class="svg-icon svg-icon-3hx"
                                      v-if="prospect_type_index % 2 == 0"
                                      ><svg
                                        width="100"
                                        height="100"
                                        viewBox="0 0 24 24"
                                        fill="none"
                                        xmlns="http://www.w3.org/2000/svg"
                                      >
                                        <path
                                          d="M6.28548 15.0861C7.34369 13.1814 9.35142 12 11.5304 12H12.4696C14.6486 12 16.6563 13.1814 17.7145 15.0861L19.3493 18.0287C20.0899 19.3618 19.1259 21 17.601 21H6.39903C4.87406 21 3.91012 19.3618 4.65071 18.0287L6.28548 15.0861Z"
                                          fill="currentColor"
                                        />
                                        <rect
                                          opacity="0.3"
                                          x="8"
                                          y="3"
                                          width="8"
                                          height="8"
                                          rx="4"
                                          fill="currentColor"
                                        />
                                      </svg>
                                    </span>
                                    <span v-else class="svg-icon svg-icon-3hx"
                                      ><svg
                                        width="100"
                                        height="100"
                                        viewBox="0 0 24 24"
                                        fill="none"
                                        xmlns="http://www.w3.org/2000/svg"
                                      >
                                        <path
                                          d="M3 2H10C10.6 2 11 2.4 11 3V10C11 10.6 10.6 11 10 11H3C2.4 11 2 10.6 2 10V3C2 2.4 2.4 2 3 2Z"
                                          fill="currentColor"
                                        />
                                        <path
                                          opacity="0.3"
                                          d="M14 2H21C21.6 2 22 2.4 22 3V10C22 10.6 21.6 11 21 11H14C13.4 11 13 10.6 13 10V3C13 2.4 13.4 2 14 2Z"
                                          fill="currentColor"
                                        />
                                        <path
                                          opacity="0.3"
                                          d="M3 13H10C10.6 13 11 13.4 11 14V21C11 21.6 10.6 22 10 22H3C2.4 22 2 21.6 2 21V14C2 13.4 2.4 13 3 13Z"
                                          fill="currentColor"
                                        />
                                        <path
                                          opacity="0.3"
                                          d="M14 13H21C21.6 13 22 13.4 22 14V21C22 21.6 21.6 22 21 22H14C13.4 22 13 21.6 13 21V14C13 13.4 13.4 13 14 13Z"
                                          fill="currentColor"
                                        />
                                      </svg>
                                    </span>
                                    <!--end::Svg Icon-->

                                    <span
                                      class="
                                        d-block
                                        fw-semibold
                                        text-start
                                        align-items-center
                                      "
                                    >
                                      <span
                                        class="text-dark fw-bold d-block fs-6"
                                        >{{ prospectType.name }}</span
                                      >
                                      <p
                                        class="text-muted fw-semibold fs-7 mb-0"
                                      >
                                        {{ prospectType.description }}
                                      </p>
                                    </span>
                                  </label>
                                </div>
                              </div>
                            </div>
                            <!--end::Step 1-->

                            <!--begin::Step 2-->
                            <div
                              class="flex-column w-50 p-3 w-50 p-3"
                              data-kt-stepper-element="content"
                            >
                              <div class="w-100">
                                <h3 class="mb-1">Select Year and Customer</h3>
                                <p class="fs-7 mb-5 text-muted">
                                  If you need more info, please check out FAQ
                                  Page
                                </p>
                                <div class="row">
                                  <div v-if="prospect.prospect_type_id == 1">
                                    <div class="mb-3">
                                      <label
                                        for="exampleFormControlInput1"
                                        class="form-label"
                                        >Year</label
                                      >
                                      <input
                                        type="text"
                                        class="form-control form-control-sm"
                                      />
                                    </div>
                                    <div class="mb-3">
                                      <label
                                        for="exampleFormControlInput1"
                                        class="form-label"
                                        >Customer</label
                                      >
                                      <multiselect
                                        v-model="customer_value"
                                        :options="customer_options"
                                        placeholder=""
                                        label="name"
                                      ></multiselect>
                                    </div>
                                    <div class="mb-3">
                                      <label
                                        for="exampleFormControlInput1"
                                        class="form-label"
                                        >Area & AMS</label
                                      >
                                      <multiselect
                                        v-if="customer_value == null"
                                        :disabled="!customer_value"
                                        v-model="area_ams_value"
                                        :options="area_ams_options"
                                        placeholder=""
                                        label="name"
                                      ></multiselect>
                                      <multiselect
                                        v-else
                                        v-model="area_ams_value"
                                        :options="area_ams_options"
                                        placeholder=""
                                        label="name"
                                      ></multiselect>
                                    </div>
                                  </div>
                                  <div
                                    v-else-if="prospect.prospect_type_id == 2"
                                  >
                                    <div class="mb-3">
                                      <label
                                        for="exampleFormControlInput1"
                                        class="form-label"
                                        >Year</label
                                      >
                                      <input
                                        type="text"
                                        class="form-control form-control-sm"
                                      />
                                    </div>
                                    <div class="mb-3">
                                      <label
                                        for="exampleFormControlInput1"
                                        class="form-label"
                                        >Customer</label
                                      >
                                      <multiselect
                                        v-model="customer_value"
                                        :options="customer_options"
                                        placeholder=""
                                        label="name"
                                      ></multiselect>
                                    </div>
                                    <div class="mb-3">
                                      <label
                                        for="exampleFormControlInput1"
                                        class="form-label"
                                        >Area & AMS</label
                                      >
                                      <multiselect
                                        v-if="customer_value == null"
                                        :disabled="!customer_value"
                                        v-model="area_ams_value"
                                        :options="area_ams_options"
                                        placeholder=""
                                        label="name"
                                      ></multiselect>
                                      <multiselect
                                        v-else
                                        v-model="area_ams_value"
                                        :options="area_ams_options"
                                        placeholder=""
                                        label="name"
                                      ></multiselect>
                                    </div>
                                    <div class="mb-3">
                                      <label
                                        for="exampleFormControlInput1"
                                        class="form-label"
                                        >Strategic Initiative</label
                                      >
                                      <multiselect
                                        v-model="strategic_initiative_value"
                                        :options="strategic_initiative_options"
                                        placeholder=""
                                        label="name"
                                      ></multiselect>
                                    </div>
                                    <div class="mb-3">
                                      <label
                                        for="exampleFormControlInput1"
                                        class="form-label"
                                        >Project Manager</label
                                      >
                                      <multiselect
                                        v-model="project_manager_value"
                                        :options="project_manager_options"
                                        placeholder=""
                                        label="name"
                                      ></multiselect>
                                    </div>
                                  </div>
                                </div>
                              </div>
                            </div>
                            <!--end::Step 2-->

                            <!--begin::Step 3-->
                            <div
                              class="flex-column w-50 p-3"
                              data-kt-stepper-element="content"
                            >
                              <div class="w-100">
                                <h3 class="mb-1">Select Transaction Type</h3>
                                <p class="fs-7 mb-5 text-muted">
                                  If you need more info, please check out FAQ
                                  Page
                                </p>
                                <!--begin::Option-->
                                <div
                                  class="mt-10"
                                  v-for="(
                                    transactionType, transactionType_index
                                  ) in transaction_type.data"
                                  :key="transactionType_index"
                                >
                                  <input
                                    type="radio"
                                    class="btn-check"
                                    name="transaction_type"
                                    v-model="prospect.transaction_type_id"
                                    :value="transactionType.id"
                                    :id="transactionType.name"
                                  />
                                  <label
                                    class="
                                      btn
                                      btn-outline
                                      btn-outline-dashed
                                      btn-active-light-primary
                                      p-7
                                      d-flex
                                      align-items-center
                                      mb-5
                                    "
                                    :for="transactionType.name"
                                  >
                                    <span
                                      class="svg-icon svg-icon-3hx"
                                      v-if="transactionType_index % 2 == 0"
                                      ><svg
                                        width="100"
                                        height="100"
                                        viewBox="0 0 24 24"
                                        fill="none"
                                        xmlns="http://www.w3.org/2000/svg"
                                      >
                                        <path
                                          d="M6.28548 15.0861C7.34369 13.1814 9.35142 12 11.5304 12H12.4696C14.6486 12 16.6563 13.1814 17.7145 15.0861L19.3493 18.0287C20.0899 19.3618 19.1259 21 17.601 21H6.39903C4.87406 21 3.91012 19.3618 4.65071 18.0287L6.28548 15.0861Z"
                                          fill="currentColor"
                                        />
                                        <rect
                                          opacity="0.3"
                                          x="8"
                                          y="3"
                                          width="8"
                                          height="8"
                                          rx="4"
                                          fill="currentColor"
                                        />
                                      </svg>
                                    </span>
                                    <span v-else class="svg-icon svg-icon-3hx"
                                      ><svg
                                        width="100"
                                        height="100"
                                        viewBox="0 0 24 24"
                                        fill="none"
                                        xmlns="http://www.w3.org/2000/svg"
                                      >
                                        <path
                                          d="M3 2H10C10.6 2 11 2.4 11 3V10C11 10.6 10.6 11 10 11H3C2.4 11 2 10.6 2 10V3C2 2.4 2.4 2 3 2Z"
                                          fill="currentColor"
                                        />
                                        <path
                                          opacity="0.3"
                                          d="M14 2H21C21.6 2 22 2.4 22 3V10C22 10.6 21.6 11 21 11H14C13.4 11 13 10.6 13 10V3C13 2.4 13.4 2 14 2Z"
                                          fill="currentColor"
                                        />
                                        <path
                                          opacity="0.3"
                                          d="M3 13H10C10.6 13 11 13.4 11 14V21C11 21.6 10.6 22 10 22H3C2.4 22 2 21.6 2 21V14C2 13.4 2.4 13 3 13Z"
                                          fill="currentColor"
                                        />
                                        <path
                                          opacity="0.3"
                                          d="M14 13H21C21.6 13 22 13.4 22 14V21C22 21.6 21.6 22 21 22H14C13.4 22 13 21.6 13 21V14C13 13.4 13.4 13 14 13Z"
                                          fill="currentColor"
                                        />
                                      </svg>
                                    </span>
                                    <!--end::Svg Icon-->

                                    <span
                                      class="
                                        d-block
                                        fw-semibold
                                        text-start
                                        align-items-center
                                      "
                                    >
                                      <span
                                        class="text-dark fw-bold d-block fs-6"
                                        >{{ transactionType.name }}</span
                                      >
                                      <p
                                        class="text-muted fw-semibold fs-7 mb-0"
                                      >
                                        {{ transactionType.description }}
                                      </p>
                                    </span>
                                  </label>
                                  <!--end::Option-->
                                </div>
                                <!--begin::Option-->
                              </div>
                            </div>
                            <!--end::Step 3-->

                            <!--begin::Step 4-->
                            <div
                              class="flex-column w-100"
                              data-kt-stepper-element="content"
                            >
                              <h3 class="mb-1">Form Add Prospect</h3>
                              <p class="fs-7 mb-5 text-muted">
                                If you need more info, please check out FAQ Page
                              </p>
                              <div v-if="prospect.transaction_type_id == 1">
                                <div class="row mb-5">
                                  <div class="col-sm-4">
                                    <div class="input-group mb-3">
                                      <multiselect
                                        v-model="product_value"
                                        placeholder="search and select product"
                                        label="name"
                                        :options="product_options"
                                      ></multiselect>
                                    </div>
                                  </div>
                                  <div class="col">
                                    <button
                                      @click="addProspectTMB(product_value)"
                                      class="btn btn-primary rounded"
                                      type="button"
                                      :disabled="product_value == null"
                                    >
                                      Add Product
                                    </button>
                                  </div>
                                </div>
                                <!--begin::Repeater-->
                                <!--begin::Form group-->
                                <div
                                  class="mb-20 mt-20"
                                  v-for="(data, data_index) in tmb"
                                  :key="data_index"
                                >
                                  <div
                                    class="row mb-10 d-flex align-items-center"
                                  >
                                    <h1 class="fw-bold mb-0">
                                      {{ data_index + 1 }}. {{ data.name }}
                                    </h1>
                                  </div>
                                  <div class="form-group">
                                    <div
                                      class="form-group row mb-5"
                                      v-for="(item, item_index) in tmb[
                                        data_index
                                      ].product"
                                      :key="item_index"
                                    >
                                      <div class="col-md-3 text-center">
                                        <label class="form-label"
                                          >Aircraft Type</label
                                        >
                                        <input
                                          v-model="item.aircraft_type"
                                          type="text"
                                          class="form-control mb-2 mb-md-0"
                                        />
                                      </div>
                                      <div class="col-md-3 text-center">
                                        <label class="form-label"
                                          >Market Share</label
                                        >
                                        <input
                                          type="text"
                                          v-model="item.market_share"
                                          class="form-control mb-2 mb-md-0"
                                        />
                                      </div>
                                      <div class="col-md-2 text-center">
                                        <label class="form-label">Remark</label>
                                        <input
                                          type="text"
                                          v-model="item.remark"
                                          class="form-control mb-2 mb-md-0"
                                        />
                                      </div>
                                      <div class="col-md-3 text-center">
                                        <label class="form-label"
                                          >Maintenance Event</label
                                        >
                                        <input
                                          type="text"
                                          v-model="item.maintenance_event"
                                          class="form-control mb-2 mb-md-0"
                                        />
                                      </div>
                                      <div class="col-md-1">
                                        <button
                                          type="button"
                                          @click="
                                            removeTMB(data_index, item_index)
                                          "
                                          class="btn btn-danger mt-3 mt-md-8"
                                        >
                                          Delete
                                        </button>
                                      </div>
                                    </div>
                                  </div>
                                  <!--begin::Form group-->
                                  <div class="form-group mt-5">
                                    <button
                                      data-repeater-create
                                      class="btn btn-primary btn-sm"
                                      type="button"
                                      @click="addTMB(data_index, data)"
                                    >
                                      <i class="la la-plus"></i>Add
                                    </button>
                                  </div>
                                  <!--end::Form group-->
                                </div>
                                <!--end::Form group-->

                                <!--end::Repeater-->
                              </div>
                              <div
                                v-else-if="prospect.transaction_type_id == 2"
                              >
                                <div class="row mb-5">
                                  <div class="col">
                                    <div class="input-group mb-3">
                                      <label class="form-label fw-bold"
                                        >Select Product</label
                                      >
                                      <multiselect
                                        v-model="product_value"
                                        label="name"
                                        placeholder="search and select product"
                                        :options="product_options"
                                      ></multiselect>
                                    </div>
                                  </div>
                                  <div class="col">
                                    <div class="input-group mb-3">
                                      <label class="form-label fw-bold"
                                        >Select Aircraft Type</label
                                      >
                                      <multiselect
                                        v-model="aircraft_type_value"
                                        placeholder="search and select aircraft type"
                                        label="name"
                                        :options="aircraft_type_options"
                                      ></multiselect>
                                    </div>
                                  </div>
                                  <div class="col d-flex align-items-end">
                                    <button
                                      class="mb-3 btn btn-primary rounded"
                                      type="button"
                                      :disabled="
                                        product_value == null ||
                                        aircraft_type_value == null
                                      "
                                      @click="
                                        addPBTH(
                                          product_value,
                                          aircraft_type_value
                                        )
                                      "
                                    >
                                      Add Data
                                    </button>
                                  </div>
                                </div>
                                <div
                                  v-for="(data_pbth, index_pbth) in pbth"
                                  :key="index_pbth"
                                >
                                  <div class="row mt-10 mb-5">
                                    <h2 class="fw-bold mb-4">
                                      {{ index_pbth + 1 }}.
                                      {{
                                        data_pbth.product_name +
                                        ' - ' +
                                        data_pbth.aircraft_type_name
                                      }}
                                    </h2>
                                    <div class="ms-7">
                                      <p class="text-muted mb-1 fw-bold">
                                        Market Share
                                      </p>
                                      <h2 class="fw-bold">$3,920.00</h2>
                                      <p
                                        class="
                                          text-muted
                                          mb-1
                                          mt-8
                                          fw-bold
                                          fs-6
                                        "
                                      >
                                        Target
                                      </p>
                                      <div
                                        class="
                                          row
                                          d-flex
                                          justify-content-between
                                        "
                                      >
                                        <div
                                          class="col-sm-6"
                                          v-for="(
                                            target_month, target_index
                                          ) in data_pbth.target"
                                          :key="target_index"
                                        >
                                          <div class="row">
                                            <div
                                              class="
                                                col-md-2
                                                d-flex
                                                align-items-center
                                              "
                                            >
                                              <h3 class="fs-7">
                                                {{ target_month.month }}
                                              </h3>
                                            </div>
                                            <div class="col-md-5">
                                              <div class="mb-3">
                                                <label
                                                  class="
                                                    form-label
                                                    text-muted
                                                    fs-7
                                                  "
                                                  >Target Rate</label
                                                >
                                                <input
                                                  type="text"
                                                  v-model="target_month.rate"
                                                  class="
                                                    form-control form-control-sm
                                                  "
                                                />
                                              </div>
                                            </div>
                                            <div class="col-md-5">
                                              <div class="mb-3">
                                                <label
                                                  class="
                                                    form-label
                                                    text-muted
                                                    fs-7
                                                  "
                                                  >Target FH</label
                                                >
                                                <input
                                                  type="text"
                                                  v-model="
                                                    target_month.flight_hour
                                                  "
                                                  class="
                                                    form-control form-control-sm
                                                  "
                                                />
                                              </div>
                                            </div>
                                          </div>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="row mt-5">
                                      <div class="col">
                                        <button
                                          type="button"
                                          class="btn btn-danger btn-sm ms-5"
                                          @click="removePBTH(index_pbth)"
                                        >
                                          <i class="la la-trash-o"></i> Delete
                                        </button>
                                      </div>
                                    </div>
                                  </div>
                                </div>
                              </div>
                            </div>
                            <!--end::Step 4-->
                          </div>
                          <!--end::Group-->
                        </div>
                        <!--end::Form-->
                      </div>
                    </div>
                    <div class="row d-flex justify-content-center me-20 ms-20">
                      <div class="col-md-6">
                        <button
                          v-if="step_number == 1"
                          type="button"
                          data-bs-dismiss="modal"
                          class="btn btn-light text-primary mt-5"
                        >
                          Close
                        </button>
                        <button
                          type="button"
                          class="btn btn-light text-primary mt-5"
                          data-kt-stepper-action="previous"
                          @click="backStep()"
                        >
                          Back
                        </button>
                      </div>
                      <div class="col-md-6 d-flex justify-content-end">
                        <!--begin::Actions-->

                        <!--begin::Wrapper-->
                        <button
                          class="btn btn-primary mt-5 align-self-end"
                          type="button"
                          data-kt-stepper-action="next"
                          @click="nextStep()"
                          :disabled="prospect.prospect_type_id == null"
                        >
                          Next
                        </button>
                        <!--end::Wrapper-->

                        <!--begin::Wrapper-->
                        <button
                          type="button"
                          class="btn btn-primary mt-5"
                          data-kt-stepper-action="submit"
                        >
                          <span class="indicator-label"> Save </span>
                          <span class="indicator-progress">
                            Please wait...
                            <span
                              class="
                                spinner-border spinner-border-sm
                                align-middle
                                ms-2
                              "
                            ></span>
                          </span>
                        </button>
                        <!--end::Wrapper-->
                        <!--end::Actions-->
                      </div>
                    </div>
                  </form>
                </div>
              </div>
            </div>
            <!--end::Stepper-->
          </div>
          <!--end::Modal body-->
        </div>
        <!--end::Modal content-->
      </div>
      <!--end::Modal dialog-->
    </div>
  </div>
</template>

<script>
import debounce from 'lodash/debounce'
export default {
  layout: 'template',
  name: 'MyProspectPage',
  layout: 'template',
  data() {
    return {
      currentYear:  new Date().getFullYear(),
      airc4aft_type_value: null,
      product_value: null,
      area_ams_value: null,
      customer_value: null,
      strategic_initiative_value: null,
      project_manager_value: null,
      product_options: [],
      aircraft_type_options: [],
      customer_options: [],
      area_ams_options: [],
      strategic_initiative_options: [],
      project_manager_options: [],
      prospect: [],
      prospect2: [],
      prospect3: [],
      step_number: 1,
      // chart: new ApexCharts(),
      pie_one: {
        series: [1],
        chartOptions: {
          chart: {
            type: 'radialBar',
            offsetY: -25,
            offsetX: 110,
            sparkline: {
              enabled: true,
            },
          },
          plotOptions: {
            radialBar: {
              startAngle: -90,
              endAngle: 90,
              track: {
                background: '#e7e7e7',
                strokeWidth: '97%',
                margin: 5, // margin is in pixels
                dropShadow: {
                  enabled: true,
                  top: 2,
                  left: 0,
                  color: '#999',
                  opacity: 1,
                  blur: 2,
                },
              },
              dataLabels: {
                name: {
                  show: true,
                  offsetY: -20,
                },
                value: {
                  offsetY: -5,
                  fontSize: '22px',
                },
              },
            },
          },
          grid: {
            padding: {
              top: -10,
              bottom: 25,
            },
            margin: {
              top: 20,
              bottom: 20,
            },
          },
          fill: {
            type: 'gradient',
            gradient: {
              shade: 'light',
              shadeIntensity: 0.4,
              inverseColors: false,
              opacityFrom: 1,
              opacityTo: 1,
              stops: [0, 50, 53, 91],
            },
          },
          labels: ['Deviation'],
        },
      },
      prospect_type: {
        data: [],
      },
      transaction_type: {
        data: [],
      },
      transaction: {
        id: null,
        name: null,
        description: null,
      },
      tmb: [],
      product: [],
      product_id: null,
      pbth: [],
      modal_create: false,
      search: null,
      order: 'id',
      by: 'desc',
      paginate: '10',
      filter: null,
      current_page: null,
      errors: {
        name: null,
        description: null,
      },
      year: this.currentYear,
    }
  },
  created() {
    this.listProduct()
    this.listAircraftType()
    this.listProspectType()
    this.listTransactionType()
    this.listCustomer()
    this.listStrategicInitiative()
    this.listUser()
    this.listProspect()
    this.listAms()
  },
  mounted() {
    KTStepper.getInstance()
    this.step()
  },
  watch: {
    filter: debounce(function () {
      this.listProspect()
    }, 500),
  },
  methods: {
    nextStep() {
      this.step_number++
    },
    backStep() {
      this.step_number--
    },
    addProspectTMB(value) {
      this.tmb.push({
        id: value.id,
        name: value.name,
        product: [
          {
            product_id: value.id,
            aircraft_type: null,
            marker_share: null,
            remark: null,
            maintenance_event: null,
          },
        ],
      })
    },
    addTMB(data_index, data) {
      this.tmb[data_index].product.push({
        product_id: data.id,
        ac_type_id: null,
        market_share: null,
        remark: null,
        maintenance_event: null,
      })
    },
    addPBTH(product_value, aircraft_type_value) {
      this.pbth.push({
        product_id: product_value.id,
        product_name: product_value.name,
        aircraft_type_id: aircraft_type_value.id,
        aircraft_type_name: aircraft_type_value.name,
        target: [
          {
            month: 'January',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'February',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'March',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'April',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'May',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'June',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'July',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'August',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'September',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'October',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'November',
            rate: null,
            flight_hour: null,
          },
          {
            month: 'December',
            rate: null,
            flight_hour: null,
          },
        ],
      })
    },
    removeProspectTMB(data_index) {
      this.tmb.splice(data_index, 1)
    },
    removeTMB(data_index, item_index) {
      this.tmb[data_index].product.splice(item_index, 1)
      if (this.tmb[data_index].product == '') {
        this.tmb.splice(data_index, 1)
      }
    },
    removePBTH(index_pbth) {
      this.pbth.splice(index_pbth, 1)
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
          console.log("Data Customer")
          console.log(this.customer_options)
        })
    },
    listStrategicInitiative() {
      this.$axios
        .get('api/strategic-initiative', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.strategic_initiative_options = response.data.data.data
        })
    },
    listUser() {
      this.$axios
        .get('api/users', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.project_manager_options = response.data.data.data
        })
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
          this.product_options = response.data.data.data
        })
    },
    listAircraftType() {
      this.$axios
        .get('api/aircraft-type', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.aircraft_type_options = response.data.data.data
        })
    },
    listProspectType() {
      this.$axios
        .get('api/prospect-type', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.prospect_type = response.data.data
        })
    },
    listProspect(paginate) {
      this.loading()
        paginate = paginate || `/api/prospect`
      this.$axios
        .get(paginate, {
          params: {
            filter: this.year,
            paginate: this.paginate,
          },
        })
        .then((response) => {
          // Data Prospect
          this.prospect = response.data.data.prospect.data
          // Data Total Market share, Total salesplan & Deviation
          this.prospect2 = response.data.data
          // Pagination
          this.prospect3 = response.data.data.prospect
          // Total Deviation
          this.totalDeviation = response.data.data.deviation
          // Current Page
          this.current_page = this.prospect3.current_page
          Swal.close()
          this.chart = new ApexCharts().updateSeries([{
            data: [32, 44, 31, 41, 22]
          }])
        })
        .catch((error) => console.log(error))
    },
    filterYear(year){
      this.year = year
      this.listProspect()
    },
    listAms() {
      this.$axios
        .get('api/ams', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.area_ams_options = response.data.data.data
          console.log("Data AMS")
          console.log(this.area_ams_options)
        })
    },
    listTransactionType() {
      this.loading()
      this.$axios
        .get('api/transaction-type', {
          params: {
            order: 'created_at',
            by: 'ASC',
          },
        })
        .then((response) => {
          this.transaction_type = response.data.data
          Swal.close()
        })
        .catch((error) => console.log(error))
    },
    directPage: debounce(function () {
      alert(this.prospect3.current_page)
      if (this.current_page < 1) {
        this.prospect3.current_page = 1
      } else if (this.prospect3.current_page > this.prospect3.last_page) {
        this.prospect3.current_page = this.prospect3.last_page
      }
      let url = new URL(this.prospect3.first_page_url)
      let filter_params = url.filterParams
      filter_params.set('page', this.prospect3.current_page)
      url.filter = filter_params.toString()
      let new_url = url.toString()
      this.listProspect(new_url)
    }, 500),
    create() {
      this.loading()
      this.$axios
        .post('/api/prospect-create', {
          year: this.prospect.year,
          transaction_type: this.prospect.transaction_type_id,
          prospect_type: this.prospect.prospect_type_id,
          strategic_initiative: this.prospect.strategic_initiative_id,
          pm: this.prospect.pm_id,
          ams_customer: this.prospect.ams_customer_id,
          prospect_id_tmb: this.prospect.prospect,
          prospect_id_tmb: this.prospect,
        })
        .then((response) => {
          toastr.success(response.data.message)
          this.list()
          this.closeModal()
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors

            toastr.error(error.response.data.message)
          }
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
      this.transaction.id = null
      this.transaction.name = null
      this.transaction.description = null
      this.errors.name = null
      this.errors.description = null
    },
    closeModal() {
      document.getElementById('close_modal').click()
      this.clearForm()
    },
    step() {
      var element = document.querySelector('#kt_stepper_example_vertical')
      var stepper = new KTStepper(element)
      stepper.on('kt.stepper.next', function (stepper) {
        stepper.goNext()
      })
      stepper.on('kt.stepper.previous', function (stepper) {
        stepper.goPrevious()
      })
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
#chart {
  height: 8.5rem;
}
</style>