# rpx-loader

## 简介 | Introduction

本loader可以让你在webpack项目中使用响应式长度单位`rpx`，用法同微信小程序。

This webpack loader is an implement of WeChat rpx in webpack projects. Please scroll down for English readme.

## 优点

1. 可以直接将UI标注图上的`px`值照搬到CSS（或SCSS等）中，loader会自动完成转换，无需手动换算为`rem`等单位
2. 单位转换由webpack处理，无需在客户端引入任何JS库，从而提高性能
3. 由于本质上是`vw`，所以能够解决真实1px、视网膜屏幕等问题

## 使用

首先确保安装了[`css-loader`](https://www.npmjs.com/package/css-loader)以及你所需的预处理器的loader

在项目根目录中，执行`npm i rpx-loader -D`

在`webpack.config.js`中, 将`rpx-loader`插入到`css-loader`之前

```javascript
module.exports = {
    module: {
        rules: [{
        test: /\.css$/,
        use: [
            'style-loader',
            'rpx-loader', // 将`rpx-loader`插入到`css-loader`之前
            'css-loader'
        ]
        }, {
        test: /\.scss$/, // 也可以用于预处理器
        use: [
            'vue-style-loader', // 可以与其它loader连环
            'rpx-loader', // 将`rpx-loader`插入到`css-loader`之前
            'css-loader',
            'sass-loader'
        ]
        }]
    }
}
```

在样式文件中，使用rpx作为单位：

```scss
div {
    height: 50rpx; // 如果UI标注图上为50px，则只需要写50rpx
}
```

最终你会得到：

```css
div {
    height: 6.67vw;
}
```

在不同宽度的设备上，视觉效果是一致的

## 注意事项

为简化配置，本loader默认UI标注图的宽度为750px

如需修改，可以自行改源码（源码极其短小，把750改成你的UI标注图宽度即可）

或者提交issue，如果需要这个功能的人多，未来的更新中会把标注图宽度抽出来作为配置项

## Features

1. Enables you to directly copy the `px` value in marked UI to your CSS (or other preprocessors), and the loader will compile them responsively without manually convert `px` values to `rem` or other units.
2. Webpack will handle the unit conversion, and you needn't import any JS libs in the client. In other words, a better performance.
3. It performs well on retina screens, and it well resolves real 1px problem, since the essence of `rpx` is `vw`.

## Usage

Ensure that you've installed [`css-loader`](https://www.npmjs.com/package/css-loader) and the loader of your preferred preprocessor.

Run `npm i rpx-loader -D` in the root directory of your project.

In `webpack.config.js`, you need to insert `rpx-loader` before `css-loader`

```javascript
module.exports = {
    module: {
        rules: [{
        test: /\.css$/,
        use: [
            'style-loader',
            'rpx-loader', // insert 'rpx-loader' before 'css-loader'
            'css-loader'
        ]
        }, {
        test: /\.scss$/, // also works in preprocessors
        use: [
            'vue-style-loader', // can be chained with other loaders
            'rpx-loader', // insert 'rpx-loader' before 'css-loader'
            'css-loader',
            'sass-loader'
        ]
        }]
    }
}
```

In your style sheet, you can write as below:

```scss
div {
    height: 50rpx; // If it is 50px in the marked UI, you just need to write 50rpx
}
```

And you will get:

```css
div {
    height: 6.67vw;
}
```

In devices with different screen widths, you will get uniform visual effects.

## P.S.

The loader takes your UI width as 750px for granted, thus to minimize the config.

If you do need to config this, you may modify the source code. Don't worry, the source code is extremely short and dead simple. Just change 750 to your preferred width.

Or you can open an issue. If many developers long for it, I will extract the UI width as a config.