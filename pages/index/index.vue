<template>
	<view class="content">
		<!-- 轮播图 -->
		<view class="swipper">
			<image class="imgSty" src="https://gw.alicdn.com/imgextra/i3/84/TB2LdRjk77mBKNjSZFyXXbydFXa_!!84-0-lubanu.jpg" mode=""></image>
		</view>
		
		<!-- 分类列表 -->
		<view class="category-list">
			<view
				class="category"
				v-for="(row, index) in categoryList"
				:key="index"
				@tap="toCategory(row)"
			>
				<view class="img"><image :src="row.img"></image></view>
				<view class="text">{{ row.name }}</view>
			</view>
		</view>
	
		<!-- 活动 -->
		<view class="activityCnt">
			<p>活动</p>
			<view class="activityItem">
				<view 
					class="activityImg"
					v-for="(row, index) in activityList"
					:key="index"
				>
					<image class="activityItemImg" :src="row.img" mode=""></image>
				</view>
			</view>
		</view>
		
		<!-- 推荐 -->
		<view class="recommendCnt">
			<p class="title">推荐</p>
			<view class="recommendTop">
				<view 
					class="recommendTopItem"
					v-for="(row, index) in  recommendList[0]"
					:key="index"
				>
					<p>{{row.name1}}</p>
					<p>{{row.name2}}</p>
					<image class="recommendTopItemImg" :src="row.img" mode=""></image>
				</view>
			</view>
			<view class="recommendBtm">
				<view 
					class="recommendBtmItem"
					v-for="(row, index) in  recommendList[1]"
					:key="index"
				>
					<p>{{row.name1}}</p>
					<p>{{row.name2}}</p>
					<image class="recommendBtmItemImg" :src="row.img" mode=""></image>
				</view>
			</view>
		</view>
	
		<!-- 猜你喜欢 -->
		<view class="subtitle">猜你喜欢</view>
		
		<view class="productCnt">
			<view 
				class="productItem"
				v-for="(row, index) in productList"
				:key="index"
			>
				<view class="img">
					<image :src="row.img" mode=""></image>
				</view>
				<view class="text">{{ row.name }}</view>
				<view class="price">{{ row.price }}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				// 分类菜单
				categoryList: [
					{ id: 1, name: '生活超市', img: 'https://m.360buyimg.com/mobilecms/jfs/t20767/52/2278642602/14820/c30f2812/5b4eaa9eN28c2a6fa.png' },
					{ id: 2, name: '服饰', img: 'https://m.360buyimg.com/mobilecms/jfs/t18865/90/1804471517/14538/72c79ba/5ad87b67N1ebcb69b.png' },
					{ id: 3, name: '生鲜到', img: 'https://m.360buyimg.com/mobilecms/jfs/t17725/156/1767366877/17404/f45d418b/5ad87bf0N66c5db7c.png' },
					{ id: 4, name: '充值服务', img: 'https://m.360buyimg.com/mobilecms/jfs/t18454/342/2607665324/6406/273daced/5b03b74eN3541598d.png' },
					{ id: 5, name: '一起拼', img: 'https://m.360buyimg.com/mobilecms/jfs/t22228/270/207441984/11564/88140ab7/5b03fae3N67f78fe3.png' },
					{ id: 6, name: '领劵', img: 'https://m.360buyimg.com/mobilecms/jfs/t19495/200/1823004232/14065/ca00ab2c/5ad87cf5N4ad8e6f1.png' },
					{ id: 7, name: '拍卖', img: 'https://m.360buyimg.com/mobilecms/jfs/t21481/263/412160889/15938/4246b4f8/5b0cea29N8fb2865f.png' },
					{ id: 8, name: '赚钱', img: 'https://m.360buyimg.com/mobilecms/jfs/t16828/63/2653634926/5662/d18f6fa1/5b03b779N5c0b196f.png' },
					{ id: 9, name: '闪电到', img: 'https://m.360buyimg.com/mobilecms/jfs/t16990/157/2001547525/17770/a7b93378/5ae01befN2494769f.png' }
				],
				// 活动
				activityList:[
					{ id: 1, img: 'https://gw.alicdn.com/tfscom/i1/TB2wFkzGamWBuNjy1XaXXXCbXXa_!!0-dgshop.jpg' },
					{ id: 2, img: 'https://gw.alicdn.com/tfscom/i1/TB2wFkzGamWBuNjy1XaXXXCbXXa_!!0-dgshop.jpg' },
					{ id: 3, img: 'https://gw.alicdn.com/tfscom/i1/TB2wFkzGamWBuNjy1XaXXXCbXXa_!!0-dgshop.jpg' },
				],
				// 推荐
				recommendList:[
					[
						{ id: 1, name1: 'gdd',name2:'求自维商。', img: 'https://m.360buyimg.com/mobilecms/s130x130_jfs/t21196/6/1392860476/62867/56c7bae8/5b27b02aNe15aafc3.png!q70.jpg.dpg' },
						{ id: 2, name1: 'cmyt',name2:'然七志议。', img: 'https://m.360buyimg.com/mobilecms/s130x130_jfs/t22666/293/257815171/29274/6b5605b1/5b2a5295N5a81ad96.jpg!q70.jpg.dpg' },
					],
					[
						{ id: 1, name1: 'tgrr',name2:'应权没加。', img: 'https://m.360buyimg.com/mobilecms/s130x130_jfs/t19918/10/2637292122/17090/1da36d9f/5b4c67c6N70c2ce3d.jpg!q70.jpg.dpg' },
						{ id: 2, name1: 'cmyt',name2:'然七志议。', img: 'https://m.360buyimg.com/mobilecms/s130x130_jfs/t19918/10/2637292122/17090/1da36d9f/5b4c67c6N70c2ce3d.jpg!q70.jpg.dpg' },
						{ id: 3, name1: 'gdd',name2:'路进道。', img: 'https://m.360buyimg.com/mobilecms/s130x130_jfs/t19918/10/2637292122/17090/1da36d9f/5b4c67c6N70c2ce3d.jpg!q70.jpg.dpg' },
						{ id: 4, name1: 'cmyt',name2:'例至府打', img: 'https://m.360buyimg.com/mobilecms/s130x130_jfs/t19918/10/2637292122/17090/1da36d9f/5b4c67c6N70c2ce3d.jpg!q70.jpg.dpg' },
					]
					
				],
				// 猜你喜欢
				productList:[
					{ id: 1,name:'Hufb Zooelqu Mduxy Bdgmiiopn Xqk',price:'¥336.08', img: 'https:////m.360buyimg.com/mobilecms/s370x370_jfs/t22354/194/2299221582/77216/db8e2ad/5b4ff8c5N36e71d00.jpg!q70.jpg.dpg' },
					{ id: 2,name:'Hufb Zooelqu Mduxy Bdgmiiopn Xqk',price:'¥336.08', img: 'https://m.360buyimg.com/mobilecms/s370x370_jfs/t22564/199/1192949265/188892/452bc26e/5b569d13N54cf5d1d.jpg!q70.jpg.dpg' },
					{ id: 3,name:'Hufb Zooelqu Mduxy Bdgmiiopn Xqk',price:'¥336.08', img: 'https://m.360buyimg.com/mobilecms/s370x370_jfs/t6076/102/8341272190/162655/7de1aa32/5987d23eN94f9cc33.jpg!q70.jpg.dpg' },
					{ id: 4,name:'Hufb Zooelqu Mduxy Bdgmiiopn Xqk',price:'¥336.08', img: 'https://m.360buyimg.com/mobilecms/s370x370_jfs/t19477/86/1499720359/137799/7e0e909d/5acb6405N3f79b732.jpg!q70.jpg.dpg' },
					{ id: 5,name:'Hufb Zooelqu Mduxy Bdgmiiopn Xqk',price:'¥336.08', img: 'https://m.360buyimg.com/mobilecms/s370x370_jfs/t19999/128/255316619/298848/5ac8a83a/5aec5901N66b75ea1.jpg!q70.jpg.dpg' },
					{ id: 6,name:'Hufb Zooelqu Mduxy Bdgmiiopn Xqk',price:'¥336.08', img: 'https://m.360buyimg.com/mobilecms/s370x370_jfs/t13459/34/789007206/39506/fb07bc4d/5a1394c3N56adbdfc.jpg!q70.jpg.dpg' },
					
				]
			}
		},
		onLoad() {

		},
		methods: {
			toCategory(e) {
					//uni.showToast({title: e.name,icon:"none"});
				Console.log(e)	
			}
		}
	}
