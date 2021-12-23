#### 1.购物车算钱

wxml

```
<view class="cart-box">
        <view class="item" wx:for="{{list}}" wx:key="list">
                <icon type="{{item.select}}" size="26" data-index="{{index}}" data-select="{{item.select}}" bindtap="change"/>
                <image src="{{item.url}}" class="goods-img" mode="widthFix"></image>
                <view class="goods-info">
                      <view class="row">
                           <view class="goods-name">{{item.name}}</view>
                           <text class="goods-price">￥{{item.price}}</text>
                      </view>
                      <view class="goods-type">
                              {{item.style}}
                      </view>
                      <view class="num-box">
                            <view class="btn-groups">
                                    <button class="goods-btn btn-minus" data-index="{{index}}" data-num="{{item.num}}" bindtap="subtraction">—</button>
                                      <view class="num">{{item.num}}</view>
                                      <button class="goods-btn btn-add" data-index="{{index}}" data-num="{{item.num}}" bindtap="addtion">+</button>
                            </view>
                      </view>
                </view>
        </view>
</view>
<view class="cart-fixbar">
       <view class="allSelect">
            <icon type="{{allSelect}}" size="26" data-select="{{allSelect}}" bindtap="allSelect"/>
            <view class="allSelect-text">全选</view>
       </view>
       <view class="count">
           <text>合计：￥</text>{{count}}
       </view>
       <view class="order">
          去结算<text class="allnum">({{num}})</text>
       </view>
</view>



```



css

```
page{
  background: #000;
}
.cart-box .item{
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 20rpx;
  background: #222;
  border-bottom: 1px solid #555;
}
.cart-box .item .goods-info{
  margin-left: 20rpx;
}
.cart-box .goods-img{
  width: 160rpx;
   margin-left: 20rpx;
}
.cart-box .row{
  color: #fff;
  display: flex;
  flex-direction: row;
  width: 430rpx;
  justify-content: space-between;
  margin-bottom: 20rpx;
}
.cart-box .goods-name{
  font-size: 32rpx;
  width: calc(100% - 100rpx);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.cart-box .goods-price{
  font-size: 32rpx;
}
.cart-box .goods-type{
  color: #999;
  font-size: 24rpx;
  margin-bottom: 20rpx;
}
.cart-box .num-box{
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
}
.cart-box .goods-btn{
  width: 60rpx;
  height: 60rpx;
  padding: 0;
  line-height: 60rpx;
  font-weight: bold;
  color: #999;
  margin: 0;
  background: #333;
}
.cart-box .num{
  color: #999;
  width: 60rpx;
  text-align: center;
  line-height: 60rpx;
  font-size: 24rpx;
}
.cart-box .btn-add{
  font-size: 50rpx;
}
.cart-box .btn-minus{
  font-size: 28rpx;
}
.cart-box .btn-groups{
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    border: 1px solid #222;
    border-radius: 10rpx;
}
.cart-fixbar{
  position: fixed;
  bottom: 0;
  background: #333;
  height: 100rpx;
  width: 100%;
  padding: 0 20rpx;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.cart-fixbar .allSelect{
  display: flex;
  flex-direction: row;
  height: 100rpx;
  align-items: center;
  color: #fff;
  font-size: 32rpx;
}
.cart-fixbar .allSelect-text{
  margin-left: 20rpx;
}
.cart-fixbar .count{
  margin-left: 80rpx;
  color: #fff;
  font-size: 36rpx;
}
.cart-fixbar .order{
  color:#fff;
  height: 100rpx;
  background: #222;
  line-height: 100rpx;
  position: absolute;
  right: 0;
  padding: 0 40rpx;
  font-size: 32rpx;
}
.cart-fixbar .allnum{
  font-size: 24rpx;
}
```

js

