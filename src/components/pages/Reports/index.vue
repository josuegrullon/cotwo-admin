<template>
<div>
  <div class="tile is-ancestor">
    <div class="tile is-parent">
      <article class="tile is-child box">
      <ul class="nav nav-tabs">
  <!-- <li class="active"><a data-toggle="tab" href="#home">General</a></li> -->
  <li class="active"><a data-toggle="tab" href="#module1" @click="loadModule('m1')">Module 1</a></li>
  <li><a data-toggle="tab" href="#module2"@click="loadModule('m2')">Module 2</a></li>
  <li><a data-toggle="tab" href="#module3"@click="loadModule('m3')">Module 3</a></li>
  <li><a data-toggle="tab" href="#module4"@click="loadModule('m4')">Module 4</a></li>
</ul>

<div class="tab-content">
  <div id="home" class="tab-pane fade in">
    <p>
      <div class="md-12">
        <table id="general"
          data-toolbar="#toolbar"
          data-search="true"
          data-show-refresh="true"
          data-show-toggle="true"
          data-show-columns="true"
          data-show-export="true"
          data-detail-view="true"
          data-detail-formatter="detailFormatter"
          data-minimum-count-columns="2"
          data-show-pagination-switch="true"
          data-pagination="true"
          data-id-field="id"
          data-page-list="[10, 25, 50, 100, ALL]"
          data-show-footer="false"
          data-response-handler="responseHandler">
        </table>
      </div>
    </p>
  </div>
  <div id="module1" class="tab-pane fade in active">
    <p>
      <div class="md-12">
        <table id="m1"
          data-toolbar="#toolbar"
          data-search="true"
          data-show-refresh="true"
          data-show-toggle="true"
          data-show-columns="true"
          data-show-export="true"
          data-detail-view="false"
          data-detail-formatter="detailFormatter"
          data-minimum-count-columns="2"
          data-show-pagination-switch="true"
          data-pagination="true"
          data-id-field="id"
          data-page-list="[10, 25, 50, 100, ALL]"
          data-show-footer="false"
          data-response-handler="responseHandler">
        </table>
      </div>
    </p>
  </div>
  <div id="module2" class="tab-pane fade">
    <p>
      <div class="md-12">
        <table id="m2"
          data-toolbar="#toolbar"
          data-search="true"
          data-show-refresh="true"
          data-show-toggle="true"
          data-show-columns="true"
          data-show-export="true"
          data-detail-view="false"
          data-detail-formatter="detailFormatter"
          data-minimum-count-columns="2"
          data-show-pagination-switch="true"
          data-pagination="true"
          data-id-field="id"
          data-page-list="[10, 25, 50, 100, ALL]"
          data-show-footer="false"
          data-response-handler="responseHandler">
        </table>
      </div>
    </p>
  </div>
  <div id="module3" class="tab-pane fade">
    <p>
      <div class="md-12">
        <table id="m3"
          data-toolbar="#toolbar"
          data-search="true"
          data-show-refresh="true"
          data-show-toggle="true"
          data-show-columns="true"
          data-show-export="true"
          data-detail-view="false"
          data-detail-formatter="detailFormatter"
          data-minimum-count-columns="2"
          data-show-pagination-switch="true"
          data-pagination="true"
          data-id-field="id"
          data-page-list="[10, 25, 50, 100, ALL]"
          data-show-footer="false"
          data-response-handler="responseHandler">
        </table>
      </div>
    </p>
  </div>
  <div id="module4" class="tab-pane fade">
    <p>
      <div class="md-12">
        <table id="m4"
          data-toolbar="#toolbar"
          data-search="true"
          data-show-refresh="true"
          data-show-toggle="true"
          data-show-columns="true"
          data-show-export="true"
          data-detail-view="false"
          data-detail-formatter="detailFormatter"
          data-minimum-count-columns="2"
          data-show-pagination-switch="true"
          data-pagination="true"
          data-id-field="id"
          data-page-list="[10, 25, 50, 100, ALL]"
          data-show-footer="false"
          data-response-handler="responseHandler">
        </table>
      </div>
    </p>
  </div>
</div>
        
      </article>
    </div>
  </div>


