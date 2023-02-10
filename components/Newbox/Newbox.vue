<template>
	<view>
		<view class="newbox">
			<view class="pic">
				<image mode="aspectFit"
					src="https://gss0.baidu.com/-fo3dSag_xI4khGko9WTAnF6hhy/zhidao/pic/item/7aec54e736d12f2e1f134d5449c2d562853568f4.jpg">
				</image>
			</view>
			<view class="txt">
				<view class="txt-title">
					默认标题默认默认标题默认默认标题默认默认标题默认默认标题默认默认标题默认默认标题默认默认标题默认默认标题默认默认标题默认	默认标题默认默认标题默认默认标题默认
				</view>
				<view class="txt-body">
					<view class="txt-author">作者</view>
					<view class="reading-volume">114514阅读</view>
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
		}
	}
</script>

<style lang="scss" scoped>
	.newbox {
		display: flex;

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
			border: 1rpx red solid;
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
