# Fabric
+ 是一个画布库；Fabric在canvas元素之上提供交互式对象模型 Fabric 还具有 SVG-to-canvas（和 canvas-to-SVG）解析器
+ 可以方便的创建几何图形
+ 绘制几百或上千路径组成的复杂形状
+ 加载图片，并将滤镜应用于图片
+ 渐变处理
+ 添加文本并动态操作其大小，对齐方式，字体系列和其他属性
+ 动画
+ 组：可以将对象组合在一起，并同时对其进行操作
+ 可以为任何对象添加阴影
+ 限制拖动区域
+ 翻转、锁定移动方向，缩放等
+ 广泛的事件系统
+ 使用模式填充其内容
+ 可以将对象剪切为任何形状
+ Canvas 可以序列化为 JSON 或 SVG，并可以随时恢复
+ 自由绘图
+ 方便扩展

# Fabric 对象缓存
+ 它是如何工作的？
  + 当布料对象缓存处于活动状态时，您在画布上绘制的对象实际上预先绘制在另一个较小的 offscren(画面以外的) 画布上，与对象像素尺寸本身一样大。在 render 方法中，这个预先绘制的画布通过 drawImage 操作被复制到主画布上。
  + 这意味着在拖动、旋转、扭曲、缩放操作期间，对象不会在画布上重绘，而只是在屏幕上绘制其复制的缓存图像。
+ 如何调整/定制它
  + objectCaching 
    + 默认值：true；则表示对象被缓存在另一个画布上
  + statefullCache
    + 默认值：false
    + 当为 true 时，将检查对象属性缓存是否失效
    + 在某些特定情况下（喷刷，非常大的路径组，组），您可能希望禁用此选项
    + 如果您的应用程序不允许您修改组的子对象属性，组可以禁用此选项
  + noScaleCache 
    + 默认值：true
    + 禁用缩放操作的缓存重新生成，避免大缩放的模糊效果
  + cacheProperties
    + 默认值：["fill", "stroke", "strokeWidth", "strokeDashArray", "width", "height", "stroke", "strokeWidth", "strokeDashArray", "strokeLineCap", "strokeLineJoin", "strokeMiterLimit", "fillRule", "backgroundColor"]
    + 检查缓存是否需要刷新时要考虑的属性列表；需要开启 statefullCache 属性
    + 当调用 set（key，value）时，都会在此属性数组中搜索 key，如果找到了 key，则将对象标记为需要重新渲染
  + stateProperties
    + 默认值：["top", "left", "width", "height", "scaleX", "scaleY", "flipX", "flipY", "originX", "originY", "transformMatrix", "stroke", "strokeWidth", "strokeDashArray", "strokeLineCap", "strokeLineJoin", "strokeMiterLimit", "angle", "opacity", "fill", "globalCompositeOperation", "shadow", "clipTo", "visible", "backgroundColor", "skewX", "skewY", "fillRule", "paintFirst"]
    + 检查对象状态是否已更改时要考虑的属性列表
  + dirty
    + 默认值：true
    + 在下一个渲染方法中强制对象的缓存重新渲染，并在缓存重新生成后自动设置为 false
  + needsItsOwnCache
    + 默认值：是一个函数，返回 false；即：function() { return false; } 
    + 当返回 true 时，强制对象拥有自己的缓存
    + 即使它在一个组内，当你的对象在缓存上以特定方式运行并且总是需要它自己的孤立画布来正确渲染时，它可能是需要的
  + fabric.perfLimitSizeTotal = 2097152;
    + 生成的缓存画布的像素区域的最大尺寸
  + fabric.maxCacheSideLimit = 4096;
    + 生成的缓存画布的最大边的限制
    + IE 将最大值修复为 5000
  + fabric.minCacheSideLimit = 256;
    + 生成的缓存画布的最小边的限制
+ 什么时候使用新版本更新缓存？
  + 设置对象属性
  + 如果该属性在 cacheProperties 数组中时，该对象和组都会标记为脏
  + 如果该属性在 stateProperties 数组中时，则只标记组为脏
+ 如何检查自定义子类以及属性的变化？
  + statefullCache 属性设置为 true
  + 可以将自定义属性添加到 cacheProperties 属性数组中
  + 

# 第一部分
+ 01、使用 canvas 画矩形 vs fabric 画矩形
  + fabric.Canvas
+ 02、使用 canvas 画矩形并旋转45° vs fabric 画矩形并旋转45°
+ 03、跟踪画布状态
  + 如果要移动矩形，需要先擦除以前绘制的内容，然后在新位置绘制矩形
  + 使用 Fabric，不再需要在尝试"修改"任何内容之前删除内容
  + fabric 实现方式：rect.set({ left: 20, top: 50 }); canvas.renderAll();
