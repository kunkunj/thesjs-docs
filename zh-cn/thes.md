## Example

```
const th = new Thes({
  el: document.body,
  view: 800,
  sceneName: 'scene1',
  width: window?.innerWidth,
  height: window?.innerHeight,
  background: 'rgb(255,255,0)',
});
```

## options

Thes 的 option 参数，使用 new Thes(options)创建一个渲染器。

`object` `必填`

| Name                 | Type                                      | Description                                                                                                                                                                                           |        |
| -------------------- | :---------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| el                   | HTMLElement                               | 需要挂载的 dom 节点，全屏的话传入 document.body                                                                                                                                                       | `必填` |
| view                 | number                                    | 视野宽广，越大视野越广，默认 200                                                                                                                                                                      | `可选` |
| camera               | [CameraType](/zh-cn/thes?id=cameratype)   | 相机参数详见相机相关，不填默认`OrthographicCamera`                                                                                                                                                    | `可选` |
| width                | number                                    | 容器宽，不填默认 window.innerWidth                                                                                                                                                                    | `可选` |
| height               | number                                    | 容器高，不填默认 window.innerHeight                                                                                                                                                                   | `可选` |
| sceneName            | string                                    | 场景名称，不填按照创建的 id 拼接 scene，例：scene1、scene2                                                                                                                                            | `可选` |
| lights               | [PointType](/zh-cn/thes?id=pointtype)     | 点光源，不填有默认                                                                                                                                                                                    | `可选` |
| ambientLight         | [AmbientType](/zh-cn/thes?id=ambienttype) | 环境光，指默认下所有模型的初始颜色，不填有默认                                                                                                                                                        | `可选` |
| background           | string/string[]                           | 渲染器背景，传`color`只能传`rgb`色值，可以传一个`图片地址`作为背景，也可以传入一个`图片数量为6的数组`,表示`上下左右前后`<br />的`VR`视野（仅当 camera 为`PerspectiveCamera`时有效），不传默认黑色背景 | `可选` |
| backgroundBlurriness | number                                    | 模糊度：0-1                                                                                                                                                                                           | `可选` |

### CameraType

Thes 的 option 参数内的 camera 相机参数详情;

`object` `可选`

| Name                     | Type   | Description                                                                                                              |        |
| ------------------------ | ------ | ------------------------------------------------------------------------------------------------------------------------ | ------ |
| type                     | string | 相机类型，可选参数`OrthographicCamera`/`CubeCamera`/`PerspectiveCamera`。可不传 camera，只要传了，此参数必传             | `必填` |
|                          |        | 正交相机（`OrthographicCamera`）: 在这种投影模式下，无论物体距离相机距离远或者近，在最终渲染的图片中物体的大小都保持不变 | `必填` |
|                          |        | 立方相机（`CubeCamera`）: threejs 中的 CubeCamera                                                                        | `必填` |
|                          |        | 透视相机（`PerspectiveCamera`）: 这一投影模式被用来模拟人眼所看到的景象，它是 3D 场景的渲染中使用得最普遍的投影模式。    | `必填` |
| position                 | object | 相机的位置。可不传 camera，只要传了，此参数必传                                                                          | `必填` |
|                          |        | `x:number`相机的 x 方向上的位置                                                                                          | `必填` |
|                          |        | `y:number`相机的 y 方向上的位置                                                                                          | `必填` |
|                          |        | `z:number`相机的 z 方向上的位置                                                                                          | `必填` |
| PerspectiveCameraOption  | object | 当 type 为`PerspectiveCamera`时，配置相机的参数                                                                          | `可选` |
|                          |        | `fov: number` 摄像机视锥体垂直视野角度，从视图的底部到顶部，以角度来表示。默认值是**50**。                               | `可选` |
|                          |        | `aspectRatio: number` 摄像机视锥体长宽比，通常是使用画布的宽/画布的高。默认值是**1**（正方形画布）。                     | `可选` |
|                          |        | `near: number` 摄像机视锥体近端面，默认值是**0.1**                                                                       | `可选` |
|                          |        | `far: number` 摄像机视锥体远端面，默认值是**2000**。                                                                     | `可选` |
| OrthographicCameraOption | object | 当 type 为`OrthographicCamera`时，配置相机的参数                                                                         | `可选` |
|                          |        | `near: number` 摄像机视锥体近端面，默认值是**0.1**                                                                       | `可选` |
|                          |        | `far: number` 摄像机视锥体远端面，默认值是**2000**。                                                                     | `可选` |
| CubeCameraOption         | object | 当 type 为`CubeCamera`时，配置相机的参数                                                                                 | `可选` |
|                          |        | `near: number` 摄像机视锥体近端面，默认值是**0.1**                                                                       | `可选` |
|                          |        | `far: number`摄像机视锥体远端面，默认值是**2000**。                                                                      | `可选` |
|                          |        | `renderTarget`:[Thes.createWebGLCubeRenderTarget]()                                                                      | `可选` |

