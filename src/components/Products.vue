<template>
  <div class="products">
    <ProductCard
      v-for="product in products"
      :key="product.name"
      :name="product.name"
      :price="product.price"
      @click="$store.dispatch('addOrder', product)"
    />
  </div>
</template>

<style scoped>
.products {
  flex-grow: 1;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: flex-start;
  gap: 10px;
  padding: 10px;
}
</style>

<script>
import ProductCard from "@/components/ProductCard.vue";

export default {
  components: {
    ProductCard,
  },

  data() {
    return {
      products: [],
    };
  },

  async created() {
    const { data } = await this.$axios.get("http://localhost:3000/products");
    this.products = data;
  },
};
</script>