```
Page({
  data: {
    list:[{
      code:"0001",
      name:"无人机",
      url:"http://i1.mifile.cn/a1/pms_1487824962.01314237!220x220.jpg",
      style:"低配版",
      price:"4999",
      select:"circle",
      num:"1"
    },
    {
      code: "0002",
      name: "智能手环",
      url: "http://i1.mifile.cn/a1/pms_1467962689.97551741!220x220.jpg",
      style: "2代",
      price: "149",
      select: "circle",
      num: "1"
    },{
      code: "0003",
      name: "指环支架",
      url: "http://i2.mifile.cn/a1/pms_1482221011.26064844.jpg",
      style: "金色",
      price: "19",
      select: "circle",
      num: "1"
    }],
    allSelect:"circle",
    num:0,
    count:0
  },
  //改变选框状态
  change:function(e){
    var that=this
    //得到下标
    var index = e.currentTarget.dataset.index
    //得到选中状态
    var select = e.currentTarget.dataset.select
    
    if(select == "circle"){
       var stype="success"
    }else{
       var stype="circle"
    }
    
    //把新的值给新的数组
   var newList= that.data.list
   newList[index].select=stype
    //把新的数组传给前台
    that.setData({
      list:newList
    })
    //调用计算数目方法
    that.countNum()
    //计算金额
    that.count()
  },
  //加法
  addtion:function(e){
    var that=this
    //得到下标
    var index = e.currentTarget.dataset.index
    //得到点击的值
    var num = e.currentTarget.dataset.num
    //默认99件最多
    if(num<100){
      num++
    }
    //把新的值给新的数组
    var newList = that.data.list
    newList[index].num =num
   
    //把新的数组传给前台
    that.setData({
      list: newList
    })
    //调用计算数目方法
    that.countNum()
    //计算金额
    that.count()
  },
  //减法
subtraction:function(e){
  var that = this
  //得到下标
  var index = e.currentTarget.dataset.index
  //得到点击的值
  var num = e.currentTarget.dataset.num
  //把新的值给新的数组
  var newList = that.data.list
  //当1件时，点击移除
  if (num == 1) {
      newList.splice(index,1)
  }else{
    num--
    newList[index].num = num
  }
  
  //把新的数组传给前台
  that.setData({
    list: newList
  })
  //调用计算数目方法
  that.countNum()
  //计算金额
  that.count()
},
//全选
allSelect:function(e){
  var that=this
  //先判断现在选中没
  var allSelect = e.currentTarget.dataset.select
  var newList = that.data.list
  if(allSelect == "circle"){
    //先把数组遍历一遍，然后改掉select值
    for (var i = 0; i < newList.length; i++) {
      newList[i].select = "success"
    }
    var select="success"
  }else{
    for (var i = 0; i < newList.length; i++) {
      newList[i].select = "circle"
    }
    var select = "circle"
  }
  that.setData({
    list:newList,
    allSelect:select
  })
  //调用计算数目方法
  that.countNum()
  //计算金额
  that.count()
},
//计算数量
countNum:function(){
  var that=this
  //遍历数组，把既选中的num加起来
  var newList = that.data.list
  var allNum=0
  for (var i = 0; i < newList.length; i++) {
        if(newList[i].select=="success"){
          allNum += parseInt(newList[i].num) 
        }
  }
  parseInt
  console.log(allNum)
  that.setData({
    num:allNum
  })
},
//计算金额方法
count:function(){
  var that=this 
  //思路和上面一致
  //选中的订单，数量*价格加起来
  var newList = that.data.list
  var newCount=0
  for(var i=0;i<newList.length;i++){
    if(newList[i].select == "success"){
      newCount += newList[i].num * newList[i].price
    }
  }
  that.setData({
    count:newCount
  })
}
})
```

#### 2.列表点赞



```
<block wx:for="{{wishList}}" wx:key="{{index}}">
  <view class="item" data-index='{{item.id}}'>
    <view class='wish_list_box_collection' wx:if="{{item.collected==1}}">
      <!-- 点赞过 -->
      <image catchtap='onCollectionTap' src="../../images/icon/wardrobe.png" data-index='{{index}}'></image>
      <text>{{item.dzzs}}</text>
    </view>
    <view class='wish_list_box_collection' wx:else>
      <!-- 未点赞 -->
      <image src='../../images/icon/wx_app_like.png' catchtap='onCollectionTap' data-index='{{index}}'></image>
      <text>{{item.dzzs}}</text>
    </view>
  </view>
</block>

```

```
.item {
  padding: 20rpx;
  border: 1rpx solid red;
}
 
.wish_list_box_collection image {
  width: 40rpx;
  height: 40rpx;
  overflow: hidden;
}

```

