<template>
	<view class="container">
		<view class="input">
			<input @input="onInput" :value="searchGeneralName" confirm-type="search" placeholder="请输入武将名" /><button
				size="mini" type="primary" plain @click="queryGeneralList">搜索</button>
		</view>
		<view>
			<button size="mini" type="primary" plain @click="setGeneralGroup(1)">魏</button>
			<button size="mini" type="primary" plain @click="setGeneralGroup(2)">蜀</button>
			<button size="mini" type="primary" plain @click="setGeneralGroup(3)">吴</button>
			<button size="mini" type="primary" plain @click="setGeneralGroup(4)">群</button>
		</view>
		<view class="list">
			<view v-for="item in generalListData">
				<button size="mini" type="primary" plain @click="selectGeneral(item)">{{item.BaseInfo.Name}}</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad(data) {
			// console.log(data)
			this.teamType = data.teamType
			this.generalIndex = data.generalIndex
		},
		onShow() {
			this.queryGeneralList()
		},
		data() {
			return {
				//传递参数
				teamType: 0,
				generalIndex: 0,

				//查询数据
				searchGeneralName: "",
				searchGeneralGroup: 0,
				generalListData: []
			}
		},
		methods: {
			onInput(e) {
				this.searchGeneralName = e.detail.value
			},
			setGeneralGroup(data) {
				this.searchGeneralGroup = data
				this.queryGeneralList()
			},
			selectGeneral(data) {
				uni.$emit('selectTeamType', this.teamType)
				uni.$emit('selectGeneralIndex', this.generalIndex)
				uni.$emit('selectGeneralData', data)
				uni.navigateBack()
			},
			queryGeneralList() {
				uni.request({
					url: 'http://3game.tech/v1/general/query',
					method: 'GET',
					header: {
						'Content-Type': 'application/json',
					},
					data: {
						Group: this.searchGeneralGroup,
						Name: this.searchGeneralName,
						PageNo: 1,
						PageSize: 500
					},
					success: res => {
						// console.log(res)
						this.generalListData = res.data.GeneralList
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

		.list {
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
		}
	}
</style>