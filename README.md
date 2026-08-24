# 牛来人格类型测试 · 网页版

与微信小程序同源数据（31 题 / 16 人格 / 木质调），**纯静态、零依赖**，可直接部署到 Vercel。

## 目录结构

```
mbti-web/
├── index.html     # 单页应用（首页 / 答题 / 结果 / 所有结果）
├── config.js      # 配置（由 mbti-miniprogram/config.js 自动生成，请勿手改）
└── images/        # 16 张人格图 + logo.jpg
```

## 本地预览

直接用浏览器打开 `index.html` 即可（无需服务器）。

## 部署到 Vercel

方式一（CLI，需先安装并登录）：

```bash
npm i -g vercel
vercel login          # 首次登录（浏览器授权）
vercel --prod         # 在 mbti-web 目录下执行
```

方式二（网页拖拽）：登录 [vercel.com](https://vercel.com) → New Project →
Import 时选择本文件夹 → Deploy，即可获得线上地址。

## 与小程序的数据一致性

`config.js` 由 `mbti-miniprogram/config.js` 生成：

```bash
node -e "const fs=require('fs');const c=require('./mbti-miniprogram/config.js');
fs.writeFileSync('mbti-web/config.js','(function(g){g.MBTI_CONFIG='+JSON.stringify(c).replace(/</g,'\\u003c')+';if(typeof module!==\"undefined\")module.exports=g.MBTI_CONFIG;})(typeof window!==\"undefined\"?window:this);')"
```

小程序里改完文案/图片后，重新生成一次网页版 config.js 并重新部署即可。

## 功能

- 首页：Logo 圆形头像 + “测测你是牛来里的谁” + 开始/继续测试
- 答题：31 题、进度条、上一题/下一题、禁止跳过、本地缓存断点续答
- 结果：角色图 + 自定义名称 + MBTI 标签 + 文案 + 四维倾向条
- 所有结果：2 列 × 8 行网格展示 16 人格（图片 + 名称，无文案），左上角返回
- 全部数据存浏览器 localStorage，无后端、无数据上传
