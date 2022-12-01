<template>
  <div>
    <dashboard :check="check" />
    <div class="main">
    <h1>Qr Code Generate Form</h1>
    <form class="login">
    <label class="content">Content</label>
    <b-form-input type="text" v-model="content" placeholder="Content"></b-form-input><br>
      <span class="error" v-if="valid">{{this.contentError}}</span><br v-if="valid">
    <label class="content mt-2">Size</label>
    <b-form-input type="number" v-model="size" placeholder="Size"></b-form-input><br>
      <span class="error"  v-if="valid">{{this.sizeError}}</span><br v-if="valid">
    <label class="content mt-2">Bg Color</label>
    <b-form-input type="color" v-model="bgColor" placeholder="Bg Color"></b-form-input>
    <label class="content mt-2">Fill Color</label>
    <b-form-input type="color" v-model="fillColor" placeholder="Fill Color"></b-form-input>
        <b-button type="button" class="btn mt-2 mr-1" @click="sendChildFormData">Generate</b-button>
      </form>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import dashboard from '../views/DashboardView'
export default {
  name: 'generateQrCodeView',
  components: {
    dashboard
  },
  props: {
  },
  data () {
    return { check: '1', content: '', size: '', bgColor: '#000000', fillColor: '#ffffff', contentError: '', sizeError: '', valid: false }
  },
  computed: {},
  created () {
  },
  mounted () {
    this.sendChildFormData()
  },

  methods: {
    async sendChildFormData (e) {
      if (this.content === '' || this.size === '') {
        e.preventDefault()
      }
      const url = process.env.VUE_APP_API_URL
      const qrCodeData = {
        qr_content: this.content,
        size: this.size,
        bg_color: this.bgColor,
        fill_color: this.fillColor
      }
      axios
        .post(url + 'qr-code', qrCodeData, {
          headers: {
            'Access-Control-Allow-Origin': '*',
            'Content-type': 'application/json'
          }
        })
        .then((res) => {
          this.$router.push('/qrcode')
        })
        .catch((err) => {
          if (err.response.data.errors.qr_content) {
            this.contentError = err.response.data.errors.qr_content[0]
            this.valid = true
          } else {
            this.contentError = ''
            this.valid = false
          }
          if (err.response.data.errors.size) {
            this.sizeError = err.response.data.errors.size[0]
            this.valid = true
          } else {
            this.sizeError = ''
            this.valid = false
          }
        })
    }
    // checked () {
    //   const check = 1
    //   return check
    // }
  }
}
</script>
<style>
.content{
  float:left;
}
.main{
  margin:10px;
}
.error{
  float: left;
}
.btn {
  background: #9693be !important;
}
</style>
