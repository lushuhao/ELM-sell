<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <!-- 路由外链 -->
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
  import header from 'components/header/header.vue';

  const ERR_OK = 0;  // 状态码

  export default {
    data() {
      return {
        seller: {}
      };
    },
    created() {
      this.$http.get('/api/seller').then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.seller = response.data;
        }
      });
    },
    components: {
      'v-header': header
    }
  }
  ;
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "common/scss/mixin.scss";

  #app {

    .tab {
      display: flex;
      width: 100%;
      height: 40px; // DPI是2，所以设计稿中的数据减半
      line-height: 40px;
      /*border: 1px solid rgba(7, 17, 21, 0.1);*/
      @include border-1px(rgba(7, 17, 21, 0.1));

      .tab-item {
        flex: 1; // 即flex: 1 1 0%
        text-align: center;

        & > a {
          display: block;
          font-size: 14px;
          color: rgb(77, 85, 93);
          line-height: 28px;

          &.active {
            color: rgb(240, 20, 20);
          }
        }
      }
    }
  }
</style>
