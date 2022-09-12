<template>
  <div>
    <div id="kt_app_toolbar" class="app-toolbar py-3 py-lg-6 bg-white" style="display: none">
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
            My SalesPlan
          </p>
          <!--end::Title-->
        </div>
        <!--end::Page title-->
      </div>
      <!--end::Toolbar container-->
    </div>

    <div class="container-fluid mt-10 mb-20">

      <div class="row mb-5">
        <div class="col-lg-6 col-sm-12">
          <h3 class="mt-3">My Salesplan</h3>
        </div>
        <div class="col-lg-6 col-sm-12 d-flex justify-content-end">
          <a href="#" class="btn btn-outline btn-outline-primary me-2 mb-2" data-bs-toggle="modal" data-bs-target="#filterdate">Filter & Date</a>
        </div>

        <!-- Modal filterdate  -->
        <div class="modal fade" id="filterdate" tabindex="-1" aria-labelledby="filterdateLabel" aria-hidden="true">
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header text-center">
                <h1 class="modal-title w-100" id="filterdateLabel">Filter & Date</h1>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
              </div>
              <div class="modal-body">
                <form action="">
                  <div class="mb-3">
                    <label for="" class="form-label">Form Date</label>
                    <input type="date" class="form-control" name="" id="">
                  </div>
                  <div class="mb-3">
                    <label for="" class="form-label">To Date</label>
                    <input type="date" class="form-control" name="" id="">
                  </div>
                  <div class="mb-3">
                    <label for="" class="form-label">Type</label>
                    <select name="" id="" class="form-select">
                      <option value="">TMB Project</option>
                    </select>
                  </div>
                </form>
              </div>
              <div class="modal-footer">
                <div class="col-md-12 text-center">
                  <button type="button" class="btn btn-light mx-3" data-bs-dismiss="modal">Cancel</button>
                  <button type="button" class="btn btn-primary">Confirm</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- Row Total -->
      <div class="rounded box-d" style="border:dashed #fff;">
        <div class="row">
          <div class="col-lg-2 mt-1 col-md-6" style="width: 207px;">
            <div class="card card-flush" style="background: #DFF0D0;">
              <div class="card-body">
                <p class="text-muted">Total Target</p>
                <h3 style="color: #5E932F;">$1,000,000</h3>
              </div>
            </div>
          </div>
          <div class="col-lg-2 mt-1 col-md-6" style="width: 207px;">
            <div class="card card-flush" style="background: #E8E9F8;">
              <div class="card-body">
                <p class="text-muted">Total Open</p>
                <h3 style="color: #2D3495;">$1,000,000</h3>
              </div>
            </div>
          </div>
          <div class="col-lg-2 mt-1 col-md-6" style="width: 207px;">
            <div class="card card-flush" style="background: #F8E8E8;">
              <div class="card-body">
                <p class="text-muted">Total Closed</p>
                <h3 style="color: #952D2D;">$1,000,000</h3>
              </div>
            </div>
          </div>
          <div class="col-lg-2 mt-1 col-md-6" style="width: 207px;">
            <div class="card card-flush" style="background: #F8E8F6;">
              <div class="card-body">
                <p class="text-muted">Total Open Closed</p>
                <h3 style="color: #952D88;">$1,000,000</h3>
              </div>
            </div>
          </div>
          <div class="col-lg-2 mt-1 col-md-6" style="width: 207px;">
            <div class="card card-flush" style="background: #F8F7E8;">
              <div class="card-body">
                <p class="text-muted">Total Cancel</p>
                <h3 style="color: #958E2D;">$1,000,000</h3>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- End row total -->

      <!-- Row 2 -->
      <div class="row mt-10">
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div class="position-absolute top-0 start-50 translate-middle d-flex justify-content-center rounded" style="background-color: #DFF0D0; width: 60px; height: 60px;">
              <h1 class="mt-5" style="color: #5E932F;">1</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 style="color: #5E932F;">$1,000,000</h2>
                <p class="text-muted">Awernesss</p>
              </div>
              <div class="text-center d-grid gap-2">
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-success btn-active-light-success me-2 mb-2">Primary</a>
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-danger btn-active-light-danger me-2 mb-2">Primary</a>
              </div>
            </div>
          </div>
        </div>
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div class="position-absolute top-0 start-50 translate-middle d-flex justify-content-center rounded" style="background-color: #D0D3F1; width: 60px; height: 60px;">
              <h1 class="mt-5" style="color: #2D3495;">2</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 style="color: #2D3495;">$1,000,000</h2>
                <p class="text-muted">Awernesss</p>
              </div>
              <div class="text-center d-grid gap-2">
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-success btn-active-light-success me-2 mb-2">Primary</a>
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-danger btn-active-light-danger me-2 mb-2">Primary</a>
              </div>
            </div>
          </div>
        </div>
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            <div class="position-absolute top-0 start-50 translate-middle d-flex justify-content-center rounded" style="background-color: #F1D0EE; width: 60px; height: 60px;">
              <h1 class="mt-5" style="color: #952D88;">3</h1>
            </div>
            <div class="card-body mt-10">
              <div class="text-center">
                <h2 style="color: #952D88;">$1,000,000</h2>
                <p class="text-muted">Awernesss</p>
              </div>
              <div class="text-center d-grid gap-2">
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-success btn-active-light-success me-2 mb-2">Primary</a>
                <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-danger btn-active-light-danger me-2 mb-2">Primary</a>
              </div>
            </div>
          </div>
        </div>
        <div class="col-lg-3 col-md-6 mt-10">
          <div class="card card-stretch-50 shadow mb-5">
            
            <div class="position-absolute top-0 start-50 translate-middle d-flex justify-content-center rounded" style="background-color: #F1EFD0; width: 60px; height: 60px;">
              <h1 class="mt-5" style="color: #958E2D;">4</h1>
            </div>
            <div class="card-body mt-10">

              <div id="carouselExampleIndicators" class="carousel slide" data-bs-ride="true">
                
                <div class="carousel-inner">
                  <div class="carousel-item active">
                    <div class="text-center">
                      <h2 style="color: #5E932F;">$1,000,000</h2>
                      <p class="text-muted">Awernesss 1</p>
                    </div>
                    <div class="text-center d-grid gap-2">
                      <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-success btn-active-light-success me-2 mb-2">Primary</a>
                      <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-danger btn-active-light-danger me-2 mb-2">Primary</a>
                    </div>
                  </div>
                  <div class="carousel-item">
                    <div class="text-center">
                      <h2>$1,000,000</h2>
                      <p class="text-muted">Awernesss 2</p>
                    </div>
                    <div class="text-center d-grid gap-2">
                      <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-success btn-active-light-success me-2 mb-2">Primary</a>
                      <a href="#" class="btn btn-outline btn-outline-dashed btn-outline-danger btn-active-light-danger me-2 mb-2">Primary</a>
                    </div>
                  </div>
                </div>
              </div>

            </div>

            <div class="card-footer">
              <div class="carousel-indicators">
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1" aria-label="Slide 2"></button>
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
          <button class="p-3 bg-warning text-white border-0 mx-2 rounded">
            <i class="fa-solid fa-magnifying-glass"></i>
          </button>
          <button class="btn btn-primary btn-sm" data-bs-toggle="modal" data-bs-target="#salesplanTotal">$Salesplan Total</button>
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
                <select class="form-select bg-primary text-white h-80 w-80">
                  <option value="">AMS</option>
                </select>
              </form>
            </div>
          </div>
          <div class="modal-body mt-20 mb-10">
            <div class="row">
              <div class="col-lg-6">
                <div class="card bg-primary">
                  <div class="card-body ">
                    <p class="text-white">Total Open</p>
                    <h3>$1,000,000</h3>
                  </div>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="card bg-danger">
                  <div class="card-body">
                    <p class="text-white">Total Closed</p>
                    <h3>$1,000,000</h3>
                  </div>
                </div>
              </div>
            </div>
            <div class="row mt-4">
              <div class="col-lg-6">
                <div class="card bg-info text-white">
                  <div class="card-body">
                    <p class="text-white">Total Open Closed</p>
                    <h3>$1,000,000</h3>
                  </div>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="card bg-warning text-white">
                  <div class="card-body">
                    <p class="text-white">Total Cancel</p>
                    <h3>$1,000,000</h3>
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
            <div class="table-responsive">
              <table
                class="table table-row-bordered table-row-gray-200 gy-4"
              >
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
                  <tr>
                    <td class="text-center">
                      1
                    </td>
                    <td class="text-center">
                      Garuda Indonesia
                    </td>
                    <td class="text-center">
                      Airframe
                    </td>
                    <td class="text-center">
                      737 - 600/700/800
                    </td>
                    <td class="text-center">
                      PK-GFM
                    </td>
                    <td class="text-center">
                      <span class="badge bg-secondary">RKAP</span>
                    </td>
                    <td class="text-center">
                      <span class="badge bg-secondary">TMB</span>
                    </td>
                    <td class="text-center">
                      <span class="badge bg-danger">Level  4</span>
                    </td>
                    <td class="text-center">
                      <span class="badge bg-success">100%</span>
                    </td>
                    <td class="text-center">
                      <span class="badge bg-danger">Closed</span>
                    </td>
                    <td class="text-center">
                      <a href="my-salesplan-detail">Detail</a>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
      <!-- End Table -->
    </div>
  </div>

</template>


<script>
export default {
  layout: 'template',
  name: 'MySalesPlanPage',
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
</style>
