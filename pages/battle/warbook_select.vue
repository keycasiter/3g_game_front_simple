<template>
	<view class="container">
		<view class="type">
			<button size="mini" type="primary" plain @click="setWarbookType(1)">作战</button>
			<button size="mini" type="primary" plain @click="setWarbookType(2)">军形</button>
			<button size="mini" type="primary" plain @click="setWarbookType(3)">虚实</button>
			<button size="mini" type="primary" plain @click="setWarbookType(4)">九变</button>
		</view>
		<view class="list">
			<view v-if="Object.keys(warBookMap).length > 0 && warBookMap[2].length>0">
				大兵书
				<view v-for="item in warBookMap[2]">
					<button size="mini" type="primary" plain @click="selectWarbookLev2(item)">{{item.Name}}</button>
				</view>
			</view>
			<view v-if="Object.keys(warBookMap).length > 0  && warBookMap[3].length>0">
				小兵书
				<view v-for="item in warBookMap[3]">
					<button size="mini" type="primary" plain @click="selectWarbookLev3(item)">{{item.Name}}</button>
				</view>
			</view>
		</view>
		<view class="show">
			已选：
			<view v-if="Object.keys(warbookData[2]).length>0">
				大兵书：
				<button size="mini" type="primary">{{warbookData[2].name}}</button>
			</view>
			<view v-if="Object.keys(warbookData[3]).length>0">
				小兵书：
				<button size="mini" type="primary" v-for="item in warbookData[3]">
					{{item.name}}
				</button>
			</view>
		</view>
		<view class="btn">
			<button size="mini" type="primary" plain @click="reset">重置</button>
			<button size="mini" type="primary" plain @click="submit">提交</button>
		</view>
	</view>
	</view>
</template>

<script>
	export default {
		onLoad(data) {
			this.generalIndex = data.generalIndex
			this.generalId = data.generalId

			//默认兵书类型
			this.searchWarbookType = 1
			this.warbookData[1] = this.searchWarbookType
		},
		onShow() {
			this.queryWarbookList()
		},
		data() {
			return {
				//传递参数
				generalIndex: 0,
				warbookData: {
					//兵书类型
					"1": 0,
					//大兵书
					"2": {},
					//小兵书
					"3": []
				},

				//查询数据
				generalId: 0,
				searchWarbookType: 0,
				warBookMap: Map,
			}
		},
		methods: {
			//选择大兵书
			selectWarbookLev2(data) {
				this.warbookData[2].id = data.Id
				this.warbookData[2].name = data.Name
				this.$forceUpdate()
			},
			//选择小兵书
			selectWarbookLev3(data) {
				if (this.warbookData[3].length >= 2) {
					uni.showToast({
						icon: "error",
						title: "小兵书最多可选择2个"
					})
					return
				}
				this.warbookData[3].push({
					id: data.Id,
					name: data.Name
				})
				this.$forceUpdate()
			},
			setWarbookType(data) {
				this.searchWarbookType = data
				this.warbookData[1] = data
				this.queryWarbookList()
			},
			queryWarbookList() {
				let that = this
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
						that.warBookMap = res.data.WarBookMapList[this.searchWarbookType]
					}
				});
				this.$forceUpdate()
			},
			reset() {
				this.warbookData[1] = 0
				this.warbookData[2] = {}
				this.warbookData[3] = []
			},
			submit() {
				// console.log(" this.warbookData:" + JSON.stringify(this.warbookData))
				uni.$emit('selectWarbookData', this.warbookData)
				uni.navigateBack()
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		margin-top: 180rpx;
	}

	.selected {
		background-color: yellowgreen;
	}
</style>