# Bootlint-Customization

[![NPM version](https://img.shields.io/npm/v/bootlint.svg)](https://www.npmjs.com/package/bootlint)
[![Build Status](https://img.shields.io/travis/twbs/bootlint/master.svg)](https://travis-ci.org/twbs/bootlint)
[![Coverage Status](https://img.shields.io/coveralls/twbs/bootlint.svg?branch=master)](https://coveralls.io/r/twbs/bootlint)
![Development Status :: 5 - Production/Stable](https://img.shields.io/badge/maturity-stable-green.svg "Development Status :: 5 - Production/Stable")
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg "MIT License")](https://github.com/twbs/bootlint/blob/master/LICENSE)
[![Dependency Status](https://img.shields.io/david/twbs/bootlint.svg)](https://david-dm.org/twbs/bootlint)
[![devDependency Status](https://img.shields.io/david/dev/twbs/bootlint.svg)](https://david-dm.org/twbs/bootlint?type=dev)

为[Bootstrap](https://getbootstrap.com/)项目开发的一个HTML的[linter](https://en.wikipedia.org/wiki/Lint_%28software%29)

## 什么是 Bootlint-Customization?

Bootlint-Customization是在Bootlint的基础上做了一些定制的开发，因为我们队Bootstrap的组件进行了一些增加，因此官方的Bootlint对新增的结构不可能支持的，所以我们只能自己动手做一些调整了，再次，非常感谢Bootstrap团队和Bootlint团队的辛勤工作。

## 什么是 Bootlint?

Bootlint是一个工具，用来检查在页面中使用[Bootstrap](https://getbootstrap.com/)时一些常见的HTML错误。Vanilla Bootstrap的组件/小部件要求其部分DOM符合某些结构。Bootlint会检查Bootstrap组件实例的DOM结构是否正确，Bootstrap的最佳用法还要求您的页面包括特定的<meta>标记、HTML5 doctype声明等；Bootlint检查这些是否存在。

### 注意事项

BooLink假设你的网页已经是有效的HTML5页面。如果您需要检查HTML5的有效性，我们推荐一些工具，比如[`vnu.jar`](https://validator.github.io/validator/)，[grunt-html](https://www.npmjs.org/package/grunt-html)，或[grunt-html-validation](https://www.npmjs.org/package/grunt-html-validation)。

BootLink假设您在网页中使用Bootstrap的默认类名，而不是利用Less或Sass 的“mixins”功能将它们映射到自定义类名。如果你使用mixins，BooLink可以报告一些不正确警告。当然，即使您使用mixins，也有一些适用于BooLink检查的。

## 入门

### 通过Grunt

通过[Grunt](https://gruntjs.com/)来使用Bootlint , 请使用官方Grunt插件: [grunt-bootlint](https://github.com/twbs/grunt-bootlint).

### 通过Gulp

如果你通过[Gulp](https://gulpjs.com/)来使用Bootlint, 有一个 *非官方* 的Gulp插件: [gulp-bootlint](https://github.com/tschortsch/gulp-bootlint)，当然我们需要使用定制的Gulp插件: [gulp-bootlint-customization](https://github.com/alex1221/gulp-bootlint-customization)

### 在命令行中

安装模块: `npm install -g bootlint-customization`

在一些HTML文件上运行它:

```shell
bootlint /path/to/some/webpage.html another_webpage.html [...]
```

这将输出适用于每个文件的lint警告.

CLI还接受一个 `--disable` (or `-d`) 选项来禁用某些lint检查。 `--disable` 采用逗号分隔的[lint问题列表](https://github.com/alex1221/bootlint-customization/wiki). 下面是列子:

```shell
bootlint -d W002,E020 /path/to/some/webpage.html another_webpage.html [...]
```

CLI也将处理 `stdin` 输入，这意味着您可以pipe输入Bootlint:

```shell
cat mypage.html | bootlint
```

或者你可以使用heredoc语法（主要用于快速测试）:

```shell
bootlint << EOF
<button class="btn btn-default">Is this correct Bootstrap markup, Bootlint?</button>
EOF
```

### 在浏览器中

Bootlint可以直接在浏览器中运行！这是通过[书签](https://en.wikipedia.org/wiki/Bookmarklet)来实现的，后者将bootlint附加到活动页面的主体。在浏览器中直接运行bootlint有几个好处。他们包括：

1. 在AJAX请求完成后检测页面结构。
2. 检测动态创建的服务器端页面（例如：CMS）。
3. 检测没有构建脚本的页面/网站。

#### 怎么安装书签

请按照以下说明启动并运行：

1. 在浏览器中创建一个新书签
2. 将名称/标题设置为易记的东西。例如：运行Bootlint
3. 将网址设置为

```js
javascript:(function(){var s=document.createElement("script");s.onload=function(){bootlint.showLintReportForCurrentDocument([]);};s.src="https://maxcdn.bootstrapcdn.com/bootlint/latest/bootlint.min.js";document.body.appendChild(s)})();
```
注意：上面的代码片段将确保您始终运行最新版本的bootlint。如果你想运行bootlint的特定版本，请参阅[BootstrapCDN](https://www.bootstrapcdn.com/bootlint/)。复制网址并更新 `s.src="PASTE-ME-HERE"`。

#### 如何使用书签

1. 点击您在上面创建的书签
2. 将出现一个弹出窗口，通知您是否检测到问题
3. 如果存在问题，请打开开发人员工具并选择控制台选项卡

#### 备选方案

##### 浏览器就绪脚本

您可以手动下载[Bootlint浏览器就绪脚本](https://github.com/alex1221/bootlint-customization/blob/master/dist/browser/bootlint.js).

##### 第三方服务

BooLink还可以作为[bootlint.com](http://www.bootlint.com/)的非官方第三方Web服务，它只需输入一个URL，类似于[W3C标记验证服务](http://Valual.W3.org/)。**请注意** 我们*不*运行此服务，因为它可能使用一个过时的BooLink版本。因此，这不是推荐使用BooLink的方式。

## Lint问题的解释

有关每个lint问题的详细说明, [请在我们的wiki中查找ID](https://github.com/alex1221/bootlint-customization/wiki) (例如：[`E001`](https://github.com/alex1221/bootlint-customization/wiki/E001) or [`W002`](https://github.com/alex1221/bootlint-customization/wiki/W002))。

## API文档

Bootlint是[CommonJS模块](http://wiki.commonjs.org/wiki/Modules/1.1)。

Bootlint代表使用  `LintError` 和 `LintWarning` 类报告的lint问题：

* `LintWarning`
  * 代表一个潜在的错误。它可能有误报。
  * 构造函数: `LintWarning(id, message, elements)`
  * 属性:
    * `id` - 这种类型的lint问题的唯一字符串ID。形式为“W ###”（例如“W123”）
    * `message` - 描述问题的字符串
    * `elements` - 引用DOM元素的jQuery或Cheerio集合，指向文档中的所有问题位置
      * (**仅在Node.js下可用**): 当从底层HTML分析器（大多数情况下）可用时, 集合中的DOM元素将有一个 `.startLocation` 属性，该属性是一个 `Location`(见下文)，指示文档HTML源中的元素的位置。
* `LintError`
  * 代表错误。根据上述“注意事项”部分所述的假设，不应该有任何误报。
  * 构造函数: `LintError(id, message, elements)`
  * 属性:
    * `id` - 这种类型的lint问题的唯一字符串ID。形式为“E ###”（例如“E123”）。
    * `message` - 描述问题的字符串
    * `elements` - 引用DOM元素的jQuery或Cheerio集合，指向文档中的所有问题位置
      * (**仅在Node.js下可用**): 当从底层HTML分析器（大多数情况下）可用时, 集合中的DOM元素将有一个 `.startLocation` 属性，该属性是一个 `Location`(见下文)，指示文档HTML源中的元素的位置。

Bootlint定义了以下公用类:

* `Location` (**仅在Node.js下可用**)
  * 代表HTML源代码中的一个位置
  * 构造函数: `Location(line, column)`
  * 属性:
    * `line` - 基于0的行号
    * `column` - 基于0的列号

一个 ***reporter*** 是一个函数，它只接受一个参数 `LintWarning` 或 `LintError` 。它的返回值被忽略。它应该以某种方式记录问题或将其显示给用户。

### 浏览器

Bootlint在 `window` 对象添加一个 `bootlint` 属性。
在浏览器环境中，以下公共API可用：

* `bootlint.lintCurrentDocument(reporter, disabledIds)`: Lints当前文档的HTML结构，并将每个lint出的问题作为参数回调给 `reporter()` 函数。
  * `reporter` 是一个 *reporter* 函数 (见上面的定义). 它包含每个lint出的问题作为参数被回调
  * `disabledIds` 是一个要禁用的 `linter id` 字符串数组
  * 什么也没有返回 (即： `undefined`)
* `bootlint.showLintReportForCurrentDocument(disabledIds, alertOpts)`: Lints当前文档的HTML结构并向用户输出结果。每个警告将分别使用 `console.warn()` 输出。.  
  * `disabledIds` 是一个要禁用的 `linter id` 字符串数组
  * `alertOpts` 是具有以下属性的可选选项对象:
    * `hasProblems` (type: `boolean`; default: `true`) - `window.alert()` 如果有lint出任何问题，一个普通的通知消息给用户?
    * `problemFree` (type: `boolean`; default: `true`) - `window.alert()` 如果没有lint问题，通知消息给用户?
  * 什么也没有返回 (即： `undefined`)

### Node.js

例:

```js
var bootlint = require('bootlint');

function reporter(lint) {
    console.log(lint.id, lint.message);
}

bootlint.lintHtml("<!DOCTYPE html><html>...", reporter, []); // calls reporter() repeatedly with each lint problem as an argument
```

在Node.js环境中，Bootlint公开以下公共API:

* `bootlint.lintHtml(html, reporter, disabledIds)`: Lints制定HTML页面并返回一个linting结果.
  * `html` 字符串形式的HTMl链接
  * `reporter` 是一个 *reporter* 函数 (见上面的定义). 它包含每个lint出的问题作为参数被回调
  * `disabledIds` 是一个要禁用的 `linter id` 字符串数组
  * 什么也没有返回 (即： `undefined`)

### HTTP API

Bootlint也可以在HTTP服务器运行，公开一些简单的API。使用 `npm run start` 运行服务。

默认情况下，运行端口为 `7070`。设置 `$PORT` 环境变量可以更改它使用的端口。

将HTML文档POST到 `/` ，文档的lint问题将作为JSON返回。

端点接受一个可选的列表字符串参数，名为 `disable` ，它的值是一个以逗号分隔的 `linter id` 列表表示禁用。

列:

```http
Request:
  POST / HTTP/1.1
  Content-Type: text/html

  <!doctype html>
  ...

Response:
  HTTP/1.1 200 OK
  Content-Type: application/json

  [
    {
      "id": "W003",
      "message": "<head> is missing viewport <meta> tag that enables responsiveness"
    },
    {
      "id": "W005",
      "message": "Unable to locate jQuery, which is required for Bootstrap's JavaScript plugins to work"
    },
    ...
  ]
```

## 特别说明

该项目的编码风格在ESLint配置中进行了规划。为任何新的或更改的功能添加单元测试。使用npm脚本测试你的代码

_另外，请不要编辑“dist”子目录中的文件，因为它们是通过 `npm run dist` 生成的。你会在“src”子目录中找到源代码！_

## 发布历史

### bootlint-customization发布历史

* 2018-05-25 - v1.0.0: 第一次发布。

### bootlint发布历史

See the [GitHub Releases page](https://github.com/twbs/bootlint/releases) for detailed changelogs.

* (next release) - `master`
* 2015-11-25 - v0.14.2: Fix critical CLI bug introduced in v0.14.0 and add tests to prevent its recurrence. Update current Bootstrap version to v3.3.6.
* 2015-11-16 - v0.14.1: Forgot to regenerate browser version when tagging v0.14.0
* 2015-11-16 - v0.14.0: Adds 3 new lint checks.
* 2015-11-15 - v0.13.0: Removes E036. Adds a few new checks. Bumps dependency versions.
* 2015-03-16 - v0.12.0: Adds warning if Bootstrap v4 is detected (since Bootlint is currently only compatible with Bootstrap v3). Minor fixes to some existing lint checks.
* 2015-02-23 - v0.11.0: Adds several new lint checks. Improves stdin handling. Bumps dependency versions.
* 2015-01-21 - v0.10.0: By default, the in-browser version now `alert()`s when no lint problems are found. Adds validity check for carousel control & indicator targets.
* 2015-01-07 - v0.9.2: Fixes a problem when using the CLI via node's `child_process.exec`.
* 2014-12-19 - v0.9.1: Fixes a W013 false positive.
* 2014-12-18 - v0.9.0: Fixes several small bugs and tweaks a few existing checks. Adds 4 new lint checks.
* 2014-11-07 - v0.8.0: When in a Node.js environment, report the locations of the HTML source code of problematic elements.
* 2014-11-01 - v0.7.0: Tweaks lint message texts. Adds 1 new lint check.
* 2014-10-31 - v0.6.0: Fixes crash bug. Adds some new lint checks. Adds HTTP API.
* 2014-10-16 - v0.5.0: Adds several new features. Adds official bookmarklet. Disables auto-lint-on-load in browser. Tweaks some checks. **Not backward compatible**
* 2014-10-07 - v0.4.0: Adds checks for correct Glyphicon usage and correct modal DOM structure; fixes `.panel-footer` false positive
* 2014-09-26 - v0.3.0: Several bug fixes and enhancements. **Not backward compatible**
* 2014-09-23 - v0.2.0: First formal release. Announcement: <https://blog.getbootstrap.com/2014/09/23/bootlint/>

## License

Copyright (c) 2014-2017 The Bootlint Authors. Licensed under the MIT License.
