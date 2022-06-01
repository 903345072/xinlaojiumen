<template>
	<view>
		<view style="position: relative;left: 0;right: 0;height: 400rpx;background-image: linear-gradient(90deg, #6bb4f9, #f70af4);">
			<view v-if="orderdetail.flag==0" @click="close()" class="cuIcon-close"
							style="position: absolute;left: 30rpx; top:30rpx;font-size: 40rpx;color: white;"></view>
						<view v-if="orderdetail.flag==1" @click="goBack()" class="cuIcon-back"
							style="position: absolute;left: 30rpx; top:30rpx;font-size: 40rpx;color: white;"></view>
		        <view style="text-align: center;padding: 30rpx 0;font-size: 35rpx;color: white;">订单详情</view>
				<view style="display: flex;align-items: center;justify-content: space-around;width: 100%;color: white;">
								<view
									style="display: flex;flex-direction: column;justify-content: center;align-items: center;line-height: 50rpx;">
									<view style="font-size: 35rpx;">{{orderdetail.award_money>0?orderdetail.award_money:'暂无'}}</view>
									<view style="font-size: 28rpx;">中奖金额</view>
								</view>
				
								<view
									style="display: flex;flex-direction: column;justify-content: center;align-items: center;line-height: 50rpx;">
									<view style="font-size: 35rpx;">{{orderdetail.en_state}}</view>
									<view style="font-size: 28rpx;">订单状态</view>
								</view>
				
								<view
									style="display: flex;flex-direction: column;justify-content: center;align-items: center;line-height: 50rpx;">
									<view style="font-size: 35rpx;">{{orderdetail.amount}}</view>
									<view style="font-size: 28rpx;">投注金额</view>
								</view>
				 </view>
		</view>
		
		<view style="display: flex;flex-direction: column;align-items: center;margin-top: -150rpx;z-index: 999999999;position: relative;">
			<view
							style="background-color: white;padding: 20rpx 20rpx;width: 90%;border-radius: 20rpx;">
							<footdetail v-if="orderdetail.type=='foot'" :orderdetail="orderdetail"></footdetail>
							<basketdetail v-if="orderdetail.type=='basket'" :orderdetail="orderdetail"></basketdetail>
			</view>
			
			<view
							style="background-color: white;padding: 20rpx 20rpx;width: 90%;border-radius: 20rpx;color: grey;line-height: 60rpx;margin: 30rpx 0;">
							<view style="display: flex;align-items: center;justify-content: space-between;">
								<text style="color: #000000;font-size: 32rpx;">订单信息</text>
			
							</view>
			
							<view style="display: flex;align-items: center;justify-content: space-between;">
								<view>订单编号</view>
								<view style="color: #323232;">{{orderdetail.order_no}}</view>
							</view>
			
							<view style="display: flex;align-items: center;justify-content: space-between;">
								<view>付款时间</view>
								<view style="color: #323232;">{{orderdetail.order_time}}</view>
							</view>
							<view style="display: flex;align-items: center;justify-content: space-between;">
								<view>出票时间</view>
								<view style="color: #323232;">{{orderdetail.tick_time}}</view>
			
							</view>
			
							<view style="display: flex;align-items: center;justify-content: space-between;">
								<view>截止时间</view>
								<view style="color: #323232;">{{orderdetail.stop_time}}</view>
							</view>
			
			
						</view>
						
						<view
										style="background-color: white;padding: 20rpx 20rpx;width: 90%;border-radius: 20rpx;color: grey;line-height: 60rpx;position: relative;margin-bottom: 140rpx;">
										<view style="display: flex;align-items: center;justify-content: space-between;">
											<text style="color: #000000;font-size: 32rpx;">彩票照片</text>
						
										</view>
										<view>
											<image :src="config.config.url+orderdetail.order_pic"></image>
										</view>
						
						
						
									</view>
			
		</view>
	</view>
	
</template>

<script>
	import footdetail from '@/components/zaiui-common/basics/footdetail';
	import basketdetail from '@/components/zaiui-common/basics/basketdetail';
	import config from '@/api/interface.js'
	import barTitle from '@/components/zaiui-common/basics/bar-title';
	export default {
		name: "orderdetail",
		components: {
			footdetail,
			basketdetail,
			barTitle
		},
		computed: {
			scrollH: function() {
				let sys = uni.getSystemInfoSync();
				let winWidth = sys.windowWidth;
				let winrate = 750 / winWidth;
				let winHeight = parseInt(sys.windowHeight * winrate)

				return winHeight

			}
		},

		data() {
			return {
				order: {},
				config: "",
				pageHeight: 0

			}
		},
		props: {
			orderdetail: null
		},
		created() {
			this.config = config
		},
		onLoad(option) {

		},
		methods: {
			close() {
				this.$emit("closeWindow")
			},
			goBack() {
				uni.navigateTo({
					url: "/pages/app/index"
				})
			}
		}
	}
</script>