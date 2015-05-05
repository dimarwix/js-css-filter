# cssfilter
Sanitize untrusted CSS with a configuration specified by a Whitelist. 根据白名单过滤CSS


## 安装

```bash
$ npm install cssfilter --save
```


## 使用方法

```javascript
var cssfilter = require('cssfilter');
var css = cssfilter('position:fixed; width:100px; height:100px; background:#aaa;');
console.log(css);
```

或者：

```javascript
options = {
  // 白名单，可选
  whiteList: {
    a: true,                 // true表示允许
    b: /^fixed|relative$/,   // 正则test()返回true表示允许
    c: function (value) {
      // 返回true表示允许
    },
    d: false                 // 除以上三张外，所有值均表示不允许
  },
  // 当匹配到一个在白名单中的属性时
  onAttr: function (name, value, options) {
    // name为属性名
    // value为属性值
    // 返回字符串表示覆盖此段CSS
    // 不返回任何值表示使用默认生成方法，即 name:value
  },
  // 当匹配到一个不在白名单中的属性时
  onIgnoreAttr: function (name, value, options) {
    // name为属性名
    // value为属性值
  }
};
mycss = new cssfilter.FilterCSS(options);
// then apply mycss.process()
html = mycss.process('position:fixed; width:100px; height:100px; background:#aaa;');
```


## License

```
The MIT License (MIT)

Copyright (c) 2015 Zongmin Lei <leizongmin@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
