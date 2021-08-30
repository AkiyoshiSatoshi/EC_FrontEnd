<template>
  <div class="detail__contents">
    <p>teest</p>
    <div class="product__item" v-for="(product,index) in products" :key="index.id">
      <!-- <p>{{product.product_name}}</p> -->
      <div class="product__item-top">
        <img :src="product.img_url" alt="">
        <p>{{ product.id }}</p>
      </div>
    </div>
    <p>毎日吐きたくなるスニーカー</p>
  </div>
</template>


<script>
export default {
  'middleware': 'auth',
  props: {
    productId: String
  },
  data() {
    return {
      products: Array
    };
  },
  methods: {
    async GetProductData() {
      await this.$axios.get('http://127.0.0.1:8000/api/product/'+ this.$route.params.id)
      .then((res) => {
        this.products = res.data.data;
        console.log(res.data.data);
      })
    },
    getData() {
      this.$axios.get('http://127.0.0.1:8000/api/user')
      .then((res) => {
        console.log(res);
      })
    }
  },
  created() {
    // this.getData()
    this.GetProductData()
  }
}
</script>