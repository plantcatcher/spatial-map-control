# Spatial Map Control

基于 Google MediaPipe 的手势识别空间交互地图系统。通过摄像头实时捕捉手势，实现对天地图的平移、缩放、点击等操作，无需触摸屏幕。

Demo网址链接：[Spatial Map Control](https://spactrl.planetgis.cn/)

## 功能特性

- 实时手部关键点检测（21 个 3D 地标点）
- 实时面部网格检测（468 个关键点）
- 手势驱动地图交互，支持 5 种操作手势
- 天地图矢量/影像底图切换
- 摄像头预览面板，可随时开启/关闭
- 全屏沉浸式暗色界面

## 手势操作说明

| 手势                        | 操作      | 说明                                 |
| --------------------------- | --------- | ------------------------------------ |
| 伸出食指                    | 光标移动  | 只有食指伸出时，光标跟随手指移动     |
| 拇指 + 食指捏合后拖动       | 地图平移  | 捏合后移动手来拖动地图               |
| 拇指 + 中指捏合             | 点击选择  | 捏合即触发，选中地图上的标记点       |
| 双手拇指食指捏合后远离/靠近 | 放大/缩小 | 两只手都捏合后，远离放大、靠近缩小   |
| 张开手掌 → 握拳             | 缩小地图  | 组合手势：先张开手掌再握拳，触发缩小 |

## 技术栈

- **手势识别**: [MediaPipe Hands](https://google.github.io/mediapipe/solutions/hands.html) / [MediaPipe Face Mesh](https://google.github.io/mediapipe/solutions/face_mesh.html)
- **地图引擎**: [Leaflet.js](https://leafletjs.com/)
- **地图底图**: [天地图](https://www.tianditu.gov.cn/) 矢量底图 + 影像底图

## 快速开始

### 1. 获取天地图 API Token

本项目使用天地图作为地图底图，你需要先申请自己的 Token：

1. 前往 [天地图开发者平台](https://console.tianditu.gov.cn/) 注册账号
2. 创建应用，选择「浏览器端」类型
3. 获取生成的 Token

### 2. 替换 Token

打开 `index.html`，找到以下代码并替换为你的 Token：

```javascript
const tdtToken = 'YOUR_TIANDITU_TOKEN'; // 请替换为你自己的天地图 API Token
```

### 3. 启动项目

本项目是纯前端项目，无需安装依赖。用任意 HTTP 服务器打开即可：

```bash
# 方式一：Python
python -m http.server 8080

# 方式二：Node.js
npx serve .

# 方式三：直接用浏览器打开
# 双击 index.html 即可（部分浏览器可能限制摄像头权限）
```

### 4. 使用

1. 点击「启动系统」按钮
2. 允许浏览器访问摄像头
3. 将手放在摄像头前，伸出食指即可看到光标
4. 按照手势指南进行地图操作

## 项目结构

```
├── index.html          # 主页面（包含所有 HTML / CSS / JavaScript）
```

单文件架构，所有代码集中在一个 HTML 文件中，无需构建工具。

## 浏览器兼容性

需要支持 `getUserMedia` API 的现代浏览器：

- Chrome 90+
- Edge 90+
- Firefox 88+
- Safari 15+

## 注意事项

- 需要摄像头设备，并授予浏览器摄像头权限
- 手势识别依赖 Google CDN 加载 MediaPipe 模型，首次加载需要网络连接
- 天地图 Token 有每日调用次数限制，个人开发者配额通常足够使用
- 建议在光线充足的环境下使用，手势识别效果更佳

## License

MIT
