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
			<view v-if="Object.keys(warbookLev2).length>0">
				已选大兵书：<br>
				<button size="mini" type="primary">{{warbookLev2.Name}}</button>
			</view>
			<view v-if="Object.keys(warbookLev3).length>0">
				已选小兵书：
				<button size="mini" type="primary" v-for="item in warbookLev3">
					{{item.Name}}
				</button>
			</view>
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
				warBookMap: Map,

				//临时数据
				warbookLev2: {},
				warbookLev3: [],
			}
		},
		methods: {
			//判断是否选择
			isSelected(lev, id) {
				switch (lev) {
					case 2:
						this.warbookLev2.Id = id
						return true
					case 3:
						if (Object.keys(this.warbookLev3).length == 0) {
							return false
						}
						for (var i = 0; i < this.warbookLev3.length; i++) {
							if (this.warbookLev3[i].Id == id) {
								return true
							}
						}
					default:
						return false
				}
			},
			//选择大兵书
			selectWarbookLev2(data) {
				this.warbookLev2 = data

			},
			//选择小兵书
			selectWarbookLev3(data) {
				if (this.warbookLev3.length >= 2) {
					uni.showToast({
						icon: "error",
						title: "小兵书最多可选择2个"
					})
					return
				}
				this.warbookLev3.push(data)
			},
			submit(data) {
				uni.$emit('selectedGeneralData', data)
				uni.navigateBack()
			},
			setWarbookType(data) {
				this.searchWarbookType = data
				this.queryWarbookList()
			},
			queryWarbookList() {
				let that = this
				if (this.searchWarbookType == 0) {
					//默认
					this.searchWarbookType = 1
				}
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
						// console.log(that.warBookMap)
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

	.selected {
		background-color: yellowgreen;
	}
</style>