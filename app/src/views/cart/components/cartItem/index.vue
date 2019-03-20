<template>
  <div class="product" type="checkbox">
    <h3 class="code">
      <input type="checkbox" v-model="product.check"/>
      <router-link class="link" :to="`/products/${product.code}`">
        商品编号: {{product.code}}
      </router-link>
    </h3>
    <div class="actions">
      <button @click="minusCount">-</button>
      <span>数量 {{product.amount}}</span>
      <button @click="plusCount">+</button>
    </div>
  </div>
</template>
<script>
  export default{
    props: {
      product: {
        type: Object,
      },
    },
    methods: {
      minusCount(){
        if (this.product.amount > 1) {
          this.$emit('amount-change', this.product.amount - 1)
        }
      },
      plusCount(){
        this.$emit('amount-change', this.product.amount + 1)
      }
    },
  }
</script>

<style scoped src="./styles.css" />
