iOS 摸鱼周报 52 | 如何规划个人发展

![](http://cdn.zhangferry.com/Images/moyu_weekly_cover.jpeg)

### 本期概要

> * 话题：
> * 本周学习：Xcode Playground Tips
> * 优秀博客：
> * 学习资料：
> * 开发工具：

## 本期话题



## 本周学习

整理编辑：[Hello World](https://juejin.cn/user/2999123453164605/posts)

### Xcode Playground Tips

`Playground`是学习 Swift 和 SwiftUI 的必不可少的工具，这里总结一些可能涉及到的 Tips，方便更好的学习和使用。

#### 模块化

`Playground` 中也是支持模块化管理的，主要涉及辅助代码和资源两部分：

- 辅助代码(位于 Sources 目录下的代码)：

    辅助代码只在编辑内容并保存后才会编译，运行时不会每次都编译。辅助代码编译后是以 module 形式引入到 Page 中的。所以被访问的符号都需要使用 `public` 修饰。

    添加到 Playground Sources 下的辅助代码，所有 Page 主代码和辅助代码 都可使用。区别在于 Page 辅助代码如果未 import 导入 module, 则不会有代码提示，主代码无需 import。

    添加到 Page Sources 下的辅助代码，只有当前的 Page 可用（apple 文档）。module 命名格式为 **xxx(PageName)_PageSources**。

    > 实际测试，如果在其他 Page 主代码中和辅助代码中同时 `import` 当前 Sources Module 也是可用的，但是只在辅助代码中 `import`，则不生效。如果有不同测试结果的同学可以交流下

- 资源（位于 Resources）：

使用时作用域同辅助代码基本相同，由于无法作为 module 被 `import` 到 Page 主代码，所以跨 Page 之间的资源是无法访问的。

`Playground` 编译时将当前 Page 和 `Playground` 项目的资源汇总到 Page 项目路径下，因此无论是项目资源还是 Page 专属资源，在 Page 主代码或 Page 的辅助代码中，都可以使用 `Bundle.main` 来访问。

#### 运行方式

`Playground` 可以修改运行方式，分别是 `Automatically Run` 和 `Manually Run`，区别就是自动模式在每次键入后自动编译。调整方式为长按运行按钮，如图：

![](http://cdn.zhangferry.com/Images/weekly_57_weeklyStudy_01.png)

另外，通过快捷键 `shift+回车` 可以只运行到当前鼠标所在位置代码，作用同直接点击代码所在行的运行按钮一致。

#### PlaygroundSupport

`PlaygroundSupport` 是用于扩展 Playground 的框架，在使用上主要有两个作用：

- 执行一些延迟、异步操作、或者存在交互的视图时，这时需要 `Playground` 在执行完最后代码后不会直接 Finish，否则一些回调和交互不会生效。需要设置属性 `needsIndefiniteExecution == true`。

    ```swift
    // 需要无限执行
    PlaygroundPage.current.needsIndefiniteExecution = true
    // 终止无限执行
    PlaygroundPage.current.finishExecution()
    ```

- 使用 `Playground` 展示实时视图时，需要将视图添加到属性 `liveView`上。如果设置了 `liveView`则系统会自动设置 `needsIndefiniteExecution`，无需重复设置。

    > 如果是 `UIKit`视图则通过 `liveView`属性赋值或者 `setLiveView()`函数调用都可以，但是 `SwiftUI` 只支持 `setLiveView()`函数调用方式。

    ```swift
    struct contentView: View {...}
    let label = UILabel(frame: .init(x: 0, y: 0, width: 200, height: 100))
    PlaygroundPage.current.setLiveView(label) // PlaygroundPage.current.liveView = label
    PlaygroundPage.current.setLiveView(contentView)
    ```

#### markup 注释

根据文档，markup 支持标题、列表、代码、粗体、斜体、链接、资产、转移字符等，目的是在 `Quick Help` 和 代码提示中显示更丰富的描述信息

书写格式分两种，单行使用 `//: 描述区` 多行使用`/*: 描述区 */`

源码/渲染模式切换方式：`Editor -> Show Rendered Markup` 或者设置右侧扩展栏的 `Playground Settings ->Render Documentation`。

由于大部分格式都是和 markdown 类似的，这里只学习一个特殊的特性，即导航。

导航可以实现在不同的 Page 页之间跳转，有三种跳转方式：previous、next、指定页

```swift
[前一页](@previous)、[下一页](@next)、[指定页](name)
```

> 指定具体页时，页面名称去掉扩展名，并且编码替换空格和特殊字符。不需要使用 `@` 符号

Markup 更多格式可以查看官方文档 [markup-apple](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/index.html#//apple_ref/doc/uid/TP40016497-CH2-SW1 "markup-apple")，另外 `Playground`还支持和框架或者工程结合使用，可以通过另一位主编的博客内容了解学习 [玩转 Xcode Playground（下）- 东坡肘子](https://www.fatbobman.com/posts/xcodePlayground2/ "玩转 Xcode Playground（下）- 东坡肘子")

## 优秀博客



## 见闻

> 这一周阅读/浏览到的有趣的资讯。


## 学习资料

整理编辑：[Mimosa](https://juejin.cn/user/1433418892590136)



## 工具推荐

整理编辑：[CoderStar](https://mp.weixin.qq.com/mp/homepage?__biz=MzU4NjQ5NDYxNg==&hid=1&sn=659c56a4ceebb37b1824979522adbb15&scene=18)



## 关于我们

iOS 摸鱼周报，主要分享开发过程中遇到的经验教训、优质的博客、高质量的学习资料、实用的开发工具等。周报仓库在这里：https://github.com/zhangferry/iOSWeeklyLearning ，如果你有好的的内容推荐可以通过 issue 的方式进行提交。另外也可以申请成为我们的常驻编辑，一起维护这份周报。另可关注公众号：iOS成长之路，后台点击进群交流，联系我们，获取更多内容。

### 往期推荐

[iOS 摸鱼周报 #51 | 游戏版号恢复发放](https://mp.weixin.qq.com/s/ogjhELipiVFRaYJkT2NQwA)

[iOS 摸鱼周报 第五十期](https://mp.weixin.qq.com/s/6IS0RlytWxjeRHyh0f2fXA)

[iOS 摸鱼周报 第四十九期](https://mp.weixin.qq.com/s/6GvVh8_CJmsm1dp-CfIRvw)

[iOS摸鱼周报 第四十八期](https://mp.weixin.qq.com/s/br4DUrrtj9-VF-VXnTIcZw)

![](http://cdn.zhangferry.com/Images/WechatIMG384.jpeg)
