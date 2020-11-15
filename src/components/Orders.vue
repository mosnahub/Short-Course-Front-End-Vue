<template>
  <div class="orders">
    <h3>Orders</h3>

    <div class="order-list">
      <div class="list" v-for="list in $store.state.orderList" :key="list.name">
        <p>{{ list.name }}</p>
        <p>{{ list.pricePerUnit }}</p>
        <p>x{{ list.quantity }}</p>
        <p>{{ list.quantity * list.pricePerUnit }}</p>
        <button class="btn" @click="$store.dispatch('removeOrder', list.id)">
          X
        </button>
      </div>
    </div>

    <div class="total">
      <p>Total</p>
      <p>{{ total }}</p>
    </div>

    <div class="button-group">
      <button
        class="btn"
        style="background-color: #5cb85c; color: white"
        @click="checkout"
      >
        check out
      </button>
    </div>
  </div>
</template>

<style scoped>
.orders {
  display: grid;
  grid-template-rows: 50px 1fr 50px 50px;
  gap: 10px;
  /* align-items: center; */
  margin-left: auto;
  min-width: 300px;
  padding: 10px;
  background-color: #dddddd;
  color: #000000;
}

.button-group {
  display: flex;
}

.button-group > button {
  flex-grow: 1;
}

.orders > h3 {
  margin: 0;
}

.total {
  display: flex;
  font-weight: bold;
  font-size: 20px;
}
.total > p {
  margin: 0;
}
.total > p:last-child {
  margin-left: auto;
}

.order-list {
  overflow-y: auto;
  overflow-x: hidden;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.list {
  display: grid;
  align-items: center;
  grid-template-columns: 1fr 50px 50px 1fr auto;
  gap: 10px;
}

.list > p {
  margin: 0;
}

.list > p:not(:first-child) {
  text-align: right;
}
</style>

<script>
export default {
  props: ["total"],

  methods: {
    checkout() {
      const history = this.$store.state.orderList.map((e) => {
        return {
          id: e.id,
          name: e.name,
          total: e.quantity * e.pricePerUnit,
        };
      });

      this.$axios.post("http://localhost:3000/history", history);
      this.$store.commit("clearOrderList");
    },
  },
};
</script>