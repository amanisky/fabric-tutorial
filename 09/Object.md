# fabric.Object 对象
+ 根对象，所有 2d 形状类都继承自它

### 属性
| 属性名 | 默认值 | 类型 | 种类 | 说明 |
| ---- | ---- | ---- | ---- | ----- |
__uid | - | number | static | 唯一ID，当创建 SVG 元素内部使用
NUM_FRACTION_DIGITS | 2 | number | static、constant | 定义序列化对象值时要使用的小数位数
__corner | 0 | number、string、any | - | ...
absolutePositioned | false | boolean | - | 仅当对象用作剪辑路径时才有意义；如果为 true，则 clipPath 将相对于画布顶部和左侧定位，并且不受对象变换的影响；
aCoords | null | object | - | 对象被添加到画布时，该对象的 aCoords 会自动保存四个重要位置点：tl、tr、bl、br；{tl: Point {x: 10, y: 10}, tr: Point {x: 111, y: 10}, br: Point {x: 111, y: 111}, bl: Point {x: 10, y: 111}}； width, height, scaleX, scaleY skewX, skewY, angle, strokeWidth, top, left 属性的改变会影响到该值结果；查看01/01.html
angle | 0 | number | - | 对象旋转的角度（单位：度）
backgroundColor | '' | string | - | 对象的背景颜色（有些对象需要将 fill 设置为 '' 才可以看到）
borderColor | 'rgba(102,153,255,0.75)' | string | - | 当对象被选中时边框的颜色
borderDashArray | null | array | - | 当对象被选中时边框的虚线样式（hasBorder 为 true 才生效）
borderOpacityWhenMoving | 0.4 | number | - | 当选中对象移动时，边框的透明度
borderScaleFactor | 1 | number | - | 对象控制边界的比例因子；修改后会影响活动对象四周的小方块以及边框
cacheProperties | [...] | array | - | 检查缓存是否需要刷新时要考虑的属性列表；需要开启 statefullCache 属性
centeredRotation | true | boolean | - | 如果为 true，则以此对象的中心点作为旋转的原点；如果为 false，则以此对象的左上顶点作为旋转的原点
centeredScaling | false | boolean | - | 如果为 true，则以此对象的中心点作为缩放的原点；
clipPath | undefined | fabric.Object | - | 设置具有其形状的剪切区域；默认以缓存画布的中心作为中心点；如果希望 0,0 的 clipPath 与对象中心对齐，请使用 clipPath.originX / clipPath.originY 设置为 center
clipTo | null | function | - | 剪切对象所使用的函数（案例：http://fabricjs.com/clipping）
cornerColor | 'rgba(102,153,255,0.5)' | string | - | 选中对象四周方框的背景颜色
cornerDashArray | null | array | - | 选中对象四周方框的虚线样式
cornerSize | 13 | number | - | 选中对象四周方框的大小
cornerStrokeColor | null | string | - | 选中对象四周方框的边框颜色（transparentCorners 必须设置为 false）
cornerStyle | 'rect' | string | - | 选中对象四周方框的形态；可选值：'rect'、'circle'
dirty | true | boolean | - | 如果为 true，对象的缓存将在下一次 render 调用时重新渲染
evented | true | boolean | - | 设置为 false 时，对象不能成为事件的目标；所有事件都通过它传播
excludeFromExport | false | boolean | - | 设置为 true 时，对象不会在 OBJECT/JSON 中导出
fill | 'rgb(0,0,0)' | string | - | 设置对象填充的颜色
fillRule | 'nonzero' | string | - | 设置对象填充规则；可选值：'nonzero'、'evenodd'
globalCompositeOperation | 'source-over' | string | - | 设置画布的复合规则
hasBorders | true | boolean | - | 对象被选中时，是否显示控件边框
hasControls | true |  boolean | - | 对象被选中时，是否显示控件；如果为 false，则对象是能拖动，不能缩放、旋转
hasRotatingPoint | true | boolean | - | 对象被选中时，是否显示旋转控件
height | 0 | number | - | 对象的高度
hoverCursor | null | string | - | 鼠标悬停在对象上的默认样式
includeDefaultValues | true | boolean | - | 当 false 时，默认对象的值不包含在其序列化中
inverted | false | boolean | - | 仅当对象用作剪辑路径时才有意义；如果为 true，则会掏空
left | 0 | number | - | 对象的左侧位置；默认情况下它相对于对象 left；可以通过设置 originX: {left/center/right} 来改变默认行为
lockMovementX | false | boolean | - | 当 true 时，对象不可以水平移动
lockMovementY | false | boolean | - | 当 true 时，对象不可以垂直移动
lockRotation | false | boolean | - | 当 true 时，对象不可以旋转
lockScalingFlip | false | boolean | - | 当 true 时，不能通过缩放为负值来翻转对象
lockScalingX | false | boolean | - | 当 true 时，对象水平缩放被锁定
lockScalingY | false | boolean | - | 当 true 时，对象垂直缩放被锁定
lockSkewingX | false | boolean | - | 当 true 时，物体水平扭曲被锁定
lockSkewingY | false | boolean | - | 当 true 时，物体垂直扭曲被锁定
lockUniScaling | false | boolean | - | 当 true 时，对象会等比缩放
matrixCache | null | any | - | 存储对象完整的变换矩阵
minScaleLimit | 0 | number | - | 对象允许缩放的最小值；即缩小多少倍之后不允许再缩小了
moveCursor | null | string | - | 移动对象放下后鼠标的样式
noScaleCache | true | boolean | - | 当为 true 禁用缩放操作的缓存重新生成，避免大缩放的模糊效果
objectCaching | true | boolean | - | 当为 true 对象缓存到一个额外的画布上；那么放大对象时，会导致失真，但缩放结束后会调整清晰；设置为 false，放大不会失真，但是性能不太好
oCoords | null | any | - | 当对象被选中时，9 个方框控件的坐标点；会受到 width, height, scaleX, scaleY skewX, skewY, angle, strokeWidth, viewportTransform, top, left, padding 属性的影响
opacity | 1 | number | - | 对象的透明度
originX | 'left' | string | - | 水平转换对象的原点；可选值：left、center、right
originY | 'top' | string | - | 垂直转换对象的原点；可选值：top、center、bottom
ownMatrixCache | null | any | - | 存储对象本身的矩阵缓存
padding | 0 | number | - | 填充对象与控件之间的间隙（单位：像素）
paintFirst | 'fill' | string | - | 确定是先绘制填充还是描边；可选值：fill（填充）、stroke（描边）
perPixelTargetFind | false | boolean | - | 当设置为 true 时，在每个像素的基础上在画布上"找到"对象，而不是根据边界框
rotatingPointOffset | 40 | number | - | 对象控制旋转点的偏移量
scaleX | 1 | number | - | 对象水平缩放值
scaleY | 1 | number | - | 对象垂直缩放值
selectable | true | boolean | - | 当设置为 false，该对象不能被选中修改；但事件仍然生效
selectionBackgroundColor | '' | string | - | 被选中对象的背景色
shadow | null | fabric.Shadow | - | 对象的阴影
skewX | 0 | number | - | 水平扭曲的角度
skewY | 0 | number | - | 垂直扭曲的角度
statefullCache | false | boolean | - | 当设置为 true，对象属性检查缓存失效
stateProperties | [...] | array | - | 检查对象状态是否已更改时要考虑的属性列表
stroke | null | string | - | 对象描边的颜色
strokeDashArray | [] | array | - | 对象描边的虚线样式
strokeLineCap | 'butt' | string | - | 设置描边每段虚线的呈现样式；可选值：butt、round、square（必须设置虚线才有效；可放大浏览器查看效果）
strokeLineJoin | 'miter' | string | - | 笔划的角落样式；可选值：bevil、round、miter
strokeMiterLimit | 4 | number | - | 笔划的最大斜接长度(strokeLineJoin: 'miter' 才生效) 
strokeWidth | 1 | number | - | 描边宽度
top | 0 | number | - | 对象的顶部位置；默认情况下它相对于对象 top；可以通过设置 originY: {top/center/bottom} 来改变默
transformMatrix | null | array | - | 对象的矩阵数组（类似 SVG 的变换矩阵）
transparentCorners | true | boolean | - | 方框控件是否透明
type | 'object' | string | - | 设置对象的类型；只读不可修改
visible | true | boolean | - | 设置为 false，则对象不渲染到画布上
width | 0 | number | - | 对象的宽度

