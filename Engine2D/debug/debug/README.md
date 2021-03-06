
## 1.使用 DEBUG 编译参数
开发者经常写一些希望仅在开发阶段使用的代码，来进行数据校验、输出日志等。

Egret 提供了 `DEBUG` 这一全局变量来实现这样的功能。

下面的代码校验 `value` 是不是由4个数字组成，如果不是，输出指定的错误信息。

```
	if (DEBUG) {
	    var rect = value.split(",");
	    if (rect.length != 4 || isNaN(parseInt(rect[0])) || isNaN(parseInt(rect[1])) ||
	        isNaN(parseInt(rect[2])) || isNaN(parseInt(rect[3]))) {
	        egret.$error(2016, this.currentClassName, toXMLString(node));
	    }
	}
```

在发行版生成过程中，Egret 命令行会移除 `if(DEBUG){ ... }` 这一整个代码块，保持发行版包体的精简。

Egret 还提供了另外一个与 `DEBUG` 对应的编译参数 `RELEASE`，用来编写只在发行版中运行的代码。


## 2.使用内置日志输出面板

在PC端可使用 `console` 提供的诸多方法输出日志，然后使用浏览器提供的开发者工具查看。

但是在移动端这个方式受到了限制，大多数移动端浏览器没有查看日志的方法。
因此 Egret 集成了向屏幕输出日志的功能，以方便移动设备调试。

![显示日志](575e991fdd5f8.png)

在 index.html 文件中有如下代码块：

```
    <div style="margin: auto;width: 100%;height: 100%;" class="egret-player"
         data-entry-class="Main"
         data-orientation="auto"
         data-scale-mode="noScale"
         data-frame-rate="30"
         data-content-width="480"
         data-content-height="800"
         data-show-paint-rect="false"
         data-multi-fingered="2"
         data-show-fps="true" data-show-log="false"
         data-log-color="#b0b0b0"> 
     </div>
```

通过 data-show-log： 设置是否在屏幕中显示日志。 true 显示，false 不显示。

在代码中可以直接调用 `egret.log(message?:any, ...optionalParams:any[])` 来输出日志。

## 3.显示脏矩形和帧频信息

在 index.html 文件中找到上述代码块：

`data-show-paint-rect="true/false"` 设置是否显示重绘区域，当这个值为 `true` 时 egret 会将舞台中的重绘区域用红框表示出来。

![重绘区域](575e943cb6ecc.png)
		

`data-show-fps="true/false"` 设置是否显示帧频信息，当这个值为 `true` 时 Egret 会在舞台的左上角显示 FPS 和 其他性能指标
		
* FPS:  60		- 帧频

* Draw: 13		- 每帧 draw 方法调用的平均次数

* Dirty 7%		- 每帧脏区域占舞台的百分比
 
* Cost: 0,0,0		- Ticker 和 EnterFrame 阶段显示的耗时,每帧舞台所有事件处理和矩阵运算耗时，绘制显示对象耗时（单位是ms） 

	