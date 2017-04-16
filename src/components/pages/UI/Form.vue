<template>
  <div>
    <div class="tile is-ancestor">
      <div class="tile is-parent">
        <article class="tile is-child box">
          <h1 class="title">Subscribe to our Newsletter</h1>
            <div class="control is-horizontal"  id="email">
              <div class="control is-grouped">
                <p class="control is-expanded">
                  <input class="input" type="email" v-model="email" placeholder="Email">
                </p>
                <div class="control">
                  <button class="button is-primary" @click="submitData">Submit</button>
                </div>
              </div>
          </div>
        </article>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import Message from '../../ui/Message'
import $ from 'jquery'
import config from '../../../config'
const { env } = config

const MessageComponent = Vue.extend(Message)

const openMessage = (propsData = {
  title: '',
  message: '',
  type: '',
  direction: '',
  duration: 1500,
  container: '.messages'
}) => {
  return new MessageComponent({
    el: document.createElement('div'),
    propsData
  })
}
export default {
  components: {
  },

  data () {
    return {
      email: '',
      url: ''
    }
  },

  computed: {
  },

  methods: {
    submitData: function () {
      var that = this
      $.ajax({
        url: this.url + 'subscribe',
        method: 'POST',
        dataType: 'json',
        data: {
          email: that.email
        },
        async: true,
        success: function (data) {
          if ('message' in data) {
            openMessage({
              title: 'Fail',
              message: data.message,
              type: 'danger'
            })
          } else {
            openMessage({
              title: 'You are successfully subscribed',
              message: 'Now you are ready to recieve our notifications.',
              type: 'success'
            })
          }
          that.email = ''
        }
      })

      $('#email').fadeOut(1000)
      setTimeout(function () {
        $('#email').fadeIn(1000)
      }, 1000)
    }
  },

  created () {
    this.url = env.API_URL
  }
}
</script>


<style scoped>
.button {
  margin: 5px 0 0;
}

.control .button {
  margin: inherit;
}
</style>
