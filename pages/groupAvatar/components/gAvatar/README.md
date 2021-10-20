# GAvatar

### 基础用法

```html
<g-avatar
		:images="images"
		:border-width="6"
		:avatar-size="40"
		background-color="#0c0c0c"
		:avatar-reverse="true"
		@loaded="getImage"
/>
```

```js
export default{
  data(){
    return {
      images: []
    }
  },
  methods: {
    getImage(base64){
      console.log(base64)
    }
  }
}
```



### Attributes

| 参数             | 说明                                                   | 类型    | 可选值 | 默认值  |
| ---------------- | ------------------------------------------------------ | ------- | ------ | ------- |
| images           | 头像数组                                               | Array   |        | []      |
| background-color | 头像背景色                                             | String  |        | #ffffff |
| avatar-reverse   | 不满三个的行显示在上面还是在下面，默认在上面（同微信） | Boolean |        | true    |
| border-width     | 边框宽度                                               | Number  |        | 2       |
| avatar-size      | 每个头像的尺寸                                         | Number  |        | 30      |

### Events

| 事件名称 | 说明                        | 回调参数  |
| -------- | --------------------------- | --------- |
| loaded   | canvas 转换为 base64 后触发 | base64 值 |

