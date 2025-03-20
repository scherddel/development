<script setup lang="ts">
import Medusa from "@medusajs/medusa-js"

const medusa = new Medusa({
  baseUrl: 'http://localhost:9000',
  publishableApiKey: 'pk_589678c9f0ee0252a1bef677929ed65361e42dc5329e7872264f8010fe36dd6a'
})

const { products } = await medusa.products.list({
  region_id: 'reg_01JPS9SZ93D0DMNGFZ153X3SQQ'
});
console.log(products);

const { cart } = await medusa.carts.create({
  region_id: 'reg_01JPS9SZ93D0DMNGFZ153X3SQQ'
});
console.log(cart);

const updatedCart = await medusa.carts.lineItems.create(cart.id, {
  variant_id: products[0].variants[0].id,
  quantity: 1
});
console.log(updatedCart);

const shippingOptions = medusa.shippingOptions.listCartOptions(updatedCart.cart.id)
console.log(shippingOptions);
</script>

<template>
  <div>
    Test
  </div>
</template>
