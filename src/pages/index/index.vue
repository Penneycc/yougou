<template>
  <div>
    <!-- 搜索框 -->
    <search-bar></search-bar>
    <!-- 轮播图 -->
    <swiper indicator-dots="true" autoplay="true">
      <swiper-item v-for="item in swiper" :key="item.goods_id">
        <img :src="item.image_src" alt />
      </swiper-item>
    </swiper>
    <!-- 菜单 -->
    <div class="menu">
      <img v-for="(item, index) in cate" :key="index" :src="item.image_src" alt="">
    </div>
    <!-- 商品 -->
    <div class="floor" v-for="(item, index) in floor" :key="index">
      <div class="title">
        <img :src="item.floor_title.image_src" alt="">
      </div>
      <div class="content">
        <div class="left">
          <img :src="item.product_list[0].image_src" alt="">
        </div>
        <div class="right">
          <img v-if="i>0" v-for="(img, i) in item.product_list" :key="i" :src="img.image_src" alt="">
        </div>
      </div>
    </div>
    <!-- 回到顶部 -->
    <div class="toTop" v-if="isShow" @click="toTop">
      ︿
      <div>顶部</div>
    </div>
  </div>
</template>

<script>
import searchBar from "../../components/searchBar";
export default {
  data() {
    return {
      swiper: [],
      cate: [],
      floor: [],
      isShow: false
    };
  },

  components: {
    "search-bar": searchBar
  },

  methods: {
    toTop() {
      wx.pageScrollTo({
        scrollTop: 0
      })
    },
    initIndex() {
      this.swiperData()
      this.cateData()
      this.floorData()
    },
    swiperData() {
      wx.request({
        url: "https://www.zhengzhicheng.cn/api/public/v1/home/swiperdata",
        success: res => {
          // console.log(res)
          if (res.data.meta.status === 200) {
            this.swiper = res.data.message;
            // console.log(this.swiper);
          }
        }
      });
    },
    cateData() {
      wx.request({
        url: "https://www.zhengzhicheng.cn/api/public/v1/home/catitems",
        success: res => {
          // console.log(res)
          if (res.data.meta.status === 200) {
            this.cate = res.data.message
            console.log(this.cate)
          }
        }
      })
    },
    floorData() {
      wx.request({
        url: "https://www.zhengzhicheng.cn/api/public/v1/home/floordata",
        success: res => {
          // console.log(res)
          if (res.data.meta.status === 200) {
            this.floor = res.data.message
            console.log(this.floor)
          }
        }
      })
    }
  },
  created() {
    this.initIndex()
  },
  onPageScroll(e) {
      this.isShow = e.scrollTop > 100
  },
  onPullDownRefresh() {
    this.initIndex()
  }
}
</script>

<style scoped lang="less">
@import "./main.less";
</style>
