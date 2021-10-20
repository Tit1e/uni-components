<template>
    <view>
        <view style="display: flex; flex-wrap: wrap;">
            <view class="flex-item">
                <g-avatar
                    class="g-canvas"
                    :images="images.slice(0,3)"
                    :border-width="6"
                    :avatar-size="40"
                    background-color="#0c0c0c"
                    :avatar-reverse="true"
                    @loaded="getImage"
                />
            </view>
            <view class="flex-item">
                <g-avatar
                    class="g-canvas"
                    :images="images.slice(0,4)"
                    :border-width="6"
                    :avatar-size="40"
                    background-color="#0c0c0c"
                    :avatar-reverse="true"
                    @loaded="getImage"
                />
            </view>
            <view class="flex-item">
                <g-avatar
                    class="g-canvas"
                    :images="images.slice(0,5)"
                    :border-width="6"
                    :avatar-size="40"
                    background-color="#0c0c0c"
                    :avatar-reverse="true"
                    @loaded="getImage"
                />
            </view>
            <view class="flex-item">
                <g-avatar
                    class="g-canvas"
                    :images="images.slice(0,6)"
                    :border-width="6"
                    :avatar-size="40"
                    background-color="#0c0c0c"
                    :avatar-reverse="true"
                    @loaded="getImage"
                />
            </view>
            <view class="flex-item">

                <g-avatar
                    class="g-canvas"
                    :images="images.slice(0,7)"
                    :border-width="6"
                    :avatar-size="40"
                    background-color="#0c0c0c"
                    :avatar-reverse="true"
                    @loaded="getImage"
                />
            </view>
            <view class="flex-item">

                <g-avatar
                    class="g-canvas"
                    :images="images.slice(0,8)"
                    :border-width="6"
                    :avatar-size="40"
                    background-color="#0c0c0c"
                    :avatar-reverse="true"
                    @loaded="getImage"
                />
            </view>
            <view class="flex-item">
                <g-avatar
                    class="g-canvas"
                    :images="images.slice(0,9)"
                    :border-width="6"
                    :avatar-size="40"
                    background-color="#0c0c0c"
                    :avatar-reverse="true"
                    @loaded="getImage"
                />
            </view>
        </view>
        <view class="base64">
            {{base64Image}}
        </view>
    </view>
</template>

<script>
    import gAvatar from './components/gAvatar/gAvatar.vue.vue'
    export default {
        components: {
            gAvatar
        },
        data() {
            return {
                images: [],
                length: 3,
                base64Image: ''
            }
        },
        onLoad() {
            this.setImages()
        },
        methods: {
            setImages() {
                this.images = new Array(9).fill(
                    'https://personal-1251959693.cos.ap-chengdu.myqcloud.com/2021-10-19-tom.png'
                    )
            },
            getImage(url) {
                this.base64Image = url
            }
        }
    }
</script>

<style lang="scss">
    .flex-item{
        width: 50%;
        flex-shrink: 0;
        margin-top: 20px;
    }
    .g-canvas{
        margin: 0 auto;
    }

    .base64 {
        word-wrap: break-word;
        padding: 10px;
        height: 200px;
        overflow: auto;
        margin: 10px;
        border: 1px solid #EAEAEA;
    }
</style>
