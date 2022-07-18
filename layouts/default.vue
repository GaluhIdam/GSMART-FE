<template>
  <body
    data-kt-name="metronic"
    id="kt_app_body"
    data-kt-app-layout="dark-sidebar"
    data-kt-app-header-fixed="true"
    data-kt-app-sidebar-enabled="true"
    data-kt-app-sidebar-fixed="true"
    data-kt-app-sidebar-hoverable="true"
    data-kt-app-sidebar-push-header="true"
    data-kt-app-sidebar-push-toolbar="true"
    data-kt-app-sidebar-push-footer="true"
    data-kt-app-toolbar-enabled="true"
    class="app-default"
  >
    <!-- <div> -->
    <div class="d-flex flex-column flex-root app-root" id="kt_app_root">
      <div class="app-page flex-column flex-column-fluid" id="kt_app_page">
        <headerApp />
        <div class="app-wrapper flex-column flex-row-fluid" id="kt_app_wrapper">
          <sideApp />
          <div class="app-main flex-column flex-row-fluid" id="kt_app_main">
            <Nuxt />
            <footerApp />
          </div>
        </div>
      </div>
    </div>
    <!-- </div> -->
  </body>
</template>

<script>
if (document.documentElement) {
  const defaultThemeMode = "system";
  const name = document.body.getAttribute("data-kt-name");
  let themeMode = localStorage.getItem(
    "kt_" + (name !== null ? name + "_" : "") + "theme_mode_value"
  );
  if (themeMode === null) {
    if (defaultThemeMode === "system") {
      themeMode = window.matchMedia("(prefers-color-scheme: dark)").matches
        ? "dark"
        : "light";
    } else {
      themeMode = defaultThemeMode;
    }
  }
  document.documentElement.setAttribute("data-theme", themeMode);
}
</script>

<style>
</style>
