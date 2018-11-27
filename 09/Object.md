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
clipTo | null | function | - | ...
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
objectCaching | true | boolean | - | 当为 true 对象缓存到一个额外的画布上
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
transformMatrix | null | array | - | 转换矩阵
transparentCorners | true | boolean | - | 方框控件是否透明
type | 'object' | string | - | 设置对象的类型；只读不可修改
visible | true | boolean | - | 设置为 false，则对象不渲染到画布上
width | 0 | number | - | 对象的宽度