```
data: {
    wishList: [
      {dzzs: '22', collected: 1, id: 1},
      {dzzs: '33', collected: 0, id: 2},
      {dzzs: '44', collected: 1, id: 3},
      {dzzs: '555', collected: 1, id: 4},
      {dzzs: '666', collected: 0, id: 5},
      {dzzs: '777', collected: 0, id: 6}
    ],
  },


// 更改点赞状态
  onCollectionTap: function(event) {
    // 获取当前点击下标
    var index = event.currentTarget.dataset.index;
    // data中获取列表
    var message = this.data.wishList;
    for (let i in message) { //遍历列表数据
      if (i == index) { //根据下标找到目标
        var collectStatus = false
        if (message[i].collected == 0) { //如果是没点赞+1
          collectStatus = true
          message[i].collected = parseInt(message[i].collected) + 1
          message[i].dzzs = parseInt(message[i].dzzs) + 1
        } else {
          collectStatus = false
          message[i].collected = parseInt(message[i].collected) - 1
          message[i].dzzs = parseInt(message[i].dzzs) - 1
        }
        wx.showToast({
          title: collectStatus ? '收藏成功' : '取消收藏',
        })
      }
    }
    this.setData({
      wishList: message
    })
  }


```

#### 3.多图上传

```
<view class="weui-cell">
  <view class="weui-cell__bd">
    <view class="weui-uploader">
      <view class="weui-uploader__hd">
        <view class="weui-uploader__title">点击可预览选好的图片</view>
        <view class="weui-uploader__info">{{pics.length}}/9</view>
      </view>
      <view class="weui-uploader__bd">
        <view class="weui-uploader__files">
          <block wx:for="{{pics}}" wx:for-item="image">
            <view class="weui-uploader__file">
              <image class="weui-uploader__img" src="{{image}}" data-src="{{image}}" bindtap="previewImage"></image>
            </view>
          </block>
        </view>
        <-- isShow 这个是判断是否进行触发点隐藏操作-->
        <view class="weui-uploader__input-box {{isShow?'true':'hideTrue'}}">
          <view class="weui-uploader__input" bindtap="chooseImage"></view>
        </view>
      </view>
    </view>
  </view>
</view>

```

```
page {
  line-height: 1.6;
  font-family: -apple-system-font, "Helvetica Neue", sans-serif;
}
icon {
  vertical-align: middle;
}
.weui-cell {
  padding: 10px 15px;
  position: relative;
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
  align-items: center;
}
.weui-cell_input {
  padding-top: 0;
  padding-bottom: 0;
}
.weui-uploader__hd {
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
  padding-bottom: 10px;
  align-items: center;
}
.weui-uploader__title {
  flex: 1;
}
.weui-uploader__info {
  color: #b2b2b2;
}
.weui-uploader__bd {
  margin-bottom: -4px;
  margin-right: -9px;
  overflow: hidden;
}
.weui-uploader__file {
  float: left;
  margin-right: 9px;
  margin-bottom: 9px;
}
.weui-uploader__img {
  display: block;
  width: 79px;
  height: 79px;
}
.weui-uploader__input-box {
  float: left;
  position: relative;
  margin-right: 9px;
  margin-bottom: 9px;
  width: 77px;
  height: 77px;
  border: 1px solid #d9d9d9;
}
.weui-uploader__input-box:before, .weui-uploader__input-box:after {
  content: " ";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #d9d9d9;
}
.weui-uploader__input-box:before {
  width: 2px;
  height: 39.5px;
}
.weui-uploader__input-box:after {
  width: 39.5px;
  height: 2px;
}
.weui-uploader__input {
  position: absolute;
  z-index: 1;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
}

.hideTrue {
  display: none
}

```

```
Page({
  data: {
    pics: [],
    count: [1, 2, 3, 4, 5, 6, 7, 8, 9],
    isShow: true
  },
  onLoad: function (options) {
    // 生命周期函数--监听页面加载
    isShow: (options.isShow == "true" ? true : false)
  },
  // 图片上传
  chooseImage: function () {
    var _this = this,
      pics = this.data.pics;
    wx.chooseImage({
      count: 9 - pics.length, // 最多可以选择的图片张数，默认9
      sizeType: ['original', 'compressed'], // original 原图，compressed 压缩图，默认二者都有
      sourceType: ['album', 'camera'], // album 从相册选图，camera 使用相机，默认二者都有
      success: function (res) {
        // success
        var imgSrc = res.tempFilePaths;
        pics = pics.concat(imgSrc);
        // 控制触发添加图片的最多时隐藏
        if (pics.length >= 9) {
          _this.setData({
            isShow : (!_this.data.isShow)
          })   
        }else {
          _this.setData({
            isShow: (_this.data.isShow)
          })  
        }
        _this.setData({
          pics: pics
        })
      },
      fail: function () {
        // fail
      },
      complete: function () {
        // complete
      }
    })
  },
  // 图片预览
  previewImage: function (e) {
    var current = e.target.dataset.src
    wx.previewImage({
      current: current,
      urls: this.data.pics
    })
  }
})


```