</script>

<style lang="scss">
ul,p{
	margin: 0;
}
.imgSty{
	display: block;
	width: 100%;
	height: 250upx;
}
*{
	box-sizing: border-box;
}
::-webkit-scrollbar{
	display: none;
}

/* 轮播图 */
.swipper{
	width: 100%;
}

/* 分类列表 */
.category-list {
	width: 92%;
	margin: 0 4%;
	padding: 0 0 30upx 0;
	border-bottom: solid 2upx #f6f6f6;
	display: flex;
	justify-content: flex-start;
	flex-wrap: wrap;
	.category {
		width: 20%;
		margin-top: 50upx;
		display: flex;
		flex-wrap: wrap;
		.img {
			width: 100%;
			display: flex;
			justify-content: center;
			image {
				width: 9vw;
				height: 9vw;
			}
		}
		.text {
			margin-top: 16upx;
			width: 100%;
			display: flex;
			justify-content: center;
			font-size: 24upx;
			color: #3c3c3c;
		}
	}
}
/* 活动 */
.activityCnt{
	display: flex;
	flex-direction: column;
	p{
		font-size: 30upx;
		font-weight: 400;
		padding: 10px;
		color: #666;
	}
	.activityItem{
		display: flex;
		flex-direction: row;
		overflow-x: auto;
		.activityImg{
			width: 40%;
			flex-shrink: 0;
			margin-left: 10px;
			.activityItemImg{
				width: 100%;
				height: 180upx;
			}
		}
	}
}


