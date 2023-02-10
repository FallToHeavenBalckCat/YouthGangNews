<template>
	<view>
		<view class="top">
			<image src="../../static/images/personCenter.png" mode=""></image>
			<view class="top-title">
				个人中心
			</view>
		</view>
		<view class="content">
			<Newbox v-for="item in hisList" :key="item.id" @click.native="goDetails(item)"
			:newsItem="item">
			</Newbox>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				hisList:[],
			};
		},
		
		onShow() {
			this.getDetails();
		},
		
		methods:{
			goDetails(item){
				uni.navigateTo({
					url:`/pages/details/details?cid=${item.classid}&id=${item.id}`,
				})
			},
			
			getDetails(){
				let historyList=uni.getStorageSync("historyList")||[];
				this.hisList=historyList;
			}
		}
	}
</script>

<style lang="scss" scoped>
.top{
	background-color: #F6F6F6;
	display:flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	image{
		width:300rpx;
		height:300rpx;
		
	}
}
</style>
