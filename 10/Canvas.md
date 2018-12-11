| 方法名 | 参数 | 返回值 | 说明 |
| -- | -- | -- | -- |
| absolutePan(point) | fabric.Point 实例 | fabric.Canvas | 平移视口以便将点放在画布的左上角（画布左上角顶点在视口中的绝对位置）
| relativePan(point) | fabric.Point 实例 | fabric.Canvas | 画布相对视口的位置
| getCenter() | - | { top: number, left: number } | 返回画布中心的坐标
| add(...objects) | fabric.Object | 画布、集合、组 | 添加对象到画布或集合或组中，然后重新渲染画布（renderOnAddRemove 属性值不为 false）；对于组不要使用该方法，因为它不会自动改变组的边界，应使用 addWithUpdate 方法；
| bringForward(object, intersecting) | 第一个参数：object	fabric.Object 需要上移的对象 第二个参数：intersecting Boolean 如果为 true 则将上移的对象移动到与它第一个相交的对象上方；如果为 false，则按照原始层叠顺序向上移动一层；| fabric.Canvas | 在绘制对象的堆栈中向上移动对象；参考 01.html
| bringToFront(object) | fabric.Object | fabric.Canvas | 将对象移动到绘制对象堆栈的顶部
| sendBackwards(object, intersecting) | 同 bringForward(object, intersecting) | fabric.Canvas | 在绘制对象的堆栈中向下移动对象；参考 02.html
| sendToBack(object) | fabric.Object | fabric.Canvas | 将对象移动到绘制对象堆栈的底部