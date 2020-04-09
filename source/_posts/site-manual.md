---
title: 书源制作手册
date: 2019-06-07 20:21:42
tags:
---
# 书源说明

## CSS SELECTOR 书源
> CSS SELECTOR 书源力求简单易学. 

{% asset_img search-steps.png 网络小说搜索流程 %}
- 搜索结果有3种可能, 先进行特征值判断. 如果没找到特征值, 则按如下优先级解析:
    > 书籍列表 > 章节列表 > 书籍详情
- 书籍列表获取到的链接有2种可能, 先进行特征值判断. 如果没找到特征值, 则按如下优先级解析:
    > 章节列表 > 书籍详情

<!-- more -->

### 格式
```json5
[
  {
    // [必填] 站点网址
    "source": "9dxs.com",
    // [必填] 名字
    "name": "久读小说|9dxs.com",
    // 描述
    "description": "描述书源信息",
    // 注意事项
    "tips": "两次搜索的间隔时间不得少于 30 秒; 搜索关键字必须大于4个字符",
    // 是否原始源
    "original": false,
    // 版本号
    "version": "1.0.0",
    // 评分
    "rating": 10,
    // 书源作者
    "author": "sososdk",
    // 书源作者主页
    "authorHomePage": "https://sososdk.github.io/zhishu",
    
    // === 搜索 ===
    // [必填] 搜索链接
    // 格式: http://xxx.xxx/search?key=%s
    "searchUrl": "https://www.9dxs.com/modules/article/search.php?searchkey=%s&page=1",
    // 搜索是否启用 JavaScript
    "javascriptSearch": true,
    // JavaScript 延时, 单位: 毫秒
    "javascriptSearchDelay": 500,
    // 搜索关键字编码
    // 默认: utf-8
    "searchKeyEncoding": "gbk",
    // 搜索 POST 参数
    "searchPostParams": "searchkey=%s",
    // 搜索 user-agent 默认桌面浏览器
    // 默认: Mozilla/5.0 (Windows NT 6.3; WOW64; rv:27.0) Gecko/20100101 Firefox/27.0
    "searchUserAgent": "Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.131 Mobile Safari/537.36",

    // === 搜索结果 ===
    // 自动检测网页编码
    // 搜索结果有3种可能:
    // 1. 书籍列表
    // 2. 书籍详情
    // 3. 章节列表
    
    // 书籍列表页特征值. 如果在页面发现这个特征值, 则表示页面是书籍列表页
    "booksCharacteristic": "[css selector]",
    // 书籍详情页特征值. 如果在页面发现这个特征值, 则表示页面是书籍详情页
    "detailCharacteristic": "[css selector]",
    // 章节列表页特征值. 如果在页面发现这个特征值, 则表示页面是章节列表页
    "chaptersCharacteristic": "[css selector]",
    // 搜索更多链接
    "searchNext": "@[css selector]@[attr]:[reg]",
    // 必要时通过替换的方式获取 searchNext
    "searchNextFormat": [
      "http://xxx.xxx/xxxx/xxx/search.html?page=%s",
      "@[css selector]@[attr]:[reg]"
    ],

    // 书籍列表
    // [必填] 书籍列表
    "books": "[css selector]",
    // [必填] 书名
    "bookName": "@[css selector]@[attr]:[reg]",
    "bookAuthor": "@[css selector]@[attr]:[reg]",
    "bookWords": "@[css selector]@[attr]:[reg]",
    "bookIcon": "@[css selector]@[attr]:[reg]",
    // 必要时通过替换的方式得到 bookIcon
    "bookIconFormat": [
      "http://xxx.xxx/%s/%s/%s.jpeg",
      "@[css selector]@[attr]:[reg]",
      "@[css selector]@[attr]:[reg]",
      "@[css selector]@[attr]:[reg]"
    ],
    "bookDesc": "@[css selector]@[attr]:[reg]",
    "bookUpdateTime": "@[css selector]@[attr]:[reg]",
    // 内置一部分解析时间规则, 如果不能解析, 请填写
    "bookUpdateTimeFormat": "y-M-d H:m:s",
    "bookCategory": "@[css selector]@[attr]:[reg]",
    // 最新章节
    "bookLastChapterName": "@[css selector]@[attr]:[reg]",
    // 书籍状态(连载|完本): 找到表达式的对象时为完本
    "bookFinished": "@[css selector]@[attr]:[reg]",
    // [必填] 章节列表链接|详情链接
    "bookUrl": "@[css selector]@[attr]:[reg]",
    // 必要时通过替换的方式得到 boolUrl
    // 例如: http://xxx.xxx/xxxx/%s/%s.html
    "bookUrlFormat": [
      "http://xxx.xxx/xxxx/%s/%s.html",
      "@[css selector]@[attr]:[reg]",
      "@[css selector]@[attr]:[reg]"
    ],

    // 搜索页面之外的 user-agent. 默认桌面浏览器
    "userAgent": null,
    // 搜索|章节内容页面之外的 javascript 支持. 默认 false
    "javascript": true,
    "javascriptDelay": 500,
    // === 书籍详情页 ===
    // 补充书籍信息; 获取章节列表链接
    "detailBookName": "@[css selector]@[attr]:[reg]",
    "detailBookAuthor": "@[css selector]@[attr]:[reg]",
    "detailBookWords": "@[css selector]@[attr]:[reg]",
    "detailBookIcon": "@[css selector]@[attr]:[reg]",
    "detailBookIconFormat": [
      "http://xxx.xxx/xxxx/xxx/%s.jpeg",
      "@[css selector]@[attr]:[reg]"
    ],
    "detailBookDesc": "@[css selector]@[attr]:[reg]",
    "detailBookUpdateTime": "@[css selector]@[attr]:[reg]",
    // 内置一部分解析时间规则, 如果不能解析, 请填写
    "detailBookUpdateTimeFormat": "y-M-d H:m:s",
    "detailBookCategory": "@[css selector]@[attr]:[reg]",
    "detailBookLastChapterName": "@[css selector]@[attr]:[reg]",
    "detailBookFinished": "@[css selector]@[attr]:[reg]",
    // 详情链接
    "detailBookUrl": "@[css selector]@[attr]:[reg]",
    "detailBookUrlFormat": [
      "http://xxx.xxx/xxxx/xxx/%s.html",
      "@[css selector]@[attr]:[reg]"
    ],

    // === 章节列表页 ===
    // 1. 分页 2. 不分页
    // 去掉无连接|无章节名的章节
    // 自动去重: 将重复链接去掉, 优先去掉列表前面的章节
    // 进行 chaptersReverse 排序
    "chaptersBookName": "@[css selector]@[attr]:[reg]",
    "chaptersBookAuthor": "@[css selector]@[attr]:[reg]",
    "chaptersBookWords": "@[css selector]@[attr]:[reg]",
    "chaptersBookIcon": "@[css selector]@[attr]:[reg]",
    "chaptersBookIconFormat": [
      "http://xxx.xxx/xxxx/xxx/%s.jpeg",
      "@[css selector]@[attr]:[reg]"
    ],
    "chaptersBookDesc": "@[css selector]@[attr]:[reg]",
    "chaptersBookUpdateTime": "@[css selector]@[attr]:[reg]",
    // 内置一部分解析时间规则, 如果不能解析, 请填写
    "chaptersBookUpdateTimeFormat": "y-M-d H:m:s",
    "chaptersBookCategory": "@[css selector]@[attr]:[reg]",
    "chaptersBookLastChapterName": "@[css selector]@[attr]:[reg]",
    "chaptersBookFinished": "@[css selector]@[attr]:[reg]",
    // 更多章节链接
    "chaptersNext": "@[css selector]@[attr]:[reg]",
    "chaptersNextFormat": [
      "http://xxx.xxx/xxxx/xxx/%s.html",
      "@[css selector]@[attr]:[reg]"
    ],
    // [必填] 章节列表
    "chapters": "[css selector]",
    // [必填] 章节名称
    "chapterName": "@[css selector]@[attr]:[reg]",
    // [必填] 章节链接. 注: chapterUrl 和 chapterUrlFormat 二选一
    "chapterUrl": "@[css selector]@[attr]:[reg]",
    "chapterUrlFormat": [
      "xxxx/xxx/%s.html",
      "@[css selector]@[attr]:[reg]"
    ],
    // 倒序
    "chaptersReverse": false,

    // === 章节内容页 ===
    // 1. 分页 2. 不分页
    "javascriptContent": true,
    "javascriptContentDelay": 500,
    // [必填] 章节内容
    "content": "[css selector]",
    // 更多内容链接
    "contentNext": "@[css selector]@[attr]:[reg]",
    "contentNextFormat": [
      "/xxxx/xxx/%s.html",
      "@[css selector]@[attr]:[reg]"
    ],
    "contentRemove": [
      "[css selector]",
      "[css selector]"
    ],
    "contentReplace": [
      {
        // 是否正则表达式
        "reg": false,
        // 是否 HTML 源码替换, HTML 替换优先文本替换. True: 在 HTML 源码中替换. False: 在文本中替换(不可跨标签)
        "html": false,
        "first": "具**置",
        "second": "具体位置"
      },
      {
        "first": "**大海",
        "second": "汪洋大海"
      }
    ],
  }
]
```

- `[css selector]` 表达式是标准的css选择器, 请参考下面的文档
    
    伪代码:
    ```javascript
    var elements = document.querySelectorAll([css selector]);
    ```

- `@[css selector]@[attr]:[reg]` 表达式
    - `@` 是分隔符, 可用其他字符代替
    - `[css selector]` 是标准的css选择器, 请参考下面的文档
    - `[attr]:[reg]` 可为空, 默认获取 `text`
        - `[attr]` 是需要获取的属性. 例如: `src` `href` `text`; 可以为空, 默认获取 `text`
        - `[reg]` 是正则表达式. 获取 `[attr]` 值后进行正则运算
    
    伪代码:
    ```javascript
    var element = document.querySelector([css selector]);
    var attr = element.getAttribute([attr]);
    var arr = attr.match(new RegExp([reg]));
    var result = arr[0];
    ```

### 相关文档
- [CSS SELECTOR 文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Selectors#%E5%9F%BA%E6%9C%AC%E9%80%89%E6%8B%A9%E5%99%A8)

### 制作教程
> 敬请期待

## JavaScript 书源

> 暂不开放