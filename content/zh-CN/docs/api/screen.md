# screen

> 检索有关屏幕大小、显示器、光标位置等的信息。

进程： [Main](../glossary.md#main-process), [renderer](../glossary.md#renderer-process) 进程

在发出 ` app ` 模块的 ` ready ` 事件之前, 您不能 `require` 或使用此模块。

`screen` 是一个 [EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter).

** 注意: **在 renderer/DevTools 中, `window.screen ` 是一个保留的 DOM 属性, 因此编写 ` 让 {screen} = require('electron') ` 将不起作用。

创建填充整个屏幕的窗口的示例:

```javascript
const electron = require('electron')
const {app, BrowserWindow} = electron

let win

app.on('ready', () => {
  const {width, height} = electron.screen.getPrimaryDisplay().workAreaSize
  win = new BrowserWindow({width, height})
  win.loadURL('https://github.com')
})
```

另一个在外部显示器中创建窗口的例子

```javascript
const electron = require('electron')
const {app, BrowserWindow} = require('electron')

let win

app.on('ready', () => {
  let displays = electron.screen.getAllDisplays()
  let externalDisplay = displays.find((display) => {
    return display.bounds.x !== 0 || display.bounds.y !== 0
  })

  if (externalDisplay) {
    win = new BrowserWindow({
      x: externalDisplay.bounds.x + 50,
      y: externalDisplay.bounds.y + 50
    })
    win.loadURL('https://github.com')
  }
})
```

## 事件

`screen`模块触发以下事件:

### Event: 'display-added'

返回:

* `event` Event
* `newDisplay` [Display](structures/display.md)

当新的窗口`newDisplay`被添加的时候触发。

### Event: 'display-removed'

返回:

* `event` Event
* `oldDisplay` [Display](structures/display.md)

当旧的窗口`oldDisplay`被移除的时候触发。

### Event: 'display-metrics-changed'

返回:

* `event` Event
* `display` [Display](structures/display.md)
* `changedMetrics` String[]

当`display`中的一个或多个值发生改变时发出。 `changedMetrics`是描述更改信息的字符串数组。 可能改变的值有`bounds`, `workArea`, `scaleFactor` 和 `rotation`.

## 方法

`screen`模块有以下方法:

### `screen.getCursorScreenPoint()`

返回 [`Point`](structures/point.md)

当前鼠标的绝对位置。

### `screen.getMenuBarHeight()` *macOS*

返回`Integer`，表示菜单栏的高度 (单位：像素)

### `screen.getPrimaryDisplay()`

返回主窗口[`Display`](structures/display.md)

### `screen.getAllDisplays()`

返回一个窗口数组[`Display[]`](structures/display.md)，表示当前可用的窗口。

### `screen.getDisplayNearestPoint(point)`

* `point` [Point](structures/point.md)

返回离指定点最近的一个窗口[`Display`](structures/display.md)

### `screen.getDisplayMatching(rect)`

* `rect` [Rectangle](structures/rectangle.md)

返回离指定的图形最密切相交一个窗口[`Display`](structures/display.md)