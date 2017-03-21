## Lottie应用于React Native、iOS和Android
Lottie组件，应用于React Native([Android](https://github.com/CRAnimation/lottie-android) 和[iOS](https://github.com/CRAnimation/lottie-ios))

* 本文由CRAnimation团队翻译
* 本项目原地址：[airbnb/lottie-react-native](https://github.com/airbnb/lottie-react-native)
* Lottie-iOS译文地址：[CRAnimation/lottie-iOS](https://github.com/CRAnimation/lottie-ios)
* Lottie-Android译文地址：[CRAnimation/lottie-Android](https://github.com/CRAnimation/lottie-android)
* Lottie-React-Native译文地址：[CRAnimation/lottie-react-native](https://github.com/CRAnimation/lottie-react-native)
* 翻译：小9
* 校正：熊熊
* 术语指导：西西
* QQ群：547897182（iOS动效特工队，入群请提供个人主页货github账号）

Lottie 是一个可应用于Andriod和iOS的动画库，它通过[bodymovin](https://github.com/bodymovin/bodymovin)插件来解析[Adobe After Effects ](http://www.adobe.com/products/aftereffects.html)动画并导出为json文件，并通过手机端原生方式渲染出来。

这是前所未有的方式，设计师可以创作并且运行优美的动画而不需要工程师煞费苦心地通过手动调整的方式来重现动画。有人说一张图片可以顶的上1000个字，那么下面就有13000个字了：
![](https://github.com/airbnb/lottie-ios/raw/master/_Gifs/Examples1.gif)
![](https://github.com/airbnb/lottie-ios/raw/master/_Gifs/Examples2.gif)
![](https://github.com/airbnb/lottie-ios/raw/master/_Gifs/Community%202_3.gif)
![](https://github.com/airbnb/lottie-ios/raw/master/_Gifs/Examples3.gif)
![](https://github.com/airbnb/lottie-ios/raw/master/_Gifs/Examples4.gif)

所有的动画都是通过After Effects创作出来，用bodymovin插件导出，不需要任何额外的工作就可以以原生的方式渲染出来。
## 相关的项目文件
这个项目只是用代码对Lottie进行包装并暴露给React Native。你可以从各自对应的库中找到解析和渲染的代码。
[Lottie for iOS](https://github.com/airbnb/lottie-ios)
[Lottie for Android](https://github.com/airbnb/lottie-android)
### 安装
你可以通过安装node模块来开始lottie：
```npm i --save lottie-react-native```
如果你在iOS中使用CocoaPods的话，你可以在`Podfile`中添加下面的代码：
```
pod 'lottie-react-native', :path => '../node_modules/lottie-react-native'
```
如果你在iOS中没有用CocoaPods的话，你可以用`react-native link`:
```
react-native link lottie-ios
react-native link lottie-react-native/
```
针对Android系统，你也可以用`react-native link`:
```
react-native link lottie-react-native
```
如果对此有任何困惑的话，请添加issue。

### 基础的用法：
[查看所有组件的API](https://github.com/airbnb/lottie-react-native/blob/master/docs/api.md)
Lottie 的动画进度可以通过改变`Animated `的Value来控制：
```
import React from 'react';
import { Animated } from 'react-native';
import Animation from 'lottie-react-native';

export default class BasicExample extends React.Component {
constructor(props) {
super(props);
this.state = {
progress: new Animated.Value(0),
};
}

componentDidMount() {
Animated.timing(this.state.progress, {
toValue: 1,
duration: 5000,
}).start();
}

render() {
return (
<Animation
style={{
width: 200,
height: 200,
}}
source={require('../path/to/animation.json')}
progress={this.state.progress}
/>
);
}
}
```
此外，还有一些API有时候会更简单：
```
import React from 'react';
import Animation from 'lottie-react-native';

export default class BasicExample extends React.Component {
componentDidMount() {
this.animation.play();
}

render() {
return (
<Animation
ref={animation => { this.animation = animation; }}
style={{
width: 200,
height: 200,
}}
source={require('../path/to/animation.json')}
/>
);
}
}
```
## 运行示例工程

你可以通过以下命令来检出示例工程：
1. 克隆仓库:``` git clone https://github.com/airbnb/lottie-react-native.git```
2. 打开目录：``` cd lottie-react-native```并且安装:```npm install```
3. 通过``` npm start``` 启动packager
4. 在另一个命令行窗口，按如下步骤操作：

针对iOS：
1. 如果你没有用CocoaPods安装，就执行``` sudo gem install cocoapods```
2. 安装pods：``` npm run build:pods```
3. 运行示例代码：```npm run run:ios```

针对Android：
1. 运行示例代码：```npm run run:android```

## 故障排查
如果你在运行```pod install```时出现：
```
[!] Unable to find a specification for `lottie-ios` 
```
那么执行``` pod repo update``` 再尝试

## 替代方案
1. 手动地创建动画。手动创建动画对于设计师以及iOS、Android工程师而言意味着付出巨额的时间。通常很难，甚至不可能证明花费这么多时间来获得动画是正确的。
2. Facebook Keyframes。 Keyframes是专门用来构建用户界面的， 是FaceBook的一个很棒，很新的库。但是Keyframes不支持一些Lottie所能支持的特性，比如： 遮罩，蒙版，裁切路径，虚线样式还有很多。
3. Gifs。Gifs 占用的大小是bodymovin生成的JSON大小的2倍还多，并且渲染的尺寸是固定的，并不能放大来适应更大更高分辨率的屏幕。
4. Png序列桢动画。 Png序列桢动画 甚至比gifs更糟糕，它们的文件大小通常是 bodymovin json文件大小的30-50倍，并且也不能被放大。

## 为什么叫Lottie？
Lottie是以德国剪影动画先驱Lotte Reiniger（洛特·雷妮格）的名字命名的。 她最出名的作品是《阿基米德王子历险记》 (1926) – 世界上第一部长篇动画电影。 比华尔特·迪士尼的长篇动画电影——《白雪公主与七个小矮人》 (1937) 还要早了10年。[The art of Lotte Reineger](https://www.youtube.com/watch?v=LvU55CUw5Ck&feature=youtu.be)
## 贡献
请查看：[Contributors Guide](https://github.com/airbnb/lottie-react-native/blob/master/CONTRIBUTING.md)
## 软件许可证书：
[Apache-2.0](https://github.com/airbnb/lottie-react-native/blob/master/LICENSE.md)

