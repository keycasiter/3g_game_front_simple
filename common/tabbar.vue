<template>
	<view class="tabbar">
		<view class="tabbar-list">
			<view class="tabbar-list-ul">
				<view class="tabbar-list-li" v-for="(item,index) in tabBar.list" :key="index"
					@click="setSelected(index)">
					<view class="tabbar-list-li-icon">
						<image :src="selected == index ? item.selectedIconPath : item.iconPath" mode=""></image>
					</view>
					<view class="selected == index ? 'tabbar-list-li-name active' : 'tabbar-list-li-name'">
						{{item.text}}
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: ['selected'],
		data() {
			return {
				tabBar: {
					list: [{
							text: '首页',
							iconPath: '/static/icon_5.png',
							selectedIconPath: '/static/icon_5_selected.png',
							pagePath: '/pages/index/index'
						},
						{
							text: '对战',
							iconPath: '/static/icon_4.png',
							selectedIconPath: '/static/icon_4_selected.png',
							pagePath: '/pages/battle/index'
						},
						{
							text: '开荒',
							iconPath: '/static/icon_3.png',
							selectedIconPath: '/static/icon_3_selected.png',
							pagePath: '/pages/openup/index'
						},
						{
							text: '攻略',
							iconPath: '/static/icon_1.png',
							selectedIconPath: '/static/icon_1_selected.png',
							pagePath: '/pages/strategy/index'
						},
						{
							text: '我的',
							iconPath: '/static/icon_2.png',
							selectedIconPath: '/static/icon_2_selected.png',
							pagePath: '/pages/me/index'
						}
					]
				}
			}
		},
		methods: {
			setSelected(index) {
				uni.switchTab({
					url: this.tabBar.list[index].pagePath
				})
			}
		}
	}
</script>

<style scoped>
	.tabbar {
		width: 100%;
		position: fixed;
		box-sizing: border-box;
	}

	.tabbar-list {
		width: 100%;
		color: #344356;
		background: #FFFFFF;
		position: fixed;
		left: 0;
		bottom: 0;
		box-shadow: 0px -12px 37px 0px;
		border-top-left-radius: 30rpx;
		border-top-right-radius: 30rpx;
		box-sizing: border-box;
	}

	.tabbar-list-ul {
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: space-around;
		align-items: center;
		box-sizing: border-box;
	}

	.tabbar-list-li-icon {
		width: 56rpx;
		height: 56rpx;
		margin: 0 auto;
		padding: 20rpx 0;
	}

	.tabbar-list-li-icon image {
		width: 56rpx;
		height: 56rpx;
	}

	.tabbar-list-li-name {
		width: 100%;
		height: 40rpx;
		text-align: center;
		line-height: 40rpx;
		font-size: 28rpx;
		font-family: Microsoft Yahei;
	}

	.active {
		color: #1296db;
	}
</style>