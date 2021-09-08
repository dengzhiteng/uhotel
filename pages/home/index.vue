<template>
	<view class="content">
		<view class="foodList">
			<view class="item" v-for="item in foodlist" :key="item._id" @click="handleDetails(item._id)">
				<image  class="item_img" :src="item.imageUrl"  @click="handleDetails(item._id)"></image>
				<view class="item_info"  @click="handleDetails(item._id)">
					<view class="item_title">
						{{item.dishName}}
					</view>
					<view class="item_desc">
						{{item.description}}
					</view>
					<view class="item_price">
						<text class="price"><del>{{item.price}}</del></text>
						<text class="activePrice"> {{item.price*item.discount|activePrice}} </text>
					</view>
				</view>
				<view class="add_cart" 	 @click="handleAddCart(item._id)"			>
					<button type="default" size="mini">+</button>
				</view>
			</view>
			
		</view>
	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				foodlist:[]
			}
		},
		filters:{
			activePrice:function(val){
				return (val/10).toFixed(1)
			}
		},
		methods:{
			handleDetails:function(_id){
				console.log(_id)
			},
			handleAddCart:function(_id){
				console.log(_id)
			},
		},
		async onLoad() {
			const res = await uniCloud.callFunction({
				name:'getcollection',
				data:{
					target:'foodList'
				}
			})
			this.foodlist  = res.result
		}
	}
</script>

<style lang="scss" scoped>
	.foodList {
		.item{
			display: flex;
			padding: 10upx 20upx;
			.item_img{
				width: 150upx;
				height: 150upx;
			}
			.item_info{
				padding: 10upx;
				flex: 1;
				.item_title{
					font-weight: bold;
				}
				.item_desc{
				  color: #999;
				  display: -webkit-box;
				  -webkit-box-orient: vertical;
				  -webkit-line-clamp: 1;
				  overflow: hidden;
				}
				.item_price{
					margin-top: 10upx;
					text{
						margin-right: 10upx;
						padding: 5upx 10upx;
					}
					.price{
						color: #999;
					}
					.activePrice{
						color: red;
					}
				}
			}
			.add_cart{
				uni-button{
					margin-top: 50upx;
				}
			}
		} 
	 }

</style>