#### 4.导航栏切换

```

<!--导航条-->
<view class="navbar">
  <text wx:for="{{navbar}}" data-idx="{{index}}" class="item {{currentTab==index ? 'active' : ''}}" wx:key="unique" bindtap="navbarTap">{{item}}</text>
</view>
 
<!--首页-->
<view hidden="{{currentTab!==0}}">
  tab_01
</view>
 
<!--搜索-->
<view hidden="{{currentTab!==1}}">
  tab_02
</view>
 
<!--我-->
<view hidden="{{currentTab!==2}}">
  tab_03
</view>

```

```
page{
  display: flex;
  flex-direction: column;
  height: 100%;
}
.navbar{
  flex: none;
  display: flex;
  background: #fff;
}
.navbar .item{
  position: relative;
  flex: auto;
  text-align: center;
  line-height: 80rpx;
}
.navbar .item.active{
  color: #FFCC00;
}
.navbar .item.active:after{
  content: "";
  display: block;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 4rpx;
  background: #FFCC00;
}

```

```
var app = getApp()
Page({
  data: {
    navbar: ['首页', '搜索', '我'],
    currentTab: 0
  },
  navbarTap: function(e){
    this.setData({
      currentTab: e.currentTarget.dataset.idx
    })
  }
})
```

#### 5.滑动导航栏切换

```
 <!--导航条--> 
<view class="top-news">
      <view class="nav-scroll">
        <scroll-view class="scroll-view_H" scroll-x="true" style="width: 100%">
        
               <text wx:for="{{section}}" data-idx="{{index}}" class="item {{currentTab==index ? 'active' : ''}}" wx:key="id" bindtap="navbarTap" id="{{item.id}}">{{item.name}}</text>
        </scroll-view>
      </view>
</view>
<!--白酒-->
<view hidden="{{currentTab!==0}}">
  tab_01
</view>
 
<!--果酒-->
<view hidden="{{currentTab!==1}}">
  tab_02
</view>
 
<!--农产品-->
<view hidden="{{currentTab!==2}}">
  tab_03
</view>
```

```

/*导航*/
.top-news{
  background-color: #fff;
  width:100%;height: 110rpx;
border-bottom:1px solid #404040;
/* position: fixed;top:0;
left:0; */
z-index: 999;
overflow: hidden;
/* background: linear-gradient(to right,#f3f3f3,#fff,#f3f3f3); */
 }
.scroll-view_H{
  white-space:nowrap;
  width: 100%;
padding-left: 16rpx;
box-sizing: border-box;
}
/* .nav-name{display:inline-block;font-size:32rpx;color: #2b2e33;border-bottom: 2px solid transparent;padding:20rpx;} */
.item{
display:inline-block;
font-size:32rpx;
color: #404040;
border-bottom: 2px solid transparent;
padding:20rpx 30rpx;
}
/* .nav-hover{color: #349393;border-bottom: 2px solid #f06000;} */
.active{
  color: #404040;
  border-bottom: 2px solid #404040;
  }

```



```
data: {
    section: [

    
  { name: '白酒', id: '1001' },
 { name: '果酒', id: '1032' },

      { name: '农产品', id: '1003' },
 { name: '其他商品', id: '1004' },
  
    { name: '电影', id: '1005' }, 
{ name: '少儿', id: '1021' },
  
    { name: '少儿', id: '1021' }
   
 ],
   

  currentTab: 0
 
 },
 
 navbarTap: function (e) {
    this.setData({
      currentTab: e.currentTarget.dataset.idx
    });
 
  },



```

#### 6.二级滑动导航栏切换

