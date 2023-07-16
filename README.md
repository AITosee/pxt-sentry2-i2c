
> 在 [https://github.com/Uniquemf/pxt-Sentry/](https://github.com/Uniquemf/pxt-Sentry/) 打开此页面

## 用作扩展

此仓库可以作为 **插件** 添加到 MakeCode 中。

* 打开 [https://makecode.microbit.org/](https://makecode.microbit.org/)
* 点击 **新项目**
* 点击齿轮图标菜单下的 **扩展**
* 搜索 **https://github.com/Uniquemf/pxt-Sentry** 并导入

## 编辑此项目 ![构建状态标志](https://github.com/Uniquemf/pxt-Sentry/workflows/MakeCode/badge.svg)

在 MakeCode 中编辑此仓库。

* 打开 [https://makecode.microbit.org/](https://makecode.microbit.org/)
* 点击 **导入**，然后点击 **导入 URL**
* 粘贴 **https://github.com/Uniquemf/pxt-Sentry** 并点击导入

## 使用方法

* Get Vision result

```blocks
// Initialized Sentry with I2C port
let index = 0
let target_num = 0
Sentry.Begin(sentry_mode_e.kI2CMode, sentry_addr_e.ADDR1)
Sentry.VisionSetStatus(SentryStatus.Enable, sentry_vision_e.kVisionCard)
basic.forever(function () {
    target_num = Sentry.Detected(sentry_vision_e.kVisionCard)
    serial.writeValue("target_num", target_num)
    index = 1
    for (let index2 = 0; index2 < target_num; index2++) {
        serial.writeValue("index", index)
        serial.writeValue("x", Sentry.GetValue(sentry_vision_e.kVisionCard, sentry_gen_info_e.kXValue, index))
        serial.writeValue("y", Sentry.GetValue(sentry_vision_e.kVisionCard, sentry_gen_info_e.kYValue, index))
        serial.writeValue("w", Sentry.GetValue(sentry_vision_e.kVisionCard, sentry_gen_info_e.kWidthValue, index))
        serial.writeValue("h", Sentry.GetValue(sentry_vision_e.kVisionCard, sentry_gen_info_e.kWidthValue, index))
        serial.writeValue("l", Sentry.GetValue(sentry_vision_e.kVisionCard, sentry_gen_info_e.kLabel, index))
        index += 1
    }
})

```

* Get Color result

```blocks
// Initialized Sentry with I2C port
let index = 0
let target_num = 0
Sentry.Begin(sentry_mode_e.kI2CMode, sentry_addr_e.ADDR1)
Sentry.VisionSetStatus(SentryStatus.Enable, sentry_vision_e.kVisionColor)
Sentry.SetParamNum(sentry_vision_e.kVisionColor, 3)
Sentry.SetColorParam(10, 10, 5, 5, 1)
Sentry.SetColorParam(40, 40, 6, 6, 2)
Sentry.SetColorParam(80, 80, 8, 8, 3)
basic.showIcon(IconNames.Heart)
basic.forever(function () {
    target_num = Sentry.Detected(sentry_vision_e.kVisionColor)
    serial.writeValue("target_num", target_num)
    index = 1
    for (let index2 = 0; index2 < target_num; index2++) {
        serial.writeValue("index", index)
        serial.writeValue("R", Sentry.ColorRcgValue(sentry_color_info_e.kRValue, index))
        serial.writeValue("G", Sentry.ColorRcgValue(sentry_color_info_e.kRValue, index))
        serial.writeValue("B", Sentry.ColorRcgValue(sentry_color_info_e.kRValue, index))
        serial.writeValue("L", Sentry.ColorRcgValue(sentry_color_info_e.kRValue, index))
        if (Sentry.DetectedColor(color_label_e.kColorBlack)) {
            serial.writeLine("black")
        } else if (Sentry.DetectedColor(color_label_e.kColorWhite)) {
            serial.writeLine("white")
        } else if (Sentry.DetectedColor(color_label_e.kColorRed)) {
            serial.writeLine("red")
        } else if (Sentry.DetectedColor(color_label_e.kColorYellow)) {
            serial.writeLine("yellow")
        }
        index += 1
    }
})


```


* Get QrCode result

```blocks
// Initialized Sentry with I2C port
Sentry.Begin(sentry_mode_e.kI2CMode, sentry_addr_e.ADDR1)
Sentry.VisionSetStatus(SentryStatus.Enable, sentry_vision_e.kVisionQrCode)
basic.forever(function () {
    if (Sentry.Detected(sentry_vision_e.kVisionQrCode) > 0) {
        serial.writeValue("x", Sentry.QrRcgValue(sentry_qr_info_e.kXValue))
        serial.writeValue("y", Sentry.QrRcgValue(sentry_qr_info_e.kYValue))
        serial.writeValue("w", Sentry.QrRcgValue(sentry_qr_info_e.kWidthValue))
        serial.writeValue("h", Sentry.QrRcgValue(sentry_qr_info_e.kHeightValue))
        serial.writeString("l=" + Sentry.GetQrCodeValue())
    }
})


```

* Get QrCode result by serial

```blocks
// Initialized Sentry with Serial port
serial.redirect(
SerialPin.P13,
SerialPin.P14,
BaudRate.BaudRate115200
)
Sentry.Begin(sentry_mode_e.kSerialMode, sentry_addr_e.ADDR1)
Sentry.VisionSetStatus(SentryStatus.Enable, sentry_vision_e.kVisionQrCode)
basic.forever(function () {
    if (Sentry.Detected(sentry_vision_e.kVisionQrCode) > 0) {
        serial.writeValue("x", Sentry.QrRcgValue(sentry_qr_info_e.kXValue))
        serial.writeValue("y", Sentry.QrRcgValue(sentry_qr_info_e.kYValue))
        serial.writeValue("w", Sentry.QrRcgValue(sentry_qr_info_e.kWidthValue))
        serial.writeValue("h", Sentry.QrRcgValue(sentry_qr_info_e.kHeightValue))
        serial.writeString("l=" + Sentry.GetQrCodeValue())
    }
})


#### 元数据（用于搜索、渲染）

* for PXT/microbit
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
