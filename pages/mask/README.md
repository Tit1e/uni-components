# MASK

## 使用方式
1. 将 mask.nvue 复制到自己的项目中
2. 在 pages.json 中添加下面代码
```json
{
    "path": "pages/mask/mask",
    "style": {
        "navigationStyle": "custom",
        "app-plus": {
            "animationType": "none",
            "background": "transparent",
            "popGesture": "none"
        }
    }
}
```
3. 使用前注意判断用户是否支持指纹 / Face ID，以及此功能是否开启