+ 04、Fabric 中提供了 7 种基本形状
  + fabric.Circle     圈
  + fabric.Ellipse    椭圆
  + fabric.Line       线
  + fabric.Polygon    多边形
  + fabric.Polyline   折线
  + fabric.Rect       矩形
  + fabric.Triangle   三角形
+ 05、通过 set 更改对象
  + 定位：left、top
  + 尺寸：width、height
  + 装饰：fill、opacity、stroke、strokeWidth
  + 缩放：scaleX、scaleY
  + 旋转：angle
  + 反转：flipX、flipY
  + 扭曲: skewX、skewY
+ 06、get -> get* 获取配置
  + get('width')
  + getWidth()
  + 矩形默认值
    + 位置：0 0、宽度：0、高度：0、背景：rgb(0, 0, 0)、无边框、透明度为：1
+ 07、层次结构与继承
  + Fabric 对象不仅彼此独立存在。它们形成了非常精确的层次结构
  + 大多数对象都继承自根 fabric.Object
    + fill、width、height、top 等属性继承自 fabric.Object
  + 如果您想在所有对象上使用 getAngleInRadians 方法，则只需在 fabric.Object.prototype上创建它，即：fabric.Object.prototype.getAngleInRadians = function() { return this.get('angle') / 180 * Math.PI; };
+ 08、fabric.Canvas
  + fabric.Canvas 充当 canvas 元素的包装器，负责管理该特定画布上的所有结构对象
    + 它接受一个元素的 id，并返回 fabric.Canvas 的实例
    + 传递第二个参数可以对画布进行设置；或不传之后通过 set 追加配置也可以
  + 通过 add 方法添加对象
  + 通过 remove 方法删除对象
  + 通过 item(index) 获取对象
  + getObjects() 获取所有对象
+ 09、初始化就有互动
  + 通过 fabric.Canvas（'...'）初始化画布，可以选择对象，拖动、缩放或旋转它们，甚至可以组合起来操作一个块
  + canvas.selection = false; 禁用组选择
  + rect.set('selectable', false) 禁止选择
+ 10、初始化不要互动
  + fabric.StaticCanvas
+ 11、将文档中的图片添加到画布中
  + fabric.Image
+ 12、通过 url 将图片添加到画布中
  + fabric.Image.fromURL  
    + scaleToWidth
+ 13、根据路径画图
  + fabric.Path
  + 手工创建路径不方便
  + M：移动到（moveto）
  + L：画直线到（lineto）
  + C：立方贝塞尔
  + Z：闭合路径
+ 总结
  + abric.loadSVGFromString、fabric.loadSVGFromURL
  + 方法来加载整个SVG文件，并让 Fabric 的 SVG 解析器完成其遍历所有 SVG 元素并创建相应 Path 对象的工作  
  + fabric.Path 通常代表 SVG 中的 path 元素
  + fabric.Group 代表 SVG 文档中经常出现的路径集合 groups
  + 组、动画、文本、SVG解析、渲染、序列化、事件、图像、滤镜

# 第二部分
+ 14、动画（Animation）
  + animate(p1, p2, p3)
    + p1 动画的属性值
    + p2 动画的结束值（支持相对值）
    + p3 可选对象，指定动画的更精细细节：持续时间、回调、缓动等
      + onChange: canvas.renderAll.bind(canvas) // 重新渲染画布，才能看到动画效果
      + from 动画属性的起始值
      + duration 动画的持续时间，默认为：500ms
      + easing 缓和功能，例如：fabric.util.ease.easeOutBounce；其他可选值：
        + easeInCubic
        + easeOutCubic
        + easeInElastic
        + easeOutElastic
        + easeInBounce
        + easeOutExpo
      + onComplete 动画结束时调用的回调
    + 动画效果
      + 设置 angle 旋转
      + 设置 top、left 移动
      + 设置 width、height 收缩或增长
      + 设置 opacity 使其淡入淡出
+ 15、图片滤镜（Image filters）
  + fabric.Image 的实力有个 filters 属性，即滤镜数组
    + 添加滤镜
      + img.filters.push(new fabric.Image.filters.Sepia());
    + 应用滤镜
      + img.applyFilters()
  + 内置滤镜可通过 console.log(fabric.Image.filters) 查看
  + 自定义滤镜（参考：http://fabricjs.com/fabric-intro-part-2；搜索：fabric.Image.filters.Redify）
