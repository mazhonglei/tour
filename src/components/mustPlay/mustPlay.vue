<template>
  <div class="play">
    <div class="header">
      <span class="text">人气必玩</span>
      <router-link :to="{path:'/tour',query:{search:iscityname}}" class="link">
        {{iscityname}}全部景点
        <i class="icon iconfont iconyou3"></i>
      </router-link>
    </div>
    <div class="scroll">
      <ul class="center"  :style="{'width':centerWidth+'px'}">
        <li class="item"  v-for="(item, index) in goodList.productInfos?goodList.productInfos.slice(2,8):{}" :keys="index">
          <router-link :to="{path:'/details',query:{id:item.id}}" class="itemA">
            <img v-lazy="item.images[0]" class="img">
            <div class="today">今日订</div>
            <div class="money">
              <P class="name">{{item.productName}}</P>
              <span class="price">
                ￥{{item.minPrice}}起
              </span>
            </div>
          </router-link>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    goodList:{
      type:Object,
      default:{
        
      }
    },
    iscityname:{
      type:String,
      default:"常州"
    },
  },
  data(){
    return {

      playArr:[]
    }
  },
  methods:{
     swiperleft: function () {
      this.$router.push({'path':'/queuehistory'});
    },
    swiperright: function () {
      this.$router.push({'path':'/home'});
    },
  },
  computed:{
    // 动态渲染宽度
    centerWidth(){
      if ( null ==  this.goodList || null == this.goodList.productInfos  || this.goodList.productInfos.length >=6 ){
        return 6*146;
      }else if ( this.goodList.productInfos.length < 6) {
        return this.goodList.productInfos.length?this.goodList.productInfos.length*146:1
      }
    },
  },
  mounted(){

  },
}
</script>

<style  lang="stylus"  rel="stylesheet/stylus"  scoped>
  .play
    background-color: #fff
    .header
      position: relative
      height: 30px
      line-height: 30px
      padding: 0 10px
      font-size: 12px
      border-style: solid
      border-width: 0 0 1px
      -webkit-border-image: url("data:image/gif;base64,R0lGODlhBQAFAPABANra2v///yH5BAUHAAEALAAAAAAFAAUAAAIHhB9pGatnCgA7") 2 stretch;
      .link 
        float: right
        // margin-right: 10px
        font-size: 12px
        .icon
          font-size:10px
    .scroll
      width:100%
      overflow-y:hidden
      overflow-x: auto
      max-height:160px
      .center
        padding: 9px 0 5px 10px
        width:1022px
        max-height: 160px
        .item
          position:relative
          float:left
          width:136px 
          margin-right:10px 
          padding-bottom: 1px
          font-size: 0
        :last-child
            margin-right:0
          .itemA
            display:block 
            width:100% 
            height:100%
            .img
              width:100% 
              min-height:90.6px
              max-height:90.66px
            .today  
              position: absolute;
              top: 0
              left: 0
              background: #ff720e
              color: #fff
              font-size: 11px
              padding: 0 6px 0 4px
              border-bottom-right-radius: 7px
              height: 16px
              line-height: 16px
            .money 
              border-width: 0 1px 1px
              padding: 5px
              background: #fff
              .name 
                height: 16px
                line-height: 16px
                font-size: 12px
                margin-bottom: 5px
                color: #666
                text-overflow: ellipsis
                overflow: hidden
              .price
                display:block
                color: #d30775
                font-size: 15px
                overflow: hidden
                height: 22px
        
</style>
