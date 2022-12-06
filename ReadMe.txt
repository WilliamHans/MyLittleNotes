# 这可能是最好、最详细的VSCode开发uni-app教程吧



![这可能是最好、最详细的VSCode开发uni-app教程吧](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ed4231cbf4954e8990cf7cc87181ac75~tplv-k3u1fbpfcp-zoom-crop-mark:3024:3024:3024:1702.awebp?)

## 开始

我们将使用VSCode写`uni-app`，不同于`Hbuilder X`，用VSCode是通过脚手架来创建项目，为什么我要用VSCode写呢？可能还是不太习惯**Hbuilder X**等等原因，还有就是不想换开发工具，觉得开发前端一个VSCode就够了，也不用去比较两者谁好谁坏，自己喜欢哪个用哪个，这里就不过多赘述了。

自己也用VSCode做了几个`uni-app`项目了，主要是写小程序，总体体验下来还是非常不错的。

![VSCode开发uni-app.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/28309fd5d44343bdb154011a82612a29~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

**简述一下**这个教程能给VSCode开发` uni-app`带来的体验

- 增强`pages.json`和`manifest.json`开发体验（语法提示、颜色块、写注释）
- 一键创建页面、组件、分包
- 完善的`API`，组件，uni.scss 变量提示
- 条件编译注释高亮

可以说，VSCode开发`uni-app`的槽点基本上都解决了，有很多地方我觉得体验还更好。

> 文章比较长，写的也比较详细，小白也能看懂。

## 初始化项目

我们使用 vue2 创建工程作为示例，uni-app中Vue2版的组件库和插件也比较多，稳定、问题少，可以先参考下官方文档：[通过vue-cli命令行](https://link.juejin.cn/?target=https%3A%2F%2Funiapp.dcloud.net.cn%2Fquickstart-cli.html%23install-vue-cli)

既然是使用vue脚手架，那肯定要全局安装`@vue/cli`，已安装的可以跳过。

> **注意**：Vue2创建的项目，脚手架版本要用@4的版本，用@5的版本运行项目会报错，这里推荐 **@4.5.15**

```bash
npm install -g @vue/cli@4.5.15
复制代码
```

创建项目，后面是你的项目名字。

```bash
vue create -p dcloudio/uni-preset-vue uni_vue2_cli
复制代码
```

这里我们选择**默认模板**。

![image-20220425115206383](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eb429ef10d764fcd8c4f29032955b5f8~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

在VSCode打开这个项目，可以看看整个项目项目结构，`src`下项目结构跟`HbuilderX`创建的根目录基本一样，说明两种项目转换还是比较方便的。

> **提示**：既然是Vue2项目，有`scss`文件，那肯定要装`vetur`和`sass`这两个插件，这不会有人还没有装吧😅😅。

![image-20220424230550420](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5d6f83638aa04b47b912a4b139816413~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

## tsconfig.json报错问题

> **2022.09 更新**：
>
> 这个问题之前评论区有人提到过，我好久没有去写博客，这个博客放了5个月，收到了非常多的点赞和收藏，感谢支持！
>
> 不过这个教程已经赶不上变化，对此我有必要去更新下这个教程，现在的话，用VSCode开发uni-app的体验比之前更好了。
>
> 目前通过vue-cli命令行创建的项目已经不再只是`tsconfig.json`，只有是使用`ts`的项目才会是`tsconfig.json`，否则会是`jsconfig.json`。所以这个问题已经不存在了。

![image-20220424230750672](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9d479e782b514cf093dc8bafc2585017~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

## 增强pages.json和manifest.json开发体验

### json文件写注释

我们打开`pages.json`和`manifest.json`，发现会报红，这是因为在`json`中是不能写注释的，而在`jsonc`是可以写注释的。

![image-20220424232513887](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/64534de95af14073a8fea774b0d01918~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

**解决方案**：我们把`pages.json`和`manifest.json`这两个文件关联到`jsonc`中，然后就以写注释了。在设置中打开`settings.json`，添加：

![image-20220424233045910](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e260e878eaa5493fa58c879b4332ede9~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

千万不要把所有`json`文件都关联到`jsonc`中，你感觉在`json`中都能写**注释**了，觉得更好用了，其实不然，json就是json，jsonc就是jsonc，这两个是不一样的，例如，你在`package.json`写注释VSCode是不报错了，但**编译**的时候还是会报错的，因为`package.json`就是不能写注释的。

### 语法提示

可以为`pages.json`、`manifest.json`等提供**语法提示**和**校验工作**。如果不使用这个插件，体验会大大折扣，这也是我认为使用vscode开发uni-app必装的一个插件。

![image-20220424234224718](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c82487eaea8b480c87fd79bd8654999c~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

而且鼠标悬浮还有提示，相当的贴心了。

![1.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3fa79c12a26842908ac1eafd0db5a457~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

### 内联颜色修饰器

> **2022.09 更新**：
>
> 我偶然发现在`json`文件中是可以显示VSCode内置的内联颜色修饰器，然后给插件的作者提了个
>
> **issue**，目前`uni-app-schemas`已经可以在`pages.json`等json支持显示**内联颜色修饰器**和**颜色选取器**了！
>
> 也欢迎各位大佬一起去改进🚀🚀🚀**Github**：[uni-helper](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2FModyQyW%2Funi-helper)，这个作者开发过很多和`uni-app`相关的包和vscode插件。
>
> 之前我是推荐使用`Color Highlight`这个插件进行辅助使用，现在已经不需要了，VSCode内置的颜色修饰器显然有着更好的体验。

### 路径提示

安装这个插件，这个我感觉比VSCode自带要好用些。**不使用**的话，不能在`pages.json`等json文件中进行**路径提示**

![image-20220425155336510](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c71bf13737af428aa47509174086a33a~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

如果使用这个插件的话，建议关掉VSCode默认的自动完成

```json
"typescript.suggest.paths": false
"javascript.suggest.paths": false
复制代码
```

并且在`tsconfig.json`or`jsconfig.json`为项目配置**根路径**和**路径别名**，这也是让`VScode`知道路径别名，可以进行跳转。当然你也可以使用插件的全局配置`path-intellisense.mappings`，使用其中一个就行，建议`tsconfig.json`。

`jsconfig.json`文件

```json
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"]
    },
    "types": ["@dcloudio/types", "miniprogram-api-typings", "mini-types"]
  }
}

复制代码
```

然后再顺手推荐一个超实用的插件`Image preview`：鼠标悬停可以预览图片。

![image-20220425154709042](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c55cdc1719f44abe84eab4885de1b242~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

```json
"gutterpreview.showImagePreviewOnGutter": false,// 关闭在行号中显示缩列图
复制代码
```

最终到达的效果

![8](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/be25fb1458b24f6ab0108c3511b777ab~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

## 一键创建页面、组件、分包

然后就是怎么快速创建页面、组件、分包，那就要推荐以下这款插件了，支持一键创建，并且添加到`paegs,json`中。

![image-20220425103031219](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c7fdb3c245d14a0e9510f4cde504b73c~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

![image-20220425103420274](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7581baa91e3945dc9afbc8162f5d1ff7~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

![2](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5155942d6be44b299d34897b4e1aba1d~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

## 条件编译注释高亮

在**Hubilder X**条件注释是有高亮的，以便区分开普通注释，在VSCode也有对应的插件可以实现，不得不说，VSCode的生态真的太好了，要啥插件都有。

> **2022.09 更新**：
>
> **注意**：目前，在`volar`下，该插件会无效，希望后期会修复这个问题。

![image-20220425104159161](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1286f6509652425999a0db6f1ba5e59a~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

![3](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6974d04cbb3d4803aeefb02fbf1d72ac~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

这个插件可以定制化我们的注释，比如**颜色**、**加粗**、**斜体**，怎么好看怎么来。

```json
"better-comments.tags":[
  {
    "tag": "#",
    "color": "#18b566",
    "strikethrough": false,
    "underline": false,
    "backgroundColor": "transparent",
    "bold": true,
    "italic": false
   },
]
复制代码
```

## API，组件，uni.scss语法提示

### API语法提示

用Vue2创建的`uni-app`的cli项目默认是已经安装对应的`Api`语法提示，并且默认已经在`tscongfig.json`or`jsconfig.json`配置好了，有三个：

- **@dcloudio/types**，`uni`语法提示
- **miniprogram-api-typings**，微信小程序`wx`语法提示
- **mini-types**，支付宝小程序`my`语法提示

![Snipaste_2022-09-23_20-48-29.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5fff484ca73743b8b64a236758b8ab6e~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

![4](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f5ae97086e064d2cbb23698fe0808dc5~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

### 组件提示

接下来就是组件语法提示，如`<view>`、`<button>`等uni-app原生组件，这个需要我们手动安装对应的依赖包。

```bash
npm i @dcloudio/uni-helper-json
复制代码
```

![5](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5ee4e73a4f8e4a35888de50f2da07bd0~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

> **2022.09 更新**：
>
> 如果是使用的`vue3`，可以使用`uni-app-types`这个包，因为`@dcloudio/uni-helper-json`不支持`vue3`。

```bash
npm i -D uni-app-types
复制代码
```

然后在`tsconfig.json`or`jsconfig.json`配置`compilerOptions.types`和`vueCompilerOptions`，确保`include` 包含了对应的 `vue` 文件。

```json
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"]
    },
    "types": ["@dcloudio/types", "uni-app-types"]
  },
 "vueCompilerOptions": {
    "experimentalRuntimeMode": "runtime-uni-app"
  },
  "include": ["src/**/*.ts", "src/**/*.d.ts", "src/**/*.tsx", "src/**/*.vue"]
}
复制代码
```

**如果你要使用uniCloud、uni-ui等，可以安装**`uni-cloud-types`、`uni-ui-types`**等**。

还有其他的，可以去这个[uni-helper](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2FModyQyW%2Funi-helper%2Ftree%2Fmain%2Fpackages)看看。

如果你觉得还不够好用，你还可以安装第三方插件来提供和**Hbuilder X**一样的`代码块`，推荐插件：[uni-app-snippets](https://link.juejin.cn/?target=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3DModyQyW.vscode-uni-app-snippets)、[uniapp小程序扩展](https://link.juejin.cn/?target=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Devils.uniapp-vscode)。

### uni.scss变量提示

> **注意**：**cli**创建的uni-app项目，跟web项目一样，需要安装对应的sass模块，才能写scss。安装sass-loader，建议版本@10，否则可能会导致vue与sass的兼容问题而报错。

```bash
npm i sass sass-loader@10 -D
复制代码
```

安装`SCSS IntelliSense`插件，就可以提示你项目中`scss`文件中定义的变量了。

![image-20220425142338060](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fb267231252b4d0d8f95eb27ff7646d0~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

![7](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a671d2a05da349e0be19c8bda748ef43~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

## 运行、发布项目

对应的命令在`package.json`，中，可以自行查看。

- npm run dev:%PLATFORM%
- npm run build:%PLATFORM%

比如：运行至微信小程序的命令：`npm run dev:mp-weixin`

发现命令还是比较长的，其实有更简便的方式，VSCode支持一键运行`npm`**脚本**，我们以微信小程序为例。

![6](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9ccf6e1847ad40d4800c5192cdf72d4d~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

![image-20220425121019517](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6eeddb719106455da8436ba9f0d74740~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

`VSCode`跟`Hbuilder x `不同的是，VSCode不会自动在**微信开发者工具**导入项目并打开，我们需要手动导入项目，只需要导入一次就行了，以后直接打开**微信开发者工具**就行了。

需要注意的是，需要在`manifest.json`配置微信小程序`appid`，不然微信开发者工具会报错。

![image-20220425121331808](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ac3d785499494c7799ca7a874da98041~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

在**微信开发者工具**导入打包出来的文件夹。

![image-20220425121540349](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d0705fa7a1b74c53b391b88f2d46274f~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

![image-20220425121643386](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4c4768d33af84e46b7910468706d6401~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

然后，就可以愉快的写代码了。不管是运行项目，还是差量化编译速度还是非常快的。

## 使用 vue3 创建工程

尤雨溪宣布Vue 3 在 **2022 年 2 月 7 日**成为新的默认版本，但目前uni-app对应的Vue3的**组件库**和**插件**太少了，生态还不成熟。容易遇到问题，不太推荐直接拿去做业务。

使用Vue3创建项目跟Vue2有点区别，Vue3创建的项目采用的是`vite`，有一说一，`vite`是确实快，初始化项目的时候遇到了一些坑，这里说一下。

![image-20220425151032580](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/918716000fb34d0eb7b9633af89e02a9~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

我一开始也卡住了，访问仓库失败，官方文档也说了解决方案，看了下，就是去更新下`@dcloudio/uvm`。

```bash
npx @dcloudio/uvm
复制代码
```

然后再试一下就没问题了，这里以`javascript`模板为例

```bash
npx degit dcloudio/uni-preset-vue#vite uni_vue3_cli
复制代码
```

**还有一个坑**，就是Vue3创建的项目默认不安装`API`**语法提示**依赖，所以要我们手动去安装一下，然后去`tsconfig.json`配置一下。

```bash
npm i @dcloudio/types miniprogram-api-typings mini-types -D
复制代码
```

VSCode有**尤雨溪团队**专门为`Vue3`打造的插件[Volar](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fjohnsoncodehk%2Fvolar)，写Vue3就用 **`Volar`**，再配合`Vite`，开发体验真的很**nice**，这里就不过多讲了。

![image-20220425153428114](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5d253b517cdf48aeb5083f26ebb9770e~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

## DCloud插件市场的使用

VSCode不能像Hbuilder X一样一键导入插件，一般用**cli**创建的项目要使用插件，一般有两种方式，第一种是支持`npm`安装的，那就用`npm`最好，如`uViewUI`，另一种不支持`npm`安装的，那就下载对应的`zip压缩包`，放到项目中，这种一般会有两个版本，我们选择**非uni_modules版本**，如`uCharts`。

![image-20220425124446742](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/23e77ad3f9f24595ad51efd871c61440~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

这点确实没有Hbuilder X方便，不过导入第三方插件这种事情不是经常做，这还是可以接受的。

## 结语

> **2022.09 更新**：
>
> 目前，仓库已经同步uni-app官方最新cli模板，另外我还上传了vue3+vite+ts的版本，可当做示例来供来学习参考。

🚀🚀🚀**Github仓库地址**：[uni-vscode-template](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fxiaodye%2Funi-vscode-template)。

总的来说，配置起来还是比较麻烦的，插件也比较多，但最终获得体验也是非常不错的。

因为`uni-app`项目跟其他前端项目差异较大，我还是比较推荐为`uni-app`项目单独做个VSCode工作区。对于**VSCode工作区概念**，可以看看我的这篇文章：[VSCode工作区指南：回归轻量，打造全能编辑器](https://juejin.cn/post/7066032710778617892)。

或者说，为每个项目单独做一个`settings.json`。

![image-20220425143813426](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/660802c1c3004ba5ab66d13a3f3df489~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

感谢读完本篇文章，希望对你能有所帮助，如有问题或有自己实用的技巧欢迎在评论区分享和讨论。

创作不易，希望可以点个赞支持一下❤️❤️。