+ 颜色（Colors）
+ 渐变（Gradients）
+ 16、文本（Text）
  + fabric.Text
  + 支持多行
  + 支持文本对齐：左、中、右，在处理多行文本时很有用
  + 支持文本背景
  + 支持文本装饰：下划线、穿透、上线、阴影、fontStyle
    + underline: true
    + linethrough: true
    + overline: true
  + 支持行高
  + 支持字符间距
  + 支持表情符号
  + 在使用交互式类进行画布编辑时，可以直接在画布上键入文本
  + 支持子范围，将颜色和属性应用于文本对象的子范围
+ 17、事件（Event）
  + on 绑定事件
  + off 关闭事件
  + 每个对象附加的事件他们彼此之间是独立的
  + 鼠标事件
    + mouse:down
    + mouse:move
    + mouse:up
  + 渲染相关事件：  
    + after:render （整个画布被重新绘制）
  + 对象相关事件（）
    + object:added （有新对象被添加）
    + object:removed
    + object:modified
    + object:selected
    + object:moving    （对象移动一个像素时，就会连续触发）
    + object:scaling   （对象缩放一个像素时，就会连续触发）
    + object:rotating
  + 选择相关事件（操作结束时触发）
    + before:selection:cleared
    + selection:cleared
    + selection:created
  + 案例：http://fabricjs.com/events

# 第三部分
+ 18、组（Groups）
  + 将多个对象作为一个单元使用
  + 每次在画布上选择多个对象时，Fabric 会在幕后隐式创建一组对象
  + fabric.Group （以编程方式使用组）
    + 设置 originX、originY 设置为 center，使得对象可以在组内居中；默认情况组成员相对于组的左上角定位
    + 默认的 top：-50.5、left: -50.5
    + addWithUpdate() 将对象添加到组中，然后重新计算组的维度和位置
+ 19、使用组时要注意对象的状态
  + 在使用图像形成组时，需要确保这些图像已完全加载
+ 20、序列化（Serialization）
  + 允许用户在服务器上保存画布内容的结果，或者将内容流式传输到不同的客户端，将需要画布序列化
  + 怎么发送画布内容？
    + 可以将画布导出到图像，但将图像上传到服务器肯定是带宽很大的。在尺寸方面，没有什么比文本好，这正是 Fabric 为画布序列化/反序列化提供出色支持的原因
  + 序列化画布
    + 使用 ES5 JSON.stringify(canvas) 方法，如果该方法存在，它会隐式调用传递对象的 toJSON() 方法。
    + 由于 Fabric 中的 canvas 实例具有 toJSON 方法，因此就相当于调用了 JSON.stringify(canvas.toJSON())
  + toJSON() -- 字符串化
  + toDatalessJSON() -- toDatalessJSON 允许我们进一步减少画布表示，并用一个简单的 SVG 链接替换大型路径数据表示
  + toObject() -- 对象化
    + 可通过继承方式自定义（http://fabricjs.com/fabric-intro-part-3 中搜索：extend rectangle's toObject）
  + toSVG() 导出为 SVG
  + excludeFromExport 设置为 true，则该对象不会被导出
+ 21、反序列化（Deserialization）
  + loadFromJSON
+ 22、toDatalessJSON --- loadFromDatalessJSON
+ 23、SVG 解析（SVG parser）
  + loadSVGFromString(p1, cb)
    + p1 是 SVG 字符串
    + cb 是回调函数，包含两个参数
      + 第一个参数包含从 SVG 解析的对象数组 - 路径，路径组（用于复杂对象），图像，文本等
      + 第二个参数是配置项
  + loadSVGFromURL
  + fabric.util.groupSVGElements
+ 24、子类（Subclassing）
  + fabric.util.createClass
    + createClass 接受一个对象并使用该对象的属性来创建具有实例级属性的"类"
    + initialize 属性用作构造函数
    + callSuper
  + 创建自定义的类和子类
  + 画矩形的同时画上文字
    + 通过 组 实现
    + 继承现有 Fabric 类来实现

# 第四部分
+ 25、自由绘图
  + 只需将 Fabric.Canvas 的 isDrawingMode 属性设置为 true 即可启用自由绘图模式
  + 只要执行任何移动，然后是 "mouseup" 事件，Fabric 就会触发 "path:created" 事件，并实际上将刚绘制的形状转换为真正的fabric.Path 实例
  + freeDrawingBrush.width 设置画笔粗细
  + freeDrawingBrush.color 设置画笔颜色
  + 还可以设置画笔类型（例如：喷雾状或粉笔状）以及自定义画笔图案
  + 甚至自定义扩展选项，类似于 Fabric 图像滤镜
  + 官方案例：http://fabricjs.com/freedrawing