### PointType

Thes 的 option 参数内的 lights 光源参数详情;

`object` `可选`

| Name                | Type   | Description                                                                                                               |        |
| ------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------- | ------ |
| type                | string | 光源类型，可选参数`PointLight`/`RectAreaLight`/`SpotLight`。可不传 lights，只要传了，此参数必传                           | `必填` |
|                     |        | 点光源（`PointLight`）: 从一个点向各个方向发射的光源。一个常见的例子是模拟一个灯泡发出的光。                              | `必填` |
|                     |        | 平面光光源（`RectAreaLight`）: 平面光光源从一个矩形平面上均匀地发射光线。这种光源可以用来模拟像明亮的窗户或者条状灯光光源 | `必填` |
|                     |        | 聚光灯（`SpotLight`）: 光线从一个点沿一个方向射出，随着光线照射的变远，光线圆锥体的尺寸也逐渐增大。                       | `必填` |
| position            | object | 光源位置。可不传 lights，只要传了，此参数必传                                                                             | `必填` |
|                     |        | `x:number`光源的 x 方向上的位置                                                                                           | `必填` |
|                     |        | `y:number`光源的 y 方向上的位置                                                                                           | `必填` |
|                     |        | `z:number`光源的 z 方向上的位置                                                                                           | `必填` |
| PointLightOption    | object | 当 type 为`PointLight`时，配置光源的参数                                                                                  | `可选` |
|                     |        | `color:string`只能传`rgb`色值                                                                                             | `可选` |
|                     |        | `intensity: number` 光照强度。 默认值 1。                                                                                 | `可选` |
|                     |        | `distance: number` 这个距离表示从光源到光照强度为 0 的位置。 当设置为 0 时，光永远不会消失(距离无穷大)。默认值 0.         | `可选` |
|                     |        | `decay: number` 沿着光照距离的衰退量。默认值 2。                                                                          | `可选` |
| RectAreaLightOption | object | 当 type 为`RectAreaLight`时，配置光源的参数                                                                               | `可选` |
|                     |        |                                                                                                                           |        |
|                     |        |                                                                                                                           |        |
|                     |        | `near: number` 摄像机视锥体近端面，默认值是**0.1**                                                                        | `可选` |
|                     |        | `far: number` 摄像机视锥体远端面，默认值是**2000**。                                                                      | `可选` |
| SpotLightOption     | object | 当 type 为`SpotLight`时，配置光源的参数                                                                                   | `可选` |
|                     |        | `near: number` 摄像机视锥体近端面，默认值是**0.1**                                                                        | `可选` |
|                     |        | `far: number`摄像机视锥体远端面，默认值是**2000**。                                                                       | `可选` |
|                     |        | `renderTarget`:[Thes.createWebGLCubeRenderTarget]()                                                                       | `可选` |

### AmbientType

Thes 的 option 参数内的 ambientLight 环境光参数详情;

`object` `可选`

| Name      | Type   | Description     |
| --------- | ------ | --------------- |
| color     | string | 只能传`rgb`色值 |
| intensity | number | 光照强度        |

## member

### opt

Thes 初始化时传入的 options

`object` `readonly`

