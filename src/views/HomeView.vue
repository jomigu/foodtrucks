<template>
  <div class="home">
    <OrderForm />
  </div>
</template>

<script>
import OrderForm from "../components/OrderForm.vue";
// @ is an alias to /src
export default {
  name: 'HomeView',
  components: {
    OrderForm
  }
}
</script>
