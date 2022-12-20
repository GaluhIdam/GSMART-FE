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
                            <p class="h2" v-if="typeChart == 'Group Chart'">Group Chart</p>
                            <p class="h2" v-if="typeChart == 'Product Chart'">Product Chart</p>
                        </div>
                        <div class="col-lg-3 col-sm-12 d-flex justify-content-end">
                            <multiselect
                            v-model="typeChart"
                            :options="typeChartOptions"
                            :allow-empty="false"
                            :searchable="false"
                            :close-on-select="false"
                            :show-labels="false"
                            ></multiselect>
                        </div>
                    </div>
                    <!-- End Of Chart Header -->

                    <!-- Area Chart -->
                    <div class="row my-5" v-if="typeChart == 'Area Chart'">
                        <div class="col-lg-6">
                            <VueApexCharts
                            type="donut"
                            :options="chart1.chartOptions"
                            :series="chart1.series"
                            id="AreaChart"
                            ></VueApexCharts>
                        </div>
                        <div class="col-lg-6 duo-chart">
                            <!-- <VueApexCharts
                            type="bar"
                            :options="chart3.chartOptions"
                            :series="chart3.series"
                            ></VueApexCharts> -->
                            <VueApexCharts type="bar" height="350" :options="chart3.chartOptions" :series="chart3.series"></VueApexCharts>
                        </div>
                    </div>
                    <!-- End Of Area Chart -->

                    <!-- Group Chart -->
                    <div class="row my-5" v-if="typeChart == 'Group Chart'">
                        <div class="col-lg-6">
                            <VueApexCharts
                            type="donut"
                            :options="chart2.chartOptions"
                            :series="chart2.series"
                            ></VueApexCharts>
                        </div>
                        <div class="col-lg-6 duo-chart">
                            <!-- <VueApexCharts
                            type="bar"
                            :options="chart4.chartOptions"
                            :series="chart4.series"
                            ></VueApexCharts> -->
                            <VueApexCharts type="bar" height="350" :options="chart4.chartOptions" :series="chart4.series"></VueApexCharts>
                        </div>
                    </div>
                    <!-- End Of Group Chart -->

                    <!-- Product Chart -->
                    <div class="row my-5" v-if="typeChart == 'Product Chart'">
                        <div class="col-lg-6">
                            <VueApexCharts
                            type="donut"
                            :options="chart5.chartOptions"
                            :series="chart5.series"
                            ></VueApexCharts>
                        </div>
                        <div class="col-lg-6 duo-chart">
                            <!-- <VueApexCharts
                            type="bar"
                            :options="chart6.chartOptions"
                            :series="chart6.series"
                            ></VueApexCharts> -->
                            <VueApexCharts type="bar" height="350" :options="chart6.chartOptions" :series="chart6.series"></VueApexCharts>
                        </div>
                    </div>
                    <!-- End Of Product Chart -->
                    </section>

                    <section class="custom-rofo">
                    <!-- Chart Header -->
                    <div class="row my-5 custom-height">
                        <div class="col-lg-9 col-sm-12">
                            <p class="h2" v-if="rofoChart == 'RoFo Total'">RoFo Total</p>
                            <p class="h2" v-if="rofoChart == 'RoFo Garuda'">RoFo Garuda</p>
                            <p class="h2" v-if="rofoChart == 'RoFo Citilink'">RoFo Citilink</p>
                        </div>
                        <div class="col-lg-3 col-sm-12 d-flex justify-content-end">
                            <multiselect
                            v-model="rofoChart"
                            :options="rofoChartOptions"
                            :allow-empty="false"
                            :searchable="false"
                            :close-on-select="false"
                            :show-labels="false"
                            ></multiselect>
                        </div>
                    </div>
                    <!-- End Of Chart Header -->
                    
                    <!-- RoFo Total Chart -->
                    <div class="row" id="single-chart" v-if="rofoChart == 'RoFo Total'">
                        <div class="col-lg-9">
                            <VueApexCharts type="bar" height="350" :options="chart7.chartOptions" :series="chart7.series"></VueApexCharts>
                        </div>
                        <div class="col-lg-3">
                            <VueApexCharts type="bar" height="350" :options="chart10.chartOptions" :series="chart10.series"></VueApexCharts>
                        </div>
                    </div>
                    
                    <!-- End Of RoFo Total Chart -->
                    
                    <!-- RoFo Sales Plan Garuda Chart -->
                    <div class="row" id="single-chart" v-if="rofoChart == 'RoFo Garuda'">
                        <div class="col-lg-9">
                            <VueApexCharts type="bar" height="350" :options="chart8.chartOptions" :series="chart8.series"></VueApexCharts>
                        </div>
                        <div class="col-lg-3">
                            <VueApexCharts type="bar" height="350" :options="chart11.chartOptions" :series="chart11.series"></VueApexCharts>
                        </div>
                    </div>
                    <!-- End Of RoFo Sales Plan Garuda Chart -->

                    <!-- RoFo Sales Plan Citilink Chart -->
                    <div class="row" id="single-chart" v-if="rofoChart == 'RoFo Citilink'">
                        <div class="col-lg-9">
                            <VueApexCharts type="bar" height="350" :options="chart9.chartOptions" :series="chart9.series"></VueApexCharts>
                        </div>
                        <div class="col-lg-3">
                            <VueApexCharts type="bar" height="350" :options="chart12.chartOptions" :series="chart12.series"></VueApexCharts>
                        </div>
                    </div>
                    <!-- End Of RoFo Sales Plan Citilink Chart -->
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
            typeChart: null,
            rofoChartOptions: ['RoFo Total', 'RoFo Garuda', 'RoFo Citilink'],
            rofoChart: null,
            
            // Donut Area 
            chart1 : {
                series: [],
                chartOptions: {
                noData: {
                    text: 'Loading...'
                },
                fill: {
                    colors:['#000000', '#278EA5', '#735F32', '#C69749']
                },
                colors:['#000000', '#278EA5', '#735F32', '#C69749'],
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
            // Donut Group
            chart2 : {
                series: [44, 55],
                chartOptions: {
                    labels: ["GA", "NGA"],
                    fill: {
                        colors:['#000000', '#278EA5']
                    },
                    colors:['#000000', '#278EA5'],
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
            // Donut Product
            chart5 : {
                series: [],
                chartOptions: {
                    labels: [
                            'Airframe',
                            'Component',
                            'Engineering',
                            'Line',
                            'Material Trading & Logistic',
                            'Engine & APU',
                            'IGTE',
                            'Learning',
                            'Others',
                        ],
                    fill: {
                        colors:['#000000', '#278EA5', '#735F32', '#C69749', '#00e396', '#B4A5A5', '#801336', '#EE4540', '#1F4287']
                    },
                    colors:['#000000', '#278EA5', '#735F32', '#C69749', '#00e396', '#B4A5A5', '#801336', '#EE4540', '#1F4287'],
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
                                        show: true,
                                        formatter: function (val) {
                                            let total_series = 0
                                            for(let i = 0; i < val.config.series.length; i++){
                                                total_series += val.config.series[i]
                                            }
                                            total_series = Math.round(total_series * 100) / 100;
                                            return total_series
                                        },
                                    },
                                },
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

            
            // Bar Area
            // chart3: {
            //     series: [
            //     {
            //         name: 'Sales',
            //         data: [
            //         {
            //             x: 'I',
            //             y: null,
            //             goals: [
            //                 {
            //                     name: 'Target',
            //                     value: null,
            //                     strokeHeight: 5,
            //                     strokeColor: '#775DD0'
            //                 }
            //             ]
            //         },
            //         {
            //             x: 'II',
            //             y: null,
            //             goals: [
            //                 {
            //                     name: 'Target',
            //                     value: null,
            //                     strokeHeight: 5,
            //                     strokeColor: '#775DD0'
            //                 }
            //             ]
            //         },
            //         {
            //             x: 'III',
            //             y: null,
            //             goals: [
            //                 {
            //                     name: 'Target',
            //                     value: null,
            //                     strokeHeight: 5,
            //                     strokeColor: '#775DD0'
            //                 }
            //             ]
            //         },
            //         {
            //             x: 'KAM',
            //             y: null,
            //             goals: [
            //                 {
            //                     name: 'Target',
            //                     value: null,
            //                     strokeHeight: 5,
            //                     strokeColor: '#775DD0'
            //                 }
            //             ]
            //         },
            //         ]
            //     }
            //     ],
            //     chartOptions: {
            //         chart: {
            //             height: "100%",
            //             type: 'bar',
            //             toolbar: {
            //                 show: false
            //             }
            //         },
            //         plotOptions: {
            //         bar: {
            //             columnWidth: '60%'
            //         }
            //         },
            //         colors: ['#00E396'],
            //         dataLabels: {
            //             enabled: false
            //         },
            //         legend: {
            //             show: true,
            //             showForSingleSeries: true,
            //             customLegendItems: ['Sales', 'Target'],
            //             markers: {
            //                 fillColors: ['#00E396', '#775DD0']
            //             }
            //         }
            //     },
            // },
            chart3: {
                series:
                [
                    {
                        name: 'Target',
                        data: []
                    },
                    {
                        name: 'Progress',
                        data: []
                    },
                ],
                chartOptions: {
                    chart: {
                        type: 'bar',
                        height: 'auto',
                        toolbar: {
                            show: false
                        }
                    },
                    plotOptions: {
                        bar: {
                            horizontal: false,
                            columnWidth: '55%',
                            endingShape: 'rounded'
                        },
                    },
                    dataLabels: {
                        enabled: false,
                        enabledOnSeries: undefined,
                        formatter: function (val, opts) {
                            return val
                        },
                        textAnchor: 'middle',
                        distributed: false,
                        offsetX: 0,
                        offsetY: 0,
                        style: {
                            fontSize: '11px',
                            fontWeight: 'bold',
                            colors: undefined
                        },
                        background: {
                            enabled: true,
                            foreColor: '#fff',
                            padding: 4,
                            borderRadius: 2,
                            borderWidth: 1,
                            borderColor: '#fff',
                            opacity: 0.9,
                            dropShadow: {
                            enabled: false,
                            top: 1,
                            left: 1,
                            blur: 1,
                            color: '#000',
                            opacity: 0.45
                            }
                        },
                        dropShadow: {
                            enabled: false,
                            top: 1,
                            left: 1,
                            blur: 1,
                            color: '#000',
                            opacity: 0.45
                        }
                    },
                    stroke: {
                        show: true,
                        width: 2,
                        colors: ['transparent']
                    },
                    xaxis: {
                        categories: [],
                        labels: {
                            minHeight: undefined,
                            maxHeight: 120,
                        }
                    },
                    fill: {
                        opacity: 1
                    },
                },
            },
            // Bar Group
            // chart4: {
            //     series: [
            //     {
            //         name: 'Sales',
            //         data: [
            //         {
            //             x: 'GA',
            //             y: 4432,
            //             goals: [
            //                 {
            //                     name: 'Target',
            //                     value: 5400,
            //                     strokeHeight: 5,
            //                     strokeColor: '#775DD0'
            //                 }
            //             ]
            //         },
            //         {
            //             x: 'NGA',
            //             y: 5423,
            //             goals: [
            //                 {
            //                     name: 'Target',
            //                     value: 5200,
            //                     strokeHeight: 5,
            //                     strokeColor: '#775DD0'
            //                 }
            //             ]
            //         },
            //         ]
            //     }
            //     ],
            //     chartOptions: {
            //         chart: {
            //             height: "100%",
            //             type: 'bar',
            //             toolbar: {
            //                 show: false
            //             }
            //         },
            //         plotOptions: {
            //         bar: {
            //             columnWidth: '60%'
            //         }
            //         },
            //         colors: ['#00E396'],
            //         dataLabels: {
            //             enabled: false,
            //         // TODO munculin persen disini
            //         // enabled: true,
            //         // formatter: function (val) {
            //         //   return val + "%";
            //         // },
            //         },
            //         legend: {
            //             show: true,
            //             showForSingleSeries: true,
            //             customLegendItems: ['Sales', 'Target'],
            //             markers: {
            //                 fillColors: ['#00E396', '#775DD0']
            //             }
            //         }
            //     },
            // },
            chart4: {
                series:
                [
                    {
                        name: 'Target',
                        data: []
                    },
                    {
                        name: 'Progress',
                        data: []
                    },
                ],
                chartOptions: {
                    chart: {
                        type: 'bar',
                        height: 'auto',
                        toolbar: {
                            show: false
                        }
                    },
                    plotOptions: {
                        bar: {
                            horizontal: false,
                            columnWidth: '55%',
                            endingShape: 'rounded'
                        },
                    },
                    
                    dataLabels: {
                        enabled: false,
                    },
                    stroke: {
                        show: true,
                        width: 2,
                        colors: ['transparent']
                    },
                    xaxis: {
                        categories: [],
                        labels: {
                            minHeight: undefined,
                            maxHeight: 120,
                        }
                    },
                    fill: {
                        opacity: 1
                    },
                },
            },
            // Bar Product
            // chart6: {
            //     series: [
            //     {
            //         name: 'Actual',
            //         data: [
            //             {
            //                 x: 'Learning',
            //                 y: null,
            //                 goals: [
            //                     {
            //                         name: 'Target',
            //                         value: null,
            //                         strokeHeight: 5,
            //                         strokeColor: '#775DD0'
            //                     }
            //                 ]
            //             },
            //             {
            //                 x: 'IGTE',
            //                 y: null,
            //                 goals: [
            //                     {
            //                         name: 'Target',
            //                         value: null,
            //                         strokeHeight: 5,
            //                         strokeColor: '#775DD0'
            //                     }
            //                 ]
            //             },
            //             {
            //                 x: 'Others',
            //                 y: null,
            //                 goals: [
            //                     {
            //                         name: 'Target',
            //                         value: null,
            //                         strokeHeight: 5,
            //                         strokeColor: '#775DD0'
            //                     }
            //                 ]
            //             },
            //             {
            //                 x: 'Engine & APU',
            //                 y: null,
            //                 goals: [
            //                     {
            //                         name: 'Target',
            //                         value: null,
            //                         strokeHeight: 5,
            //                         strokeColor: '#775DD0'
            //                     }
            //                 ]
            //             },
            //             {
            //                 x: 'Material Trading & Logistic',
            //                 y: null,
            //                 goals: [
            //                     {
            //                         name: 'Target',
            //                         value: null,
            //                         strokeHeight: 5,
            //                         strokeColor: '#775DD0'
            //                     }
            //                 ]
            //             },
            //             {
            //                 x: 'Line',
            //                 y: null,
            //                 goals: [
            //                     {
            //                         name: 'Target',
            //                         value: null,
            //                         strokeHeight: 5,
            //                         strokeColor: '#775DD0'
            //                     }
            //                 ]
            //             },
            //             {
            //                 x: 'Engineering',
            //                 y: null,
            //                 goals: [
            //                     {
            //                         name: 'Target',
            //                         value: null,
            //                         strokeHeight: 5,
            //                         strokeColor: '#775DD0'
            //                     }
            //                 ]
            //             },
            //             {
            //                 x: 'Component',
            //                 y: null,
            //                 goals: [
            //                     {
            //                         name: 'Target',
            //                         value: null,
            //                         strokeHeight: 5,
            //                         strokeColor: '#775DD0'
            //                     }
            //                 ]
            //             },
            //             {
            //                 x: 'Airframe',
            //                 y: null,
            //                 goals: [
            //                     {
            //                         name: 'Target',
            //                         value: null,
            //                         strokeHeight: 5,
            //                         strokeColor: '#775DD0'
            //                     }
            //                 ]
            //             },
            //         ]
            //     }
            //     ],
            //     chartOptions: {
            //         chart: {
            //             height: "100%",
            //             type: 'bar',
            //             toolbar: {
            //                 show: false
            //             }
            //         },
            //         plotOptions: {
            //             bar: {
            //                 columnWidth: '60%'
            //             }
            //         },
            //         colors: ['#00E396'],
            //         dataLabels: {
            //             enabled: false
            //         },
            //         legend: {
            //             show: true,
            //             showForSingleSeries: true,
            //             customLegendItems: ['Sales', 'Target'],
            //             markers: {
            //                 fillColors: ['#00E396', '#775DD0']
            //             }
            //         }
            //     },
            // },
            chart6: {
                series:
                [
                    {
                        name: 'Target',
                        data: []
                    },
                    {
                        name: 'Progress',
                        data: []
                    },
                ],
                chartOptions: {
                    chart: {
                        type: 'bar',
                        height: '450px',
                        toolbar: {
                            show: false
                        }
                    },
                    plotOptions: {
                        bar: {
                            horizontal: false,
                            columnWidth: '55%',
                            endingShape: 'rounded'
                        },
                    },
                    dataLabels: {
                        enabled: false,
                    },
                    stroke: {
                        show: true,
                        width: 2,
                        colors: ['transparent']
                    },
                    xaxis: {
                        categories: [],
                        labels: {
                            minHeight: 150,
                            maxHeight: 200,
                        }
                    },
                    fill: {
                        opacity: 1
                    },
                },
            },

            // RoFo Total Month
            chart7: {
                series:
                [
                    {
                        name: 'Target',
                        data: []
                    },
                    {
                        name: 'Progress',
                        data: []
                    },
                ],
                chartOptions: {
                    chart: {
                        type: 'bar',
                        height: 350,
                        toolbar: {
                            show: false
                        }
                    },
                    plotOptions: {
                        bar: {
                            horizontal: false,
                            columnWidth: '55%',
                            endingShape: 'rounded'
                        },
                    },
                    dataLabels: {
                        enabled: false
                    },
                    stroke: {
                        show: true,
                        width: 2,
                        colors: ['transparent']
                    },
                    xaxis: {
                        categories: [],
                    },
                    fill: {
                        opacity: 1
                    },
                },
            },
            // RoFo Total Year
            chart10: {
                series: [
                    {
                        name: 'Target',
                        data: []
                    },
                    {
                        name: 'Progress',
                        data: []
                    },
                ],
                chartOptions: {
                    chart: {
                        type: 'bar',
                        height: 350,
                        toolbar: {
                            show: false
                        }
                    },
                    plotOptions: {
                        bar: {
                            horizontal: false,
                            columnWidth: '55%',
                            endingShape: 'rounded'
                        },
                    },
                    dataLabels: {
                        enabled: false
                    },
                    stroke: {
                        show: true,
                        width: 2,
                        colors: ['transparent']
                    },
                    xaxis: {
                        categories: [],
                    },
                    fill: {
                        opacity: 1
                    },
                },
            },
            
            // RoFo Garuda Month
            chart8: {
                series: [
                    {
                        name: 'Target',
                        data: []
                    },
                    {
                        name: 'Progress',
                        data: []
                    },
                ],
                chartOptions: {
                    chart: {
                        type: 'bar',
                        height: 350,
                        toolbar: {
                            show: false
                        }
                    },
                    plotOptions: {
                        bar: {
                            horizontal: false,
                            columnWidth: '55%',
                            endingShape: 'rounded'
                        },
                    },
                    dataLabels: {
                        enabled: false
                    },
                    stroke: {
                        show: true,
                        width: 2,
                        colors: ['transparent']
                    },
                    xaxis: {
                        categories: [],
                    },
                    fill: {
                        opacity: 1
                    },
                },
            },
            // RoFo Garuda Year
            chart11: {
                series: [
                    {
                        name: 'Target',
                        data: []
                    },
                    {
                        name: 'Progress',
                        data: []
                    },
                ],
                chartOptions: {
                    chart: {
                        type: 'bar',
                        height: 350,
                        toolbar: {
                            show: false
                        }
                    },
                    plotOptions: {
                        bar: {
                            horizontal: false,
                            columnWidth: '55%',
                            endingShape: 'rounded'
                        },
                    },
                    dataLabels: {
                        enabled: false
                    },
                    stroke: {
                        show: true,
                        width: 2,
                        colors: ['transparent']
                    },
                    xaxis: {
                        categories: [],
                    },
                    fill: {
                        opacity: 1
                    },
                },
            },
            
            // RoFo Citilink Month
            chart9: {
                series: [
                    {
                        name: 'Target',
                        data: []
                    },
                    {
                        name: 'Progress',
                        data: []
                    },
                ],
                chartOptions: {
                    chart: {
                        type: 'bar',
                        height: 350,
                        toolbar: {
                            show: false
                        }
                    },
                    plotOptions: {
                        bar: {
                            horizontal: false,
                            columnWidth: '55%',
                            endingShape: 'rounded'
                        },
                    },
                    dataLabels: {
                        enabled: false
                    },
                    stroke: {
                        show: true,
                        width: 2,
                        colors: ['transparent']
                    },
                    xaxis: {
                        categories: [],
                    },
                    fill: {
                        opacity: 1
                    },
                },
            },
            // RoFo Citilink Year
            chart12: {
                series: [
                    {
                        name: 'Target',
                        data: []
                    },
                    {
                        name: 'Progress',
                        data: []
                    },
                ],
                chartOptions: {
                    chart: {
                        type: 'bar',
                        height: 350,
                        toolbar: {
                            show: false
                        }
                    },
                    plotOptions: {
                        bar: {
                            horizontal: false,
                            columnWidth: '55%',
                            endingShape: 'rounded'
                        },
                    },
                    dataLabels: {
                        enabled: false
                    },
                    stroke: {
                        show: true,
                        width: 2,
                        colors: ['transparent']
                    },
                    xaxis: {
                        categories: [],
                    },
                    fill: {
                        opacity: 1
                    },
                },
            },
        }
    },
    created() {
        this.loading()
        this.areaChart()
        this.groupChart()
        this.productChart()
        this.rofoTotal()
        this.rofoTotalYear()
        this.rofoTotalGaruda()
        this.rofoTotalGarudaYear()
        this.rofoTotalCitilink()
        this.rofoTotalCitilinkYear()
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
        areaChart() {
            this.$axios
                .get('api/dashboard-area')
                .then((response) => {
                // Chart 1 Update Series
                this.chart1.series = response.data.data.pie

                // Chart 3 Update Value
                // this.chart3.series[0].data[0].goals[0].value = response.data.data.bar.area1.target
                // this.chart3.series[0].data[1].goals[0].value = response.data.data.bar.area2.target
                // this.chart3.series[0].data[2].goals[0].value = response.data.data.bar.area3.target
                // this.chart3.series[0].data[3].goals[0].value = response.data.data.bar.kam.target

                // Chart 3 Update Value
                // this.chart3.series[0].data[0].y = response.data.data.bar.area1.progress
                // this.chart3.series[0].data[1].y = response.data.data.bar.area2.progress
                // this.chart3.series[0].data[2].y = response.data.data.bar.area3.progress
                // this.chart3.series[0].data[3].y = response.data.data.bar.kam.progress
            
                this.chart3.series[0].data = response.data.data.bar.target
                this.chart3.series[1].data = response.data.data.bar.progress
                this.chart3.chartOptions.xaxis.categories = response.data.data.bar.percentage
            

                this.typeChart = 'Area Chart'
                this.rofoChart = 'RoFo Garuda'
                })
                .catch((error) => console.log(error))
        },
        groupChart() {
            this.$axios
                .get('api/dashboard-group')
                .then((response) => {
                // Chart 1 Update Series
                this.chart2.series = response.data.data.pie

                // Chart 4 Update Value
                // this.chart4.series[0].data[0].goals[0].value = response.data.data.bar.group1.target
                // this.chart4.series[0].data[1].goals[0].value = response.data.data.bar.group2.target

                // Chart 4 Update Value
                // this.chart4.series[0].data[0].y = response.data.data.bar.group1.progress
                // this.chart4.series[0].data[1].y = response.data.data.bar.group2.progress

                this.chart4.series[0].data = response.data.data.bar.target
                this.chart4.series[1].data = response.data.data.bar.progress
                this.chart4.chartOptions.xaxis.categories = response.data.data.bar.percentage
                
                })
                .catch((error) => console.log(error))
        },
        productChart() {
            this.$axios
                .get('api/dashboard-product')
                .then((response) => {
                // Chart 5 Update Series
                this.chart5.series = response.data.data.pie

                // Chart 6 Update Value
                // this.chart6.series[0].data[0].goals[0].value = response.data.data.bar.learning.target
                // this.chart6.series[0].data[1].goals[0].value = response.data.data.bar.igte.target
                // this.chart6.series[0].data[2].goals[0].value = response.data.data.bar.others.target
                // this.chart6.series[0].data[3].goals[0].value = response.data.data.bar.engapu.target
                // this.chart6.series[0].data[4].goals[0].value = response.data.data.bar.material.target
                // this.chart6.series[0].data[5].goals[0].value = response.data.data.bar.line.target
                // this.chart6.series[0].data[6].goals[0].value = response.data.data.bar.engineering.target
                // this.chart6.series[0].data[7].goals[0].value = response.data.data.bar.component.target
                // this.chart6.series[0].data[8].goals[0].value = response.data.data.bar.airframe.target

                // Chart 6 Update Value
                // this.chart6.series[0].data[0].y = response.data.data.bar.learning.progress
                // this.chart6.series[0].data[1].y = response.data.data.bar.igte.progress
                // this.chart6.series[0].data[2].y = response.data.data.bar.others.progress
                // this.chart6.series[0].data[3].y = response.data.data.bar.engapu.progress
                // this.chart6.series[0].data[4].y = response.data.data.bar.material.progress
                // this.chart6.series[0].data[5].y = response.data.data.bar.line.progress
                // this.chart6.series[0].data[6].y = response.data.data.bar.engineering.progress
                // this.chart6.series[0].data[7].y = response.data.data.bar.component.progress
                // this.chart6.series[0].data[8].y = response.data.data.bar.airframe.progress

                this.chart6.series[0].data = response.data.data.bar.target
                this.chart6.series[1].data = response.data.data.bar.progress
                this.chart6.chartOptions.xaxis.categories = response.data.data.bar.percentage
                
                this.rofoChart = 'RoFo Citilink'
                })
                .catch((error) => console.log(error))
        },
        rofoTotal() {
            this.$axios
                .get('api/dashboard-rofo-total-month')
                .then((response) => {
                    // Chart 7 Update Series
                    this.chart7.series[0].data = response.data.data.target
                    this.chart7.series[1].data = response.data.data.progress
                    this.chart7.chartOptions.xaxis.categories = response.data.data.percentage

                this.rofoChart = 'RoFo Total'
                })
            .catch((error) => console.log(error))
        },
        rofoTotalYear() {
            this.$axios
                .get('api/dashboard-rofo-total-year')
                .then((response) => {
                    // chart10 Update Series
                    this.chart10.series[0].data = response.data.data.target
                    this.chart10.series[1].data = response.data.data.progress
                    this.chart10.chartOptions.xaxis.categories = response.data.data.percentage

                this.rofoChart = 'RoFo Total'
                })
            .catch((error) => console.log(error))
        },
        rofoTotalGaruda() {
            this.$axios
                .get('api/dashboard-rofo-garuda-month')
                .then((response) => {
                // Chart 8 Update Series
                    this.chart8.series[0].data = response.data.data.target
                    this.chart8.series[1].data = response.data.data.progress
                    this.chart8.chartOptions.xaxis.categories = response.data.data.percentage
                })
                .catch((error) => console.log(error))
        },
        rofoTotalGarudaYear() {
            this.$axios
                .get('api/dashboard-rofo-garuda-year')
                .then((response) => {
                    // chart11 Update Series
                    this.chart11.series[0].data = response.data.data.target
                    this.chart11.series[1].data = response.data.data.progress
                    this.chart11.chartOptions.xaxis.categories = response.data.data.percentage

                this.rofoChart = 'RoFo Total'
                })
            .catch((error) => console.log(error))
        },
        rofoTotalCitilink() {
            this.$axios
                .get('api/dashboard-rofo-citilink-month')
                .then((response) => {
                // Chart 9 Update Series
                    this.chart9.series[0].data = response.data.data.target
                    this.chart9.series[1].data = response.data.data.progress
                    this.chart9.chartOptions.xaxis.categories = response.data.data.percentage

                })
                .catch((error) => console.log(error))
        },
        rofoTotalCitilinkYear() {
            this.$axios
                .get('api/dashboard-rofo-citilink-year')
                .then((response) => {
                // Chart 12 Update Series
                    this.chart12.series[0].data = response.data.data.target
                    this.chart12.series[1].data = response.data.data.progress
                    this.chart12.chartOptions.xaxis.categories = response.data.data.percentage

                })
                .catch((error) => console.log(error))
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
    .single-chart{
        max-width: 1080px;
        margin: auto;
    }
    .duo-chart{
        max-width: 720px;
        margin: auto;
    }
</style>
