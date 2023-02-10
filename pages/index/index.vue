<template>
	<view class="home">
		<view class="scrollNav">
			<scroll-view scroll-x class="navscroll">
				<view class="item" v-for="nameItem in titleName">
					{{nameItem}}
				</view>
			</scroll-view>
			
		</view>
		<view class="content">
			<Newbox></Newbox>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				titleName: ["国内", "国际", "军事", "科技", "娱乐", "商业"],
			}
		},
		onLoad() {

		},
		methods: {

		}
	} 
	
</script>

<style lang="scss" scoped>
.navscroll{
	white-space: nowrap;
	background:#f7f8fa;
	/deep/::-webkit-scrollbar{
		width:4px !important;
		height: 1px !important;
		overflow: auto !important;
		background: transparent !important;
		-webkit-appearance: auto !important;
		display:block;
	}
}	
.item{
	background-color: #f7f8fa;
	display:inline-block;
	line-height: 100rpx;
	padding: 0 30rpx;
	font-size:36rpx;
	color:#333;
		
}
</style>
