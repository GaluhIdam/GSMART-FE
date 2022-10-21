<template>
  <div>
    <div class="container-fluid mt-10 mb-20">

      <div class="row mb-5">
        <div class="col-lg-6 col-sm-12">
          <h3 class="mt-3">My Salesplan</h3>
        </div>
        <div class="col-lg-6 col-sm-12 d-flex justify-content-end">
          <button type="button" class="btn btn-outline btn-outline-primary me-2 mb-2" data-bs-toggle="modal" data-bs-target="#filterdate">
            Filter & Date <i class="fa-solid fa-chevron-down"></i>
          </button>
        </div>

        <!-- Modal filterdate  -->
        <div class="modal fade" id="filterdate" tabindex="-1" aria-labelledby="filterdateLabel" aria-hidden="true">
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header text-center">
                <h1 class="modal-title w-100" id="filterdateLabel">Filter & Date</h1>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" @click="closeModal()"></button>
              </div>
              <form>
                <div class="modal-body">
                  <div class="mb-3">
                    <label for="" class="form-label">Form Date</label>
                    <input type="date" class="form-control" v-model="start_date">
                  </div>
                  <div class="mb-3">
                    <label for="" class="form-label">To Date</label>
                    <input type="date" class="form-control" v-model="end_date">
                  </div>
                  <div class="mb-3">
                    <label for="" class="form-label">Type</label>
                    <select v-model="type" class="form-select">
                      <option value="1">TMB</option>
                      <option value="2">PBTH</option>
                    </select>
                  </div>
                </div>
                <div class="modal-footer">
                  <div class="col-md-12 text-center">
                    <button type="button" class="btn btn-light mx-3" data-bs-dismiss="modal" @click="closeModal()">Cancel</button>
                    <button type="button" class="btn btn-primary" data-bs-dismiss="modal" @click="list()">Filter</button>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Row Total -->
      <div class="rounded box-d" id="cardTopDashed">
        <div class="row">
          <div class="col-lg-2 mt-1 col-md-6" id="cardTop">
            <div class="card card-flush" id="bgGreen">
              <div class="card-body">
                <p class="text-muted" id="fontSm">Total Target</p>
                <h4 id="textGreen" v-if="sales_user">${{ formatPrice(sales_user.totalTarget) }}</h4>
              </div>
            </div>
          </div>
          <div class="col-lg-2 mt-1 col-md-6" id="cardTop">
            <div class="card card-flush" id="bgBlue">
              <div class="card-body">
                <p class="text-muted" id="fontSm">Total Open</p>
                <h4 id="textBlue" v-if="sales_user">${{ formatPrice(sales_user.totalOpen) }}</h4>
              </div>
            </div>
          </div>
          <div class="col-lg-2 mt-1 col-md-6" id="cardTop">
            <div class="card card-flush" id="bgRed">
              <div class="card-body">
                <p class="text-muted" id="fontSm">Total Closed</p>
                <h4 id="textRed" v-if="sales_user">${{ formatPrice(sales_user.totalClosed) }}</h4>
              </div>
            </div>
          </div>
          <div class="col-lg-2 mt-1 col-md-6" id="cardTop">
            <div class="card card-flush" id="bgPurple">
              <div class="card-body">
                <p class="text-muted" id="fontSm">Total Open Closed</p>
                <h4 id="textPurple" v-if="sales_user">${{ formatPrice(sales_user.totalOpenClosed) }}</h4>
              </div>
            </div>
          </div>
          <div class="col-lg-2 mt-1 col-md-6" id="cardTop">
            <div class="card card-flush" id="bgGold">
              <div class="card-body">
                <p class="text-muted" id="fontSm">Total Cancel</p>
                <h4 id="textGold" v-if="sales_user">${{ formatPrice(sales_user.totalCancel) }}</h4>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- End row total -->

      <!-- Row 2 -->
      <div class="row mt-10">
        
        <!-- Level 4 -->
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div class="position-absolute top-0 start-50 translate-middle d-flex justify-content-center rounded" id="bgGreen2">
              <h1 class="mt-5" id="textGreen">4</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 id="textGreen" v-if="sales_user">${{ formatPrice(sales_user.level4.total) }}</h2>
                <p class="text-muted">Awareness</p>
              </div>
              <div class="d-grid gap-2">
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-success d-flex justify-content-start btn-active-light-success me-2 mb-2">
                  <div class="d-flex align-items-center gap-2">
                    <span id="btnGreen" v-if="sales_user">{{ formatPrice(sales_user.level4.countOpen) }}</span>
                    <span id="textGreen" v-if="sales_user">${{ formatPrice(sales_user.level4.open) }}</span>
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span class="text-muted ms-10" id="fontSm">Open</span>
                  </div>
                </a>
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-danger d-flex justify-content-start btn-active-light-danger me-2 mb-2">
                  <div class="d-flex align-items-center gap-2">
                    <span id="btnRed" v-if="sales_user">{{ formatPrice(sales_user.level4.countCancel) }}</span>
                    <span id="textRed" v-if="sales_user">${{ formatPrice(sales_user.level4.cancel) }}</span>
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span class="text-muted ms-10" id="fontSm">Cancel</span>
                  </div>
                </a>
              </div>
            </div>
            <div class="card-footer border-0">
            </div>
          </div>
        </div>

        <!-- Level 3 -->
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div class="position-absolute top-0 start-50 translate-middle d-flex justify-content-center rounded" id="bgBlue2">
              <h1 class="mt-5" id="textBlue">3</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 id="textBlue" v-if="sales_user">${{ formatPrice(sales_user.level3.total) }}</h2>
                <p class="text-muted">Opportunity</p>
              </div>
              <div class="d-grid gap-2">
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-success d-flex justify-content-start btn-active-light-success me-2 mb-2">
                  <div class="d-flex align-items-center gap-2">
                    <span id="btnGreen" v-if="sales_user">{{ formatPrice(sales_user.level3.countOpen) }}</span>
                    <span id="textGreen" v-if="sales_user">${{ formatPrice(sales_user.level3.open) }}</span>
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span class="text-muted ms-10" id="fontSm">Open</span>
                  </div>
                </a>
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-danger d-flex justify-content-start btn-active-light-danger me-2 mb-2">
                  <div class="d-flex align-items-center gap-2">
                    <span id="btnRed" v-if="sales_user">{{ formatPrice(sales_user.level3.countCancel) }}</span>
                    <span id="textRed" v-if="sales_user">${{ formatPrice(sales_user.level3.cancel) }}</span>
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span class="text-muted ms-10" id="fontSm">Cancel</span>
                  </div>
                </a>
              </div>
            </div>
            <div class="card-footer border-0">
            </div>
          </div>
        </div>

        <!-- Level 2 -->
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div class="position-absolute top-0 start-50 translate-middle d-flex justify-content-center rounded" id="bgPurple2">
              <h1 class="mt-5" id="textPurple">2</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 id="textPurple" v-if="sales_user">${{ formatPrice(sales_user.level2.total) }}</h2>
                <p class="text-muted">Attractive Proposal</p>
              </div>
              <div class="d-grid gap-2">
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-success d-flex justify-content-start btn-active-light-success me-2 mb-2">
                  <div class="d-flex align-items-center gap-2">
                    <span id="btnGreen" v-if="sales_user">{{ formatPrice(sales_user.level2.countOpen) }}</span>
                    <span id="textGreen" v-if="sales_user">${{ formatPrice(sales_user.level2.open) }}</span>
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span class="text-muted ms-10" id="fontSm">Open</span>
                  </div>
                </a>
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-danger d-flex justify-content-start btn-active-light-danger me-2 mb-2">
                  <div class="d-flex align-items-center gap-2">
                    <span id="btnRed" v-if="sales_user">{{ formatPrice(sales_user.level2.countCancel) }}</span>
                    <span id="textRed" v-if="sales_user">${{ formatPrice(sales_user.level2.cancel) }}</span>
                  </div>
                  <div class="d-flex align-items-center justify-content-end">
                    <span class="text-muted ms-10" id="fontSm">Cancel</span>
                  </div>
                </a>
              </div>
            </div>
            <div class="card-footer border-0">
            </div>
          </div>
        </div>
        
        <!-- Level 1 -->
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div class="position-absolute top-0 start-50 translate-middle d-flex justify-content-center rounded" id="bgGold2">
              <h1 class="mt-5" id="textGold">1</h1>
            </div>
            <div class="card-body mt-10">
              <div id="card1carousel" class="carousel slide" data-bs-ride="true">
                <div class="carousel-inner">
                  <div class="carousel-item active">
                    <div class="text-center">
                      <h2 id="textGold" v-if="sales_user">${{ formatPrice(sales_user.level1.total) }}</h2>
                      <p class="text-muted">Attractive Proposal</p>
                    </div>
                    <div class="d-grid gap-2">
                      <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-success d-flex justify-content-start btn-active-light-success me-2 mb-2">
                        <div class="d-flex align-items-center gap-2">
                          <span id="btnGreen" v-if="sales_user">{{ formatPrice(sales_user.level1.countOpen) }}</span>
                          <span id="textGreen" v-if="sales_user">${{ formatPrice(sales_user.level1.open) }}</span>
                        </div>
                        <div class="d-flex align-items-center justify-content-end">
                          <span class="text-muted ms-10" id="fontSm">Open</span>
                        </div>
                      </a>
                      <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-danger d-flex justify-content-start btn-active-light-danger me-2 mb-2">
                        <div class="d-flex align-items-center gap-2">
                          <span id="btnRed" v-if="sales_user">{{ formatPrice(sales_user.level1.countCancel) }}</span>
                          <span id="textRed" v-if="sales_user">${{ formatPrice(sales_user.level1.cancel) }}</span>
                        </div>
                        <div class="d-flex align-items-center justify-content-end">
                          <span class="text-muted ms-10" id="fontSm">Cancel</span>
                        </div>
                      </a>
                    </div>
                  </div>
                  <div class="carousel-item">
                    <div class="text-center">
                      <h2 id="textGold" v-if="sales_user">${{ formatPrice(sales_user.level1.total) }}</h2>
                      <p class="text-muted">Contract Signing</p>
                    </div>
                    <div class="text-center d-grid gap-2">
                      
                      <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-info d-flex justify-content-start btn-active-light-info me-2 mb-2">
                        <div class="d-flex align-items-center gap-2">
                          <span id="btnPurple" v-if="sales_user">{{ formatPrice(sales_user.level1.countClosed) }}</span>
                          <span id="textPurple" v-if="sales_user">${{ formatPrice(sales_user.level1.closed) }}</span>
                        </div>
                        <div class="d-flex align-items-center justify-content-end">
                          <span class="text-muted ms-10" id="fontSm">Closed</span>
                        </div>
                      </a>
                      <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-warning d-flex justify-content-start btn-active-light-warning me-2 mb-2">
                        <div class="d-flex align-items-center gap-2">
                          <span id="btnGold" v-if="sales_user">{{ formatPrice(sales_user.level1.countCloseIn) }}</span>
                          <span id="textGold" v-if="sales_user">${{ formatPrice(sales_user.level1.closeIn) }}</span>
                        </div>
                        <div class="d-flex align-items-center justify-content-end">
                          <span class="text-muted ms-10" id="fontSm">Close in</span>
                        </div>
                      </a>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="card-footer">
              <div class="carousel-indicators">
                <button type="button" data-bs-target="#card1carousel" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
                <button type="button" data-bs-target="#card1carousel" data-bs-slide-to="1" aria-label="Slide 2"></button>
              </div>
            </div>
          </div>
        </div>

      </div>
      <!-- End row 2 -->

      <div class="row">
        <div class="col-lg-6 col-sm-12">
          <h3 class="mt-3">Salesplan Table</h3>
        </div>
        <div class="col-lg-6 col-sm-12 d-flex justify-content-end">
          <button class="btn btn-primary btn-sm" data-bs-toggle="modal" data-bs-target="#salesplanTotal">$ Salesplan Total</button>
        </div>
      </div>
      
    <!-- Modal Salesplan total -->
    <div class="modal fade" id="salesplanTotal" tabindex="-1" aria-labelledby="salesplanTotalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <div class="col-lg-6">
              <h1 class="modal-title" id="salesplanTotalLabel">Salesplan Total</h1>
            </div>
            <div class="col-lg-6 d-flex justify-content-end">
              <form action="">
                <!-- <select class="form-select bg-primary text-white h-80 w-80">
                  <option value="">AMS</option>
                </select> -->
              </form>
            </div>
          </div>
          <div class="modal-body mt-10 mb-10">
            <div class="row">
              <div class="col-lg-6">
                <div class="card" id="bgBlue">
                  <div class="card-body ">
                    <p class="text-muted">Total Open</p>
                    <h2 id="textBlue" v-if="sales_all">${{ formatPrice(sales_all.totalOpen) }}</h2>
                  </div>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="card" id="bgRed">
                  <div class="card-body">
                    <p class="text-muted">Total Closed</p>
                    <h2 id="textRed" v-if="sales_all">${{ formatPrice(sales_all.totalClosed) }}</h2>
                  </div>
                </div>
              </div>
            </div>
            <div class="row mt-4">
              <div class="col-lg-6">
                <div class="card" id="bgPurple">
                  <div class="card-body">
                    <p class="text-muted">Total Open Closed</p>
                    <h2 id="textPurple" v-if="sales_all">${{ formatPrice(sales_all.totalOpenClosed) }}</h2>
                  </div>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="card" id="bgGold">
                  <div class="card-body">
                    <p class="text-muted">Total Cancel</p>
                    <h2 id="textGold" v-if="sales_all">${{ formatPrice(sales_all.totalCancel) }}</h2>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <div class="col-md-12 text-center">
              <div class="d-grid gap-2">
                <button type="button" class="btn btn-primary" data-bs-dismiss="modal">Close</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

      <!-- Table -->
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
                    <th class="text-center">No</th>
                    <th class="text-center">CUTOMER</th>
                    <th class="text-center">PRODUCT</th>
                    <th class="text-center">AC/ENG/APU/COMP</th>
                    <th class="text-center">REGISTRATION</th>
                    <th class="text-center">Other</th>
                    <th class="text-center">Type</th>
                    <th class="text-center">Level</th>
                    <th class="text-center">Progress</th>
                    <th class="text-center">STATUS</th>
                    <th class="text-center">ACTION</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(p_sales, p_sales_index) in sales.data" :key="p_sales_index">
                    <td class="text-center">
                      {{ sales.from + p_sales_index }}
                    </td>
                    <!-- Customer -->
                    <td class="text-center">
                      {{ p_sales.customer }}
                    </td>
                    <!-- Product -->
                    <td class="text-center">
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
                        <span class="badge badge-info">RKAP</span>
                      </div>
                      <div v-if="p_sales.other === 'Additional'">
                        <span class="badge badge-primary">Additional</span>
                      </div>
                    </td>
                    <!-- Type -->
                    <td class="text-center">
                      <div v-if="p_sales.type === 'TMB'">
                        <span class="badge badge-danger">TMB</span>
                      </div>
                      <div v-if="p_sales.type === 'PBTH'">
                        <span class="badge badge-warning">PBTH</span>
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
                        <span class="badge badge-danger">10%</span>
                      </div>
                      <div v-if="p_sales.progress === 20">
                        <span class="badge badge-danger">20%</span>
                      </div>
                      <div v-if="p_sales.progress === 30">
                        <span class="badge badge-danger">30%</span>
                      </div>
                      <div v-if="p_sales.progress === 40">
                        <span class="badge badge-warning">40%</span>
                      </div>
                      <div v-if="p_sales.progress === 50">
                        <span class="badge badge-warning">50%</span>
                      </div>
                      <div v-if="p_sales.progress === 60">
                        <span class="badge badge-warning">60%</span>
                      </div>
                      <div v-if="p_sales.progress === 70">
                        <span class="badge badge-primary">70%</span>
                      </div>
                      <div v-if="p_sales.progress === 80">
                        <span class="badge badge-primary">80%</span>
                      </div>
                      <div v-if="p_sales.progress === 90">
                        <span class="badge badge-success">90%</span>
                      </div>
                      <div v-if="p_sales.progress === 100">
                        <span class="badge badge-success">100%</span>
                      </div>
                    </td>
                    <!-- Status -->
                    <td class="text-center">
                      <div v-if="p_sales.status === 'Cancel'">
                        <span class="badge badge-danger">Cancel</span>
                      </div>
                      <div v-if="p_sales.status === 'Open'">
                        <span class="badge badge-success">Open</span>
                      </div>
                      <div v-if="p_sales.status === 'Close in'">
                        <span class="badge badge-warning">Close in</span>
                      </div>
                      <div v-if="p_sales.status === 'Closed'">
                        <span class="badge badge-primary">Closed</span>
                      </div>
                    </td>
                    <td class="text-center">
                      <nuxt-link
                        v-if="p_sales"
                        :to="{ path: '/my-salesplan-detail', query: { id: p_sales.id }}"
                        >
                          <span class="menu-title">Detail</span>
                        </nuxt-link>
                    </td>
                  </tr>
                  <!-- Jika data kosong -->
                  <tr v-if="sales.data.length < 1">
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
                          disabled: !sales.prev_page_url,
                        }"
                        @click="sales.prev_page_url && list(sales.prev_page_url)"
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
                          disabled: !sales.next_page_url,
                        }"
                        @click="sales.next_page_url && list(sales.next_page_url)"
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
      <!-- End Table -->
    </div>
  </div>

