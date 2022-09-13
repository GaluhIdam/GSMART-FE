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
            My SalesPlan Detail
          </p>
          <!--end::Title-->
        </div>
        <!--end::Page title-->
      </div>
      <!--end::Toolbar container-->
    </div>

    <!-- Content -->
    <div class="container-fluid mt-5 mb-5">
      <!-- Breadcrumb -->
      <div class="row mb-5">
        <div class="col-lg-6">
          <a href="my-salesplan"><i class="fa-solid fa-angle-left"></i> Back</a>
        </div>
        <div class="col-lg-6">
          <div class="position-relative">
            <div class="position-absolute top-0 end-0">
              <nav aria-label="breadcrumb">
                <ol class="breadcrumb">
                  <li class="breadcrumb-item"><a href="#">Salesplan </a></li>
                  <li class="breadcrumb-item"><a href="#">My Prospect </a></li>
                  <li class="breadcrumb-item active" aria-current="page">Detail </li>
                </ol>
              </nav>
            </div>
          </div>
        </div>
      </div>
      <!-- End Breadcrumb -->

      <!-- Detail -->
      <div class="row mt-4">
        <div class="card">
          <div class="card-body">
            <!-- header -->
            <div class="row">
              <div class="col-lg-6">
                <h3>Detail</h3>
              </div>
              <div class="col-lg-6">
                <div class="text-right">
                  <div class="position-absolute top-0 end-0 mx-15 mt-4">
                    <button class="btn btn-outline btn-outline-info btn-sm" data-bs-toggle="modal" data-bs-target="#switchAMS">Switch AMS</button>
                    <button class="btn btn-primary btn-sm"><i class="fa-solid fa-pen"></i> Edit Salesplan</button>
                  </div>
                </div>
              </div>
            </div>
            <!-- End header -->

            <!-- Modal -->
            <div class="modal fade" id="switchAMS" tabindex="-1" aria-labelledby="switchAMSLabel" aria-hidden="true">
              <div class="modal-dialog">
                <div class="modal-content">
                  <div class="modal-header">
                    <h5 class="modal-title w-100" id="switchAMSLabel">Switch AMS</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                  </div>
                  <div class="modal-body">
                    <form action="">
                      <div class="mb-3">
                        <label class="form-label">To</label>
                        <input type="text" class="form-control">
                      </div>
                      <div class="mb-3">
                        <label class="form-label">Description</label> <br>
                        <span style="background: #F1F5F9; border-radius: 8px">
                          Level: <b>Level 4</b> Status: <b>Open</b> Other: <b>RKAP</b> Type: <b>TMB</b> Month Sales: <b>Januari</b>
                          Years: <b>2022</b> Start Date Project: <b>01 - 07 - 2022</b> End Date Project: <b>30 - 07 - 2022</b>
                          TAT: <b>30 Days</b> Progress: <b>30%</b> Product: <b>Airframe</b> Location: <b>Component Shop</b>
                          Maintenance: <b>permohonan Instruktur untuk pelaksanaan practical batch 2 kelas amto PNM</b>
                        </span>
                      </div>
                    </form>
                  </div>
                  <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Back</button>
                    <button type="button" class="btn btn-primary">Send</button>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Card -->
            <div class="row mt-3">
              <div class="col-lg-4 col-md-12 col-sm-12">
                <div class="card mb-3" style="max-width: 540px;">
                  <div class="row no-gutters">
                    <div class="col-md-2 mt-2">
                      <img src="https://dummyimage.com/70x70/000/fff" class="rounded" style="width: 70px;">
                    </div>
                    <div class="col-md-10" style="margin-top: -20px;">
                      <div class="card-body">
                        <h5 class="card-title">PK-GFM</h5>
                        <p class="card-text"><small class="text-muted"><i class="fa-solid fa-plane-up"></i> B737-600/700/800/900</small></p>
                        <p class="card-text"><small class="text-muted"><i class="fa-solid fa-spa"></i> Garuda Indonesia</small></p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-lg-2 col-md-12 col-sm-12" style="width: 218px;">
                <div class="text-center d-grid gap-2">
                  <span class="me-2 mb-2" style="border: dotted #04C8C8; border-radius: 10px; padding-top: 10px;">
                    <h3 class="mt-2" style="color: #04C8C8;">$1,500,000.00</h3>
                    <p><small class="text-muted">Market Share</small></p>
                  </span>
                </div>
              </div>
              <div class="col-lg-2 col-md-12 col-sm-12" style="width: 218px;">
                <div class="text-center d-grid gap-2">
                  <span class="me-2 mb-2" style="border: dotted #50CD89; border-radius: 10px; padding-top: 10px;">
                    <h3 class="mt-2" style="color: #50CD89;">$1,000,000.00</h3>
                    <p><small class="text-muted">Total Sales Plan</small></p>
                  </span>
                </div>
              </div>
              <div class="col-lg-2 col-md-12 col-sm-12" style="width: 218px;">
                <div class="text-center d-grid gap-2">
                  <span class="me-2 mb-2" style="border: dotted #F1416C; border-radius: 10px; padding-top: 10px;">
                    <h3 class="mt-2" style="color: #F1416C;">$500,000.00</h3>
                    <p><small class="text-muted">Devisiasi</small></p>
                  </span>
                </div>
              </div>
            </div>
            <!-- End Card -->

            <!-- Detail -->
            <div class="row mt-3">
              <div class="col-lg-1">
                <p class="text-muted">Level</p>
                <span class="badge badge-danger"><b>Level 4</b></span>
                <p class="text-muted mt-5">Status</p>
                <span class="badge badge-warning"><b>Open</b></span>
              </div>
              <div class="col-lg-1">
                <p class="text-muted">Other</p>
                <span class="badge badge-warning"><b>RKAP</b></span>
                <p class="text-muted mt-5">Type</p>
                <span class="badge badge-info"><b>TMB</b></span>
              </div>
              <div class="col-lg-2">
                <p class="text-muted">Progress</p>
                <span class="badge badge-success"><b>60%</b></span>
                <p class="text-muted mt-5">Month Sales</p>
                <p><b>Januari</b></p>
              </div>
              <div class="col-lg-1">
                <p class="text-muted">TAT</p>
                <p><b>30 Days</b></p>
                <p class="text-muted mt-5">Years</p>
                <p><b>2022</b></p>
              </div>
              <div class="col-lg-2">
                <p class="text-muted">Start Date Project</p>
                <p><b>01 - 07 - 2022</b></p>
                <p class="text-muted mt-5">End Date Project</p>
                <p><b>30 - 07 - 2022</b></p>
              </div>
              <div class="col-lg-2">
                <p class="text-muted">Location</p>
                <p><b>Component Shop</b></p>
                <p class="text-muted mt-5">Product</p>
                <p><b>Airframe</b></p>
              </div>
              <div class="col-lg-3">
                <p class="text-muted">Maintenance</p>
                <p><b>permohonan Instruktur untuk pelaksanaan practical batch 2 kelas amto PNM</b></p>
              </div>
            </div>
            <!-- End Detail -->

            <!-- Tab -->
            <div class="row mt-5">
              <ul class="nav nav-tabs" id="myTab" role="tablist">
                <li class="nav-item" role="presentation">
                  <button class="nav-link active" id="upgrade-level-tab" data-bs-toggle="tab" data-bs-target="#upgrade-level-tab-pane" type="button" role="tab" aria-controls="upgrade-level-tab-pane" aria-selected="true">Upgrade Level</button>
                </li>
                <li class="nav-item" role="presentation">
                  <button class="nav-link" id="history-tab" data-bs-toggle="tab" data-bs-target="#history-tab-pane" type="button" role="tab" aria-controls="history-tab-pane" aria-selected="false">History</button>
                </li>
                <li class="nav-item" role="presentation">
                  <button class="nav-link" id="contact-tab" data-bs-toggle="tab" data-bs-target="#contact-tab-pane" type="button" role="tab" aria-controls="contact-tab-pane" aria-selected="false">Contact Person</button>
                </li>
                <li class="nav-item" role="presentation">
                  <button class="nav-link" id="reschedule-tab" data-bs-toggle="tab" data-bs-target="#reschedule-tab-pane" type="button" role="tab" aria-controls="reschedule-tab-pane" aria-selected="false">Reschedule/Cancel</button>
                </li>
              </ul>

              <div class="tab-content" id="myTabContent">
                <!-- Tab Upgrade Level -->
                <div class="tab-pane fade show active" id="upgrade-level-tab-pane" role="tabpanel" aria-labelledby="upgrade-level-tab" tabindex="0">
                  <!--begin::Stepper-->
                  <div class="stepper stepper-pills mt-5" id="kt_stepper_example_basic">
                  <!--begin::Nav-->
                  <div class="stepper-nav flex-center flex-wrap mb-10">
                      <!--begin::Step 1-->
                      <div class="stepper-item mx-8 my-4 current" data-kt-stepper-element="nav">
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                              <!--begin::Icon-->
                              <div class="stepper-icon w-40px h-40px">
                                  <i class="stepper-check fas fa-check"></i>
                                  <span class="stepper-number">4</span>
                              </div>
                              <!--end::Icon-->

                              <!--begin::Label-->
                              <div class="stepper-label">
                                  <!-- <h3 class="stepper-title">
                                      Step 1
                                  </h3> -->

                                  <div class="stepper-desc">
                                    Awareness
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
                      <div class="stepper-item mx-8 my-4" data-kt-stepper-element="nav">
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
                                  <!-- <h3 class="stepper-title">
                                      Step 2
                                  </h3> -->

                                  <div class="stepper-desc">
                                    Opportunity
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
                      <div class="stepper-item mx-8 my-4" data-kt-stepper-element="nav">
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
                                  <!-- <h3 class="stepper-title">
                                      Step 3
                                  </h3> -->

                                  <div class="stepper-desc">
                                    Attractive Proposal
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
                      <div class="stepper-item mx-8 my-4" data-kt-stepper-element="nav">
                          <!--begin::Wrapper-->
                          <div class="stepper-wrapper d-flex align-items-center">
                              <!--begin::Icon-->
                              <div class="stepper-icon w-40px h-40px">
                                  <i class="stepper-check fas fa-check"></i>
                                  <span class="stepper-number">1</span>
                              </div>
                              <!--begin::Icon-->

                              <!--begin::Label-->
                              <div class="stepper-label">
                                  <!-- <h3 class="stepper-title">
                                      Step 4
                                  </h3> -->

                                  <div class="stepper-desc">
                                      Contract Signing
                                  </div>
                              </div>
                              <!--end::Label-->
                          </div>
                          <!--end::Wrapper-->

                          <!--begin::Line-->
                          <div class="stepper-line h-40px"></div>
                          <!--end::Line-->
                      </div>
                      <!--end::Step 4-->
                  </div>
                  <!--end::Nav-->

                      <!--begin::Form-->
                      <div class="form mx-auto" novalidate="novalidate" id="kt_stepper_example_basic_div">
                          <!--begin::Group-->
                          <div class="mb-5">
                              <!--begin::Step 1-->
                              <div class="flex-column current" data-kt-stepper-element="content">
                                <form action="">
                                  <div class="row">
                                    <!-- Fill in Contact Person of Customer -->
                                    <div class="col-lg-6">
                                      <h3>Fill in Contact Person of Customer</h3>
                                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                                    </div>
                                    <div class="col-lg-6">
                                      <div class="position-relative">
                                        <div class="position-absolute top-0 end-0">
                                        <a href="" class="btn btn-primary btn-sm">Add Contact Person</a>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="rounded box-d" style="border:dashed #CDE7FE;">
                                      <div class="mt-3">
                                        <table class="table">
                                          <tr>
                                            <td class="text-center">
                                              <strong>Endang Tardiana</strong>
                                            </td>
                                            <td class="text-center">
                                              <strong>081703621382</strong>
                                            </td>
                                            <td class="text-center">
                                              <strong>endang.tardiana@garuda-indonesia.co.id</strong>	
                                            </td>
                                            <td class="text-center">
                                              <strong>SM. Engine & Component Planning & Contro</strong>
                                            </td>
                                            <td class="text-center">
                                              <strong>JKTMLE, Hangar 2 GMF AeroAsia</strong>
                                            </td>
                                            <td class="text-center">
                                              <a href="" class="btn btn-danger btn-sm"><span class="fas fa-trash"></span></a>
                                            </td>
                                          </tr>
                                        </table>
                                      </div>
                                    </div>

                                    <!-- Upload Attachment RFQ or Email Request -->
                                    <div class="col-lg-6 mt-3">
                                      <h3>Upload Attachment RFQ or Email Request</h3>
                                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                                    </div>
                                    <div class="col-lg-6 mt-3">
                                      <div class="position-relative">
                                        <div class="position-absolute top-0 end-0">
                                        <a href="" class="btn btn-primary btn-sm">Upload Document</a>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="rounded box-d" style="border:dashed #CDE7FE;">
                                      <div class="mt-3">
                                        <table class="table">
                                          <tr>
                                            <td class="">
                                              <strong>Project Term</strong>
                                              <p>1.2mb</p>
                                            </td>
                                            <td class="d-flex justify-content-end">
                                              <a href="" class="btn btn-danger btn-sm"><span class="fas fa-trash"></span></a>
                                            </td>
                                          </tr>
                                        </table>
                                      </div>
                                    </div>

                                    <!-- Upload Attachment Workscope -->
                                    <div class="col-lg-6 mt-3">
                                      <h3>Upload Attachment Workscope</h3>
                                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                                    </div>
                                    <div class="col-lg-6 mt-3">
                                      <div class="position-relative">
                                        <div class="position-absolute top-0 end-0">
                                        <a href="" class="btn btn-primary btn-sm">Upload Document</a>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="rounded box-d" style="border:dashed #CDE7FE;">
                                      <div class="mt-3">
                                        <table class="table">
                                          <tr>
                                            <td>
                                              <strong>Project Term</strong>
                                              <p>1.2mb</p>
                                            </td>
                                            <td class="d-flex justify-content-end">
                                              <a href="" class="btn btn-danger btn-sm"><span class="fas fa-trash"></span></a>
                                            </td>
                                          </tr>
                                        </table>
                                      </div>
                                    </div>

                                    <div class="text-center mt-20">
                                      <button type="button" class="btn btn-danger">Back</button>
                                      <button type="submit" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#addContact">Upgrade & Notify CBO</button>
                                    </div>

                                  </div>
                                </form>
                              </div>
                              <!--begin::Step 1-->

                              <!--begin::Step 1-->
                              <div class="flex-column" data-kt-stepper-element="content">
                                <form action="">
                                  <div class="row">
                                    <h5>File has been upload</h5>
                                    <!-- Attachment of Financial Assesment Form (optional) -->
                                    <div class="col-lg-6 mt-3">
                                      <h3>Attachment of Financial Assesment Form (optional)</h3>
                                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                                    </div>
                                    <div class="col-lg-6 mt-3">
                                      <div class="position-relative">
                                        <div class="position-absolute top-0 end-0">
                                        <a href="" class="btn btn-outline-primary btn-outline btn-sm">Upload Document</a>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="rounded box-d" style="border:dashed #CDE7FE;">
                                      <div class="mt-3">
                                        <table class="table">
                                          <tr>
                                            <td class="">
                                              <strong>Project Term</strong>
                                              <p>1.2mb</p>
                                            </td>
                                            <td class="d-flex justify-content-end">
                                              <a href="" class="btn btn-danger btn-sm"><span class="fas fa-trash"></span></a>
                                            </td>
                                          </tr>
                                        </table>
                                      </div>
                                    </div>

                                    <!-- Attachment of Maintenance Proposal for Customer -->
                                    <div class="col-lg-6 mt-3">
                                      <h3>Attachment of Maintenance Proposal for Customer</h3>
                                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                                    </div>
                                    <div class="col-lg-6 mt-3">
                                      <div class="position-relative">
                                        <div class="position-absolute top-0 end-0">
                                          <a href="" class="btn btn-outline-primary btn-outline btn-sm">Upload Document</a>
                                          <a href="" class="btn btn-outline-warning btn-outline btn-sm">Sync</a>
                                          <a href="" class="btn btn-success btn-sm">Notify COGS</a>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="rounded box-d" style="border:dashed #CDE7FE;">
                                      <div class="mt-3">
                                        <table class="table">
                                          <tr>
                                            <td class="">
                                              <strong>Project Term</strong>
                                              <p>1.2mb</p>
                                            </td>
                                            <td class="d-flex justify-content-end">
                                              <a href="" class="btn btn-danger btn-sm"><span class="fas fa-trash"></span></a>
                                            </td>
                                          </tr>
                                        </table>
                                      </div>
                                    </div>

                                    <!-- Attachment of Profitability Analysis Form Signed -->
                                    <div class="col-lg-6 mt-3">
                                      <h3>Attachment of Profitability Analysis Form Signed</h3>
                                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                                    </div>
                                    <div class="col-lg-6 mt-3">
                                      <div class="position-relative">
                                        <div class="position-absolute top-0 end-0">
                                          <span class="btn btn-sm" style="background-color: #F1E0D0; color: #955F2D;">Waiting Approve VP TP</span>
                                          <a href="" class="btn btn-outline-primary btn-outline btn-sm">Upload Document</a>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="rounded box-d" style="border:dashed #CDE7FE;">
                                      <div class="mt-3">
                                        <table class="table">
                                          <tr>
                                            <td>
                                              <strong>Project Term</strong>
                                              <p>1.2mb</p>
                                            </td>
                                            <td class="d-flex justify-content-end">
                                              <a href="" class="btn btn-danger btn-sm"><span class="fas fa-trash"></span></a>
                                            </td>
                                          </tr>
                                        </table>
                                      </div>
                                    </div>

                                    <div class="text-center mt-20">
                                      <button type="button" class="btn btn-danger">Back</button>
                                      <button type="submit" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#addContact">Upgrade & Notify CBO</button>
                                    </div>

                                  </div>
                                </form>
                              </div>
                              <!--begin::Step 1-->

                              <!--begin::Step 2-->
                              <div class="flex-column" data-kt-stepper-element="content">
                                <form action="">
                                  <div class="row">
                                    <h5>File has been upload</h5>
                                    <!-- Attachment of Customer Approval (SOW Signed / Proposal Approved) -->
                                    <div class="col-lg-6 mt-3">
                                      <h3>Attachment of Customer Approval (SOW Signed / Proposal Approved)</h3>
                                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                                    </div>
                                    <div class="col-lg-6 mt-3">
                                      <div class="position-relative">
                                        <div class="position-absolute top-0 end-0">
                                        <a href="" class="btn btn-outline-primary btn-outline btn-sm">Upload Document</a>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="rounded box-d" style="border:dashed #CDE7FE;">
                                      <div class="mt-3">
                                        <table class="table">
                                          <tr>
                                            <td class="">
                                              <strong>Project Term</strong>
                                              <p>1.2mb</p>
                                            </td>
                                            <td class="d-flex justify-content-end">
                                              <a href="" class="btn btn-danger btn-sm"><span class="fas fa-trash"></span></a>
                                            </td>
                                          </tr>
                                        </table>
                                      </div>
                                    </div>

                                    <!-- Slot Request -->
                                    <div class="col-lg-6 mt-5">
                                      <h3>Slot Request</h3>
                                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                                    </div>
                                    <div class="col-lg-6 mt-5">
                                      <div class="position-relative">
                                        <div class="position-absolute top-0 end-0">
                                        <a href="" class="btn btn-outline-primary btn-outline btn-sm">Request to CBO</a>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="row">
                                      <div class="col-lg-4">
                                        <div class="mb-3">
                                          <label>Hangar</label>
                                          <input type="number" class="form-control form-control-solid" name=""/>
                                        </div>
                                        <div class="mb-3">
                                          <label>Line Hangar</label>
                                          <input type="number" class="form-control form-control-solid" name=""/>
                                        </div>
                                      </div>
                                      <div class="col-lg-4">
                                        <div class="mb-3">
                                          <label>Registration</label>
                                          <input type="text" class="form-control form-control-solid" readonly name=""/>
                                        </div>
                                        <div class="mb-3">
                                          <label>TAT</label>
                                          <input type="number" class="form-control form-control-solid" name=""/>
                                        </div>
                                      </div>
                                      <div class="col-lg-4">
                                        <div class="mb-3">
                                          <label>Start Date</label>
                                          <input type="date" class="form-control form-control-solid" name=""/>
                                        </div>
                                        <div class="mb-3">
                                          <label>End Date</label>
                                          <input type="date" class="form-control form-control-solid" name=""/>
                                        </div>
                                      </div>
                                    </div>

                                    <div class="text-center mt-20">
                                      <button type="button" class="btn btn-danger">Back</button>
                                      <button type="submit" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#addContact">Upgrade & Notify CBO</button>
                                    </div>

                                  </div>
                                </form>
                              </div>
                              <!--begin::Step 2-->

                              <!--begin::Step 1-->
                              <div class="flex-column" data-kt-stepper-element="content">
                                <form action="">
                                  <div class="row">
                                    <h5>File has been upload</h5>
                                    <!-- Attachment of Customer Approval (SOW Signed / Proposal Approved) -->
                                    <div class="col-lg-6 mt-3">
                                      <h3>Attachment of Customer Approval (SOW Signed / Proposal Approved)</h3>
                                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                                    </div>
                                    <div class="col-lg-6 mt-3">
                                      <div class="position-relative">
                                        <div class="position-absolute top-0 end-0">
                                          <a href="" class="btn btn-outline-primary btn-outline btn-sm">Closed Sales</a>
                                          <a href="" class="btn btn-primary btn-sm">Upload Document</a>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="rounded box-d" style="border:dashed #CDE7FE;">
                                      <div class="mt-3">
                                        <table class="table">
                                          <tr>
                                            <td class="">
                                              <strong>Project Term</strong>
                                              <p>1.2mb</p>
                                            </td>
                                            <td class="d-flex justify-content-end">
                                              <a href="" class="btn btn-danger btn-sm"><span class="fas fa-trash"></span></a>
                                            </td>
                                          </tr>
                                        </table>
                                      </div>
                                    </div>

                                    <!-- Input SO Number -->
                                    <div class="col-lg-6 mt-5">
                                      <h3>Input SO Number</h3>
                                    </div>
                                    <div class="row">
                                      <label for="">SO Number</label>
                                      <div class="input-group mb-3">
                                        <input type="text" class="form-control">
                                        <button class="btn btn-sm" type="button" style="background-color: #F1E0D0; color: #955F2D;">Sync</button>
                                      </div>
                                    </div>

                                    <div class="text-center mt-20">
                                      <button type="button" class="btn btn-danger">Back</button>
                                      <button type="submit" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#addContact">Request to Closed</button>
                                    </div>

                                  </div>
                                </form>
                              </div>
                              <!--begin::Step 1-->
                          </div>
                          <!--end::Group-->

                          <!--begin::Actions-->
                          <div class="d-flex flex-stack">
                              <!--begin::Wrapper-->
                              <div class="me-2">
                                  <button type="button" class="btn btn-light btn-active-light-primary" data-kt-stepper-action="previous">
                                      Back
                                  </button>
                              </div>
                              <!--end::Wrapper-->

                              <!--begin::Wrapper-->
                              <div>
                                  <button type="button" class="btn btn-primary" data-kt-stepper-action="submit">
                                      <span class="indicator-label">
                                          Submit
                                      </span>
                                      <span class="indicator-progress">
                                          Please wait... <span class="spinner-border spinner-border-sm align-middle ms-2"></span>
                                      </span>
                                  </button>

                                  <button type="button" class="btn btn-primary" data-kt-stepper-action="next">
                                      Continue
                                  </button>
                              </div>
                              <!--end::Wrapper-->
                          </div>
                          <!--end::Actions-->
                      </div>
                      <!--end::Form-->
                  </div>
                  <!--end::Stepper-->
                </div>

                <!-- Tab History -->  
                <div class="tab-pane fade" id="history-tab-pane" role="tabpanel" aria-labelledby="history-tab" tabindex="0">
                  <div class="mt-5">
                    <!-- Filter -->
                    <div class="row">
                      <div class="col-lg-6 col-sm-12">
                        <h3 class="mt-3"><span class="fas fa-calendar-days"></span> 08 July 2022</h3>
                      </div>
                      <div class="col-lg-6 col-sm-12 d-flex justify-content-end">
                        <ul class="nav nav-tabs">
                          <li class="nav-item">
                            <a class="nav-link active" aria-current="page" href="#">Today</a>
                          </li>
                          <li class="nav-item">
                            <a class="nav-link" aria-current="page" href="#">Week</a>
                          </li>
                          <li class="nav-item dropdown">
                            <a class="nav-link dropdown-toggle" data-bs-toggle="dropdown" href="#" role="button" aria-expanded="false">Month</a>
                            <ul class="dropdown-menu">
                              <li><a class="dropdown-item" href="#"></a></li>
                            </ul>
                          </li>
                          <li class="nav-item dropdown">
                            <a class="nav-link dropdown-toggle" data-bs-toggle="dropdown" href="#" role="button" aria-expanded="false">Year</a>
                            <ul class="dropdown-menu">
                              <li><a class="dropdown-item" href="#">2022</a></li>
                            </ul>
                          </li>
                        </ul>
                      </div>
                    </div>

                    <!-- Isi -->
                    <div class="row mt-4">
                      <h3>3 File Uploaded</h3>
                      <p class="text-muted"><small>02:30 AM by <a href="">You</a></small></p>
                      <div class="rounded box-d" style="border:dashed #CDE7FE;">
                        <div class="mt-3">
                          <h6>Project Term</h6>
                          <p class="text-muted"><small>1.2mb</small></p>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Tab Contact -->
                <div class="tab-pane fade" id="contact-tab-pane" role="tabpanel" aria-labelledby="contact-tab" tabindex="0">
                  <div class="mt-5">
                    <div class="table-responsive">
                      <table class="table table-row-bordered table-row-gray-200 gy-4">
                        <thead>
                          <tr class="fw-bold fs-6 text-gray-800">
                            <th class="text-center">No</th>
                            <th class="text-center">Name</th>
                            <th class="text-center">Phone</th>
                            <th class="text-center">Email</th>
                            <th class="text-center">Title</th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr>
                            <td class="text-center">
                              1
                            </td>
                            <td class="text-center">
                              Endang Tardiana
                            </td>
                            <td class="text-center">
                              081703621382
                            </td>
                            <td class="text-center">
                              endang.tardiana@garuda-indonesia.co.id	
                            </td>
                            <td class="text-center">
                              SM. Engine & Component Planning & Contro
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                    <div class="text-center mt-20">
                      <button type="button" class="btn btn-danger">Back</button>
                      <button type="submit" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#addContact">Add Contact Person</button>
                    </div>
                  </div>
                </div>

                <!-- Modal Add Contact -->
                <div class="modal fade" id="addContact" tabindex="-1" aria-labelledby="addContactLabel" aria-hidden="true">
                  <div class="modal-dialog">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h5 class="modal-title" id="addContactLabel">Add Contact</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                      </div>
                      <div class="modal-body">
                        <form action="">
                          <div class="mb-3">
                            <label class="form-label">Name</label>
                            <input type="text" class="form-control" name="">
                          </div>
                          <div class="mb-3">
                            <label class="form-label">Phone</label>
                            <input type="number" class="form-control" name="">
                          </div>
                          <div class="mb-3">
                            <label class="form-label">Email</label>
                            <input type="email" class="form-control" name="">
                          </div>
                          <div class="mb-3">
                            <label class="form-label">Title</label>
                            <input type="text" class="form-control" name="">
                          </div>
                          <div class="mb-3">
                            <label class="form-label">Address</label>
                            <textarea type="text" class="form-control" name=""></textarea>
                          </div>
                          <div class="mb-3">
                            <label class="form-label">Status</label>
                            <select class="form-select">
                              <option value="">Active</option>
                            </select>
                          </div>
                        </form>
                      </div>
                      <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                        <button type="button" class="btn btn-primary">Save</button>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Tab Reschedule -->
                <div class="tab-pane fade" id="reschedule-tab-pane" role="tabpanel" aria-labelledby="reschedule-tab" tabindex="0">
                  <div class="mt-5">
                    <form action="">
                      <div class="mb-3">
                        <label class="form-label">Reschedule/Cancel</label>
                        <select class="form-select">
                          <option value="">Cancel</option>
                        </select>
                      </div>
                      <div class="mb-3">
                        <label class="form-label">Category</label>
                        <select class="form-select">
                          <option value="">-- Select One --</option>
                        </select>
                      </div>
                      <div class="mb-3">
                        <label class="form-label">Reason of Cancel <span class="text-danger">*</span></label>
                        <textarea name="" class="form-control" cols="30" rows="10"></textarea>
                      </div>
                      <div class="text-center">
                        <button type="reset" class="btn btn-danger">Cancel</button>
                        <button type="submit" class="btn btn-primary">Submit</button>
                      </div>
                    </form>
                  </div>
                </div>
              </div>
            </div>
            <!-- End Tab -->
          </div>
        </div>
      </div>
      <!-- End Detail -->
    </div>
    <!-- End Content -->
  </div>

</template>


<script>
export default {
  layout: 'template',
  name: 'MySalesPlanDetailPage',
  mounted() {
    KTStepper.getInstance()
    KTFormRepeaterBasic.init()
    this.step()
  },
  // watch: {
  //   search: debounce(function () {
  //     this.list()
  //   }, 500),
  // },
  methods: {
    step() {
      var element = document.querySelector("#kt_stepper_example_basic");

      var stepper = new KTStepper(element);

      stepper.on("kt.stepper.next", function (stepper) {
          stepper.goNext(); // go next step
      });

      stepper.on("kt.stepper.previous", function (stepper) {
          stepper.goPrevious(); // go previous step
      });
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
</style>