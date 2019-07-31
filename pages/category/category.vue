<template>
    <view style='height:100%;'>
        <view style="width:90%; padding:10px 5%; flex-wrap:nowrap;">
            <view class="grace-search">
            	<view class="icons grace-icons icon-scancode"></view>
            	<view class="grace-search-in" style="background:#F1F2F3;">
            		<view class="icons grace-icons icon-search"></view>
            		<input type="search" style="background:#F1F2F3;" placeholder="关键字"></input>
            	</view>
            </view>
        </view>
        <view class="grace-cate" style='width:100%; height:calc(100% - 64px);'>
            <scroll-view scroll-y class="grace-cate-left" :scroll-into-view="leftTo">
                <view v-for="(item, index) in mainCate" :key="index" :class="['item', currentCateIndex == item.cateid ? 'current' : '']" :data-cateid="item.cateid" @tap='changCate' :id="'cate'+item.cateid">{{item.name}}</view>
            </scroll-view>
            <scroll-view class="grace-cate-right" scroll-y :scroll-into-view="productListTo" @scroll="rscroll">
                <block v-for="(cate, index) in mainCate" :key="index">
                    <view class="grace-title grace-nowrap grace-space-between" style="margin-top:10px;" :id="'productList'+cate.cateid">
                        <view class="grace-bold">{{cate.name}}</view>
                    </view>
                    <view class="grace-news-list">
                        <view class="item" v-for="(product, productIndex) in allProducts['cate'+cate.cateid+'products']" :key="productIndex">
							<view class="img img-l">
								<image :src="product.img" mode="widthFix"></image>
							</view>
							<view class="body">
								<view class="title">{{product.name}}</view>
                                <view class="price">￥{{product.price}}</view>
                                <view>
									<view :data-productid='product.productId' class='grace-add-to-card' @tap='addtocard'>+</view>
								</view>
                            </view>
                        </view>
                    </view>
                </block>
            </scroll-view>
      </view>
    </view>
</template>
<script>
var scrollTimer = null;
var pageHeight = 100;
var productsData = require('../../graceUI/demoData/products.js');
export default {
    data() {
        return {
            currentCateIndex : 1,
            // 左侧滚动定位
            leftTo : 'cate1',
            // 产品列表滚动定位
            productListTo: 'productList1',
            //分类
            mainCate: [
                { cateid: 1, name: '热门推荐' },
                { cateid: 2, name: '促销打折' },
                { cateid: 3, name: '国际名牌' },
                { cateid: 4, name: '大衣外套' },
                { cateid: 5, name: '汽车用品' },
                { cateid: 6, name: '儿童用品' },
                { cateid: 7, name: '文具用品' },
                { cateid: 8, name: '精品男装' },
                { cateid: 9, name: '精品女装' },
                { cateid: 10, name: '电脑办公' },
                { cateid: 11, name: '礼品鲜花' }
            ],
            // 产品列表对应分类
            allProducts: productsData.allProducts
        }
    },
    onLoad:function(){
        uni.getSystemInfo({
            success: function(res) {
            pageHeight = res.windowHeight;
            },
        });
		console.log(productsData)
    },
    methods:{
        // 分类切换
        changCate:function(e){
            var cateid = e.currentTarget.dataset.cateid;
            this.currentCateIndex = cateid;
            this.leftTo           = 'cate'+cateid;
            this.productListTo    = 'productList' + cateid;
        },
        // 产品区域滚动
        rscroll : function(e){
            var sctop = e.detail.scrollTop;
            if (scrollTimer != null) { clearTimeout(scrollTimer);}
            scrollTimer = setTimeout(function(){
              this.getIndex(0, sctop);
            }.bind(this), 80);
        },
        // 动态识别分类激活
        getIndex: function (i, sctop){
            var _self = this;
            var query = wx.createSelectorQuery();
            query.select('#productList' + this.mainCate[i].cateid).boundingClientRect();
            query.selectViewport().scrollOffset();
            query.exec(function (res){
                if (res[0].top + pageHeight / 2 > 0){
                    _self.currentCateIndex =  _self.mainCate[i].cateid;
                    _self.leftTo           =  'cate' + _self.mainCate[i].cateid;
                }else{
                    i++;
                    if (i < _self.mainCate.length) { _self.getIndex(i, sctop); }
                }
            });
        },
        // 加入到购物车
        addtocard : function(e){
            var productid = e.currentTarget.dataset.productid;
            uni.showToast({
                title: '产品id : ' + productid+', 请根据项目需求自行完善后续代码',
                icon:"none"
            })
        },
        // 搜索
        searchNow : function(e){
            var k = e.detail.value;
            uni.showToast({
                title: '关键字 : ' + k + ', 请根据项目需求自行完善后续代码',
                icon: "none"
            });
        }
    }
}
</script>
<style>
page{height:100%;}
.grace-news-list .img{width:110upx; height:110upx; flex-shrink:0; font-size:0;}
.grace-news-list .img image{width:110%; height:110upx; border-radius:5upx;}
.grace-news-list .price{line-height:1.8em; color:#E2231A;}
.grace-add-to-card{width:25px; height:25px; line-height:22px; border:1px solid #E2231A; font-size:20px; color:#E2231A; float:right; text-align:center; border-radius:26px;}
</style>