### scene

Thes 当前使用的 threejs 的原生场景对象，当 [useScene(sceneBox)](/zh-cn/thes?id=usescenescenebox)后，会动态切换。

`Object3D`

### sceneBox

Thes 当前使用的场景对象，当 [useScene(sceneBox)](/zh-cn/thes?id=usescenescenebox)后，会动态切换

- `.camera`：当前场景下的相机对象，为 threejs 原生对象
- `.cid`：当前场景的唯一自增 id
- `.name`：当前场景的名称
- `.opt`：当前场景的初始化 options
- `.scene`：当前场景下的 threejs 原生场景对象

### camera

Thes 的相机对象，为 threejs 原生对象

`Object3D`

### control

Thes 的动作控制对象，为 threejs 的原生对象

`Object3D`

- `.enabled`：鼠标控制是否可用，默认为 true
- `.target`：聚焦坐标，[Thes.createVector3]()
- `.minDistance`：最小相机移动距离，默认 0，仅`PerspectiveCamera`相机有效
- `.maxDistance`：最大相机移动距离，默认 Infinity，仅`PerspectiveCamera`相机有效
- `.minZoom`：最小鼠标缩放大小，默认 0，仅`OrthographicCamera `相机有效
- `.maxZoom`：最大鼠标缩放大小，默认 Infinity，仅`OrthographicCamera `相机有效
- `.maxPolarAngle`：最大仰视角度，默认 0
- `.maxZoom`：最大俯视角度，默认 Math.PI
- `.minAzimuthAngle`：最小水平方向视角限制，默认\-Infinity
- `.maxAzimuthAngle`：最小水平方向视角限制，默认 Infinity
- `.enableDamping`：是否开启惯性滑动，默认 true
- `.zoomSpeed`：惯性滑动速度，默认 1
- `.enableRotate`：是否可旋转，默认 true
- `.rotateSpeed`：旋转速度，默认 1
- `.enablePan`：是否可平移，默认 true
- `.keyPanSpeed`：平移速度，默认 0.1px
- `.autoRotate`：是否自动旋转，默认 false
- `.autoRotateSpeed`：自动旋转速度，默认 2，每秒 30 圈
- `.enableKeys`：是否能使用键盘，默认 true
- `.keys`：键盘控制上下左右的键，默认 LEFT: 37, UP: 38, RIGHT: 39, BOTTOM: 40
- `.mouseButtons`：鼠标点击按钮，默认 ORBIT: [Thes.MOUSE.LEFT](), ZOOM: [Thes.MOUSE.MIDDLE](), PAN: [Thes.MOUSE.RIGHT]()

### events

Thes 的事件开关,使用 on 注册后就会打开，off 注销后则会关闭

`object` `readonly`

### renderer

Thes 当前的渲染器，为 threejs 原生对象

### scenes

Thes 一个 sceneBox 集合，[useScene(sceneBox)](/zh-cn/thes?id=usescenescenebox)必须是这其中的某一个场景对象

`array` `readonly`

## methods

### createScene(options)

在渲染器中再新增一个场景，新增的场景会放到[scenes](/zh-cn/thes?id=scenes)中，

参数：

- `options`：`require` 同[Thes 的 options](/zh-cn/thes?id=options)

示例：

1. 创建一个渲染器

```
const th = new Thes({
  el: document.body
});
th.add(...)
```

2. 创建第二个场景

```
const th2 = th.createScene({
  el: document.body
});
th2.add(...)
```

### useScene(sceneBox)

从当前场景切换到 sceneBox 场景。

参数：

- `sceneBox`：`require` .createScene()的返回结果

示例：

```
//渲染器
const th = new Thes({
  el: document.body
});
//第二个场景
const th2 = th.createScene({
  el: document.body
});
//在第二个场景加入模型
th2.add(...)
//切换到第二个场景
th.useScene(th2)
```

### add(con,sceneBoxId)

往场景加入一个[模型]()、一个[组]()或者一个[外部模型]()

参数：

- `con`：`require` 一个模型对象
- `sceneBoxId`：场景的唯一自增 cid

