<template>
  <div class="home">
    <OrderForm :truck="truck"  />
  </div>
</template>

<script>
import OrderForm from "../components/OrderForm.vue";
// @ is an alias to /src
export default {
  name: 'HomeView',
  data() {
    return {
      truck: this.$route.query.truck
    }
  },
  components: {
    OrderForm
  }
}
</script>
