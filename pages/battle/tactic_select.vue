<template>
	<view class="container">
		<view class="input">
			<input @input="onInput" :value="searchTacticName" confirm-type="search" placeholder="请输入战法名" /><button
				size="mini" type="primary" plain @click="queryTacticList">搜索</button>
		</view>
		<view>
			<button size="mini" type="primary" plain @click="setTacticType(1)">主动</button>
			<button size="mini" type="primary" plain @click="setTacticType(2)">被动</button>
			<button size="mini" type="primary" plain @click="setTacticType(3)">指挥</button>
			<button size="mini" type="primary" plain @click="setTacticType(4)">突击</button>
			<button size="mini" type="primary" plain @click="setTacticType(5)">阵法</button>
			<button size="mini" type="primary" plain @click="setTacticType(6)">兵种</button>
		</view>
		<view class="list" v-for="item in tacticListData">
			<button size="mini" type="primary" plain @click="selectTactic(item)">{{item.Name}}</button>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad(data) {
			this.generalIndex = data.generalIndex
			this.tacticIndex = data.tacticIndex
		},
		onShow() {
			this.queryTacticList()
		},
		data() {
			return {
				//传递参数
				generalIndex: 0,
				tacticIndex: 0,

				//查询数据
				searchTacticName: "",
				searchTacticType: 0,
				tacticListData: []
			}
		},
		methods: {
			onInput(e) {
				this.searchTacticName = e.detail.value
			},
			setTacticType(data) {
				this.searchTacticType = data
				this.queryTacticList()
			},
			selectTactic(data) {
				uni.$emit('selectGeneralIndex', this.generalIndex)
				uni.$emit('selectTacticIndex', this.tacticIndex)
				uni.$emit('selectTacticData', data)
				uni.navigateBack()
			},
			queryTacticList() {
				uni.request({
					url: 'http://3game.tech/v1/tactic/query',
					method: 'GET',
					header: {
						'Content-Type': 'application/json',
					},
					data: {
						Type: this.searchTacticType,
						Name: this.searchTacticName,
						Sources: [2, 3],
						PageNo: 1,
						PageSize: 500
					},
					success: res => {
						console.log(res)
						this.tacticListData = res.data.TacticList
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