/* 推荐 */
.recommendCnt{
	display: flex;
	flex-direction: column;
	padding: 10px;
	.title {
		font-size: 30upx;
		font-weight: 400;
		padding: 10px;
		color: #666;
	}
	.recommendTop{
		display: flex;
		flex-direction: row;
		padding:0 10px;
		border-top: 1px solid #dedede;
		.recommendTopItem{
			display: flex;
			flex-direction: column;
			width: 50%;
			padding: 5px 10px;
			border-right:1px solid #dedede;
			&:last-child{
				border-right:none;
			}
			 p{
				font-size: 22upx;
				color: #666;
			}
			.recommendTopItemImg{
				width: 120upx;
				height: 120upx;
			}
		}
	}
	.recommendBtm{
		display: flex;
		flex-direction: row;
		padding:0 10px;
		border-top: 1px solid #dedede;
		.recommendBtmItem{
			flex: 1;
			display: flex;
			flex-direction: column;
			padding: 5px 10px;
			border-right: 1px solid #dedede;
			&:last-child{
				border-right: none;
			}
			p {
				font-size: 22upx;
				color: #666;
			}
			.recommendBtmItemImg{
				width: 120upx;
				height: 120upx;
			}
		}
	}
}

/* 猜你喜欢 */
.subtitle {
	position: relative;
	font-size: 30upx;
	color: #999999;
	height: 45px;
	line-height: 45px;
	text-align: center;
	&:before {
	  content: "";
	  position: absolute;
	  width: 35%;
	  height: 1px;
	  top: 50%;
	  background-color: #ededed;
	  left: 2%;
	}
	&:after {
	  content: "";
	  position: absolute;
	  width: 35%;
	  height: 1px;
	  top: 50%;
	  background-color: #ededed;
	  right: 2%;
	}
}
.productCnt{
	width: 100%;
	margin: 0 4%;
	box-sizing: border-box;
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	.productItem{
		width: 47%;
		padding-top: 50upx;
		display: flex;
		flex-wrap: wrap;
		box-sizing: border-box;
		border-bottom: 3px solid #f5f5f5;
		border-right: 3px solid #f5f5f5;
		&:nth-child(even){
			border-right:none;
		}
		.img {
			width: 100%;
			display: flex;
			justify-content: center;
			image {
				// width: 20vw;
				// height: 20vw;
				width: 100%;
				height: 50vw;
			}
		}
		.text {
			margin-top: 16upx;
			width: 100%;
			display: flex;
			justify-content: center;
			font-size: 24upx;
			color: #3c3c3c;
		}
		.price{
			color: #f23030;
			font-size: 32upx;
		}
	}
}
	
</style>