```
<!--pages/channel/c_management/index.wxml-->
<view class='nav_header'>
<view class="navbar">
  <view class='add'></view>
  <text wx:for="{{navbar}}" data-idx="{{index}}" class="item {{currentTab==index ? 'active' : ''}}" wx:key="unique" bindtap="navbarTap">{{item}}</text>
  <view class='add_1'>+</view>
</view>
</view>


 
 <!--商品列表-->
<view hidden="{{currentTab!==0}}">
<view class="top-news">
      <view class="nav-scroll">
        <scroll-view class="scroll-view_H" scroll-x="true" style="width: 100%">
               <text wx:for="{{section}}" data-idx="{{index}}" class="item_1 {{currentTab1==index ? 'active_1' : ''}}" wx:key="id" bindtap="navbarTap_1" id="{{item.id}}">{{item.name}}</text>
        </scroll-view>
      </view>
</view>


<!--所有商品1-->
<view hidden="{{currentTab1!==0}}">
<view class='box_list'>

<view class='box_list_group'>
<view class='list_top'>
<view class='list_left'><image src='img/header_bg.png'></image></view>
<view class='list_right'>
<view class='shop_text_1'>坚果坚果坚果坚果坚果坚果坚坚果坚果坚果坚果坚果坚果坚果坚果坚果</view>
<view class='shop_text_2'>￥1020/份</view>
<view class='shop_text_3'>库存：   不限库存</view>
<view class='shop_text_4'>销量： 0</view>
</view>
<view class='clear_both'></view>
</view>
<view class='list_bottom'>
<view class='box_flex'>删除</view>
<view class='box_flex'>清除</view>
<view class='box_flex'>下架</view>
</view>
</view>

<view class='box_list_group'>
<view class='list_top'>
<view class='list_left'><image src='img/header_bg.png'></image></view>
<view class='list_right'>
<view class='shop_text_1'>坚果坚果坚果坚果坚果坚果坚坚果坚果坚果坚果坚果坚果坚果坚果坚果</view>
<view class='shop_text_2'>￥1020/份</view>
<view class='shop_text_3'>库存：   不限库存</view>
<view class='shop_text_4'>销量： 0</view>
</view>
<view class='clear_both'></view>
</view>
<view class='list_bottom'>
<view class='box_flex'>删除</view>
<view class='box_flex'>清除</view>
<view class='box_flex'>下架</view>
</view>
</view>


</view>
</view>
 
<!--上架中-->
<view hidden="{{currentTab1!==1}}">
  tab_02
</view>
 
<!--已下架-->
<view hidden="{{currentTab1!==2}}">
  tab_03
</view>

<!--不限-->
<view hidden="{{currentTab1!==3}}">
  tab_04
</view>





</view>
 
<!--商品分组-->
<view hidden="{{currentTab!==1}}">

<view class="top-news">
      <view class="nav-scroll">
        <scroll-view class="scroll-view_H" scroll-x="true" style="width: 100%">
               <text wx:for="{{section2}}" data-idx="{{index}}" class="item_2 {{currentTab2==index ? 'active_1' : ''}}" wx:key="id" bindtap="navbarTap_2" id="{{item.id}}">{{item.name}}</text>
        </scroll-view>
      </view>
</view>


<!--所有商品2-->
<view hidden="{{currentTab2!==0}}">
<view class='box_list'>

<view class='box_list_group'>
<view class='list_top'>
<view class='list_right'>
<view class='shop_text_1'>坚果坚果坚果坚果坚果坚果坚坚果坚果坚果坚果坚果坚果坚果坚果坚果</view>
<view class='shop_text_2'>上架中</view>
<view class='shop_text_3'></view>
<view class='shop_text_4'>共：1件</view>
</view>
<view class='clear_both'></view>
</view>
<view class='list_bottom'>
<view class='box_flex'>删除</view>
<view class='box_flex'>清除</view>
<view class='box_flex'>下架</view>
<view class='box_flex'>商品</view>
</view>
</view>

<view class='box_list_group'>
<view class='list_top'>
<view class='list_right'>
<view class='shop_text_1'>坚果坚果坚果坚果坚果坚果坚坚果坚果坚果坚果坚果坚果坚果坚果坚果</view>
<view class='shop_text_2'>上架中</view>
<view class='shop_text_3'></view>
<view class='shop_text_4'>共：1件</view>
</view>
<view class='clear_both'></view>
</view>
<view class='list_bottom'>
<view class='box_flex'>删除</view>
<view class='box_flex'>清除</view>
<view class='box_flex'>下架</view>
<view class='box_flex'>商品</view>
</view>
</view>


</view>
</view>
 
<!--上架中-->
<view hidden="{{currentTab2!==1}}">
  tab_02
</view>
 
<!--已下架_2-->
<view hidden="{{currentTa2!==2}}">
  tab_03
</view>


</view>
 



```

