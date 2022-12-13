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
                        <div class="col-md-6">
                            <VueApexCharts
                            type="donut"
                            :options="chart1.chartOptions"
                            :series="chart1.series"
                            id="AreaChart"
                            ></VueApexCharts>
                        </div>
                        <div class="col-md-6 duo-chart">
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
                        <div class="col-md-6">
                            <VueApexCharts
                            type="donut"
                            :options="chart2.chartOptions"
                            :series="chart2.series"
                            ></VueApexCharts>
                        </div>
                        <div class="col-md-6 duo-chart">
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
                        <div class="col-md-6">
                            <VueApexCharts
                            type="donut"
                            :options="chart5.chartOptions"
                            :series="chart5.series"
                            ></VueApexCharts>
                        </div>
                        <div class="col-md-6 duo-chart">
                            <VueApexCharts
                            type="bar"
                            :options="chart6.chartOptions"
                            :series="chart6.series"
                            ></VueApexCharts>
                        </div>
                    </div>
                    <!-- End Of Product Chart -->

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
                    <div class="col-md-12 single-chart" v-if="rofoChart == 'Rofo Total'">
                    <VueApexCharts
                        type="bar"
                        :options="chart7.chartOptions"
                        :series="chart7.series"
                    ></VueApexCharts>
                    </div>
                    <!-- End Of Rofo Total Chart -->
                    
                    <!-- RoFo Sales Plan Garuda Chart -->
                    <div class="col-md-12 single-chart" v-else-if="rofoChart == 'Rofo Garuda'">
                    <VueApexCharts
                        type="bar"
                        :options="chart8.chartOptions"
                        :series="chart8.series"
                    ></VueApexCharts>
                    </div>
                    <!-- End Of RoFo Sales Plan Garuda Chart -->

                    <!-- RoFo Sales Plan Citilink Chart -->
                    <div class="col-md-12 single-chart" v-else-if="rofoChart == 'Rofo Citilink'">
                    <VueApexCharts
                        type="bar"
                        :options="chart9.chartOptions"
                        :series="chart9.series"
                    ></VueApexCharts>
                    </div>
                    <!-- End Of RoFo Sales Plan Citilink Chart -->

                    <!-- Else Condition Rofo Chart -->
                    <div class="col-md-12 single-chart" v-else>
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
        typeChart: null,
        rofoChartOptions: ['Rofo Total', 'Rofo Garuda', 'Rofo Citilink'],
        rofoChart: null,
        chart1 : {
            series: [],
            chartOptions: {
            noData: {
                text: 'Loading...'
            },
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
                name: 'Sales',
                data: [
                {
                    x: 'KAM',
                    y: null,
                    goals: [
                    {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                    }
                    ]
                },
                {
                    x: 'I',
                    y: null,
                    goals: [
                    {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                    }
                    ]
                },
                {
                    x: 'II',
                    y: null,
                    goals: [
                    {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                    }
                    ]
                },
                {
                    x: 'III',
                    y: null,
                    goals: [
                    {
                        name: 'Target',
                        value: null,
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
                height: "100%",
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
                customLegendItems: ['Sales', 'Target'],
                markers: {
                    fillColors: ['#00E396', '#775DD0']
                }
                }
            },
        },
        chart4: {
            series: [
            {
                name: 'Sales',
                data: [
                {
                    x: 'GA',
                    y: 4432,
                    goals: [
                    {
                        name: 'Target',
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
                        name: 'Target',
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
                height: "100%",
                type: 'bar'
                },
                plotOptions: {
                bar: {
                    columnWidth: '60%'
                }
                },
                colors: ['#00E396'],
                dataLabels: {
                enabled: false,
                // TODO munculin persen disini
                // enabled: true,
                // formatter: function (val) {
                //   return val + "%";
                // },
                },
                legend: {
                show: true,
                showForSingleSeries: true,
                customLegendItems: ['Sales', 'Target'],
                markers: {
                    fillColors: ['#00E396', '#775DD0']
                }
                }
            },
        },
        chart5 : {
            series: [],
            chartOptions: {
                labels: ["Learning", "IGTE", "Others", "Engine & APU", "Material Trading & Logistic", "Line", "Engineering", "Component", "Airframe"],
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
                    x: 'Learning',
                    y: null,
                    goals: [
                        {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                        }
                    ]
                    },
                    {
                    x: 'IGTE',
                    y: null,
                    goals: [
                        {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                        }
                    ]
                    },
                    {
                    x: 'Others',
                    y: null,
                    goals: [
                        {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                        }
                    ]
                    },
                    {
                    x: 'Engine & APU',
                    y: null,
                    goals: [
                        {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                        }
                    ]
                    },
                    {
                    x: 'Material Trading & Logistic',
                    y: null,
                    goals: [
                        {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                        }
                    ]
                    },
                    {
                    x: 'Line',
                    y: null,
                    goals: [
                        {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                        }
                    ]
                    },
                    {
                    x: 'Engineering',
                    y: null,
                    goals: [
                        {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                        }
                    ]
                    },
                    {
                    x: 'Component',
                    y: null,
                    goals: [
                        {
                        name: 'Target',
                        value: null,
                        strokeHeight: 5,
                        strokeColor: '#775DD0'
                        }
                    ]
                    },
                    {
                    x: 'Airframe',
                    y: null,
                    goals: [
                        {
                        name: 'Target',
                        value: null,
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
                height: "100%",
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
                customLegendItems: ['Sales', 'Target'],
                markers: {
                    fillColors: ['#00E396', '#775DD0']
                }
                }
            },
        },
        chart7: {
            series: [{
                name: 'Rofo Sales Plan',
                data: []
            }, {
                name: 'GAP',
                data: []
            }, {
                name: 'RKAP Sales Plan',
                data: []
            }],
            chartOptions: {
                chart: {
                    type: 'bar',
                    height: "100%",
                    stacked: true,
                    toolbar: {
                        show: true
                    },
                    zoom: {
                        enabled: true
                    }
                },
                responsive: [{
                    breakpoint: undefined,
                    options: {},
                    width: "100%"
                }],
                plotOptions: {
                bar: {
                    horizontal: false,
                    borderRadius: 10,
                    dataLabels: {
                    total: {
                        enabled: false,
                        style: {
                        fontSize: '13px',
                        fontWeight: 900
                        }
                    }
                    }
                },
                },
                xaxis: {
                type: 'category',
                categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec', 'RoFo YTD'],
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
                name: 'Rofo Sales Plan',
                data: []
            }, {
                name: 'GAP',
                data: []
            }, {
                name: 'RKAP Sales Plan',
                data: []
            }],
            chartOptions: {
                chart: {
                    type: 'bar',
                    height: "100%",
                    stacked: true,
                    toolbar: {
                        show: true
                    },
                    zoom: {
                        enabled: true
                    }
                },
                responsive: [{
                    breakpoint: undefined,
                    options: {},
                    width: "100%"
                }],
                plotOptions: {
                bar: {
                    horizontal: false,
                    borderRadius: 10,
                    dataLabels: {
                    total: {
                        enabled: false,
                        style: {
                        fontSize: '13px',
                        fontWeight: 900
                        }
                    }
                    }
                },
                },
                xaxis: {
                type: 'category',
                categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec', 'RoFo YTD'],
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
                name: 'Rofo Sales Plan',
                data: []
            }, {
                name: 'GAP',
                data: []
            }, {
                name: 'RKAP Sales Plan',
                data: []
            }],
            chartOptions: {
                chart: {
                    type: 'bar',
                    height: "100%",
                    stacked: true,
                    toolbar: {
                        show: true
                    },
                    zoom: {
                        enabled: true
                    }
                },
                responsive: [{
                    breakpoint: undefined,
                    options: {},
                    width: "100%"
                }],
                plotOptions: {
                bar: {
                    horizontal: false,
                    borderRadius: 10,
                    dataLabels: {
                    total: {
                        enabled: false,
                        style: {
                        fontSize: '13px',
                        fontWeight: 900
                        }
                    }
                    }
                },
                },
                xaxis: {
                type: 'category',
                categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec', 'RoFo YTD'],
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
    this.areaChart()
    this.groupChart()
    this.productChart()
    this.rofoTotal()
    this.rofoTotalGaruda()
    this.rofoTotalCitilink()
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
                this.chart3.series[0].data[0].goals[0].value = response.data.data.bar.area1.target
                this.chart3.series[0].data[1].goals[0].value = response.data.data.bar.area2.target
                this.chart3.series[0].data[2].goals[0].value = response.data.data.bar.area3.target
                this.chart3.series[0].data[3].goals[0].value = response.data.data.bar.kam.target

                // Chart 3 Update Value
                this.chart3.series[0].data[0].y = response.data.data.bar.area1.progress
                this.chart3.series[0].data[1].y = response.data.data.bar.area2.progress
                this.chart3.series[0].data[2].y = response.data.data.bar.area3.progress
                this.chart3.series[0].data[3].y = response.data.data.bar.kam.progress

                this.typeChart = 'Area Chart'
                this.rofoChart = 'Rofo Total'
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
                this.chart4.series[0].data[0].goals[0].value = response.data.data.bar.group1.target
                this.chart4.series[0].data[1].goals[0].value = response.data.data.bar.group2.target

                // Chart 4 Update Value
                this.chart4.series[0].data[0].y = response.data.data.bar.group1.progress
                this.chart4.series[0].data[1].y = response.data.data.bar.group2.progress
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
                this.chart6.series[0].data[0].goals[0].value = response.data.data.bar.learning.target
                this.chart6.series[0].data[1].goals[0].value = response.data.data.bar.igte.target
                this.chart6.series[0].data[2].goals[0].value = response.data.data.bar.others.target
                this.chart6.series[0].data[3].goals[0].value = response.data.data.bar.engapu.target
                this.chart6.series[0].data[4].goals[0].value = response.data.data.bar.material.target
                this.chart6.series[0].data[5].goals[0].value = response.data.data.bar.line.target
                this.chart6.series[0].data[6].goals[0].value = response.data.data.bar.engineering.target
                this.chart6.series[0].data[7].goals[0].value = response.data.data.bar.component.target
                this.chart6.series[0].data[8].goals[0].value = response.data.data.bar.airframe.target

                // Chart 6 Update Value
                this.chart6.series[0].data[0].y = response.data.data.bar.learning.progress
                this.chart6.series[0].data[1].y = response.data.data.bar.igte.progress
                this.chart6.series[0].data[2].y = response.data.data.bar.others.progress
                this.chart6.series[0].data[3].y = response.data.data.bar.engapu.progress
                this.chart6.series[0].data[4].y = response.data.data.bar.material.progress
                this.chart6.series[0].data[5].y = response.data.data.bar.line.progress
                this.chart6.series[0].data[6].y = response.data.data.bar.engineering.progress
                this.chart6.series[0].data[7].y = response.data.data.bar.component.progress
                this.chart6.series[0].data[8].y = response.data.data.bar.airframe.progress

                this.rofoChart = 'Rofo Garuda'
                })
                .catch((error) => console.log(error))
        },
        rofoTotal() {
            this.$axios
                .get('api/dashboard-rofo-total')
                .then((response) => {
                // Chart 7 Update Series
                this.chart7.series[0].data = response.data.data.progress
                this.chart7.series[1].data = response.data.data.gap
                this.chart7.series[2].data = response.data.data.target

                this.rofoChart = 'Rofo Total'
                })
            .catch((error) => console.log(error))
        },
        rofoTotalGaruda() {
            this.$axios
                .get('api/dashboard-rofo-garuda')
                .then((response) => {
                // Chart 8 Update Series
                this.chart8.series[0].data = response.data.data.progress
                this.chart8.series[1].data = response.data.data.gap
                this.chart8.series[2].data = response.data.data.target
                })
                .catch((error) => console.log(error))
        },
        rofoTotalCitilink() {
            this.$axios
                .get('api/dashboard-rofo-citilink')
                .then((response) => {
                // Chart 9 Update Series
                this.chart9.series[0].data = response.data.data.progress
                this.chart9.series[1].data = response.data.data.gap
                this.chart9.series[2].data = response.data.data.target
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
