<template>
	<view class="container">
		<view class="input">
			<input @input="onInput" :value="searchTechName" confirm-type="search" placeholder="请输入特技名" /><button
				size="mini" type="primary" plain @click="queryTechList">搜索</button>
		</view>
		<view class="type">
			<button size="mini" type="primary" plain @click="setTechType(1)">武器</button>
			<button size="mini" type="primary" plain @click="setTechType(2)">防具</button>
			<button size="mini" type="primary" plain @click="setTechType(3)">坐骑</button>
			<button size="mini" type="primary" plain @click="setTechType(4)">宝物</button>
		</view>
		<view class="list">
			<view v-for="item in techListData">
				<button size="mini" type="primary" plain @click="selectTech(item)">{{item.Name}}</button>
			</view>
		</view>
		已选特技：
		<view class="selected">
			<view v-for="item in selectedTechData">
				{{item.Name}}
			</view>
		</view>
		<view>
			<button size="mini" type="primary" plain @click="reset()">重置</button>
			<button size="mini" type="primary" plain @click="submit()">提交</button>
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
				//选择特技
				selectedTechData: [],
				//查询数据
				searchTechName: "",
				searchTechType: 0,
				techListData: []
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
				this.selectedTechData.push(data)
			},
			reset() {
				this.selectedTechData = []
			},
			submit() {
				uni.$emit('selectTechData', this.selectedTechData)
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
						this.techListData = res.data.SpecialTechList
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

		.type {
			border: 1rpx solid #CCC;
		}

		.list {
			display: flex;
			flex-direction: row;
			flex-wrap: wrap
		}

		.selected {
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
			color: blue
		}
	}
</style>