### 方法
| 方法名 | 参数说明 | 返回值 | 方法说明 |
| - | - | - | - |
_calcRotateMatrix() | - | array | 计算对象的旋转矩阵
_calcTranslateMatrix() | - | array | 计算对象变换的平移矩阵
_limitCacheSize(dims) | {width, height, zoomX, zoomY} | {Object|Object|Object|Object} | 限制缓存尺寸（性能）
_removeCacheCanvas() | - | - | 从对象中删除缓存画布及其尺寸
_renderControls(ctx, styleOverrideopt) | ctx：要渲染的上下文；styleOverrideopt：用于覆盖对象样式的属性(可选) | 渲染对象的控件和边框
_setupCompositeOperation(ctx) | ctx：渲染画布上下文 | - | 为特定对象设置canvas globalCompositeOperation可以使用globalCompositeOperation属性指定特定对象的自定义合成操作
adjustPosition(to) | to 可选值：left、center、right | - | 调整位置
animate(property, value) | property：动画的属性值；value：动画的结束值（支持相对值） | {fabric.Object} | 动画
bringForward(intersectingopt) | intersectingopt：是否相交？如果是 true，则在下一个上方交叉对象前面发送对象 | {fabric.Object} | 将对象向上移动到绘制对象的堆栈中
bringToFront() | - | {fabric.Object} | 将对象移动到绘制对象堆栈的顶部
calcCoords() | - | {Object} | 计算并返回对象的9个控件方框
calcTransformMatrix(skipGroupopt) | skipGroupopt：是否跳过组？可选值：true、false | {Array} | 计算变换表示来自对象属性的当前变换的矩阵
center() | - | {fabric.Object} | 让对象水平、垂直居中；在居中后，您可能需要在对象上调用 setCoords 来更新控件区域
centerH() | - | {fabric.Object} | 让对象水平居中
centerV() | - | {fabric.Object} | 让对象垂直居中
clone(callback, propertiesToIncludeopt) | callback：回调函；propertiesToIncludeopt：另外包含的任何属性 | - | 克隆对象
cloneAsImage(callback, optionsopt) | - | {fabric.Object} | 克隆为图片
complexity() | - | {Number} | 返回实例的复杂性（默认为：1）
containsPoint(point, linesopt, absoluteopt, calculateopt) | - | {Boolean} | 检查点是否在对象内；如果 point 在对象内，则返回 true
drawBorders(ctx, styleOverride) | - | {fabric.Object} | 绘制对象边界框的边框；需要公共属性：width，height；需要公共选项：padding，borderColor
drawBordersInGroup(ctx, options, styleOverride) | - |  {fabric.Object} | 当对象的边界框位于组内时，绘制边框；需要公共属性：width，height；需要公共选项：padding，borderColor
drawCacheOnCanvas(ctx) | - | - | 在目标上下文上绘制对象的缓存副本
drawClipPathOnCache(ctx) | - | - | 执行对象 clipPath 的绘制操作
drawControls(ctx, styleOverride) | - | {fabric.Object} | 绘制对象边界框的角（即9个控件）；需要公共属性：width，height；需要公共选项：cornerSize，padding
drawObject(ctx) | - | - | 对指定上下文中的对象执行绘制操作
drawSelectionBackground(ctx) | - | {fabric.Object} | 在对象后面，在其选择边框内绘制彩色图层
fxStraighten(callbacks) | - | {fabric.Object} | 整理了一下一个对象(从当前角度旋转的0,90,180,270,等根据近)带动画效果
getBoundingRect(absoluteopt, calculateopt) | - | {Object} | 返回对象的边界矩形的坐标(左,上,宽度、高度)盒子的态度作为轴对齐的画布
getCenterPoint() | - | {fabric.Point} | 返回对象的真正的中心坐标
getCoords() | - | - | 返回4个重要控件的坐标点
getLocalPointer(e, pointeropt) | - | {Object} | 返回指针相对于物体的坐标
getObjectOpacity() | - | {Number} | 获取对象的透明度值
getObjectScaling() | - | {Object} | 获取对象水平和垂直的缩放值
getPointByOrigin(originX, originY) | - | {fabric.Point} | 获取相对原点的坐标点
getScaledHeight() | - | {Number} | 获取缩放后的高度值
getScaledWidth() | - | {Number} | 获取缩放后的宽度值
getSvgCommons() | - | {String} | 获取输出的 SVG 的 ID 值
getSvgFilter() | - | {String} | 获取 SVG 的过滤器
getSvgSpanStyles(style, useWhiteSpace) | - | {String} | 获取 SVG 容器指定的样式值
getSvgStyles(skipShadow) | - | {String} | 获取 SVG 的样式
getSvgTextDecoration(style) | - | {String} | 获取 SVG 文件的  text-decoration 属性值
getSvgTransform(use) | - | {String} | 获取 SVG Transform 值
getSvgTransformMatrix() | - | {String} | 获取单个元素 SVG 转换矩阵
getTotalObjectScaling() | - | {Object} | 获取对象比例因子
getViewportTransform() | - | {Boolean} | 获取视口转换
hasStateChanged(propertySetopt) | - | {Boolean} | 是否改变了对象的状态
initialize(optionsopt) | - | - | 构造函数
intersectsWithObject(other, absoluteopt, calculateopt) | - | {Boolean} | 检查对象是否与另一个对象相交（重叠）
intersectsWithRect(pointTL, pointBR, absoluteopt, calculateopt) | - | {Boolean} | 检查对象是否与由2个点形成的区域相交
isCacheDirty(skipCanvas) | - | {Boolean} | 检查缓存是否脏了
isContainedWithinRect(pointTL, pointBR, absoluteopt, calculateopt) | - | {Boolean} | 检查对象是否完全包含在由2个点组成的区域内
isControlVisible(controlName) | - | {Boolean} | 检查指定的控件是否可见
isOnScreen(calculateopt) | - | {Boolean} | 使用当前viewportTransform检查画布中是否包含对象，检查是否在屏幕上显示的第一个点停止
isPartiallyOnScreen(calculateopt) | - | {Boolean} | 使用当前viewportTransform检查对象是否部分包含在画布中
isType(type) | - | {Boolean} | 判断对象是否是指定的类型
moveTo(index) | - | {fabric.Object} | 将对象移动到绘制对象堆栈中的指定级别
needsItsOwnCache() | - | - | 当设置为 "true" 时，强制对象拥有自己的缓存，即使它在组中，当对象在缓存上以特定方式运行并且始终需要自己的孤立画布才能正确呈现时，可能需要它
onDeselect(optionsopt) | - | - | 当丢弃活动对象或设置活动对象时该函数会被执行
onSelect(optionsopt) | - | - | 当丢弃活动对象或设置活动对象时该函数会被执行
render(ctx) | - | - | 在指定的上下文中渲染对象
rotate(angle) | - | {fabric.Object} | 设置对象以中心点的旋转角度
saveState(optionsopt) | - | {fabric.Object} | 保存对象的状态
scale(value) | - | {fabric.Object} | 缩放对象（包括水平和垂直方向）
scaleToHeight(value, absolute) | - | {fabric.Object} | 将对象缩放到指定高度
scaleToWidth(value, absolute) | - | {fabric.Object} | 将对象缩放到指定高度
sendBackwards(intersectingopt) | - | {fabric.Object} | 将对象向下移动到绘制对象的堆栈中
sendToBack() | - | {fabric.Object} | 将对象移动到绘制对象堆栈的底部
setColor(color) | - | {fabric.Object} | 等价于 set('fill', 'red')，用指定颜色填充对象
setControlsVisibility(optionsopt) | - | {fabric.Object} | 设置对象被选中时，哪些控件可见
setControlVisible(controlName, visible) | - | {fabric.Object} | 设置对象被选中时，指定控件的可见性
setCoords(ignoreZoomopt, skipAbsoluteopt) | - | {fabric.Object} | 根据当前角度，宽度和高度设置控件位置坐标
setGradient(property, optionsopt) | - | {fabric.Object} | 设置渐变
setOnGroup() | - | - | ...
setOptions(optionsopt) | - | - | 设置对象的属性
setPatternFill(options, callbackopt) | - | {fabric.Object} | 设置对象的填充图案
setPositionByOrigin(pos, originX, originY) | - | {void} | 设置对象的位置，同时考虑对象的原点
setShadow(optionsopt) | - | {fabric.Object} | 设置对象的阴影
setupState(optionsopt) | - | {fabric.Object} | 设置对象的状态
shouldCache() | - | {Boolean} | 对象是否需要缓存；
straighten() | - | {fabric.Object} | 拉直物体（将其从当前角度旋转到0,90,180,270等之一，具体取决于哪个更接近）
toClipPathSVG(reviveropt) | - | {String} | 返回实例的svg clipPath表示形式
toDatalessObject(propertiesToIncludeopt) | - | {Object} | 返回实例的更少数据对象表示
toDataURL(options) | - | {String} | 返回实例的 data-url-like 的字符串表示形式
toJSON(propertiesToIncludeopt) | - | {Object} | 返回实例的 JSON 表示形式
toLocalPoint(point, originX, originY) | - | {fabric.Point} | 返回本地坐标中的点
toObject(propertiesToIncludeopt) | - | {Object} | 返回实例的对象表示形式
toString() | - | {String} | 返回实例的字符串表示形式
toSVG(reviveropt) | - | {String} | 返回实例的 svg 表示形式
transform(ctx) | - | - | 渲染对象时转换上下文
translateToCenterPoint(point, originX, originY) | - | {fabric.Point} | 将坐标从原点坐标转换为中心坐标（基于对象的尺寸）
translateToGivenOrigin(point, fromOriginX, fromOriginY, toOriginX, toOriginY) | - |  {fabric.Point} | 将坐标从一组原点转换为另一个原点（基于对象的尺寸）
translateToOriginPoint(center, originX, originY) | - | {fabric.Point} | 将坐标从中心坐标转换为原点坐标（基于对象的尺寸）
viewportCenter() | - | {fabric.Object} | 在最后添加它的画布的当前视口上的中心对象。 在居中后，您可能需要在对象上调用 setCoords 来更新控件区域
viewportCenterH() | - | {fabric.Object} | 视口水平居中
viewportCenterV() | - | {fabric.Object} | 视口垂直居中
willDrawShadow() | - | {Boolean} | 是否画阴影