</template>

<script>
// import $ from 'jquery'
// import bootstrap from 'bootstrap'
// import bt from 'bootstrap-table'
import config from '../../../config'
import moment from 'moment'
const { env } = config

let $ = window.jQuery

export default {
  name: 'A',
  http: {
    root: '/root',
    emulateJSON: true,
    emulateHTTP: true
  },
  data () {
    return {
    }
  },

  created: function () {
    this.loadModule('m1')
  },

  components: {
    // bootstrap
  },

  watch: {
  },

  computed: {
  },

  methods: {
    viewProfile: function (id) {
      console.log('view profile with id:', id)
    },
    totalTextFormatter (data) {
      return 'Total'
    },
    responseHandler (res) {
      console.log(res)
      return {
        rows: res.repos,
        total: res.repos.length
      }
    },

    formatDate (date) {
      return moment().format('LLLL')
    },

    getGeneralData () {
      $.ajax({
        url: env.API_URL + 'datatable',
        method: 'GET',
        dataType: 'json',
        async: true,
        success: (data) => {
          console.log(data)
          let $table = $('#general')
          // console.log(jsondata)
          $table.bootstrapTable({
            data: data,
            height: '300px',
            columns: [
              [
                {
                  field: 'identifier',
                  checkbox: true,
                  rowspan: 2,
                  align: 'center',
                  valign: 'middle'
                }, {
                  title: 'Item ID',
                  field: 'velocity',
                  rowspan: 2,
                  align: 'center',
                  valign: 'middle',
                  sortable: true
                }, {
                  title: 'Item Detail',
                  colspan: 3,
                  align: 'center'
                }
              ],
              [
                {
                  field: 'identifier',
                  title: 'Item Name'
                }, {
                  field: 'velocity',
                  title: 'ItemPrice'
                }, {
                  field: 'velocity',
                  title: 'Item Operate'
                }
              ]
            ]
          })
        }
      })
    },
    loadModule (id) {
      // console.log(id)
      let identifier = ''

      if (id === 'm1') identifier = '0001'
      if (id === 'm2') identifier = '0002'
      if (id === 'm3') identifier = '0003'
      if (id === 'm4') identifier = '0004'

      // console.log(identifier)
      $.ajax({
        url: env.API_URL + 'datatable/' + identifier,
        method: 'GET',
        dataType: 'json',
        async: true,
        success: (data) => {
          // console.log(data)
          let $table = $('#' + id)
          // console.log(jsondata)
          $table.bootstrapTable({
            data: data,
            height: '300px',
            columns: [
              // [
              //   // {
              //   //   // field: 'identifier',
              //   //   // checkbox: true,
              //   //   // rowspan: 2,
              //   //   align: 'center',
              //   //   // valign: 'middle',
              //   //   title: 'Item IDcd'
              //   // },
              //   {
              //     title: 'Modules Information',
              //     colspan: 3,
              //     align: 'center',
              //     // valign: 'middle',
              //     sortable: true
              //   }, {
              //     title: 'Weather Information',
              //     colspan: 3,
              //     align: 'center'
              //   },
              //   {
              //     title: 'Date',
              //     colspan: 1,
              //     align: 'center'
              //   }
              // ],
              [
                {
                  field: 'ppm',
                  title: 'CO2 (ppm)',
                  sortable: true
                },
                {
                  field: 'dir',
                  title: 'Wind Direction',
                  sortable: true
                },
                {
                  field: 'velocity',
                  title: 'Velocity (m/s)',
                  sortable: true
                },
                {
                  field: 'temperature',
                  title: 'Temperature (C)',
                  sortable: true
                },
                {
                  field: 'presure',
                  title: 'Pressure (hPa)',
                  sortable: true
                },
                {
                  field: 'humidity',
                  title: 'Humidity (%)',
                  sortable: true
                },
                {
                  field: 'created_at',
                  title: 'Time',
                  sortable: true,
                  footerFormatter: 'formatDate'
                }
              ]
            ]
          })
        }
      })
    }
  },

  events: {
  },

  ready: function () {
    // this.getGeneralData()
  }
}
</script>

<style ></style>
