<template>
	<view class="home">
		<scroll-view scroll-x class="navscroll">
			<view class="item" :class="index==curIndex?'active':''" @click="changeIndex(index,nameItem.id)"
				v-for="(nameItem,index) in navArr" :key="nameItem.id">
				{{nameItem.classname}}
			</view>
		</scroll-view>
		<view class="content">
			<Newbox v-for="newBoxItem in newsList" :key="newBoxItem.id" :newsItem="newBoxItem"
				@click.native="goDetails(newBoxItem)"></Newbox>
		</view>
		<view class="loading" v-if="newsList.length">
			<view class="data-loading" v-show="loadState==1">数据加载中...</view>
			<view class="no-data-loading" v-show="loadState==2">没有数据了...</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				curIndex: 0,
				navArr: [],
				newsList: [],
				currentPage: 1,
				loadState:0,//0代表不显示，1代表加载中，2代表没有数据了
			}
		},

		onReachBottom() {
			if(this.loadState==2){
				return;//如果已经到底了就不要再继续向服务器请求数据了;
			}
			this.currentPage++; //触底之后进行一次页码的++;
			this.getNewsData();
			this.loadState=1;
			
		},

		methods: {
			changeIndex(index, id) {
				this.curIndex = index;
				this.currentPage = 1;
				this.newsList = [];
				this.loadState=0;//切换到其他页面的时候重置加载状态；
				this.getNewsData(id);
			},

			//跳转到详情页
			goDetails(item) {
				uni.navigateTo({
					// url: "/pages/details/details",
					url:`/pages/details/details?cid=${item.classid}&id=${item.id}` 
				})
			},

			//获取导航栏列表数据
			getNavData() { //id默认是50；
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/navlist.php",
					success: res => {
						this.navArr = res.data;
					},
					fail: res => {},
				})
			},

			//获取新闻列表数据
			getNewsData(id = 50) {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/newslist.php",
					data: {
						cid: id,
						page: this.currentPage,
					},
					success: res => {
						if(res.data.length<=0){
							this.loadState=2;
						}
						this.newsList = [...this.newsList, ...res.data]; //将新老数据进行拼接,将老数组和新数组分别进行解构;
					},
					fail: res => {
					}
				})
			}
		},

		onLoad() {
			this.getNavData();
			this.getNewsData();
		}

	}
</script>

<style lang="scss" scoped>
	.navscroll {
		white-space: nowrap;
		background: #f7f8fa;
		height: 100rpx;
		position: fixed;
		top:var(--window-top);
		left:0;
		z-index:10;
		// top: var(--window-top);
		// left: 0;
		// z-index: 10;

		// top: 1;
		/deep/::-webkit-scrollbar {
			width: 4px !important;
			height: 1px !important;
			overflow: auto !important;
			background: transparent !important;
			-webkit-appearance: auto !important;
			display: block;
		}
	}
	
	.content{
		padding-top:100rpx;
	}

	.item {
		background-color: #f7f8fa;
		display: inline-block;
		line-height: 100rpx;
		padding: 0 40rpx;
		font-size: 36rpx;
		color: #333;
	}

	.active {
		color: #55A5E0;
	}
	
	.loading{
		text-align: center;
		font-size:26rpx;
		color:#888;
		line-height: 1.5rem;
	}
</style>
