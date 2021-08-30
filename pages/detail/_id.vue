<template>
  <div>
    <p>{{$route.name}}</p>
    <p>{{ $route.params.id}}</p>
    <div class="product__item" v-for="(product,index) in products" :key="index.id">
      <div class="product__item-top">
        <img :src="product.img_url" alt="">
      </div>
    </div>
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
      products: []
    };
  },
  methods: {
    async GetProductData() {
      await this.$axios.get('http://127.0.0.1:8000/api/product/'+this.$route.params.id)
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
    this.getData()
    // this.GetProductData()
  }
}
</script>