<template>
	<view class="grace-margin">
		<!-- 购物车为空 -->
		<view v-if="shoppingCard.length < 1">
			<view class="grace-h5 grace-blod grace-center-title" style="margin-top:88px;">
				<text class="grace-icons icon-spliter"></text>
				您的购物车空空如也 ~
				<text class="grace-icons icon-spliter"></text>
			</view>
			<view class="grace-title-small-text grace-text-center">
				“再忙，也要记得买点什么犒赏自己 ~”
			</view>
		</view>
		<!-- 购物车为空 -->
		<!-- 购物车主结构  -->
		<view class="grace-shoppingcard" v-for="(item, index) in shoppingCard" :key="index">
			<view class="grace-title" style="margin-top:10px;">
				<view>{{item.shopName}}</view>
				<navigator class="grace-more">进店<text class="grace-icons icon-arrow-right"></text></navigator>
			</view>
			<view class="goods" v-for="(item, indexItem) in item.items" :key="indexItem">
				<image :src="item.img" mode="widthFix"></image>
				<view class="body">
					<view class="goods-title">{{item.goodsName}}</view>
					<view class="goods-price">
						￥{{item.price}}
						<view class="goods-number">
							<graceNumberBox :index="indexItem" :datas="index+''" :value="item.count" :maxNum="100" :minNum="1" v-on:change="numberChange"></graceNumberBox>
						</view>
					</view>
					<view class="goods-remove grace-icons icon-remove" @tap="removeGoods" :id="'removeIndex_' + index + '_' + indexItem">
						<text>删除</text>
					</view>
				</view>
			</view>
		</view>
		<view style="height:120upx;"></view>
		<!-- 底部  -->
		<view class="grace-footer bottomSet">
			<view style="width:48%; float:left; line-height:100upx; text-indent:1em;">
				总计 <text style="font-size:36upx; color:#F00;">￥{{totalprice}}</text>
			</view>
			<button type="warn" style="background:#E55D52; width:50%;">立即支付</button>
		</view>
	</view>
</template>
<script>
var _self;
import graceNumberBox from "../../graceUI/components/graceNumberBox.vue";
export default {
	data() {
		return {
			// 总价
			totalprice : '',
			// 购物车数据
			shoppingCard : ['']
		}
	},
	onLoad : function(){
		_self = this;
	},
	onShow : function () {
		// api 获取购物车数据
		uni.showLoading({title:'加载中'});
		uni.request({
			method:"GET",
			url:"https://www.easy-mock.com/mock/5cb9701f18a6f325b717f772/gmall/shoppingCard",
			success:function(res){
				console.log(res);
				this.shoppingCard = res.data.data;
				this.countTotoal();
				uni.hideLoading();
			}.bind(this)
		});
	},
	methods:{
		//计算总计函数
		countTotoal:function(){
			var total = 0;
			for (var i = 0; i < this.shoppingCard.length; i++){
				for (var ii = 0; ii < this.shoppingCard[i].items.length; ii++){
					total += Number(this.shoppingCard[i].items[ii].price) * Number(this.shoppingCard[i].items[ii].count);
				}
			}
			this.totalprice = total;
		},
		numberChange:function(data){
			this.shoppingCard[data[2]].items[data[1]].count = data[0];
			//计算总价
			this.countTotoal();
		},
		removeGoods : function(e){
			var index = e.currentTarget.id.replace('removeIndex_', '');
			index = index.split('_');
			var index1 = Number(index[0]);
			var index2 = Number(index[1]);
			wx.showModal({
				title: '确认提醒',
				content: '您确定要移除此商品吗？',
				success:function(e){
					if (e.confirm) {
						_self.shoppingCard[index1].items.splice(index2, 1);
						// 是否全部删除包含商铺
						if(_self.shoppingCard[index1].items.length < 1){
							_self.shoppingCard.splice(index1, 1);
						}
						//计算总价
						_self.countTotoal();
					}
				}
			})
		},
		checkout:function(){
			uni.showToast({
				title: '计算的数据保存在 shoppingCard 变量内 ^_^',
				icon : "none"
			})
		}
	},
	components:{
		graceNumberBox
	}
}
</script>
<style>
page{background:#F5F6F7;}
/* #ifdef H5 */
.bottomSet{bottom:50px !important;}
/* #endif */
</style>