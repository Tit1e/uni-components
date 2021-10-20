<template>
    <canvas
        :style="{height: canvasSize + 'px', width: canvasSize + 'px'}"
        :canvas-id="canvasId"
        :id="canvasId"
    >
    </canvas>
</template>

<script>
    export default {
        props: {
            // 不满三个的行显示在上面还是在下面，默认在上面（同微信）
            avatarReverse: {
                type: Boolean,
                default: true
            },
            // 头像数组
            images: {
                type: Array,
                default: () => ([])
            },
            // 头像背景色
            backgroundColor: {
                type: String,
                default: '#ffffff'
            },
            // 边框宽度
            borderWidth: {
                type: Number,
                default: 2
            },
            // 每个头像的尺寸
            avatarSize: {
                type: Number,
                default: 30
            }
        },
        data() {
            // 如果同时渲染多个，会出现 id 重复问题，所以 加上时间戳跟随机数
            const now = (+new Date() + Math.random().toFixed(4) * 10000)
            return {
                canvasId: `__myCanvas${now}`,
                avatarArray: [],
                colNumber: 3
            }
        },
        computed: {
            canvasSize() {
                return this.avatarSize * 3 + this.borderWidth * 4
            },
            avatarSize2() {
                return (this.canvasSize - this.borderWidth * 3) / 2
            },
            pointMap() {
                // 这里的 1，2，3 为每行 / 每列的数组长度
                return {
                    1: (this.canvasSize - this.avatarSize) / 2,
                    2: (this.canvasSize - (this.avatarSize * 2 + this.borderWidth)) / 2,
                    3: this.borderWidth
                }
            }
        },
        created() {
            this.init()
        },
        mounted() {
            this.drawAvatar()
        },
        methods: {
            drawAvatar() {
                const ctx = uni.createCanvasContext(this.canvasId, this)
                ctx.setFillStyle(this.backgroundColor)
                ctx.fillRect(0, 0, this.canvasSize, this.canvasSize)

                for (let i = 0; i < this.avatarArray.length; i++) {
                    const item = this.avatarArray[i]
                    // 按九宫格分的情况
                    if (this.colNumber === 3) {
                        const colStart = this.pointMap[this.avatarArray.length]
                        const rowStart = this.pointMap[item.length]
                        for (let v = 0; v < item.length; v++) {
                            ctx.drawImage(
                                item[v],
                                rowStart + (this.avatarSize + this.borderWidth) * v, colStart + (this.avatarSize + this
                                    .borderWidth) * i, this.avatarSize, this.avatarSize)
                        }
                    }
                    // 按4宫格分的情况
                    if (this.colNumber === 2) {
                        for (let v = 0; v < item.length; v++) {
                            ctx.drawImage(
                                item[v],
                                this.borderWidth + (this.borderWidth + this.avatarSize2) * i,
                                this.borderWidth + (this.borderWidth + this.avatarSize2) * v,
                                this.avatarSize2,
                                this.avatarSize2)
                        }
                    }
                }
                ctx.draw(true, ret => {
                    // #ifdef APP-PLUS
                    uni.canvasToTempFilePath({
                        x: 0, // 起点坐标
                        y: 0,
                        width: this.canvasSize, // canvas 宽
                        height: this.canvasSize, // canvas 高
                        canvasId: this.canvasId, // canvas id
                        success: res => {
                            const savedFilePath = res.tempFilePath // 相对路径
                            const path = plus.io.convertLocalFileSystemURL(savedFilePath) // 绝对路径
                            const fileReader = new plus.io.FileReader()
                            fileReader.readAsDataURL(path)
                            fileReader.onloadend = (res) => { // 读取文件成功完成的回调函数
                                this.$emit('loaded', res.target.result)
                            }
                        }
                    })
                    // #endif
                })
            },
            init() {
                const images = this.images.slice(0, 9)
                this.avatarArray = this.splitArray(this.avatarReverse ? images.reverse() : images)
            },
            splitArray(data) {
                if (data.length === 4) {
                    this.colNumber = 2
                }
                const result = []
                for (let i = 0, len = data.length; i < len; i += this.colNumber) {
                    result.push(data.slice(i, i + this.colNumber))
                }
                return this.avatarReverse ? result.reverse() : result
            }
        }
    }
</script>

<style>
</style>
