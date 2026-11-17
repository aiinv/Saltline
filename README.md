# Saltline（盐线）

单文件 WebGL 第一人称射击游戏。基于 Three.js r180，所有模型、纹理与音效均为程序化生成，无外部资源请求。

## 在线玩

| 版本 | 链接 |
| --- | --- |
| 原版 | https://aiinv.github.io/Saltline/ |
| 低延时版 | https://aiinv.github.io/Saltline/lowlatency.html |
| 低延时版 + 一键性能模式 | https://aiinv.github.io/Saltline/lowlatency.html?fast=1 |

原版保留原始渲染逻辑，低延时版降低了默认 high 档负载、加快动态分辨率收敛、减少阴影更新频率，并新增 `?fast=1`。

## 模型检视页（九个入口）

在任意版本地址后追加 `?show=<模块名>`，即可绕过游戏流程，直接进入对应模块的独立展示场景。例如：

```
https://aiinv.github.io/Saltline/?show=mats
https://aiinv.github.io/Saltline/lowlatency.html?show=mats
```

九个入口如下：

| 入口 | 展示内容 | 常用附加参数 |
| :--- | :--- | :--- |
| `?show=mats` | **材质库**：以球体、地面、立方体三种载体陈列程序化材质（金属、油漆、木材、混凝土、玻璃、网布等），含贴花预览 | `&only=paint_red,steel`<br>按材质名筛选，逗号分隔 |
| `?show=props` | **场景道具**：集装箱（20 尺／40 尺／高柜）、隔离墩、灯杆、发电机、垃圾箱、工具车，按尺寸自动排布 | `&names=container20,light_mast`<br>按道具名筛选 |
| `?show=enemies` | **敌人单位**：机械猎犬与机械飞鸥的静态、巡逻、战斗姿态 | `&eshow=gull\|hound`<br>另有 `fight\|dead\|both`，默认 `both` |
| `?show=weapon` | **武器检视**：盐线九式突击步枪的侧面／右侧／顶部／手部／枪口／瞄具／下挂分解视角，以及开火／换弹／空仓／瞄准／冲刺动作 | `&wpose=hip\|ads\|fire\|reload`<br>另有 `&wt=`、`&cam=`、`&fov=`、`&exposure=` |
| `?show=fx` | **特效演示**：爆炸、火花、烟尘、弹孔与命中反馈，可冻结逐帧观察 | `&fxshow=<类型>`、`&fxage=<秒>`、`&fxsize=<倍率>`<br>默认 `all` |
| `?show=render` | **渲染管线**：粗糙度／金属度渐变材质球与测试几何体，观察色调映射、阴影与后处理效果 | `&cam=`、`&fov=`、`&exposure=` |
| `?show=ground` | **地面系统**：沥青、混凝土、积水等程序化地面与参考道具组合 | `&cam=`、`&exposure=` |
| `?show=backdrop` | **远景与天空**：起重机、货轮、疏散艇、天空盒四个独立镜头 | `&bshow=crane\|ship`<br>另有 `boat\|sky`，默认 `crane` |
| `?show=level` | **完整关卡**：集装箱堆场、仓库、码头与中继站的整场景，可观察布局与动态更新 | `&cam=`、`&fov=` |

### 检视页参数速查（完整枚举）

- **敌人** `&eshow=`：`gull`（飞鸥）｜`hound`（猎犬）｜`fight`（战斗）｜`dead`（死亡）｜`both`（默认）
- **武器** `&wpose=`：`hip`（默认）｜`ads`｜`fire`｜`reload`｜`empty`｜`sprint`｜`side`｜`right`｜`top`｜`hands`｜`rhand`｜`muzzle`｜`optic`｜`lower`；另有 `&wt=<秒>`、`&cam=x,y,z,tx,ty,tz`、`&fov=N`、`&exposure=N`
- **特效** `&fxshow=`：默认 `all`；`&fxage=<秒>`、`&fxsize=<倍率>` 控制爆炸帧与规模
- **远景** `&bshow=`：`crane`（默认）｜`ship`｜`boat`｜`sky`

说明：这些页面是只读检视场景，不加载玩家、任务与 HUD；参数与游戏本体完全兼容，可与 `&q=`、`&bench=`、`&noaudio=1` 等组合使用。模块名区分大小写，必须使用表中给出的小写形式。

## 操作（游戏本体）

- 点击画面锁定鼠标；`WASD` 移动，鼠标瞄准，左键射击，`Shift` 冲刺
- `Esc` 释放鼠标；设置中可调整灵敏度、视角反转、音量、FOV 与全屏
- 支持触屏虚拟摇杆与手柄
- 任务目标：切断堆场、仓库、码头三处上行中继，最后前往撤离艇

## 可用 URL 参数

| 参数 | 作用 |
| --- | --- |
| `?fast=1` | 低延时版专属：低画质 + 关体积光/AO/辉光 + 关动态分辨率 + 像素比上限 1 |
| `?show=<模块>` | 进入上表所列的模型检视页 |
| `?q=low\|medium\|high\|ultra` | 指定画质档位 |
| `?tex=256` | 缩小程序化纹理尺寸 |
| `?vol=0` / `?ao=0` / `?bloom=0` | 关闭体积光 / AO / 辉光 |
| `?post=0` | 关闭整条后处理链，延迟最低、画质下降明显 |
| `?dynres=0` | 关闭动态分辨率，锁定当前分辨率 |
| `?dpr=N` | 设置设备像素比上限（低延时版专属，默认 2） |
| `?noaudio=1` | 跳过音频合成 |
| `?bench` | 显示性能测试面板（帧时间、GPU、draw call） |

参数可组合，例如：`?fast=1&bench`、`?q=medium&dynres=0`、`?show=enemies&eshow=fight`。

## 浏览器要求

需要支持 WebGL2 的桌面浏览器（Chrome / Edge 推荐）。首次点击画面后才会锁定鼠标并启动音频，这是浏览器的自动播放策略要求。若设备有独立显卡，建议在浏览器系统设置中指定高性能 GPU。
