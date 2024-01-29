<template>
	<view class="container">
		<view>
			<button size="mini" type="primary" plain @click="setWarbookType(1)">作战</button>
			<button size="mini" type="primary" plain @click="setWarbookType(2)">军形</button>
			<button size="mini" type="primary" plain @click="setWarbookType(3)">虚实</button>
			<button size="mini" type="primary" plain @click="setWarbookType(4)">九变</button>
		</view>
		<view>
			大兵书
			<view v-for="item in warBookMapList[2]">
				<button size="mini" type="primary" plain>{{item.Name}}</button>
			</view>
			小兵书
			<view v-for="item in warBookMapList[3]">
				<button size="mini" type="primary" plain>{{item.Name}}</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad(data) {
			this.generalIndex = data.generalIndex
			this.generalId = data.generalId
		},
		onShow() {
			this.queryWarbookList()
		},
		data() {
			return {
				//传递参数
				generalIndex: 0,

				//查询数据
				generalId: 0,
				searchWarbookType: 0,
				warBookMapList: []
			}
		},
		methods: {
			setWarbookType(data) {
				this.searchWarbookType = data
				this.queryWarbookList()
			},
			selectWarbook(data) {
				uni.$emit('selectedGeneralData', data)
				uni.navigateBack()
			},
			queryWarbookList() {
				uni.request({
					url: 'http://3game.tech/v1/general_warbook/query',
					method: 'GET',
					header: {
						'Content-Type': 'application/json',
					},
					data: {
						GeneralId: this.generalId,
						WarbookType: this.searchWarbookType
					},
					success: res => {
						console.log("warbook res:" + JSON.stringify(res))
						this.warBookMapList = res.data.WarBookMapList[1]
					}
				});
				this.$forceUpdate()
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		margin-top: 180rpx;
	}
</style>