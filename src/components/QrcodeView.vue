<template>
  <div>
    <router-link to="/generateQrCode"><b-button class="btn mr-4 mb-3">Generate Qr Code</b-button></router-link>
    <table id="customers">
      <tr>
        <th>Qr Code</th>
        <th>Content</th>
      </tr>
      <tr v-for="qrcode in qrCodes" :key="qrcode.id">
        <td><img :src="qrcode.svg_url"  :width="qrcode.size" /></td>
        <td>{{ qrcode.qr_content }},{{ qrcode.size }},{{ qrcode.bg_color }},{{ qrcode.fill_color}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      check: true,
      qrCodes: []
    }
  },
  mounted () {
    const url = process.env.VUE_APP_API_URL
    axios
      .get(url + 'qr-code', {
        headers: {
          'Access-Control-Allow-Origin': '*',
          'Content-type': 'application/json'
        }
      })
      .then((res) => {
        this.qrCodes = res.data.qrData
      })
      .catch((err) => {
        this.error = err
        console.log(err)
      })
  },
  methods: {
  }
}
</script>
<style>
.btn{
  float:right;
  background: #9693be !important;
}
#customers {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

#customers td, #customers th {
  border: 1px solid #ddd;
  padding: 8px;
}

#customers tr:nth-child(even){background-color: #f2f2f2;}

#customers tr:hover {background-color: #ddd;}

#customers th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: center;
  background-color: #9693be;
  color: white;
}
</style>
