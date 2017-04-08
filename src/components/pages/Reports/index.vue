<template>
<div>
  <div class="tile is-ancestor">
    <div class="tile is-parent">
      <article class="tile is-child box">
      <div class="md-12">
          <table id="table"
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
           <!-- data-side-pagination="server" -->
        <!--    data-method="get" 
           data-url="" -->
            <!-- data-content-type="application/text-plain" -->
           <!-- data-url="http://api.fideclub.com/v1/spots" -->
        <!-- <table id="example" class="display" cellspacing="0" width="100%">
          <thead>
            <tr>
              <th>PPM</th>
              <th>Velocity</th>
              <th>Direction</th>
              <th>Direction</th>
            </tr>
          </thead>
          <tfoot>
          <tr>
            <th>PPM</th>
            <th>Velocity</th>
            <th>Direction</th>
            <th>Direction</th>
          </tr>
          </tfoot>
        </table> -->
      </article>
    </div>
  </div>

</template>

<script>
// import $ from 'jquery'
// import bootstrap from 'bootstrap'
// import bt from 'bootstrap-table'
import config from '../../../config'
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
    }
  },

  events: {
  },

  ready: function () {
    $.ajax({
      url: env.API_URL + 'datatable',
      method: 'GET',
      dataType: 'json',
      async: true,
      success: (data) => {
        console.log(data)
        let $table = $('#table')
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
    // console.log(window.a)
    // console.log(dt)
    // $(document).ready(() => {
    //   $('#example').DataTable({
    //     'ajax': 'http://localhost:81/v1/datatable'
    //   })
    // })
  }
}
</script>

<style ></style>
