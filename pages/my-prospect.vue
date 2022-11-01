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
                  Last 30 day earnings calculated. Apart from arranging the
                  order of topics.
                </p>
                <div class="col">
                  <div class="border-dashed p-4">
                    <h1 class="fw-bold mb-0">$1,500,000.00</h1>
                    <p class="mb-0 fw-bold text-gray-500">Total Market Share</p>
                  </div>
                </div>
                <div class="col">
                  <div class="border-dashed p-4">
                    <h1 class="fw-bold mb-0">$1,300,000.00</h1>
                    <p class="mb-0 fw-bold text-gray-500">Total Salesplan</p>
                  </div>
                </div>
              </div>
            </div>
            <div class="col justify-content-center text-center">
              <div id="chart">
                <VueApexCharts
                  width="350"
                  type="radialBar"
                  :options="pie_one.chartOptions"
                  :series="pie_one.series"
                ></VueApexCharts>
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
                    class="nav-link active text-dark"
                    exact-active-class="active"
                    data-bs-toggle="tab"
                    href="#kt_tab_pane_1"
                    >This Year</a
                  >
                </li>
                <li class="nav-item">
                  <a
                    class="nav-link text-dark"
                    active-class="active"
                    data-bs-toggle="tab"
                    href="#kt_tab_pane_2"
                    >2021</a
                  >
                </li>
                <li class="nav-item">
                  <a
                    class="nav-link text-dark"
                    active-class="active"
                    data-bs-toggle="tab"
                    href="#kt_tab_pane_3"
                    >2020</a
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
                          <th class="text-center">AMS</th>
                          <th class="text-center">Market Share</th>
                          <th class="text-center">Sales Plan</th>
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
                          <td class="text-center">
                            {{ transaction_type.from + transaction_index }}
                          </td>
                          <td class="text-center">{{ transaction.name }}</td>
                          <td class="text-center">
                            {{ transaction.description }}
                          </td>
                          <td class="d-flex justify-content-center">
                            <button
                              class="btn btn-sm btn-light"
                              data-bs-toggle="modal"
                              data-bs-target="#modal"
                              @click="edit(transaction)"
                            >
                              View
                            </button>
                          </td>
                        </tr>
                        <tr v-if="transaction_type.data.length < 1">
                          <td colspan="8">
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
                          <th class="text-center">AMS</th>
                          <th class="text-center">Market Share</th>
                          <th class="text-center">Sales Plan</th>
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
                          <td class="text-center">
                            {{ transaction_type.from + transaction_index }}
                          </td>
                          <td class="text-center">{{ transaction.name }}</td>
                          <td class="text-center">
                            {{ transaction.description }}
                          </td>
                          <td class="d-flex justify-content-center">
                            <button
                              class="btn btn-sm btn-light"
                              data-bs-toggle="modal"
                              data-bs-target="#modal"
                              @click="edit(transaction)"
                            >
                              View
                            </button>
                          </td>
                        </tr>
                        <tr v-if="transaction_type.data.length < 1">
                          <td colspan="8">
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
                          <th class="text-center">AMS</th>
                          <th class="text-center">Market Share</th>
                          <th class="text-center">Sales Plan</th>
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
                          <td class="text-center">
                            {{ transaction_type.from + transaction_index }}
                          </td>
                          <td class="text-center">{{ transaction.name }}</td>
                          <td class="text-center">
                            {{ transaction.description }}
                          </td>
                          <td class="d-flex justify-content-center">
                            <button
                              class="btn btn-sm btn-light"
                              data-bs-toggle="modal"
                              data-bs-target="#modal"
                              @click="edit(transaction)"
                            >
                              View
                            </button>
                          </td>
                        </tr>
                        <tr v-if="transaction_type.data.length < 1">
                          <td colspan="8">
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
                        @change="list()"
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
                  <div class="row mt-5 px-10">
                    <div class="col d-flex justify-content-end">
                      <button
                        type="button"
                        data-bs-dismiss="modal"
                        class="btn btn-light text-primary"
                      >
                        Close
                      </button>
                    </div>
                  </div>
                  <form class="w-100 p-3">
                    <div class="row mt-5">
                      <!--begin::Content-->
                      <div class="flex-row-fluid">
                        <!--begin::Form-->
                        <div
                          class="form px-10 py-10 mx-auto px-5"
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
                                <input
                                  type="radio"
                                  class="btn-check"
                                  name="prospect_type"
                                  value="apps"
                                  id="organic"
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
                                  for="organic"
                                >
                                  <!--begin::Svg Icon | path: /var/www/preview.keenthemes.com/kt-products/metronic/releases/2022-07-14-092914/core/html/src/media/icons/duotune/communication/com013.svg-->
                                  <span class="svg-icon svg-icon-3hx"
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
                                  <!--end::Svg Icon-->

                                  <span
                                    class="
                                      d-block
                                      fw-semibold
                                      text-start
                                      align-items-center
                                    "
                                  >
                                    <span class="text-dark fw-bold d-block fs-6"
                                      >Organic</span
                                    >
                                    <p class="text-muted fw-semibold fs-7 mb-0">
                                      If you need more info, please check it out
                                    </p>
                                  </span>
                                </label>
                                <!--end::Option-->

                                <!--begin::Option-->
                                <input
                                  type="radio"
                                  class="btn-check"
                                  name="prospect_type"
                                  value="sms"
                                  id="in_organic"
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
                                  "
                                  for="in_organic"
                                >
                                  <!--begin::Svg Icon | path: icons/duotune/communication/com003.svg-->
                                  <!--begin::Svg Icon | path: /var/www/preview.keenthemes.com/kt-products/metronic/releases/2022-07-14-092914/core/html/src/media/icons/duotune/general/gen008.svg-->
                                  <span class="svg-icon svg-icon-3hx"
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
                                  <!--end::Svg Icon-->

                                  <span
                                    class="
                                      d-block
                                      fw-semibold
                                      text-start
                                      align-items-center
                                    "
                                  >
                                    <span class="text-dark fw-bold d-block fs-6"
                                      >In Organic</span
                                    >
                                    <p class="text-muted fw-semibold fs-7 mb-0">
                                      Need to define which Strategic Initiative
                                      and selected PM
                                    </p>
                                  </span>
                                </label>
                                <!--end::Option-->
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
                                    <input
                                      type="text"
                                      class="form-control form-control-sm"
                                    />
                                  </div>
                                  <div class="mb-3">
                                    <label
                                      for="exampleFormControlInput1"
                                      class="form-label"
                                      >Area & AMS</label
                                    >
                                    <input
                                      type="text"
                                      class="form-control form-control-sm"
                                    />
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
                                <input
                                  type="radio"
                                  class="btn-check"
                                  name="transaction_type"
                                  value="apps"
                                  id="tmb"
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
                                  for="tmb"
                                >
                                  <!--begin::Svg Icon | path: /var/www/preview.keenthemes.com/kt-products/metronic/releases/2022-07-14-092914/core/html/src/media/icons/duotune/communication/com013.svg-->
                                  <span class="svg-icon svg-icon-3hx"
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
                                  <!--end::Svg Icon-->

                                  <span
                                    class="
                                      d-block
                                      fw-semibold
                                      text-start
                                      align-items-center
                                    "
                                  >
                                    <span class="text-dark fw-bold d-block fs-6"
                                      >TMB</span
                                    >
                                    <p class="text-muted fw-semibold fs-7 mb-0">
                                      Time Material Based
                                    </p>
                                  </span>
                                </label>
                                <!--end::Option-->

                                <!--begin::Option-->
                                <input
                                  type="radio"
                                  class="btn-check"
                                  name="transaction_type"
                                  value="sms"
                                  id="pbth"
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
                                  "
                                  for="pbth"
                                >
                                  <!--begin::Svg Icon | path: /var/www/preview.keenthemes.com/kt-products/metronic/releases/2022-07-14-092914/core/html/src/media/icons/duotune/general/gen008.svg-->
                                  <span class="svg-icon svg-icon-3hx"
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
                                  <!--end::Svg Icon-->

                                  <span
                                    class="
                                      d-block
                                      fw-semibold
                                      text-start
                                      align-items-center
                                    "
                                  >
                                    <span class="text-dark fw-bold d-block fs-6"
                                      >PBTH</span
                                    >
                                    <p class="text-muted fw-semibold fs-7 mb-0">
                                      Power By The Hours
                                    </p>
                                  </span>
                                </label>
                                <!--end::Option-->
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
                              <div class="row mb-5">
                                <div class="col">
                                  <div class="input-group mb-3">
                                    <multiselect
                                      v-model="value"
                                      placeholder="Search or add a product"
                                      label="name"
                                      track-by="code"
                                      :options="options"
                                      :multiple="true"
                                      :taggable="false"
                                    ></multiselect>
                                  </div>
                                </div>
                                <!-- <div class="col">
                                  <button
                                    class="btn btn-primary rounded"
                                    type="button"
                                  >
                                    Add Product
                                  </button>
                                </div> -->
                              </div>
                              <!--begin::Repeater-->
                              <div
                                v-for="(item, item_index) in value"
                                :key="item_index"
                              ></div>
                              <div id="kt_docs_repeater_basic">
                                <!--begin::Form group-->
                                <h3 class="mb-5 mt-5">Lable</h3>
                                <div class="form-group">
                                  <div
                                    data-repeater-list="kt_docs_repeater_basic"
                                  >
                                    <div data-repeater-item>
                                      <div class="form-group row mb-5">
                                        <div class="col-md-3 text-center">
                                          <label class="form-label"
                                            >Aircraft Type</label
                                          >
                                          <input
                                            type="email"
                                            class="form-control mb-2 mb-md-0"
                                          />
                                        </div>
                                        <div class="col-md-3 text-center">
                                          <label class="form-label"
                                            >Market Share</label
                                          >
                                          <input
                                            type="email"
                                            class="form-control mb-2 mb-md-0"
                                          />
                                        </div>
                                        <div class="col-md-2 text-center">
                                          <label class="form-label"
                                            >Remark</label
                                          >
                                          <input
                                            type="email"
                                            class="form-control mb-2 mb-md-0"
                                          />
                                        </div>
                                        <div class="col-md-3 text-center">
                                          <label class="form-label"
                                            >Maintenance Event</label
                                          >
                                          <input
                                            type="email"
                                            class="form-control mb-2 mb-md-0"
                                          />
                                        </div>
                                        <div class="col-md-1">
                                          <a
                                            data-repeater-delete
                                            class="
                                              btn btn-light-danger
                                              mt-3 mt-md-8
                                            "
                                          >
                                            <i class="la la-trash-o"></i>
                                          </a>
                                        </div>
                                      </div>
                                    </div>
                                  </div>
                                </div>
                                <!--end::Form group-->

                                <!--begin::Form group-->
                                <div class="form-group mt-5">
                                  <a
                                    data-repeater-create
                                    class="btn btn-light-primary"
                                  >
                                    <i class="la la-plus"></i>Add
                                  </a>
                                </div>
                                <!--end::Form group-->
                              </div>
                              <!--end::Repeater-->
                            </div>
                            <!--end::Step 4-->
                          </div>
                          <!--end::Group-->
                        </div>
                        <!--end::Form-->
                      </div>
                    </div>
                    <div class="row mt-5">
                      <!--begin::Actions-->
                      <div class="d-flex flex-stack mt-5">
                        <!--begin::Wrapper-->
                        <div class="me-2">
                          <button
                            type="button"
                            class="btn btn-light text-primary mt-5"
                            data-kt-stepper-action="previous"
                          >
                            Back
                          </button>
                        </div>
                        <!--end::Wrapper-->

                        <!--begin::Wrapper-->
                        <div>
                          <button
                            type="button"
                            class="btn btn-primary"
                            data-kt-stepper-action="submit"
                          >
                            <span class="indicator-label"> Submit </span>
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

                          <button
                            type="button"
                            class="btn btn-primary mt-5"
                            data-kt-stepper-action="next"
                          >
                            Continue
                          </button>
                        </div>
                        <!--end::Wrapper-->
                      </div>
                      <!--end::Actions-->
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
      value: [],
      options: [
        { name: 'Vue.js', code: 'vu' },
        { name: 'Javascript', code: 'js' },
        { name: 'Open Source', code: 'os' },
      ],
      pie_one: {
        series: [78],
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

      transaction_type: {
        data: [],
        link: [],
      },
      transaction: {
        id: null,
        name: null,
        description: null,
      },
      modal_create: false,
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
  mounted() {
    KTStepper.getInstance()
    KTFormRepeaterBasic.init()
    this.step()
  },
  watch: {
    search: debounce(function () {
      this.list()
    }, 500),
  },
  methods: {
    addTag(newTag) {
      const tag = {
        name: newTag,
      }
      this.options.push(tag)
      this.value.push(tag)
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
    submit() {
      if (this.modal_create) {
        this.create()
      } else {
        this.update()
      }
    },
    add() {
      this.modal_create = true
    },
    create() {
      this.loading()
      this.$axios
        .post('/api/transaction-type-create', {
          name: this.transaction.name,
          description: this.transaction.description,
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
    edit(transaction) {
      this.modal_create = false
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
                toastr.success(response.data.message)
                this.list()
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
a.nav-link.active {
  font-weight: 650;
  color: black;
}
#chart {
  height: 8.5rem;
}
</style>
