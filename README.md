# MD电竞官网 - 维护说明

## 目录结构

```
/
├── index.html          页面结构（一般不用改）
├── css/
│   └── style.css        样式（一般不用改）
├── js/
│   ├── products.js      ★ 所有项目数据，新增/改价/删除项目改这里
│   └── app.js            页面逻辑（联系方式、下单表单地址在这里改）
└── images/
    ├── products/         项目封面图 + 详情图放这里
    ├── banner/            收款码等横幅图片
    └── icons/             预留
```

## 以后怎么新增一个项目？

1. 把封面图、详情图丢进 `images/products/` 文件夹（文件名自己起，比如 `b6-cover.jpg`）。
2. 打开 `js/products.js`，在 `PRODUCTS` 数组里复制一份现有的项目对象，
   改成新项目的信息，把 `cover` / `detailImage` 填成刚才上传的图片路径。
3. 保存、上传到 GitHub，页面会自动更新，不用改 `index.html`。

## 怎么改价格 / 简介 / 下架某个项目？

- 改价格、简介：在 `js/products.js` 里找到对应项目，直接改字段。
- 下架某个项目：把它对应的那一整段对象删掉，或者暂时用 `//` 注释掉即可。

## 怎么新增一个分类？

不用手动加分类，只要在 `js/products.js` 新项目的 `cat` 字段填一个新的值
（比如 `peiwan`），页面顶部会自动多出一个分类 Tab。
如果想要这个分类有专属的中文名字和图标，去 `products.js` 顶部的
`CATEGORY_META` 里加一行就行，不加也不会报错（会直接显示 cat 原始值）。

## 手游/端游价格不同怎么配置？

不用做二级页面，详情页里会直接出现"手游／端游"按钮，点哪个价格就变成哪个，
下单按钮也会跳到对应平台的表单。

在 `js/products.js` 里，把这个项目的 `price` / `unit` 换成 `platforms` 数组：

```js
platforms: [
  { key: 'mobile', label: '手游', price: 60, unit: '局', desc: '60r保底600w', formUrl: '手游表单地址' },
  { key: 'pc',     label: '端游', price: 80, unit: '局', desc: '80r保底600w', formUrl: '端游表单地址' },
],
```

参考 `products.js` 里的 `b1` 项目就是这么写的。没有 `platforms` 字段的项目，
跟以前一样只显示单一价格，不受影响。

## 联系方式 / 下单表单地址

在 `js/app.js` 顶部：

```js
const ORDER_FORM_URL = '...'; // 腾讯文档等收单表单地址
const CONTACT = {
  wechatId: 'your_wechat_id',
  qq: '000000000',
};
```

## 图片说明

- 全部使用「路径引用」，没有使用 Base64，图片文件和代码是分开的，
  以后可以直接在 GitHub 网页端上传/替换/删除图片文件，不用碰代码。
- 某个项目暂时没有图，把 `cover` / `detailImage` 留空字符串 `""` 即可，
  卡片会自动显示一个分类图标占位，不会破图。
