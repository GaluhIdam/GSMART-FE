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
            Dashboard
          </p>
          <!--end::Title-->
        </div>
        <!--end::Page title-->
      </div>
      <!--end::Toolbar container-->
    </div>
    <div class="container mt-5">
      <div class="card shadow-sm">
        <div class="row my-5 mx-2">
          <div class="col-lg-9 col-sm-12">
            <p class="h2">Chart Sales Plan</p>
          </div>
        </div>
    
        <div class="card-body">
          <div class="container">
            <section class="mb-20">
            <!-- Chart Header -->
            <div class="row my-2">
              <div class="col-lg-9 col-sm-12">
                <p class="h2" v-if="typeChart == 'Area Chart'">Area Chart</p>
                <p class="h2" v-else-if="typeChart == 'Group Chart'">Group Chart</p>
                <p class="h2" v-else-if="typeChart == 'Product Chart'">Product Chart</p>
                <p class="h2" v-else>Area Chart</p>
              </div>
              <div class="col-lg-3 col-sm-12 d-flex justify-content-end">
                <multiselect
                  v-model="typeChart"
                  :options="typeChartOptions"
                ></multiselect>
              </div>
            </div>
            <!-- End Of Chart Header -->

            <!-- Area Chart -->
            <div class="row my-5" v-if="typeChart == 'Area Chart'">
              <div class="col-md-4">
                <VueApexCharts
                  type="donut"
                  :options="chart1.chartOptions"
                  :series="chart1.series"
                ></VueApexCharts>
              </div>
              <div class="col-md-8">
                <VueApexCharts
                  type="bar"
                  :options="chart3.chartOptions"
                  :series="chart3.series"
                ></VueApexCharts>
              </div>
            </div>
            <!-- End Of Area Chart -->

            <!-- Group Chart -->
            <div class="row my-5" v-else-if="typeChart == 'Group Chart'">
              <div class="col-md-4">
                <VueApexCharts
                  type="donut"
                  :options="chart2.chartOptions"
                  :series="chart2.series"
                ></VueApexCharts>
              </div>
              <div class="col-md-8">
                <VueApexCharts
                  type="bar"
                  :options="chart4.chartOptions"
                  :series="chart4.series"
                ></VueApexCharts>
              </div>
            </div>
            <!-- End Of Group Chart -->

            <!-- Product Chart -->
            <div class="row my-5" v-else-if="typeChart == 'Product Chart'">
              <div class="col-md-4">
                <VueApexCharts
                  type="donut"
                  :options="chart5.chartOptions"
                  :series="chart5.series"
                ></VueApexCharts>
              </div>
              <div class="col-md-8">
                <VueApexCharts
                  type="bar"
                  :options="chart6.chartOptions"
                  :series="chart6.series"
                ></VueApexCharts>
              </div>
            </div>
            <!-- End Of Product Chart -->

            <!-- Else Condition Chart -->
            <div class="row my-5" v-else>
              <div class="col-md-4">
                <VueApexCharts
                  type="donut"
                  :options="chart1.chartOptions"
                  :series="chart1.series"
                ></VueApexCharts>
              </div>
              <div class="col-md-8">
                <VueApexCharts
                  type="bar"
                  :options="chart3.chartOptions"
                  :series="chart3.series"
                ></VueApexCharts>
              </div>
            </div>
            <!-- End Of Else Condition Chart -->
            </section>

            <section class="custom-rofo">
            <!-- Chart Header -->
            <div class="row my-5 custom-height">
              <div class="col-lg-9 col-sm-12">
                <p class="h2" v-if="rofoChart == 'Rofo Total'">Rofo Total</p>
                <p class="h2" v-else-if="rofoChart == 'Rofo Garuda'">Rofo Garuda</p>
                <p class="h2" v-else-if="rofoChart == 'Rofo Citilink'">Rofo Citilink</p>
                <p class="h2" v-else>Rofo Total</p>
              </div>
              <div class="col-lg-3 col-sm-12 d-flex justify-content-end">
                <multiselect
                  v-model="rofoChart"
                  :options="rofoChartOptions"
                ></multiselect>
              </div>
            </div>
            <!-- End Of Chart Header -->
            
            <!-- Rofo Total Chart -->
            <div class="col-md-12" v-if="rofoChart == 'Rofo Total'">
              <VueApexCharts
                type="bar"
                :options="chart7.chartOptions"
                :series="chart7.series"
              ></VueApexCharts>
            </div>
            <!-- End Of Rofo Total Chart -->
            
            <!-- RoFo Sales Plan Garuda Chart -->
            <div class="col-md-12" v-else-if="rofoChart == 'Rofo Garuda'">
              <VueApexCharts
                type="bar"
                :options="chart8.chartOptions"
                :series="chart8.series"
              ></VueApexCharts>
            </div>
            <!-- End Of RoFo Sales Plan Garuda Chart -->

            <!-- RoFo Sales Plan Citilink Chart -->
            <div class="col-md-12" v-else-if="rofoChart == 'Rofo Citilink'">
              <VueApexCharts
                type="bar"
                :options="chart9.chartOptions"
                :series="chart9.series"
              ></VueApexCharts>
            </div>
            <!-- End Of RoFo Sales Plan Citilink Chart -->

            <!-- Else Condition Rofo Chart -->
            <div class="col-md-12" v-else>
              <VueApexCharts
                type="bar"
                :options="chart7.chartOptions"
                :series="chart7.series"
              ></VueApexCharts>
            </div>
            <!-- End Of Else Condition Rofo Chart -->
            </section>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'template',
  name: 'IndexPage',
  data(){
    return {
      typeChartOptions: ['Area Chart', 'Group Chart', 'Product Chart'],
      typeChart: 'Area Chart',
      rofoChartOptions: ['Rofo Total', 'Rofo Garuda', 'Rofo Citilink'],
      rofoChart: 'Rofo Total',
      chart1 : {
        series: [44, 55, 41, 17],
        chartOptions: {
            labels: ["Area 1", "Area 2", "Area 3", "KAM"],
            chart: {
              type: 'donut',
            },
            plotOptions: {
              pie: {
                donut: {
                  labels: {
                    show: true,
                    total: {
                      label: 'MUSD',
                      showAlways: true,
                      show: true
                    }
                  }
                }
              }
            },
            responsive: [{
              breakpoint: 480,
              options: {
                chart: {
                  width: 200
                },
                legend: {
                  position: 'bottom'
                }
              }
            }]
          },
      },
      chart2 : {
        series: [44, 55],
        chartOptions: {
            labels: ["GA", "NGA"],
            chart: {
              type: 'donut',
            },
            plotOptions: {
              pie: {
                donut: {
                  labels: {
                    show: true,
                    total: {
                      label: 'MUSD',
                      showAlways: true,
                      show: true
                    }
                  }
                }
              }
            },
            responsive: [{
              breakpoint: 480,
              options: {
                chart: {
                  width: 200
                },
                legend: {
                  position: 'bottom'
                }
              }
            }]
          },
      },
      chart3: {
        series: [
          {
            name: 'Actual',
            data: [
              {
                x: 'KAM',
                y: 1292,
                goals: [
                  {
                    name: 'Expected',
                    value: 1400,
                    strokeHeight: 5,
                    strokeColor: '#775DD0'
                  }
                ]
              },
              {
                x: 'I',
                y: 4432,
                goals: [
                  {
                    name: 'Expected',
                    value: 5400,
                    strokeHeight: 5,
                    strokeColor: '#775DD0'
                  }
                ]
              },
              {
                x: 'II',
                y: 5423,
                goals: [
                  {
                    name: 'Expected',
                    value: 5200,
                    strokeHeight: 5,
                    strokeColor: '#775DD0'
                  }
                ]
              },
              {
                x: 'III',
                y: 6653,
                goals: [
                  {
                    name: 'Expected',
                    value: 6500,
                    strokeHeight: 5,
                    strokeColor: '#775DD0'
                  }
                ]
              },
            ]
          }
        ],
        chartOptions: {
            chart: {
              height: 350,
              type: 'bar'
            },
            plotOptions: {
              bar: {
                columnWidth: '60%'
              }
            },
            colors: ['#00E396'],
            dataLabels: {
              enabled: false
            },
            legend: {
              show: true,
              showForSingleSeries: true,
              customLegendItems: ['Actual', 'Expected'],
              markers: {
                fillColors: ['#00E396', '#775DD0']
              }
            }
          },
      },
      chart4: {
        series: [
          {
            name: 'Actual',
            data: [
              {
                x: 'GA',
                y: 4432,
                goals: [
                  {
                    name: 'Expected',
                    value: 5400,
                    strokeHeight: 5,
                    strokeColor: '#775DD0'
                  }
                ]
              },
              {
                x: 'NGA',
                y: 5423,
                goals: [
                  {
                    name: 'Expected',
                    value: 5200,
                    strokeHeight: 5,
                    strokeColor: '#775DD0'
                  }
                ]
              },
            ]
          }
        ],
        chartOptions: {
            chart: {
              height: 350,
              type: 'bar'
            },
            plotOptions: {
              bar: {
                columnWidth: '60%'
              }
            },
            colors: ['#00E396'],
            dataLabels: {
              enabled: false
            },
            legend: {
              show: true,
              showForSingleSeries: true,
              customLegendItems: ['Actual', 'Expected'],
              markers: {
                fillColors: ['#00E396', '#775DD0']
              }
            }
          },
      },
      chart5 : {
        series: [44, 55, 41, 17],
        chartOptions: {
            labels: ["Area 1", "Area 2", "Area 3", "KAM"],
            chart: {
              type: 'donut',
            },
            plotOptions: {
              pie: {
                donut: {
                  labels: {
                    show: true,
                    total: {
                      label: 'MUSD',
                      showAlways: true,
                      show: true
                    }
                  }
                }
              }
            },
            responsive: [{
              breakpoint: 480,
              options: {
                chart: {
                  width: 200
                },
                legend: {
                  position: 'bottom'
                }
              }
            }]
          },
      },
      chart6: {
        series: [
          {
            name: 'Actual',
            data: [
              {
                  x: '2012',
                  y: 4432,
                  goals: [
                    {
                      name: 'Expected',
                      value: 5400,
                      strokeHeight: 5,
                      strokeColor: '#775DD0'
                    }
                  ]
                },
                {
                  x: '2013',
                  y: 5423,
                  goals: [
                    {
                      name: 'Expected',
                      value: 5200,
                      strokeHeight: 5,
                      strokeColor: '#775DD0'
                    }
                  ]
                },
                {
                  x: '2014',
                  y: 6653,
                  goals: [
                    {
                      name: 'Expected',
                      value: 6500,
                      strokeHeight: 5,
                      strokeColor: '#775DD0'
                    }
                  ]
                },
                {
                  x: '2015',
                  y: 8133,
                  goals: [
                    {
                      name: 'Expected',
                      value: 6600,
                      strokeHeight: 13,
                      strokeWidth: 0,
                      strokeLineCap: 'round',
                      strokeColor: '#775DD0'
                    }
                  ]
                },
                {
                  x: '2016',
                  y: 7132,
                  goals: [
                    {
                      name: 'Expected',
                      value: 7500,
                      strokeHeight: 5,
                      strokeColor: '#775DD0'
                    }
                  ]
                },
                {
                  x: '2017',
                  y: 7332,
                  goals: [
                    {
                      name: 'Expected',
                      value: 8700,
                      strokeHeight: 5,
                      strokeColor: '#775DD0'
                    }
                  ]
                },
                {
                  x: '2018',
                  y: 6553,
                  goals: [
                    {
                      name: 'Expected',
                      value: 7300,
                      strokeHeight: 2,
                      strokeDashArray: 2,
                      strokeColor: '#775DD0'
                    }
                  ]
                },
                {
                  x: '2019',
                  y: 6553,
                  goals: [
                    {
                      name: 'Expected',
                      value: 7300,
                      strokeHeight: 2,
                      strokeDashArray: 2,
                      strokeColor: '#775DD0'
                    }
                  ]
                },
                {
                  x: '2020',
                  y: 6553,
                  goals: [
                    {
                      name: 'Expected',
                      value: 7300,
                      strokeHeight: 2,
                      strokeDashArray: 2,
                      strokeColor: '#775DD0'
                    }
                  ]
                },
            ]
          }
        ],
        chartOptions: {
            chart: {
              height: 350,
              type: 'bar'
            },
            plotOptions: {
              bar: {
                columnWidth: '60%'
              }
            },
            colors: ['#00E396'],
            dataLabels: {
              enabled: false
            },
            legend: {
              show: true,
              showForSingleSeries: true,
              customLegendItems: ['Actual', 'Expected'],
              markers: {
                fillColors: ['#00E396', '#775DD0']
              }
            }
          },
      },
      chart7: {
        series: [{
            name: 'PRODUCT A',
            data: [44, 55, 41, 67, 22, 43]
          }, {
            name: 'PRODUCT B',
            data: [13, 23, 20, 8, 13, 27]
          }, {
            name: 'PRODUCT C',
            data: [11, 17, 15, 15, 21, 14]
          }, {
            name: 'PRODUCT D',
            data: [21, 7, 25, 13, 22, 8]
          }],
        chartOptions: {
            chart: {
              type: 'bar',
              height: 350,
              stacked: true,
              toolbar: {
                show: true
              },
              zoom: {
                enabled: true
              }
            },
            responsive: [{
              breakpoint: 480,
              options: {
                legend: {
                  position: 'bottom',
                  offsetX: -10,
                  offsetY: 0
                }
              }
            }],
            plotOptions: {
              bar: {
                horizontal: false,
                borderRadius: 10,
                dataLabels: {
                  total: {
                    enabled: true,
                    style: {
                      fontSize: '13px',
                      fontWeight: 900
                    }
                  }
                }
              },
            },
            xaxis: {
              type: 'datetime',
              categories: ['01/01/2011 GMT', '01/02/2011 GMT', '01/03/2011 GMT', '01/04/2011 GMT',
                '01/05/2011 GMT', '01/06/2011 GMT'
              ],
            },
            legend: {
              position: 'right',
              offsetY: 40
            },
            fill: {
              opacity: 1
            }
        },
      },
      chart8: {
        series: [{
            name: 'PRODUCT E',
            data: [44, 55, 41, 67, 22, 43]
          }, {
            name: 'PRODUCT F',
            data: [13, 23, 20, 8, 13, 27]
          }, {
            name: 'PRODUCT G',
            data: [11, 17, 15, 15, 21, 14]
          }, {
            name: 'PRODUCT H',
            data: [21, 7, 25, 13, 22, 8]
          }],
        chartOptions: {
            chart: {
              type: 'bar',
              height: 350,
              stacked: true,
              toolbar: {
                show: true
              },
              zoom: {
                enabled: true
              }
            },
            responsive: [{
              breakpoint: 480,
              options: {
                legend: {
                  position: 'bottom',
                  offsetX: -10,
                  offsetY: 0
                }
              }
            }],
            plotOptions: {
              bar: {
                horizontal: false,
                borderRadius: 10,
                dataLabels: {
                  total: {
                    enabled: true,
                    style: {
                      fontSize: '13px',
                      fontWeight: 900
                    }
                  }
                }
              },
            },
            xaxis: {
              type: 'datetime',
              categories: ['01/01/2011 GMT', '01/02/2011 GMT', '01/03/2011 GMT', '01/04/2011 GMT',
                '01/05/2011 GMT', '01/06/2011 GMT'
              ],
            },
            legend: {
              position: 'right',
              offsetY: 40
            },
            fill: {
              opacity: 1
            }
        },
      },
      chart9: {
        series: [{
            name: 'PRODUCT I',
            data: [44, 55, 41, 67, 22, 43]
          }, {
            name: 'PRODUCT J',
            data: [13, 23, 20, 8, 13, 27]
          }, {
            name: 'PRODUCT K',
            data: [11, 17, 15, 15, 21, 14]
          }, {
            name: 'PRODUCT L',
            data: [21, 7, 25, 13, 22, 8]
          }],
        chartOptions: {
            chart: {
              type: 'bar',
              height: 350,
              stacked: true,
              toolbar: {
                show: true
              },
              zoom: {
                enabled: true
              }
            },
            responsive: [{
              breakpoint: 480,
              options: {
                legend: {
                  position: 'bottom',
                  offsetX: -10,
                  offsetY: 0
                }
              }
            }],
            plotOptions: {
              bar: {
                horizontal: false,
                borderRadius: 10,
                dataLabels: {
                  total: {
                    enabled: true,
                    style: {
                      fontSize: '13px',
                      fontWeight: 900
                    }
                  }
                }
              },
            },
            xaxis: {
              type: 'datetime',
              categories: ['01/01/2011 GMT', '01/02/2011 GMT', '01/03/2011 GMT', '01/04/2011 GMT',
                '01/05/2011 GMT', '01/06/2011 GMT'
              ],
            },
            legend: {
              position: 'right',
              offsetY: 40
            },
            fill: {
              opacity: 1
            }
        },
      },
    }
  },
  created() {
    this.loading()
  },
  methods: {
    loading() {
      Swal.fire({
        timer: 100,
        didOpen: () => {
          Swal.showLoading()
        },
        background: 'transparent',
        allowOutsideClick: false,
      })
    },
  },
}
</script>
<style>
  .center-chart{
    margin: auto;
  }
  .mt-20 {
    margin-top: 20px;
  }
  .mb-20 {
    margin-bottom: 20px;
  }
  .custom-height{
    min-height: 50px;
  }
  .custom-rofo{
    min-height: 50vh;
  }
</style>
