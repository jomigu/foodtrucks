<template>
  <div>
    <iframe :src="orderFormUrl + '/chinolatino/' + truck + '/' + email"></iframe>
  </div>
</template>

<script>
const BACKUP_URL = 'https://script.google.com/macros/s/AKfycbx7dSXvmv_lNIualRBwYMBRL1axzE_cFpVyc_QER0h2Q1n0BrkntSTd2_WoJBviY-0g/exec'
const orderFormUrl = process.env.VUE_APP_ORDER_FORM_URL || BACKUP_URL

export default {
  props: {
    truck: {
      type: String
    }
  },
  data() {
    return {
      email: localStorage.getItem('email'),
      orderFormUrl
    }
  }
}
</script>