+ 26、定制
  + 可以在画布或画布对象上调整许多各种参数，以使事物按照您想要的方式运行
  + 锁定对象（Locking objects）
    + 取值：true、false
    + lockMovementX、lockMovementY 是否可移动
    + lockRotation 是否可旋转
    + lockScalingX、lockScalingY 是否可放大、缩小
  + 设置选择对象的边界和角落
    + hasBorders 是否边界的边框
    + borderColor 边框颜色
    + hasControls 是否边界上的小方块，如果为 false，则无法旋转、放大或缩小对象
    + hasRotatingPoint 是否显示边界旋转小方块
    + rotatingPointOffset 旋转小方块的偏移量
    + setControlVisible 设置边界小方块是否显示
    + centeredRotation 是否已中心旋转
  + 禁止组选择（Disabling selection）
    + canvas 对象上设置 selection: false
    + 否在可以用鼠标框选，或按住 shift 点选
  + 设置用鼠标框选时的样式
    + selectionColor 设置背景色
    + selectionLineWidth 边框宽度
    + selectionBorderColor 边框颜色
    + selectionDashArray 虚线边框
  + 给对象设置虚线边框
    + strokeDashArray
  + 可点击区域（Clickable area）
    + 默认点击 bounding area（绑定区域） 就能操作对象
    + 可改为点击 actual object（实际对象）才能操作
    + perPixelTargetFind
  + 是否等比缩放
    + uniScaleTransform: false、true
    + centeredScaling 是否已对象中心进行缩放
    + centeredRotation 是否已对象中心进行旋转
    + originX、originY 可改变对象的转换点
      + originX 默认值为：left；可选值：left、center、right
      + originY 默认值为：top；可选值：top、center、bottom
  + 官方案例：http://fabricjs.com/controls-customization
+ 27、画布图背景或遮罩
  + backgroundImage  
  + overlayImage

# 第五部分
+ 28、缩放和移动
  + 缩放
    + 默认点缩放
    + 中心点缩放
  + 移动
    + 按住 alt 键才可移动
    + 限制边界的移动

# 第六部分
+ 29、转换
  + 矩阵（matrix）称为6个数字的数组，表示平面上的变换，并指向一个简单的JS对象，它看起来像{x：number，y：number}或fabric.Point类实例
    + x轴缩放比例、x轴斜切角度、y轴斜切角度、y轴缩放比例、x轴平移量、y轴平移量
    + canvas.vieportTransform 获取 canvas 的矩阵
  + 计算机科学中，三维动画制作需要用到矩阵
    + canvas矩阵转换：https://blog.csdn.net/qq_27682041/article/details/72779213
    + 彻底弄懂matrix和canvas：https://blog.csdn.net/oubin66/article/details/52337022
    + HTML5 MatrixTransform矩阵变换：https://blog.csdn.net/piziliweiguang/article/details/7802994
  + 与转换相关的方法和属性
    + Canvas（画布的矩阵）:
      + vieportTransform = matrix;
    + Objects（对象的矩阵）:
      + matrix = fabric.Object.prototype.calcTransformMatrix();
      + matrix = fabric.Object.prototype.calcOwnMatrix();
    + Utils:
      + point = fabric.util.transformPoint(point, matrix);
        + 将矩阵转换为点，如：{x: 50.5, y: 50.5}
        + 简略代码：
        + var rect = new fabric.Rect({ width: 50, height: 50, fill: 'red' })
        + var point = new fabric.Point(0, 0);
        + var position = fabric.util.transformPoint(point, rect.calcTransformMatrix()); // {x: 50.5, y: 50.5}
      + matrix = fabric.util.multiplyTransformMatrices(matrix, matrix);
      + matrix = fabric.util.invertTransform(matrix);
      + options = fabric.util.qrDecompose(matrix);
        + 将矩阵转换为：{ angle: 0, scaleX: 0.5, scaleY: 1, skewX: 0, skewY: 0, translateX: 10 ,translateY: 10 }
        + 简略代码：
        + var matrix = canvas.viewportTransform; // [1, 0, 0, 1, 0, 0] 即：[x轴缩放比例, x轴斜切角度, y轴斜切角度, y轴缩放比例, x轴平移量, y轴平移量]
        + var options = fabric.util.qrDecompose(matrix); // { angle: 0, scaleX: 1, scaleY: 1, skewX: 0, skewY: 0, translateX: 0, translateY: 0 }
  + 从一个空间移动到另一个空间
    + 使用 fabricJS，经常需要与坐标和位置进行交互，但是如果没有合适的背景，那么理解这些坐标的位置会很麻烦
    + canvas.vieportTransform 转换（以Canvas转换的格式）聚焦视口
  + 转换顺序
    1. zoom and pan                            （缩放和移动）   
    1. object transformation                   （对象转换）
    1. nested object ( group )                 （嵌套对象(组)）
    1. nested object deeper ( nested groups )  （更深层嵌套对象(嵌套组)）
  + 矩阵原始形态
    + { angle: number, scaleX: number, scaleY: number, skewX: number, skewY: 0, translateX: number ,translateY: number }
    + skew 改变元素在页面中的形状
      + skewX 横向倾斜指定度数
        + x 取值为正，x 轴不动，y 轴逆时针倾斜一定角度
        + x 取值为负，x 轴不动，y 轴顺时针倾斜一定角度
      + skewY 纵向倾斜指定度数
        + y 取值为正，y 轴不动，x 轴顺时针倾斜一定角度
        + y 取值为负，y 轴不动，x 轴逆时针倾斜一定角度

