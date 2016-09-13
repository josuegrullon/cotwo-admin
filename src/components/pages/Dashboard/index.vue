<template>
<div>
  <div class="tile is-ancestor">
    <div class="tile is-parent">
      <article class="tile is-child box">
          <iframe  class="content" src="http://cotwo-web.com"  
        style=" width: 600px;  height:400px;"  scrolling="no"></iframe>
      </article>
    </div>
    <div style="width:400px;" >
      <div class="tile is-parent">
        <article class="tile is-child box"> 
           <div class="block styles-box">
           <label>Sensor 1 | {{s1}} %</label>
            <progress-bar :type="setLabel(s1)" :value="s1" :max="100"></progress-bar>
          </div>
        </article>
      </div>
      <div class="tile is-parent">
        <article class="tile is-child box">
          <label>Sensor 2 | {{s2}} %</label>
           <div class="block styles-box">
            <progress-bar :type="setLabel(s2)" :value="s2"  :max="100"></progress-bar>
          </div>
        </article>
      </div>
      <div class="tile is-parent">
        <article class="tile is-child box">
          <label>Sensor 3 | {{s3}} %</label>
           <div class="block styles-box">
            <progress-bar :type="setLabel(s3)" :value="s3" :max="100"></progress-bar>
          </div>
        </article>
      </div>
      <div class="tile is-parent">
        <article class="tile is-child box">
          <label>Sensor 4 | {{s4}} %</label>
           <div class="block styles-box">
            <progress-bar :type="setLabel(s4)" :value="s4"  :max="100"></progress-bar>
          </div>
        </article>
      </div>
    </div>
    
  </div>
  <div class="tile is-ancestor">
    <div class="tile is-parent">
      <article class="tile is-child box">
        <h4 class="title"></h4>
      <chartist class="lines-bars" :type="'Bar'" :data="linesData" :options="linesOptions"></chartist>
      </article>
    </div>
    <!-- <div class="tile is-parent">
      <article class="tile is-child box">
       <h4 class="title">Wind Sensor 2</h4>
        <chart :type="'radar'" :data="waveData" :options="options"></chart>
      </article>
    </div>
    <div class="tile is-parent">
      <article class="tile is-child box">
        <h4 class="title">Wind Sensor 3</h4>
        <chart :type="'radar'" :data="waveData" :options="options"></chart>
      </article>
    </div>
    <div class="tile is-parent">
      <article class="tile is-child box">
        <h4 class="title">Wind Sensor 4</h4>
        <chart :type="'radar'" :data="waveData" :options="options"></chart>
      </article>
    </div> -->
  </div>
  
</div>
</template>

<script>
import Chart from '../../ui/Chart'
import ProgressBar from '../../ui/ProgressBar'
import Chartist from '../../ui/Chartist'
import $ from 'jquery'

export default {
  components: {
    Chart,
    ProgressBar,
    Chartist
  },

  data () {
    return {
      series: [
        [0, 0, 0, 0]
      ],
      labels: [''],
      linesOptions: {
        fullWidth: true,
        chartPadding: {
          right: 40
        }
      },
      ws1: '',
      s1: 0,
      s2: 0,
      s3: 0,
      s4: 0,
      // labels: ['Sleeping', 'Designing', 'Coding', 'Cycling'],
      options: {
        segmentShowStroke: false
      },
      backgroundColor: ['#4ae748']
    }
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
    }
  },

  created () {
    setInterval(() => {
      // https://vuejs.org/guide/list.html#Mutation-Methods
      // this.series.pop()
      // this.series.pop()
      // this.series.push(
      //   [Math.random() * 10, Math.random() * 20, Math.random() * 10, Math.random() * 20],
      //   [Math.random() * 10, Math.random() * 20, Math.random() * 10, Math.random() * 20])
      // // this.series.shift(this.series.pop())
    }, 1000)
    setInterval(() => {
      // https://vuejs.org/guide/list.html#Mutation-Methods
      // this.s2.sort(this.data.pop())
      // console.log('a')
      var that = this
      $.ajax({
        url: 'http://cotwo-api.com/v1/movements',
        method: 'GET',
        dataType: 'json',
        async: true,
        success: function (data) {
          that.labels.pop()
          that.labels.pop()
          that.labels.pop()
          that.labels.pop()
          that.labels.push('W1')
          that.labels.push('W2')
          that.labels.push('W3')
          that.labels.push('W4')

          that.series.pop()
          that.series.pop()
          that.series.push(
            [Math.random() * 10, Math.random() * 20, Math.random() * 10, Math.random() * 20],
            [Math.random() * 10, Math.random() * 20, Math.random() * 10, Math.random() * 20])
          if (data.active_sensors.length === 0) {
            that.s1 = 0
            that.s2 = 0
            that.s3 = 0
            that.s4 = 0
          }
          $.each(data.active_sensors, function (sensor, value) {
            if ('group' in value) {
              if (sensor === '0001') {
                that.s1 = value.group.avg
              } else if (sensor === '0002') {
                that.s2 = value.group.avg
              } else if (sensor === '0003') {
                that.s3 = value.group.avg
              } else if (sensor === '0004') {
                that.s4 = value.group.avg
              } else {
              }
            } else {
            }
          })
        }
      })
      // this.s1 = Math.random() * 80
      // this.s2 = Math.random() * 80
      // this.s3 = Math.random() * 80
      // this.s4 = Math.random() * 80
    }, 2000)
  }
}
</script>

<style lang="scss" scoped>
</style>
