<template>
	<view>
		<view class="newbox">
			<view class="pic">
				<image mode="aspectFit"
					:src="newsItem.picurl">
				</image>
			</view>
			<view class="txt">
				<view class="txt-title">
					{{newsItem.title}}
				</view>
				<view class="txt-body">
					<view class="txt-author">{{newsItem.author}}</view>
					<!-- <view class="reading-volume">{{newsItem.hits}}</view> -->
				</view>
				<view class="txt-body">
					<view class="time">{{newsItem.posttime}}</view>
				</view>
			</view>

		</view>
	</view>
</template>

<script>
	export default {
		name: "Newbox",
		data() {
			return {

			};
		},
		
		props:{
			newsItem:{
				type:Object,
				default(){
					return {
						id:1,
						title:"《俺妹》第三季更新，作者伏见司发表感慨到:五更琉璃告白最新剧情",
						author:"黑猫",
						picurl:"https://gss0.baidu.com/-fo3dSag_xI4khGko9WTAnF6hhy/zhidao/pic/item/7aec54e736d12f2e1f134d5449c2d562853568f4.jpg",
						posttime:"2023-2-10 10:31:25",
						classid:1,
					}	
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.newbox {
		display: flex;
		margin-bottom:10rpx;
		margin-top:10rpx;

		.pic {
			width: 230rpx;
			height: 160rpx;

			image {
				width: 100%;
				height: 100%;
				// 在父标签中100%填充
			}
		}

		.txt {
			flex: 1;
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			// border: 1rpx red solid;
			padding-left: 10rpx;
			margin-right: 10rpx;

			.txt-title {
				font-size: 36rpx;
				color: #333;
				
				text-overflow: -o-ellipsis-lastline;
				overflow: hidden;	//溢出内容隐藏
				text-overflow: ellipsis;//文本溢出部分用省略号表示
				display: -webkit-box;//特别显示模式
				-webkit-line-clamp: 3;//行数
				line-clamp: 2;
				-webkit-box-orient: vertical;//盒子中内容竖直排列：
			}

			.txt-body {
				display: flex;
				flex-direction: row;
				justify-content: flex-end;
				font-size: 16rpx;
				color: #999;

				.txt-author {
					margin-right: 20rpx;
				}
			}
		}
	}
</style>
