<template>
  <router-link
    :to="{ name: 'product', params: { id: product.id } }"
    class="rounded w-56 relative"
  >
    <img
      :src="product.images.photos[0]"
      alt="`Image produit"
      class="h-72 object-cover rounded-lg"
    />
    <div class="absolute grid grid-cols-2 gap-4 mx-4 top-2">
      <div
        v-if="product.priceDiscount"
        class="text-white text-xs w-12 p-1 rounded bg-green-600"
      >
        %
      </div>
      <div
        v-if="product.stock == 0"
        class="text-white text-xs top-2 left-2 p-1 rounded bg-red-600"
      >
        out of stock
      </div>
    </div>
    <div class="text-left my-4 text-gray-500">
      {{ product.title }}
    </div>
    <ProductPrice :product="product" />
    <div class="text-xs text-gray-300">
      {{ product.stock > 0 ? "" : "Out of stock" }}
    </div>
  </router-link>
</template>
<script lang="ts">
import ProductPrice from "@/components/ProductPrice.vue";
export default {
  name: "ProducItem",
  props: ["product"],
  components: { ProductPrice },
  data() {
    return {
      cart: this.getCart(),
    };
  },
  created() {
    console.log(this.props);
  },
  methods: {
    getCart() {
      return JSON.parse(localStorage.getItem("cart"));
    },

    logCart() {
      console.log(this.getCart());
    },
  },
};
</script>
