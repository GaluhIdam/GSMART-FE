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
            Region
          </p>
          <!--end::Title-->
        </div>
        <!--end::Page title-->
      </div>
      <!--end::Toolbar container-->
    </div>
    <div class="container mt-20 mb-20">
      <div class="card shadow-sm">
        <div class="card-header">
          <h3 class="card-title">Title</h3>
          <div class="card-toolbar">
            <button type="button" class="btn btn-sm btn-light">Action</button>
          </div>
        </div>
        <div class="card-body">Lorem Ipsum is simply dummy text...</div>
        <div class="card-footer">Footer</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'template',
  name: 'RegionPage',
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
