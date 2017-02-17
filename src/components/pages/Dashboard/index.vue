<template>
<div>
  <div class="tile is-ancestor">
   <!-- <div> -->
    <div class="tile is-parent">
      <article class="tile is-child box">
          <iframe  class="content" src="http://138.197.7.114:82"  
        style=" width: 100%;  height:400px;"  scrolling="no"></iframe>
         <div class="tile is-parent">
      <article class="tile is-child box" style="width:110px; height:105px;">
        <p>
          <label>Direction 1: </label>
          <b>{{windDir_1}}</b>
        </p>
        <p>
            <label>Approximate Distance: </label>
            <b>{{  Math.round((w_a * 0.26) * 100) / 100}}m</b>
           </p>
      </article> 
      <article class="tile is-child box" style="width:110px; height:105px;">
      <label>Direction 2: </label>
          <b>{{windDir_2}}</b>
          <p>
             <label>Approximate Distance: </label>
            <b>{{  Math.round((w_b * 0.26) * 100) / 100}}m</b>
           </p>
      </article>
    </div>
    <div class="tile is-parent">
      <article class="tile is-child box" style="width:110px; height:105px;">
      <label>Direction 3: </label>
          <b>{{windDir_3}}</b>
          <p>
             <label>Approximate Distance: </label>
            <b>{{  Math.round((w_c * 0.26) * 100) / 100}}m</b>
           </p>
      </article> 
      <article class="tile is-child box" style="width:110px; height:105px;">
        <div class="block styles-box">
        <label>Direction 4: </label>
           <label><b>{{windDir_4}}</b> </label>
           <p>
             <label>Approximate Distance: </label>
            <b>{{  Math.round((w_d * 0.26) * 100) / 100}}m</b>
           </p>
        </div>
      </article>
    </div>
      </article>
    <!-- </div> -->
  </div>
    <div style="width:400px;" >
      <div class="tile is-parent">
        <article class="tile is-child box"> 
          <h4>Sensor 1:</h4>
           <div class="block styles-box">
           <label>{{ Math.round(s1 * 100) / 100}}% <i>Avg</i> </label>
            <progress-bar :type="setLabel(s1)" :value="s1" :max="100"></progress-bar>
            <label> {{ppm_1}} ppm</label>
            <progress-bar :type="setPpm(ppm_1)" :value="parseInt(ppm_1)" :max="10000"></progress-bar>
          </div>
        </article>
      </div>
      <div class="tile is-parent">
       <article class="tile is-child box"> 
          <h4>Sensor 2:</h4>
           <div class="block styles-box">
           <label>{{Math.round(s2 * 100) / 100}}% <i>Avg</i> </label>
            <progress-bar :type="setLabel(s2)" :value="s2" :max="100"></progress-bar>
            <label> {{ppm_2}} ppm</label>
            <progress-bar :type="setPpm(ppm_2)" :value="parseInt(ppm_2)" :max="10000"></progress-bar>
          </div>
        </article>
      </div>
      <div class="tile is-parent">
        <article class="tile is-child box"> 
          <h4>Sensor 3:</h4>
           <div class="block styles-box">
           <label>{{Math.round(s3 * 100) / 100}}% <i>Avg</i> </label>
            <progress-bar :type="setLabel(s3)" :value="s3" :max="100"></progress-bar>
            <label> {{ppm_3}} ppm</label>
            <progress-bar :type="setPpm(ppm_3)" :value="parseInt(ppm_3)" :max="10000"></progress-bar>
          </div>
        </article>
      </div>
      <div class="tile is-parent">
        <article class="tile is-child box"> 
          <h4>Sensor 4:</h4>
           <div class="block styles-box">
           <label>{{ Math.round(s4 * 100) / 100  }}% <i>Avg</i> </label>
            <progress-bar :type="setLabel(s4)" :value="s4" :max="100"></progress-bar>
            <label> {{ppm_4}} ppm</label>
            <progress-bar :type="setPpm(ppm_4)" :value="parseInt(ppm_4)" :max="10000"></progress-bar>
          </div>
        </article>
      </div>
    </div>
    
  </div>

