<template>
  <!--■ 商品项增加checkbox，表示商品是否选中
  ■ 新增加的商品，默认勾选，⽤户可以⼿动修改选择或者不选择商品
  ■ 勾选或者不勾选会影响购物⻋上的总价
  ■ 显示购物⻋总商品数据，以及选中商品数量
  ■ 基于ws7-vuex-done-->
  <div>
    <div class="top">
      <div class="shopping-cart">我的购物车</div>
    </div>
    <div class="title">
      <div class="total">总商品数： {{totalCommodity}}</div>
      <div class="total">选中商品数： {{selectionCommodity}}</div>
      <div class="total">总价： {{totalPrice}}</div>
    </div>
    <div class="list">
      <input class="select-all" type="checkbox" v-model="checked" @click="selectAll();"/>全选
      <cart-item
        v-for="(product, index) in cartProducts"
        :key="index"
        :product="product"
        @amount-change="handleAmountChange(product, arguments)"
      />
    </div>
    <add-product @add="handleAddProduct" />
  </div>
</template>

<script>
  import { mapState, mapGetters, mapActions } from 'vuex'
  import cartItem from './components/cartItem'
  import addProduct from './components/addProduct'

  const generateProduct = code => ({
    check: true,
    code,
    amount: 1,
    price: 100,
  })

  export default {
    name: 'cart',
    data:function() {
      return {
        checked: true
      }
    },
    components: {
      cartItem,
      addProduct,
    },
    computed: {
      ...mapState({
        cartProducts: state => state.cart.cartProducts,
      }),
      ...mapGetters({
        totalPrice: 'cartTotalPrice',
        totalCommodity: 'cartCommodity',
        selectionCommodity: 'selectionCommodity'
      }),
    },
    methods: {
      ...mapActions([
        'cartAddProduct',
        'cartChangeCount',
      ]),
      handleAmountChange(product, agrs) {
        const amount = agrs[0]
        this.cartChangeCount({
          code: product.code,
          amount,
        })
      },
      selectAll: function() {
        for (let i = 0;i < this.cartProducts.length;i++) {
          this.cartProducts[i].check = !this.checked;
        }
      },
      handleAddProduct: function(code) {
        this.cartAddProduct(generateProduct(code))
      },
    },
  }
</script>

<style src="./cart.css"></style>