```
.nav_header{
margin-top: 30rpx;
}
 .navbar{
 font-size: 32rpx;
 padding:30rpx;
  flex: none;
  display: flex;
  /* background: #fe2d4a; */
  background-color: #FFD161;
}
.navbar .item{

  border:2rpx solid #fff;
  float: left;
  flex: 3;

  position: relative;
  /* flex: auto; */
  text-align: center;
  line-height: 60rpx;
  color:#fff;
}
.navbar .item.active{
  /* color: #fe2d4a; */
  color: #FFD161;
  background-color: #fff;
  
}
/* .navbar .item .active:after{
  content: "";
  display: block;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 4rpx;
  background: #FFCC00;
} */
.navbar .add{
flex: 1;
}
.navbar .add_1{
flex: 1;
text-align: right;
font-size: 38rpx;
color:#fff;
}



/*子导航*/
.top-news{
  background-color: #fff;
  width:100%;
  height: 89rpx;

z-index: 999;
overflow: hidden;

 }
.scroll-view_H{
  white-space:nowrap;
  width: 100%;
padding-left: 16rpx;
box-sizing: border-box;
}

.item_1{
display:inline-block;
font-size:32rpx;
color: #404040;
/* border-bottom: 2px solid #404040; */
padding:20rpx 50rpx;
}
.active_1{
  color: #FFD161;
  border-bottom: 2px solid #FFD161;
  }
  /* 产品分组下的导航 */
.item_2{
display:inline-block;
font-size:32rpx;
color: #404040;
padding:20rpx 70rpx;
}




```

```
data: {
    navbar: ['商品列表', '商品分组', ],

    section: [
      { name: '所有商品', id: '1001' }, { name: '上架中', id: '1032' },
      { name: '已下架', id: '1003' }, { name: '不限', id: '1004' },
   
    ],
    // 商品分组
    section2: [
      { name: '所有商品', id: '1001' }, { name: '上架中', id: '1032' },
      { name: '已下架', id: '1003' },
    ],
  // 商品列表// 商品分组
    currentTab: 0,
     // 商品列表
    currentTab1:0,
      // 商品分组
    currentTab2: 0,
   
  },
  // 商品列表// 商品分组
  navbarTap: function (e) {
    this.setData({
      currentTab: e.currentTarget.dataset.idx
    })
  },
  
      // 商品列表
  navbarTap_1: function (e) {
    this.setData({
      currentTab1: e.currentTarget.dataset.idx
    });
  },
    // 商品分组
    navbarTap_2: function (e) {
    this.setData({
      currentTab2: e.currentTarget.dataset.idx
    });
  }


```

#### 7.自定义底部弹出层

```
<view class='yourPurse' bindtap='showModal1'><button>123</button></view>

<view class="commodity_screen" bindtap="hideModal" wx:if="{{showModalStatus}}"></view>
<view animation="{{animationData}}" class="commodity_attr_box" wx:if="{{showModalStatus}}">
这是内容
</view>

```

```
.commodity_screen {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background: #000;
  opacity: 0.2;
  overflow: hidden;
  z-index: 1000;
  color: #fff;
}

.commodity_attr_box {
  width: 100%;
  overflow: hidden;
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 2000;
  background: #fff;
  padding-top: 20rpx;
}

```

```
showModal: function () {
    // 显示遮罩层
    var animation = wx.createAnimation({
      duration: 200,
      timingFunction: "linear",
      delay: 0
    })
    this.animation = animation
    animation.translateY(300).step()
    this.setData({
      animationData: animation.export(),
      showModalStatus: true
    })
    setTimeout(function () {
      animation.translateY(0).step()
      this.setData({
        animationData: animation.export()
      })
    }.bind(this), 200)
  },
  hideModal: function () {
    // 隐藏遮罩层
    var animation = wx.createAnimation({
      duration: 200,
      timingFunction: "linear",
      delay: 0
    })
    this.animation = animation
    animation.translateY(300).step()
    this.setData({
      animationData: animation.export(),
    })
    setTimeout(function () {
      animation.translateY(0).step()
      this.setData({
        animationData: animation.export(),
        showModalStatus: false
      })
    }.bind(this), 200)
  }


```

