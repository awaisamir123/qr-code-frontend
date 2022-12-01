<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="">
      <b-navbar-brand to="/dashboard" >Qr Code</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item to="/qrcode">QrCode</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">

          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em>User</em>
            </template>
<!--            <b-dropdown-item href="#">Profile</b-dropdown-item>-->
            <b-dropdown-item @click="signOut">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <h1 v-if="check != 1" >Qr Codes</h1>
    <QrcodeView v-if="check != 1" />
  </div>
</template>

<script>
// @ is an alias to /src
import QrcodeView from '@/components/QrcodeView.vue'
import axios from 'axios'
export default {
  name: 'DashboardView',
  components: {
    QrcodeView
  },
  props: {
    check: {
      type: String,
      default: ''
    }
  },
  data () {
    return { token: '' }
  },
  created () {
  },
  mounted () {
  },

  methods: {
    async signOut () {
      const userToken = localStorage.getItem('loginToken')
      const url = process.env.VUE_APP_API_URL
      // const tokenData = {
      //   token: 'Bearer ' + userToken
      // }
      axios
        .post(url + 'logout', {
          token: userToken
        },
        {
          headers: {
            Authorization: `Bearer ${userToken}`
          }
        })
        .then((response) => {
          localStorage.removeItem('loginToken')
          localStorage.removeItem('userInfo')
          this.$router.push('/')
        }, (error) => {
          console.log(error)
        })
    }
  }
}
</script>
<style>
nav {
  padding: 30px;
}
.navbar{
  background: #9693be;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

</style>
