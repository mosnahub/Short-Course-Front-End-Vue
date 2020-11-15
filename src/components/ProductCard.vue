<template>
  <div class="product-card" @click="$emit('click')">
    <p>{{ name }}</p>
    <p>{{ price }}</p>
  </div>
</template>

<style scoped>
.product-card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  width: 200px;
  height: 200px;
  background-color: rgb(255, 96, 96);
  box-shadow: 0 0 4px gray;
  cursor: pointer;
  border-radius: 15px;
}

.product-card > p {
  margin: 0;
}
</style>    

<script>
export default {
  props: ["name", "price"],
};
</script>