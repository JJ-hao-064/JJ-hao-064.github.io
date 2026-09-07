# Jinghao Jiang · 学术个人主页

姜京浩的学术个人主页:**单文件、零依赖、零构建**,推送即自动部署到 GitHub Pages。

- 所有页面内容都在 `index.html` 一个文件里,改完推送 1~2 分钟自动上线
- 纯 HTML + CSS(无框架无构建),自带吸顶导航、经历时间轴、获奖分组、深色模式、手机适配
- 全站资源用**相对路径**引用,不管仓库名是 `用户名.github.io` 还是别的名字都能直接跑

## 目录结构

```
个人主页/
├── index.html                  # 站点本体:全部内容 + 样式都在这里(日常只改它)
├── assets/
│   ├── avatar.svg              # 头像占位图 → 换成你的 avatar.jpg
│   ├── banner.svg              # About 头部背景图 → 可换成你的照片
│   ├── cv.pdf                  # 对外发布的简历(CV 按钮指向它)
│   └── teaser-placeholder.svg  # 论文缩略图占位(暂未用到)
├── .github/workflows/deploy.yml  # GitHub Actions:push 到 main 自动部署
├── .nojekyll                   # 告诉 GitHub Pages 跳过 Jekyll 处理
├── .gitignore                  # 忽略 .DS_Store、简历原件等
└── README.md
```

## 本地预览

```bash
cd ~/Desktop/个人主页
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

(直接双击 `index.html` 也能看,但起本地服务和线上一致。)

## 怎么更新内容(日常维护)

打开 `index.html`,顶部有一段"修改指南"注释,对应关系:

| 想改什么 | 怎么做 |
|---|---|
| 加新闻 | 在 News 里复制一行 `<li>`,新的放最上面 |
| 加论文/专利 | 在 Publications & Patents 里复制一个 `<article class="paper">...</article>` 整块 |
| 加经历 | 复制一个 `<article class="exp-item">...</article>` 整块;时间轴上再复制一个 `<a class="tl-seg">` 并按公式改 `left/width` 百分比(公式写在时间轴代码的注释里) |
| 加获奖 | Awards 板块里:分组标题直接改文字,加一条 = 复制一行 `<li>`,新的放最上面;不要的分组连标题一起删 |
| 头像 | 照片存为 `assets/avatar.jpg`,把 `<img class="avatar">` 的 `avatar.svg` 改成 `avatar.jpg` |
| 背景横幅 | 替换 `assets/banner.svg`(或改 `banner.jpg` 并更新 CSS 里 `.hero` 的 `url(...)`);图上文字是白色,图太亮就调大遮罩透明度 |
| 社交链接 | GitHub / Google Scholar 的 `<a>` 已注释好,填入 ID 取消注释即可 |
| 调导航栏 | 编辑 `<nav class="nav">` 里的 `<a>`,`href="#xxx"` 对应各板块 `id`;删板块时记得同步删链接 |
| 简历更新 | 用新简历覆盖 `assets/cv.pdf`(文件名保持 `cv.pdf`) |

改完保存、本地刷新确认没问题就可以发布了。

## 首次部署(一次性,3 步)

**① 在 GitHub 新建仓库**,两种命名任选:

- `你的用户名.github.io` → 网址 `https://你的用户名.github.io`(最干净,推荐)
- 其他名字(如 `homepage`)→ 网址 `https://你的用户名.github.io/homepage/`(页面全是相对路径,无需改代码)

**② 推送仓库**(仓库已在本文件夹初始化并完成首次提交):

```bash
cd ~/Desktop/个人主页
git remote add origin git@github.com:你的用户名/仓库名.git
git push -u origin main
```

**③ 打开网页版仓库 → Settings → Pages → Build and deployment 下的 Source 选择 "GitHub Actions"** → Save。

然后到仓库 **Actions** 标签页看 "Deploy to GitHub Pages" 跑完(约 1 分钟),网址就生效了。

> 如果是用 SSH 推送报权限错误:先在 GitHub 配置 SSH key,或改用 HTTPS 地址 + Personal Access Token。

## 日常发布

```bash
git add -A && git commit -m "update: xxx" && git push
```

推送后 Actions 自动部署,1~2 分钟生效;可在仓库 Actions 页看进度。

## 可选进阶

- **自定义域名**:仓库根目录加 `CNAME` 文件(内容只有你的域名),DNS 加一条 CNAME 记录指向 `你的用户名.github.io`
- **访问统计**:页脚前插入 Google Analytics 或 [不蒜子](https://busuanzi.ibruce.info/) 一段代码
- **内容多了**:以后要博客/多页站可迁移到 [al-folio](https://github.com/alshedivat/al-folio)(Jekyll)或 Hugo

## 隐私提醒

`assets/cv.pdf` 是**公开展示**的简历,里面包含手机号;不想公开手机号的话,发布前用删掉联系方式的版本覆盖 `assets/cv.pdf`(页面 Email 按钮已单独写,不受影响)。
