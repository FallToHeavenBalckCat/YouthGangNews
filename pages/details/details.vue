<template>
	<view>
		<view class="details">
			<view class="title">{{detail.title}}</view>
			<view class="info">
				<view class="author">作者:{{detail.author}}</view>
				<view class="time">发布时间:{{detail.posttime}}</view>
			</view>

			<view class="content">
				<!-- 使用富文本对发送过来的数据进行解析； -->
				
				<rich-text :nodes="detail.content"></rich-text>
			</view>
		
			<view class="description">
				声明:本站的内容均采集与腾讯新闻,如果侵权请联系管理(1838186830@qq.com)进行整改删除,本站进行了内容采集不代表本站及作者观点,若有侵犯请及时联系管理员，谢谢您的支持。
			</view>

		</view>
	</view>
</template>

<script>
	import { timestampToTime,timestampToTimeLong } from "../../utils/tool.js";
	export default {
		data() {
			return {
				detail:{},
				options:null,
			};
		},

		onLoad(e){ 
			this.options=e;
			this.get();
		},
		
		methods: {
			// timestampToTime(timestamp) {
			//     var date = new Date(timestamp * 1000);//时间戳为10位需*1000，时间戳为13位的话不需乘1000
			//     var Y = date.getFullYear() + '-';
			//     var M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-';
			//     var D = (date.getDate() < 10 ? '0'+(date.getDate()) : date.getDate()) + ' ';
			//     var h = (date.getHours() < 10 ? '0'+(date.getHours()) : date.getHours()) + ':';
			//     var m = (date.getMinutes() < 10 ? '0'+(date.getMinutes()) : date.getMinutes()) + ':';
			//     var s = (date.getSeconds() < 10 ? '0'+(date.getSeconds()) : date.getSeconds());
			//     return Y+M+D+h+m+s;
			// }
			get(){
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/detail.php",
					data:{
						cid:this.options.cid,
						id:this.options.id,
					},
					success:res=>{
						console.log(res);
						this.detail=res.data;
						this.savaHistory();
						this.detail.posttime=timestampToTime(res.data.posttime);
					},
					fail:res=>{
						console.log("请求数据错误");
					}
				})
			},
			
			savaHistory(){
				let historyList=uni.getStorageSync("historyList")||[];	
				let item={
					id:this.detail.id,
					classid:this.detail.id,
					picurl:this.detail.picurl,
					title:this.detail.title,
					author:this.detail.author,
					posttime:timestampToTimeLong(Date.now()),
				};
				//去重,返回historyList已经存在的和当前打开的相等的id,如果没有返回-1；
				let index=historyList.findIndex(i=>{
					return i.id==this.detail.id;
				})
				console.log(index);
				//如果存在的话将原来的删除掉，在后边追加新的;
				if(index>=0){
					historyList.splice(index,1);
				}
				
				historyList.unshift(item);
				uni.setStorageSync("historyList",historyList);
			}
		},
	}
</script>

<style lang="scss" scoped>
	.details {
		padding: 20rpx;

		.title {
			font-size: 50rpx;
			font-weight: bold;
			font-family: "Gill Sans", sans-serif;
		}

		.info {
			display: flex;
			background-color: #F6F6F6;
			justify-content: space-between;
			line-height: 60rpx;
			margin: 30rpx 0;

			.author {
				color: #999;
				font-size: 26rpx;
				padding-left: 25rpx;
			}

			.time {
				color: #999;
				font-size: 26rpx;
				padding-right: 25rpx;
			}
		}

		.content {
			padding: 50rpx;
			//富文本中携带的图片等，直接对content类下边的所有img标签进行渲染;
			img{
				width:100%;
			}
			// /deep/ img{
			// 	width: 100%;
			// }推荐使用的渲染方式，加上/deep/
		}

		.description {
			background: #FFD4D4;
			font-size: 26rpx;
			color: #F89898;
			line-height: 1.8rem;
			padding: 20rpx;
		}


	}
</style>