</template>

<script>
import debounce from 'lodash/debounce'
export default {
  layout: 'template',
  name: 'MySalesPlanPage',
  data() {
    return {
      sales: {
        data: [],
        link: [],
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
      start_date: null,
      end_date: null,
      type: null,
      order: 'id',
      by: 'desc',
      paginate: '10',
      current_page: null,
      sales_user: null,
      sales_all: null,
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
      },
    }
  },
  watch: {
    search: debounce(function () {
      this.list()
    }, 500),
  },
  created() {
    this.list()
  },
  methods: {
    // Mengubah format menjadi ada komanya
    formatPrice(value) {
      let val = (value/1).toFixed(0).replace(',', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
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
    list(paginate) {
      this.loading()
      paginate = paginate || `/api/sales`
      this.$axios
        .get(paginate, {
          params: {
            search: this.search,
            order: this.order,
            by: this.by,
            paginate: this.paginate,
            start_date: this.start_date,
            end_date: this.end_date,
            type: this.type,
          },
        })
        .then((response) => {
          this.sales = response.data.data.user.salesPlan
          this.sales_user = response.data.data.user
          this.sales_all = response.data.data.all
          this.current_page = this.sales.current_page
          console.log(this.sales)
          Swal.close()
        })
        .catch((error) => console.log(error))
    },
    directPage: debounce(function () {
      if (this.current_page < 1) {
        this.current_page = 1
      } else if (this.current_page > this.sales.last_page) {
        this.current_page = this.sales.last_page
      }
      let url = new URL(this.sales.first_page_url)
      let search_params = url.searchParams
      search_params.set('page', this.current_page)
      url.search = search_params.toString()
      let new_url = url.toString()
      this.list(new_url)
    }, 500),

    closeModal() {
      this.list()
      this.clearForm()
    },
    clearForm() {
      this.start_date = null
      this.end_date = null
      this.type = null
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
    opacity: .5;
    transition: opacity .6s ease;
    border-radius: 100%;
}

.carousel-indicators .active{
    background-color: #188AF8;
}

#cardTopDashed {
  border:dashed #fff;
}

#cardTop {
  width: 207px;
}

#btnGreen {
  background-color: #DFF0D0; 
  color: #5E932F; 
  border-radius: 100%; 
  padding: 5px 13px 5px 13px;
}

#btnRed {
  background-color: #F8E8E8; 
  color: #952D2D; 
  border-radius: 100%; 
  padding: 5px 13px 5px 13px;
}