# 第七部分
+ 30、在 fabricJS 中使用位图而不是字体来替换文本
  + 实现了 BitmapText 自定义类

# 第八部分
+ 31、使用 clipPaths 剪切对象为任何形状
  + 所有对象都有 clipPath 属性
  + ClipPath 需要对象缓存
  + 如何使用：
    + var canvas = new fabric.Canvas('c', { width: 500, height: 300, backgroundColor: '#eee' });
    + var circle = new fabric.Circle({ radius: 40, top: -40, left: -40 });
    + 将 circle 赋值给 rect 的 clipPath 属性即可
    + var rect = new fabric.Rect({ width: 300, height: 200, fill: 'red', clipPath: circle });
    + canvas.add(rect);
  + 根据 SVG 规范中的定义，clipPath 没有笔划并且用黑色填充，与黑色像素重叠的对象的像素将是可见的，其他的不可见
  + 注意：clipPath 位于从对象中心开始的位置，对象的 originX 和 originY 不起任何作用，而clipPath 的 originX 和 originY 则起作用 
  + 三个示例
    + clipPath 基本示例
    + clipPath 应用于组
    + 组作为 clipPath 应用于组
+ 32、嵌套 clipPath
+ 33、两个 clipPath，一个应用于组，另一个应用于组内的某个对象
+ 34、文本作为 clipPath 应用于组
+ 35、clipPath 应用于画布
  + controlsAboveOverlay 属性为 true 控制方块会在画布外围，否则在画布内；默认为 false
+ 36、clipPath 动画
+ 37、clipPath 绝对定位
  + absolutePositioned 属性
  + 可以将一个 clipPath 应用于一个对象，指定它应该是绝对定位的。这意味着，clipPath 不是相对于对象的中心，只是位于画布上。
  + 对象将无移动，而 clipPath 将稳定。结果是 clipPath 在画布上创建了一个形状，并且只允许它自己的对象出现在那里
+ 38、挖空对象
  + inverted: true
+ 39、组挖空对象
  + 只能将 inverted 设置到组对象上，设置到组内对象上将无效

# 第九部分
+ fabric.Object 对象

# 方法
+ getObjects() 获取组中的所有对象
+ size() 获取组中对象的数量
+ item() 检索组中的特定对象
+ contains() 检查特定对象是否在组中
+ animate() 动画
+ renderAll() 重新渲染
+ add() 添加对象
+ remove() 删除对象
+ clone()
+ clear()
+ toDataURL('png')

# 相关插件

### fabric.js
+ https://github.com/fabricjs/fabric.js
+ http://fabricjs.com/articles/
+ http://www.hangge.com/blog/cache/search.php?key=Fabric.js
  + 改变鼠标指针样式
  + 画布视图 viewport 的自适应
  + 鼠标拖动画布、滚轮缩放画布
  + 添加鼠标右键点击事件响应（右键菜单）

### SVG.js
+ https://svgjs.com/docs/2.7/#svg-js

### Snap.svg
+ http://snapsvg.io/

### Raphael
+ http://dmitrybaranovskiy.github.io/raphael/

### d3
+ https://d3js.org/
+ https://github.com/d3/d3/wiki/API--%E4%B8%AD%E6%96%87%E6%89%8B%E5%86%8C

### three.js
+ https://threejs.org/

### 62款前端数据可视化插件大盘点
+ https://cloud.tencent.com/developer/article/1051994

### 效果参考
+ https://www.draw.io/?demo=1
+ https://www.draw.io
