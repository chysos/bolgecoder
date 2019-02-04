<template>
    <div >
        <div class="search-bar">
              <van-row class="test">
          <van-col span="3">
              <img :src="locationIcon" width="80%" class="location-icon">
          </van-col>
          <van-col span="16"> 
              <input type="text" class="search-input">
          </van-col>
          <van-col span="5">
              <van-button size="mini">搜索</van-button>
          </van-col>
      </van-row>
        </div>
        <!-- swiper area -->
        <div class="swiper-area">
            <van-swipe :autoplay="1000">
                <van-swipe-item v-for="(banner,index) in bannerPicArry " :key="index">
                    <img :src="banner.image" class="imager-banner" >
                </van-swipe-item>
            </van-swipe>
        </div>
     <!--type bar-->
     <div class="type-bar">
         <div v-for="(cate,index) in category" :key="index" >
             <img v-lazy="cate.image" width="90%">
             <span>{{cate.mallCategoryName}}</span>
         </div>
     </div>
    <!-- addbanner area -->

    <div>
        <img v-lazy='adbanner' width="100%" alt="">
    </div>
    <!-- Recommend goods area -->
    <div class="recommend-are">
        <div class="recommend-tittle">
            商品推荐
        </div>
        <div class="recommen-body">
            <swiper  :options="swipeOption">
                <swiper-slide v-for="(item,index) in recommendGoods" :key="index">
                    <div class="recommend-item">
                        <img :src="item.image" width="80%">
                        <div>{{item.goodsName}}</div>
                        <div>${{item.price}}(${{item.mallPrice}})</div>
                    </div>
                </swiper-slide>
            </swiper>
        </div>
    </div>
     
     
     <floor-component :floorData="floor1"></floor-component>
    </div>
</template>

<script>
import axios from 'axios'
import 'swiper/dist/css/swiper.css'
import {swiper,swiperSlide} from 'vue-awesome-swiper'
// import swiperDefsult from '../swiper/swiperDefsult'
// import swiperDefsult2 from '../swiper/swiperDefsult2'
import floorComponent from '../component/floorComponent'
    export default {
        data() {
            return {
                swipeOption:{
                    slidesPerView:3,

                },
                msg: 'ShoppingMall',
                locationIcon:require('../../assets/images/location.png'),
                bannerPicArry:[],
                category:[],
                adbanner:'',
                recommendGoods:[],
                floor1:[],
                floor1_0:{},
                floor1_1:{},
                floor1_2:{},
                floor1_3:{},

            }
        },
        components:{
        swiper,swiperSlide,floorComponent
        },
        created(){
            axios({
                url:' https://www.easy-mock.com/mock/5c52d8ceef451d538b8a56bf/SmileVue/index',
                method:'get',
            })
            .then(response=>{
                console.log(response)
                if(response.status==200){
                    this.category=response.data.data.category;
                    this.adbanner =response.data.data.advertesPicture.PICTURE_ADDRESS
                    this.bannerPicArry =response.data.data.slides
                    this.recommendGoods =response.data.data.recommend
                    this.floor1 =response.data.data.floor1
                   

                }
            }).catch(error=>{
                console.log(error)
            })
        }
    }
</script>

<style scoped>
  .search-bar{
      height: 2.2rem;
      background-color: #e5017d;
      line-height: 2.2rem;
      overflow: hidden;
      
  }.search-input{
      width: 100%;
      height: 1.3rem;
      border-top: 0px;
      border-left: 0px;
      border-right: 0px;
      border-bottom: 1px solid #fff !important;
      background-color: #e5017d;
      color: #fff;
  }.location-icon{
   padding-top: .2rem;
   padding-left: .3rem;
  }
  .swiper-area{
      clear: both;
      max-height: 10rem;
      overflow: hidden;
  }
  .imager-banner{
width: 100%;
height: 10rem;

  }
 .type-bar{
      background-color: #fff;
      margin:0 .3rem .3rem .3rem;
      border-radius: .3rem;
      font-size:14px;
      display: flex;
      flex-direction:row;
      flex-wrap:nowrap;
  }
  .type-bar div{
      width: 20%;
      padding: .3rem;
      font-size: 12px;
      text-align: center;
  }
  .recommend-are{
      background-color: #fff;
      margin-top: .3rem;

  }.recommend-tittle{
      border-bottom: 1px solid #eee;
      font-size: 14px;
      padding:.2rem;
      color: #e5017d;
  }
  .recommend-body{
      border-bottom: 1px solid #eee;


  }
  .recommend-item{
      width: 99%;
      border-right: 1px solid #eee;
      font-size: 12px;
      text-align: center;

  }
  .floor-anomaly{
      display: flex;
      flex-direction: row;
      background-color: #fff;
      border-bottom: 1px solid #dddddd;
  }
  .floor-anomaly div{
        width: 10rem;
        box-sizing: border-box;
        -webkit-box-sizing: border-box;
  }
  .floor-one{
      border-bottom: 1px solid #ddd;
  }
   .floor-two{
      border-bottom: 1px solid #ddd;
  }
  .floor-rule{
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
      background-color: #fff;
  }
  .floor-rule div{
      -webkit-box-sizing: border-box;
      box-sizing: border-box;
      width: 10rem;
      border-bottom: 1px solid #ddd;
  }
</style>