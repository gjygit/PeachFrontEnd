<template>
  <div>
    <a-page-header
      style="border: 1px solid rgb(235, 237, 240)"
      title="Title"
      sub-title="This is a subtitle"
      @back="() => null"
    />

  </div>
</template>

<script>
import axios from 'axios'
import store from '@/store/index'

export default {
  name: 'MerchantHomepage',
  data () {
    return {
      business: {
        id: '',
        roleName: 'business',
        username: '',
        lastname: '',
        firstname: '',
        idCard: '',
        phone: '',
        bankCardNumber: '',
        password: '',
        shopName: '',
        businessInformation: '',
        classification: ''
      }
    }
  },
  created () {
    this.business.username = store.state.username
    console.log(store.state.username)
    axios.get('/api/business?username=' + this.business.username).then(response => {
      const result = response.data
      console.log('返回值为')
      console.log(result)
      this.business.id = result.id
      this.business.shopName = result.shopName
      this.business.businessInformation = result.businessInformation
      this.business.phone = result.phone
      this.business.classification = result.classification
    }).catch(error => {
      console.log(error)
    })
  },
  methods: {
    getAllCommodity: function () {
      axios.get('/api/')
    }
  }
}
</script>

<style scoped>

</style>