### setHDRbackground(url)

设置 HDR 模型背景，应用于 vr 效果

参数：

- `url`: `require` HDR 文件地址

### setFPS(geometry)

把对象模型作为第一人称对象，用于 FPS 操作

参数：

- `geometry`: `require` 模型对象

示例：

```
const th = new Thes({
  el: document.body
});
const geo = Thes.createGeometry({
    geometry: 'box',
    material: 'basic',
    position: [0, 0, 0],
});
th.setFPS(geo)
```

### on(event,callback)

注册一个监听事件[event](/zh-cn/thes?id=events-1)

参数：

- `event`: `require` 事件名称
- `callback`: `require` 回调函数

示例：

```
const th = new Thes({
  el: document.body
});

th.on('loaded',() => {
    alert('初始化完毕')
})
```

### off(event)

注销一个事件[event](/zh-cn/thes?id=events-1)

参数：

- `event`: `require` 事件名称

示例：

```
const th = new Thes({
  el: document.body
});

th.on('click',(e) => {
   console.log(e)
})

th.off('click')
```

### flyTo(option)

相机飞到某个位置

参数：

- `option`: `object`

  | Name | Type   | Description    |        |
  | ---- | ------ | -------------- | ------ |
  | x    | number | x 方向上的位置 | `必填` |
  | y    | number | y 方向上的位置 | `必填` |
  | z    | number | z 方向上的位置 | `必填` |
  | time | number | 飞行过程时间   | `可选` |

### lookAt(option)

相机朝着某个一个模型或者某一个方向

参数：

- `option`: `object`或者`模型对象`，当为 object 时，必须是{position:[x,y,z]}格式

示例：

```
const th = new Thes({
    el: document.body
});

//创建模型
const geo = Thes.createGeometry({
    geometry: 'box',
    material: 'basic',
    position: [0, 0, 0],
});

//以模型为目标
th.lookAt(geo)

//以某一位置为目标
th.lookAt({
    position:[0,0,0]
})

```

### moveAt(geometry,view,distance,cb)

第三人称跟随模型运动

参数：

- `geometry`: `require` 跟随中的模型对象
- `view`: 跟随中的视角高度
- `distance`: 跟随中的跟随点距离，移动一次为一个点
- `cb`: 跟随中的实时位置回调,返回两个值，`point`是当前物体运动到的位置,`firstExcute`是追随临界值，可配合`.flyTo`平滑过渡

示例：

```
const th = new Thes({
    el: document.body
});
const geo = Thes.createGeometry({
    geometry: 'box',
    material: 'basic',
    position: [0, 0, 0],
});
//运动
geo.moveTo([
    { x: 365, y: 32, z: 150, time: 1000, deg: Math.PI / 2 },
    { x: 0, y: 32, z: 150, time: 10000, deg: -Math.PI / 2 },
    { x: 0, y: 32, z: -100, time: 5000, deg: Math.PI / 2 },
    { x: -350, y: 32, z: -100, time: 9000, deg: -Math.PI / 2 },
]);
//平滑过渡，这里Y和moveAt的view参数保持一致
th.flyTo({x: -50, y: 100, z: 0, time: 1786})
//跟随
th.moveAt(geo,100,100,(point)=>{
	//可得到firstExcute，然后配置th.flyTo(firstExcute)平滑过渡
	//例：得到firstExcute:{date: 1786,point: {x: -50, y: 0, z: 0, line: 1}}
})

```

### setCenter()

全局切换视图中心,把所有的场景中心焦点都设置

参数:

- `x`:`require` x坐标
- `y`:`require` y坐标
- `z`:`require` z坐标

### getCenter()

获取当前焦点中心，格式为[x,y,z]

### getGPSCenter()

在切换为GPS模式后，该方法获取获取当前GPS中心，格式为[x,y,z]

返回：

- `isGps`: 是否开始GPS坐标
- `GPScenter`: GPS坐标
- `MercatorCenter`: 墨卡托坐标

### closeGPScenter()

关闭GPS坐标模式

### clear()

情况渲染器
