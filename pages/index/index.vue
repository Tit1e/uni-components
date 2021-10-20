<template>
	<view class="content">
        <view class="list-item" @click="toPage('/pages/groupAvatar/groupAvatar')">
            群聊头像
        </view>
        <view class="list-item" @click="toPage('/pages/mask/mask')">
            应用锁
        </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		onLoad() {

		},
		methods: {
            toPage(url) {
                uni.navigateTo({
                    url
                })
            }
		}
	}
</script>

<style lang="scss" scoped>
    .content{
        padding: 20px;
        .list-item{
            padding: 10px;
            text-align: center;
            background-color: #eaeaea;
            border-radius: 4px;
            & + .list-item{
                margin-top: 10px;
            }
        }
    }
</style>
