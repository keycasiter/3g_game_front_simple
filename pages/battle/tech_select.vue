<template>
	<view class="container">
		<view class="input">
			<input @input="onInput" :value="searchTechName" confirm-type="search" placeholder="请输入特技名" /><button
				size="mini" type="primary" plain @click="queryTechList">搜索</button>
		</view>
		<view>
			<button size="mini" type="primary" plain @click="setTechType(1)">武器</button>
			<button size="mini" type="primary" plain @click="setTechType(2)">防具</button>
			<button size="mini" type="primary" plain @click="setTechType(3)">坐骑</button>
			<button size="mini" type="primary" plain @click="setTechType(4)">宝物</button>
		</view>
		<view class="list" v-for="item in TechListData">
			<button size="mini" type="primary" plain @click="selectTech(item)">{{item.Name}}</button>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad(data) {

		},
		onShow() {
			this.queryTechList()
		},
		data() {
			return {
				//查询数据
				searchTechName: "",
				searchTechType: 0,
				TechListData: []
			}
		},
		methods: {
			onInput(e) {
				this.searchTechName = e.detail.value
			},
			setTechType(data) {
				this.searchTechType = data
				this.queryTechList()
			},
			selectTech(data) {
				uni.$emit('selectedGeneralData', data)
				uni.navigateBack()
			},
			queryTechList() {
				uni.request({
					url: 'http://3game.tech/v1/special_tech/query',
					method: 'GET',
					header: {
						'Content-Type': 'application/json',
					},
					data: {
						Type: this.searchTechType,
						Name: this.searchTechName,
						PageNo: 1,
						PageSize: 500
					},
					success: res => {
						console.log(res)
						this.TechListData = res.data.SpecialTechList
					}
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		margin-top: 180rpx;

		.input {
			display: flex;
			flex-direction: row;
		}
	}
</style>