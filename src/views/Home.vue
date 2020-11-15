<template>
  <div class="layout">
    <div class="main">
      <Products />
      <Orders :total="getTotal" />
    </div>

    <v-
  </div>
</template>

<style scoped>
.main {
  display: flex;
  flex-grow: 1;
  max-height: 100vh;
}
</style>

<script>
import Products from "@/components/Products.vue";
import Orders from "@/components/Orders.vue";

export default {
  components: {
    Orders,
    Products,
  },
  name: "Home",
  data() {
    return {
      orderList: [
        // {
        //   name: "Snake",
        //   quantity: 1,
        //   pricePerUnit: 220,
        // },
      ],
    };
  },

  computed: {
    getTotal() {
      const total = this.$store.state.orderList.reduce(
        (prev, current) => prev + current.quantity * current.pricePerUnit,
        0
      );

      return new Intl.NumberFormat("th-TH", {
        style: "currency",
        currency: "THB",
      }).format(total);
    },
  },

  mounted() {
    console.log(this.$axios);
  },
};
</script>