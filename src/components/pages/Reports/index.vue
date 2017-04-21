<template>
<div>
  <div class="tile is-ancestor">
    <div class="tile is-parent">
      <article class="tile is-child box">
      <ul class="nav nav-tabs">
  <li class="active"><a data-toggle="tab" href="#home">General</a></li>
  <li><a data-toggle="tab" href="#module1" @click="loadModule('m1')">Module 1</a></li>
  <li><a data-toggle="tab" href="#module2"@click="loadModule('m2')">Module 2</a></li>
  <li><a data-toggle="tab" href="#module3"@click="loadModule('m3')">Module 3</a></li>
  <li><a data-toggle="tab" href="#module4"@click="loadModule('m4')">Module 4</a></li>
</ul>

<div class="tab-content">
  <div id="home" class="tab-pane fade in active">
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
          data-detail-formatter=detailFormatter
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
  <div id="module1" class="tab-pane fade">
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

    detailFormatter (index, row) {
      let html = []
      $.each(row, function (key, value) {
        html.push('<p><b>' + key + ':</b> ' + value + '</p>')
      })
      return html.join('')
    },

    getGeneralData () {
      $.ajax({
        url: env.API_URL + 'datatable',
        method: 'GET',
        dataType: 'json',
        async: true,
        success: (data) => {
          // console.log(data)
          let $table = $('#general')
          // console.log(jsondata)
          $table.bootstrapTable({
            data: data,
            height: '300px',
            columns: [
              [
                {
                  field: 'avg_data.ppm',
                  title: 'CO2 (Avg ppm)',
                  sortable: true
                },
                {
                  field: 'avg_data.dir',
                  title: 'Wind Direction (Avg)',
                  sortable: true
                },
                {
                  field: 'avg_data.velocity',
                  title: 'Velocity (Avg m/s)',
                  sortable: true
                },
                {
                  field: 'avg_data.temperature',
                  title: 'Temperature (Avg K)',
                  sortable: true
                },
                {
                  field: 'avg_data.presure',
                  title: 'Pressure (Avg hPa)',
                  sortable: true
                },
                {
                  field: 'avg_data.humidity',
                  title: 'Humidity (Avg %)',
                  sortable: true
                },
                {
                  field: 'f_date',
                  title: 'Time',
                  sortable: true,
                  footerFormatter: 'formatDate'
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

      console.log(identifier)
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
                  title: 'Temperature (K)',
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
    this.getGeneralData()
    window.detailFormatter = (index, row) => {
      let A = row.sensors['0001']
      let B = row.sensors['0002']
      let C = row.sensors['0003']
      let D = row.sensors['0004']
      return [
        '<table>',
        '<thead>',
        '<tr>',
        '<th>Module 0001</th>',
        '<th>Module 0002</th>',
        '<th>Module 0003</th>',
        '<th>Module 0004</th>',
        '<tr>',
        '</thead>',
        '<tr>',
        '<td>',
        '<span style="display: inline-block;"><b>Direction:</b></span> <span >' + A.dir + '</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Direction:</b></span> <span >' + B.dir + '</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Direction:</b></span> <span >' + C.dir + '</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Direction:</b></span> <span >' + D.dir + '</span> ',
        '</td>',
        '</tr>',
        '<tr>',
        '<td>',
        '<span style="display: inline-block;"><b>CO2:</b></span> <span >' + A.ppm + ' (ppm)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>CO2:</b></span> <span >' + B.ppm + ' (ppm)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>CO2:</b></span> <span >' + C.ppm + ' (ppm)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>CO2:</b></span> <span >' + D.ppm + ' (ppm)</span> ',
        '</td>',
        '</tr>',
        '<tr>',
        '<td>',
        '<span style="display: inline-block;"><b>Wind Velocity:</b></span> <span >' + A.velocity + ' (m/s)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Wind Velocity:</b></span> <span >' + B.velocity + ' (m/s)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Wind Velocity:</b></span> <span >' + C.velocity + ' (m/s)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Wind Velocity:</b></span> <span >' + D.velocity + ' (m/s)</span> ',
        '</td>',
        '</tr>',
        '<tr>',
        '<td>',
        '<span style="display: inline-block;"><b>Temperature:</b></span> <span >' + A.temperature + ' (C)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Temperature:</b></span> <span >' + B.temperature + ' (C)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Temperature:</b></span> <span >' + C.temperature + ' (C)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Temperature:</b></span> <span >' + D.temperature + ' (C)</span> ',
        '</td>',
        '</tr>',
        '<tr>',
        '<td>',
        '<span style="display: inline-block;"><b>Pressure:</b></span> <span >' + A.presure + ' (hPa)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Pressure:</b></span> <span >' + B.presure + ' (hPa)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Pressure:</b></span> <span >' + C.presure + ' (hPa)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Pressure:</b></span> <span >' + D.presure + ' (hPa)</span> ',
        '</td>',
        '</tr>',
        '<tr>',
        '<td>',
        '<span style="display: inline-block;"><b>Humidity:</b></span> <span >' + A.humidity + ' (%)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Humidity:</b></span> <span >' + B.humidity + ' (%)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Humidity:</b></span> <span >' + C.humidity + ' (%)</span> ',
        '</td>',
        '<td>',
        '<span style="display: inline-block;"><b>Humidity:</b></span> <span >' + D.humidity + ' (%)</span> ',
        '</td>',
        '</tr>',
        '</table>'
      ].join('')
    }
  }
}
</script>

<style ></style>
