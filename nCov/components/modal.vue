<template>
	<view>
		<view class="cu-modal" :class="modalName==true?'show':''">
			<view class="cu-dialog">
				<view class="cu-bar bg-white justify-end">
					<view class="content">{{modalcontent.title}}</view>
					<view class="action" v-on:tap="toexplain">
						<text class="cuIcon-close text-red"></text>
					</view> 
				</view>
				<view class="padding-xl text-gray">
					{{modalcontent.text}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"modal",
		props:[
			'modalName',
			'modalcontent'
		],
		data() {
			return {
				
			};
		},
		methods:{
			toexplain(){
				this.$emit('toexplain')
			}
		}
	}
</script>

<style>

</style>