#btnPurple {
  background-color: #F8E8F6; 
  color: #952D88; 
  border-radius: 100%; 
  padding: 5px 13px 5px 13px;
}

#btnGold {
  background-color: #F8F7E8; 
  color: #958E2D; 
  border-radius: 100%; 
  padding: 5px 13px 5px 13px;
}

#bgGreen {
  background: #DFF0D0;
}

#bgBlue {
  background: #E8E9F8;
}

#bgRed {
  background: #F8E8E8;
}

#bgPurple {
  background: #F8E8F6;
}

#bgGold {
  background: #F8F7E8;
}

#bgGreen2 {
  background-color: #DFF0D0; 
  width: 60px; 
  height: 60px;
}

#bgBlue2 {
  background-color: #D0D3F1; 
  width: 60px; 
  height: 60px;
}

#bgPurple2 {
  background-color: #F1D0EE; 
  width: 60px; 
  height: 60px;
}

#bgGold2 {
  background-color: #F1EFD0; 
  width: 60px; 
  height: 60px;
}

#textGreen {
  color: #5E932F;
}

#textRed {
  color: #952D2D;
}

#textBlue {
  color: #2D3495;
}

#textPurple {
  color: #952D88;
}

#textGold {
  color: #958E2D;
}

#fontSm {
  font-size: 12px;
}
</style>
