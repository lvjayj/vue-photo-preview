# vue-photo-preview

> \"基于 photoswipe 的 vue 图片预览插件\"

该项目 Fork 自https://github.com/826327700/vue-photo-preview; 原项目中使用`Vue.mixin`混入了`extend`方法，容易跟其他库产生命名冲突，故 Fork 一份修改

## 说明

1.简化了`photoswipe`的默认设置  
2.取消了图片需设定尺寸的要求  
3.默认关闭了分享按钮  
4.简化了 html 结构

## 使用

### NPM 安装

```bash
npm install @mvpleung/vue-photo-preview --save
```

```javascript
import preview from '@mvpleung/vue-photo-preview'
import '@mvpleung/vue-photo-preview/dist/skin.css'
Vue.use(preview, options?) //option配置请查看 http://photoswipe.com/documentation/options.html
```

### Script 引入

```html
<link rel="stylesheet" type="text/css" href="path/dist/skin.css" />

<script
    src="path/dist/vue-photo-preview.js"
    type="text/javascript"
    charset="utf-8"
></script>
<script type="text/javascript">
    // 不需要自定义配置时，不需要 use
    // 仅当需要自定义配置时，需要显示 use
    var options = {
        fullscreenEl: false //关闭全屏按钮
    }
    Vue.use(vuePhotoPreview, options)

    new Vue({
        el: '#app'
    })
</script>
```

```html
## 在img标签添加preview属性 preview值相同即表示为同一组

<img src="xxx.jpg" preview="0" preview-text="描述文字" />

//分组
<img src="xxx.jpg" preview="1" preview-text="描述文字" />
<img src="xxx.jpg" preview="1" preview-text="描述文字" />

<img src="xxx.jpg" preview="2" preview-text="描述文字" />
<img src="xxx.jpg" preview="2" preview-text="描述文字" />

<img
    src="xxx.jpg"
    large="xxx_3x.jpg"
    preview="2"
    preview-text="缩略图与大图模式"
/>
```

### 2020-01-12 更新

修复因使用`Vue.mixin`混入了`extend`导致的命名冲突。

### 2019-02-02 更新

修复打开和关闭图片页面时，动画起始位置总是位于图片组最后一张的问题。调整默认点击放大倍数。

### 2018-11-28 更新

解决图片多次点击问题。缩略图只可点击一次，直至图片加载完成后，才可再次打开。

### 2018-11-15 更新

重命名 this.init 为 this.initPreview，解决部分冲突问题。
去除所有 console 打印

### 2018-10-15 更新

解决原图与大图模式下的 BUG

### 2018-09-28 更新

//添加对原插件 photoswipe 的事件响应，示例：

```javascript
this.$preview.on('close',())=>{//close只是众多事件名的其中一个，更多请查看文档
	console.log('图片查看器被关闭')
})
```

//添加图片查看器实例--this.\$preview.self 注意：此实例仅在图片查看器被打开时生效

```javascript
this.$preview.on('imageLoadComplete', (e, item) => {
    console.log(this.$preview.self) //此时this.$preview.self拥有原插件photoswipe文档中的所有方法和属性
})
```

//demo 文件夹中 index.html 可以供参考写法
//本次更新后继承了原插件的所有事件、方法和属性，如需复杂使用请多多查看[原插件文档](http://photoswipe.com/documentation/api.html)

//应性能要求 新增大图查看 large 标签填写大图路径 （插件的思路是 img 的 src 默认为缩略图），如不填写 large，则展示 src

```html
<img src="xxx.jpg" large="xxx_3x.jpg" preview="2" preview-text="描述文字" />
```

### 2018-05-17 更新

//如果图片是异步生成的，在图片数据更新后调用：

```javascript
this.$previewRefresh()
```

## Options

[插件配置文档](http://photoswipe.com/documentation/options.html)

## DEMO

[地址](https://826327700.github.io/vue-photo-preview/demo/)