<div>
    <div class="tile is-ancestor">
      <div class="tile is-parent">
        <article class="tile is-child box">
          <h4 class="title">Velocity Sensors</h4>
          <div class="block">
            <chartist v-ref:chartist class="lines-bars" :type="'Line'" :data="linesData" :options="linesOptions"></chartist>
          </div>
          <div class="block" style="display: flex;">
            <div class='square-box-a marg'>
              <div class='square-content'><div><span> W Sensor 1 {{w_a}} km/h</span></div></div>
            </div>
            <div class='square-box-b marg'>
              <div class='square-content'><div><span> W Sensor 2: {{w_b}} km/h</span></div></div>
            </div>
            <div class='square-box-c marg'>
              <div class='square-content'><div><span> W Sensor 3: {{w_c}} km/h</span></div></div>
            </div>
            <div class='square-box-d marg'>
              <div class='square-content'><div><span> W Sensor 4: {{w_d}} km/h</span></div></div>
            </div>
          </div>
        </article>
      </div>
    </div>
</div>
</template>

<script>
import Vue from 'vue'
import ProgressBar from '../../ui/ProgressBar'
import Chartist from '../../ui/Chartist'
import $ from 'jquery'
import moment from 'moment'

Vue.config.debug = true

export default {
  name: 'A',
  components: {
    ProgressBar,
    Chartist
  },

  data () {
    return {
      current: {},
      w_a: '',
      w_b: '',
      w_c: '',
      w_d: '',
      ppm_1: 0,
      ppm_2: 0,
      ppm_3: 0,
      ppm_4: 0,
      windDir_1: '--',
      windDir_2: '--',
      windDir_3: '--',
      windDir_4: '--',
      colors: {
        sensor_a: 'red',
        sensor_b: 'blue',
        sensor_c: 'orange',
        sensor_d: 'black'
      },
      series: [],
      props: {},
      labels: ['0', '1', '2', '3', '4'],
      linesOptions: {
        fullWidth: true,
        chartPadding: {
          right: 40
        }
      },
      s1: 0,
      s2: 0,
      s3: 0,
      s4: 0,
      options: {
        segmentShowStroke: false
      },
      backgroundColor: ['#4ae748']
    }
  },
  created: function () {

  },
  watch: {
    // 's4': function (val) {
    //   this.s4 = (
    // }
  },
  computed: {
    linesData () {
      return {
        labels: this.labels,
        series: this.series,
        backgroundColor: this.backgroundColor[0]
      }
    }
  },
  methods: {
    setLabel: function (val) {
      if (val >= 0 && val <= 25) {
        return 'success'
      } else if (val > 25 && val <= 50) {
        return 'primary'
      } else if (val > 50 && val <= 75) {
        return 'warning'
      } else {
        return 'danger'
      }
    },
    setPpm: function (val) {
      return 'primary'
    },
    getDirection (dir) {
      switch (dir) {
        case 'n':
          return 'North'
        case 's':
          return 'South'
        case 'e':
          return 'East'
        case 'o':
          return 'Weast'
        case 'so':
          return 'South Weast'
        case 'se':
          return 'South East'
        case 'no':
          return 'North Weast'
        case 'ne':
          return 'North East'
        default:
          return '--'
      }
    },
    setZero: function (data) {
      if (data) {
        var info = data.sensors_current_union
        var series = data.sensors_current_info

        let interval = 10
        let sensors = info[4]
        let diffA = moment().diff(moment(sensors[0].updated), 'seconds')
        let diffB = moment().diff(moment(sensors[1].updated), 'seconds')
        let diffC = moment().diff(moment(sensors[2].updated), 'seconds')
        let diffD = moment().diff(moment(sensors[3].updated), 'seconds')
        // this.ppm_1 = 0
        // this.ppm_2 = 0
        // this.ppm_3 = 0
        // this.ppm_4 = 0
        $.each(data.active_sensors, (sensor, value) => {
          if ('group' in value) {
            if (sensor === '0001') {
              this.windDir_1 = this.getDirection(Object.keys(value.group.w_dir)[0])
            } else if (sensor === '0002') {
              this.windDir_2 = this.getDirection(Object.keys(value.group.w_dir)[0])
            } else if (sensor === '0003') {
              this.windDir_3 = this.getDirection(Object.keys(value.group.w_dir)[0])
            } else if (sensor === '0004') {
              this.windDir_4 = this.getDirection(Object.keys(value.group.w_dir)[0])
            }
          }
        })

        this.ppm_1 = sensors[0].ppm === 0 ? this.ppm_1 : sensors[0].ppm
        this.ppm_2 = sensors[1].ppm === 0 ? this.ppm_2 : sensors[1].ppm
        this.ppm_3 = sensors[2].ppm === 0 ? this.ppm_3 : sensors[2].ppm
        this.ppm_4 = sensors[3].ppm === 0 ? this.ppm_4 : sensors[3].ppm

        if (diffA > interval) {
          this.w_a = this.ppm_1 = 0
          this.windDir_1 = '--'
          series[0] = [0, 0, 0, 0, 0]
          this.s1 = 0
        }
        if (diffB > interval) {
          this.w_b = this.ppm_2 = 0
          this.windDir_2 = '--'
          series[1] = [0, 0, 0, 0, 0]
        }

        if (diffC > interval) {
          this.w_c = this.ppm_3 = 0
          this.windDir_3 = '--'
          series[2] = [0, 0, 0, 0, 0]
        }

        if (diffD > interval) {
          this.w_d = this.ppm_4 = 0
          this.windDir_4 = '--'
          series[3] = [0, 0, 0, 0, 0]
          this.s4 = 0
        }

        return series
      }
    }
  },
  ready: function () {
    setInterval(() => {
      $.ajax({
        url: 'http://138.197.7.114:81/v1/movements',
        method: 'GET',
        dataType: 'json',
        async: true,
        success: (data) => {
          this.current = data.sensors_current_info
          this.w_a = data.sensors_current_info[0][3]
          this.w_b = data.sensors_current_info[1][3]
          this.w_c = data.sensors_current_info[2][3]
          this.w_d = data.sensors_current_info[3][3]

          let series = this.setZero(data)

          this.$refs.chartist.$set('chart.data.series', series)
          this.$refs.chartist.chart.update()
          $('.ct-series-a *').css('stroke', this.colors.sensor_a)
          $('.ct-series-b *').css('stroke', this.colors.sensor_b)
          $('.ct-series-c *').css('stroke', this.colors.sensor_c)
          $('.ct-series-d *').css('stroke', this.colors.sensor_d)

          if (data.active_sensors.length === 0) {
            this.s1 = 0
            this.s2 = 0
            this.s3 = 0
            this.s4 = 0
          }
          $.each(data.active_sensors, (sensor, value) => {
            if ('group' in value) {
              if (sensor === '0001') {
                this.s1 = (parseFloat(value.group.avg) / 10000) * 100
              } else if (sensor === '0002') {
                this.s2 = (parseFloat(value.group.avg) / 10000) * 100
              } else if (sensor === '0003') {
                this.s3 = (parseFloat(value.group.avg) / 10000) * 100
              } else if (sensor === '0004') {
                this.s4 = (parseFloat(value.group.avg) / 10000) * 100
              } else {
              }
            } else {
            }
          })
        }
      })
    }, 2000)
  }
}
</script>

<style >
.marg {
  margin-left:  30px;
}

.square-box-a{
    position: relative;
    width: 30%;
    overflow: hidden;
    background: red;
}
.square-box-a:before{
    content: "";
    display: block;
    padding-top: 10%;
}

.square-box-b{
    position: relative;
    width: 30%;
    overflow: hidden;
    background: blue;
}
.square-box-b:before{
    content: "";
    display: block;
    padding-top: 10%;
}

.square-box-c{
    position: relative;
    width: 30%;
    overflow: hidden;
    background: orange;
}
.square-box-c:before{
    content: "";
    display: block;
    padding-top: 10%;
}
.square-box-d{
    position: relative;
    width: 30%;
    overflow: hidden;
    background:  black;
}
.square-box-d:before{
    content: "";
    display: block;
    padding-top: 10%;
}
.square-content{
    position:  absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    color: white;
}
.square-content div {
   display: table;
   width: 100%;
   height: 50%;
}
.square-content span {
    display: table-cell;
    text-align: center;
    vertical-align: middle;
    color: white
}
</style>
