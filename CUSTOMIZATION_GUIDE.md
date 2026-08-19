# 824legend 个人简历网站 · 自定义修改指南

> 适用对象：希望自行维护本站内容的任何人（不需要会编程，只需会改 YAML / Markdown 文本）。
> 核心原则：**内容与样式彻底分离** —— 改内容只动 `content/` 与 `data/`，改外观动 `config/_default/`，底层框架（`_vendor/`）不要碰。

---

## 0. 项目速览

| 项目 | 说明 |
| --- | --- |
| 站点性质 | 个人学术简历网站（HugoBlox 官方 `academic-cv` 模板） |
| 站主 | 曾磊（厦门大学经济学院金融专硕） |
| 技术栈 | Hugo（0.164.0）+ Tailwind CSS v4 + Pagefind 搜索 + pnpm |
| 内容形式 | 纯 Markdown + YAML，无数据库，无锁定性 |
| 部署方式 | GitHub Actions 推送至 GitHub Pages（`main` 分支触发） |
| 关键配置文件 | `hugoblox.yaml`（Hugo 版本 + 部署目标） |

---

## 1. 目录结构与职责（三层架构）

```
824legend/
├── config/_default/        ← 配置层：站点「怎么呈现」（外观、导航、语言）
│   ├── hugo.yaml            站点标题 / 域名 / 语言 / 输出格式
│   ├── params.yaml          品牌名、主题色、排版、页头页脚、SEO、统计
│   ├── menus.yaml           顶部导航菜单
│   ├── languages.yaml       多语言设置（当前仅 zh）
│   └── module.yaml          Hugo 模块挂载（一般不动）
├── content/                ← 内容层：站点「展示什么」（页面与条目）
│   ├── _index.md            首页（板块编排，核心）
│   ├── experience.md        经历页（板块编排）
│   ├── authors/_index.md    作者页开关（保持默认）
│   ├── blog/                博客区（当前为空，可扩展）
│   ├── courses/             课程区（当前为空，可扩展）
│   ├── events/              讲座/演讲区（当前为空，可扩展）
│   ├── projects/            项目条目（现有 3 个）
│   └── publications/        论文条目（现有 1 篇）
├── data/authors/me.yaml    ← 内容层：★个人资料单一真源（最重要）
├── layouts/_partials/      ← 引擎层：用户自定义覆盖（footer 等）
├── assets/media/           ← 引擎层：头像、图标等图片资源
├── static/uploads/         ← 引擎层：可直接下载的文件（简历 PDF）
├── _vendor/                ← 引擎层：HugoBlox 主题模块缓存（勿动！）
├── hugoblox.yaml           ← 顶层配置：Hugo 版本 + 部署目标
├── netlify.toml            ← 残留的 Netlify 部署配置（当前未使用）
└── .github/workflows/      ← GitHub Actions 自动构建部署脚本（一般不动）
```

---

## 2. 修改速查表（想改什么 → 改哪里）

| 你想改的内容 | 改哪个文件 | 具体位置 | 难度 |
| --- | --- | --- | --- |
| 姓名 / 头衔 / 个人简介 | `data/authors/me.yaml` | `name` / `status` | ★ |
| 联系邮箱 / 电话 | `data/authors/me.yaml` | `links` | ★ |
| 教育背景 | `data/authors/me.yaml` | `education` | ★ |
| 实习 / 工作经历 | `data/authors/me.yaml` | `experience` | ★ |
| 技能 / 证书 | `data/authors/me.yaml` | `skills` | ★ |
| 奖项荣誉 | `data/authors/me.yaml` | `awards` | ★ |
| 语言能力 | `data/authors/me.yaml` | `languages` | ★ |
| 研究兴趣 | `data/authors/me.yaml` | `interests` | ★ |
| 头像照片 | `assets/media/authors/me.jpg` | 同名替换图片文件 | ★ |
| 简历 PDF | `static/uploads/resume.pdf` | 同名替换 PDF 文件 | ★ |
| 首页「研究方向」文字 | `content/_index.md` | `markdown` block 的 `text` | ★ |
| 首页板块增删 / 顺序 | `content/_index.md` | `sections` 数组 | ★★ |
| 经历页板块（技能/奖项标题） | `content/experience.md` | `sections` | ★ |
| 新增 / 修改项目 | `content/projects/<名称>/index.md` | 新建或编辑 | ★★ |
| 新增 / 修改论文 | `content/publications/<名称>/index.md` | 新建或编辑 | ★★ |
| 顶部导航菜单 | `config/_default/menus.yaml` | `main` 列表 | ★ |
| 站点域名 / 默认语言 | `config/_default/hugo.yaml` | `baseURL` / `defaultContentLanguage` | ★ |
| 品牌名（页头/页脚/浏览器标题） | `config/_default/params.yaml` | `hugoblox.identity.name` | ★ |
| 站点副标题 / SEO 描述 | `config/_default/params.yaml` | `hugoblox.identity.tagline/description` | ★ |
| 主题色 / 明暗模式 | `config/_default/params.yaml` | `hugoblox.theme` | ★★ |
| 字体 | `config/_default/params.yaml` | `hugoblox.typography.pack` | ★ |
| 圆角 / 间距 / 头像形状 | `config/_default/params.yaml` | `hugoblox.layout` | ★ |
| 页头搜索 / 主题切换按钮 | `config/_default/params.yaml` | `hugoblox.header` | ★ |
| 页脚样式 / 版权文案 | `config/_default/params.yaml` | `hugoblox.footer` / `copyright` | ★ |
| 评论系统（giscus/disqus） | `config/_default/params.yaml` | `hugoblox.comments` | ★★ |
| 统计（GA/百度统计等） | `config/_default/params.yaml` | `hugoblox.analytics` | ★ |
| 数学公式渲染 | `config/_default/params.yaml` | `hugoblox.content.math.enable` | ★ |
| 页脚自定义 HTML | `layouts/_partials/site_footer.html` | 整体替换 | ★★★ |
| 部署目标 / Hugo 版本 | `hugoblox.yaml` | `deploy.host` / `build.hugo_version` | ★★ |

> ★=复制粘贴即可；★★=需理解结构；★★★=涉及 Hugo 模板语法，谨慎操作。

---

## 3. 核心文件详解

### 3.1 `data/authors/me.yaml` —— 个人资料（最重要，先学这个）

这是全站**信息最集中**的文件，首页、经历页、论文作者都从这里取数据。

```yaml
schema: hugoblox/author/v1     # 固定，勿改
slug: me                       # 标识符，页面引用 username: me 即指本文件
is_owner: true

name:
  display: 曾磊                # 显示名（全站展示用）
  given: 磊                    # 名
  family: 曾                   # 姓
  alternate: Zeng Lei          # 英文名
  pronunciation: ''            # 音标（可留空）
  pronouns: he/him             # 人称代词（可留空）
  postnominals: []             # 头衔后缀，如 [PhD]，可留空

status:
  icon: "📈"                   # 状态栏 emoji
  role: 金融专硕硕士研究生       # 头衔
  bio: |                       # 个人简介（首页展示）
    曾磊，厦门大学经济学院金融专硕硕士研究生……（多行文本，保持缩进）

affiliations:                  # 所属机构（可多条）
  - name: 厦门大学经济学院
    url: https://economic.xmu.edu.cn/

links:                         # 联系方式（图标名见 HugoBlox 图标库）
  - icon: at-symbol            # at-symbol=邮箱, phone=电话
    url: mailto:xxx@xx.com
    label: 电子邮箱
  - icon: phone
    url: tel:1xxxxxxxxxx
    label: 手机

interests:                     # 研究兴趣（首页「研究兴趣」卡片）
  - 量化金融
  - 金融工程

education:                     # 教育经历（每段一个 -）
  - degree: 金融专硕（硕士）
    institution: 厦门大学经济学院
    start: 2024-09-01          # 日期格式 YYYY-MM-DD
    end: 2027-06-30            # 在校可写未来日期；结束则写实际日期
    summary: |                 # 支持多行（GPA、课程等）
      GPA: 3.88/4.00（排名 1/93）
      主修课程：……

experience:                    # 实习/工作经历（每段一个 -）
  - role: 金融工程暑期实习生    # 职位
    org: 深圳证券交易所 会员管理部  # 单位
    start: 2026-07-01
    end: 2026-09-30
    summary: |                 # 成果描述（支持多行、自动渲染为列表）
      第一点工作成果……
      第二点工作成果……

skills:                        # 技能（分组展示，首页按 name 分组）
  - name: 编程与软件           # 组名
    items:
      - label: Python          # 技能名
        level: 5               # 熟练度 1-5，控制进度条长度
      - label: DolphinDB
        level: 4

languages:                     # 语言能力
  - name: 中文
    level: 5                   # 1-5
    label: 母语                # 补充说明

awards:                        # 奖项（每段一个 -）
  - title: 鸿儒奖学金
    awarder: 鸿儒金融教育基金会 # 颁奖单位
    date: "2025-12-01"        # 日期用引号包裹更安全
    summary: 全国20名获奖硕士生之一  # 可留空 ""
    icon: hero/trophy          # 图标：hero/trophy、hero/academic-cap、hero/star
```

**改完要点**：只改值，不改键名与缩进（YAML 对缩进敏感，统一用两个空格）。

### 3.2 `config/_default/params.yaml` —— 站点外观与功能

所有内容都挂在 `hugoblox:` 下，常用项：

```yaml
hugoblox:
  identity:                    # 站点品牌（注意：与 me.yaml 的 name 两处都要同步）
    name: "曾磊"               # 页头/页脚/浏览器标题
    tagline: "金融专硕硕士研究生 | 量化金融研究"
    description: "……SEO 描述……"
    social:
      twitter: ""              # Twitter/X 用户名（可留空）

  theme:                       # 主题
    mode: system               # light | dark | system（跟随系统）
    pack: "default"            # 主题包名
    colors:                    # 覆盖主题色（可留空）
      primary: ""              # 例: "indigo" 或 "#6366f1"
      secondary: ""
      neutral: ""

  typography:
    pack: "academic"           # 字体包：academic | developer | editorial ...

  layout:
    radius: "md"               # none | sm | md | lg | full（卡片圆角）
    spacing: "spacious"        # compact | comfortable | spacious
    avatar_shape: circle       # circle | square | rounded（头像形状）

  header:                      # 页头导航
    enable: true
    style: navbar
    sticky: true               # 滚动时吸顶
    align: center
    search: true               # 搜索框开关（需配合 Pagefind）
    theme_toggle: true         # 明暗切换按钮
    theme_picker: true
    language_switcher: true
    cta:                       # 页头右侧按钮（默认关闭）
      enable: false
      text: ""
      url: ""

  footer:
    style: minimal             # minimal | columns | centered

  copyright:
    notice: "© {year} {name}"  # 支持占位符 {year} {name} {license}

  content:
    math:
      enable: false            # 改为 true 启用 LaTeX 数学公式
    toc:
      enable: true             # 目录
    citations:
      style: apa               # apa | mla | chicago | ieee

  search:
    enable: true               # 全站搜索

  comments:                    # 评论（默认关闭）
    enable: false
    provider: ""               # giscus | disqus

  analytics:                   # 统计（留空=关闭）
    google:
      measurement_id: ""       # GA4: G-XXXXXXXXXX
    baidu:
      site_id: ""

  pro:
    hide_attribution: true     # 隐藏「Powered by HugoBlox」
```

### 3.3 `config/_default/hugo.yaml` —— 站点基础设置

```yaml
title: ''                                   # 留空即可（品牌名在 params.yaml 设置）
baseURL: 'https://example.com/'             # ⚠️ 占位符！上线前必须改成真实域名
defaultContentLanguage: zh                  # 默认语言
hasCJKLanguage: true                        # 中文站点必须为 true（否则字数统计不准）
enableEmoji: true                           # 支持 emoji
pagination:
  pagerSize: 10                             # 每页条数
taxonomies:                                 # 分类法（一般不动）
  author: authors
  tag: tags
  publication_type: publication_types
```

### 3.4 `config/_default/menus.yaml` —— 导航菜单

```yaml
main:
  - name: 简介        # 显示文字
    url: /            # 链接
    weight: 10        # 权重越小越靠前
  - name: 论文
    url: /#papers     # 锚点链接（跳转首页某板块，需与 _index.md 的 block id 对应）
    weight: 11
  - name: 项目
    url: /#projects
    weight: 12
  - name: 经历
    url: experience/  # 相对路径页面
    weight: 20
```

> 提示：`/#papers` 指向首页中 `id: papers` 的 collection 板块；删改首页板块时记得同步菜单。

### 3.5 `content/_index.md` —— 首页板块编排（核心中的核心）

首页由 `sections` 数组从上到下渲染，每个 `- block:` 是一块：

```yaml
---
title: ''
type: landing          # 固定，landing 类型页面

sections:
  # 板块 1：个人简介（头像 + 姓名 + 简介 + 按钮）
  - block: resume-biography-3
    content:
      username: me                    # 指向 data/authors/me.yaml
      text: ''                        # 可追加文字
      button:
        text: 下载简历
        url: uploads/resume.pdf       # 对应 static/uploads/resume.pdf
      headings:
        about: '关于我'
        education: '教育背景'
        interests: '研究兴趣'
    design:
      background:
        gradient_mesh:
          enable: true                # 渐变网格背景
      name:
        size: md                      # xs|sm|md|lg|xl
      avatar:
        size: medium                  # small|medium|large|xl|xxl
        shape: circle

  # 板块 2：自由 Markdown 文本块
  - block: markdown
    content:
      title: '研究方向'
      text: |-                        # |- 表示保留换行的多行文本
        第一段……
        第二段……

  # 板块 3：论文集合（featured 标记的论文）
  - block: collection
    id: papers                        # 锚点 id，供菜单 /#papers 跳转
    content:
      title: 学术论文
      filters:
        folders:
          - publications
        featured_only: true           # 只显示 featured: true 的论文
    design:
      view: article-grid              # 展示样式
      columns: 2

  # 板块 4：全部论文
  - block: collection
    content:
      title: 全部论文
      filters:
        folders:
          - publications
        exclude_featured: false
    design:
      view: citation                  # 引用样式

  # 板块 5：项目集合
  - block: collection
    id: projects
    content:
      title: 科研与项目经历
      filters:
        folders:
          - projects
    design:
      view: article-grid
      columns: 2
      show_date: true
      show_read_more: true
---
```

**常见操作**：
- 想调整板块顺序：上下移动整个 `- block:` 段落；
- 想删除板块：删掉对应段落；
- 想新增板块：复制一段，改 `title` 和 `filters`；
- 板块 id 是菜单锚点的目标，改名后要同步 `menus.yaml`。

### 3.6 `content/experience.md` —— 经历页板块

与首页同构，目前包含四个板块：`resume-experience`（经历时间线）、`resume-skills`（技能）、`resume-awards`（奖项）、`resume-languages`（语言）。数据全部来自 `data/authors/me.yaml`，这里只控制展示顺序与标题：

```yaml
sections:
  - block: resume-experience
    content:
      username: me
    design:
      date_format: '2006年1月'        # Go 时间格式，中文习惯写法
      is_education_first: false       # true=先教育后经历
  - block: resume-skills
    content:
      title: 专业技能                  # 可自定义标题
      username: me
```

### 3.7 新增一篇论文 / 一个项目（照着模板复制）

**新增论文**：在 `content/publications/` 下新建文件夹，如 `content/publications/my-paper/index.md`：

```yaml
---
title: "论文标题"
authors:
  - me                                # 引用 data/authors/me.yaml
date: "2025-07-01T00:00:00Z"
publishDate: "2025-07-01T00:00:00Z"
publication_types: ["article-journal"] # 期刊类型标识
publication:
  name: "期刊名称"
  volume: 2025
  issue: 7
peer_reviewed: true
open_access: true
abstract: |
  摘要内容……
summary: |
  一句话摘要……
tags:
  - 关键词
featured: true                        # true 会出现在首页「学术论文」板块
links:
  - type: pdf
    url: ""                           # 论文 PDF 链接（可留空）
---

## 正文（可选）
论文详细介绍……
```

**新增项目**：在 `content/projects/` 下新建文件夹 + `index.md`：

```yaml
---
title: '项目名称'
date: 2024-09-01
tags:
  - 量化金融
  - Python
---

项目一句话简介（首页卡片上显示）。

<!--more-->                          # 分隔线：之前是摘要，之后是正文

## 正文
详细内容……
```

> 注意：`<!--more-->` 之前的文字会作为卡片摘要显示，务必精炼。

### 3.8 媒体资源

| 资源 | 路径 | 说明 |
| --- | --- | --- |
| 头像 | `assets/media/authors/me.jpg` | 同名替换即可，建议正方形 |
| 简历 PDF | `static/uploads/resume.pdf` | 同名替换，注意保持文件名 |
| 页脚/页头图标 | `assets/media/icons/custom/` | 自定义图标目录（高级） |

### 3.9 `layouts/_partials/` —— 自定义覆盖（高级）

| 文件 | 作用 |
| --- | --- |
| `site_footer.html` | 覆盖主题默认页脚（当前为极简版） |
| `hooks/head-end/github-button.html` | 在 `<head>` 末尾注入 GitHub 按钮脚本 |

原理：Hugo 优先使用本站 `layouts/` 下的同名模板覆盖 `_vendor/` 中的主题模板。想进一步自定义外观可在此新增文件（需要了解 Hugo 模板语法）。

---

## 4. 本地预览与部署

### 本地预览（改完先看效果）

```bash
# 方式一（推荐，带实时刷新）
pnpm dev
# 方式二
hugo server

# 浏览器打开 http://localhost:1313
```

### 发布到线上（GitHub Pages）

1. 修改文件后提交并推送到 `main` 分支：
   ```bash
   git add -A
   git commit -m "更新内容"
   git push origin main
   ```
2. 自动触发 `.github/workflows/deploy.yml`，构建完成后站点自动更新（约 1-2 分钟）。
3. 部署状态可在 GitHub 仓库的 **Actions** 页面查看。

### 部署相关文件

| 文件 | 作用 | 通常需要改吗 |
| --- | --- | --- |
| `hugoblox.yaml` | 指定 Hugo 版本（0.164.0）与部署目标（github-pages） | 换 Hugo 版本/换平台时改 |
| `.github/workflows/deploy.yml` | GitHub Pages 自动部署 | 一般不动 |
| `netlify.toml` | Netlify 部署配置 | **当前未使用**，可忽略或删除 |

---

## 5. 注意事项与坑（务必先读）

1. **`baseURL` 还是占位符**：`config/_default/hugo.yaml` 中 `baseURL: 'https://example.com/'` 尚未改成真实域名，上线前必须修改，否则站内链接/SEO 会异常。
2. **两套部署配置并存**：`hugoblox.yaml` 声明部署目标是 `github-pages`，但项目内残留 `netlify.toml`（Hugo 版本 0.162.0，与 hugoblox.yaml 的 0.164.0 不一致）。请确认你实际用 GitHub Pages，可删除 `netlify.toml` 避免混淆。
3. **品牌名两处同步**：「曾磊」同时存在于 `params.yaml`（`hugoblox.identity.name`）和 `me.yaml`（`name.display`），改名要两处一起改。
4. **`_vendor/` 目录禁止手动修改**：它是 HugoBlox 主题模块缓存，由 `go.mod` 与 `module.yaml` 管理；升级/换主题走 Hugo 模块命令，直接改会在下次构建时被覆盖。
5. **YAML 缩进严格**：一律两个空格，不要用 Tab；改错缩进会导致构建失败（`hugo server` 会直接报错提示）。
6. **日期格式**：`me.yaml` 中的日期用 `YYYY-MM-DD`；`experience.md` 中 `date_format: '2006年1月'` 是 Go 时间格式（2006 代表年份），按需调整。
7. **新增条目命名**：`content/projects/`、`content/publications/` 下每个条目一个文件夹（文件夹名建议用英文短横线，如 `my-paper`），文件夹内 `index.md` 为内容，也可放配图（如 `featured.png`）。
8. **本地构建报错排查**：先跑 `hugo server` 看错误提示（会定位到具体文件和字段），常见原因是 YAML 缩进或引号问题。

---

## 6. 常见操作实例（抄作业）

### 实例 A：更新一段实习经历

编辑 `data/authors/me.yaml` → `experience`，新增一段：

```yaml
experience:
  - role: 新岗位
    org: 新单位
    start: 2027-01-01
    end: 2027-06-30
    summary: |
      成果一……
      成果二……
```

### 实例 B：新增一篇论文并让它出现在首页

1. 新建 `content/publications/xxx/index.md`（内容模板见 3.7）；
2. 设置 `featured: true` → 自动出现在首页「学术论文」板块（`featured_only: true` 筛选）；
3. 首页「全部论文」板块自动包含所有论文（含非 featured）。

### 实例 C：换主题色

编辑 `config/_default/params.yaml`：

```yaml
theme:
  colors:
    primary: "indigo"   # 或 "#6366f1"
```

### 实例 D：启用数学公式（写论文需要 LaTeX 时）

编辑 `config/_default/params.yaml`：

```yaml
content:
  math:
    enable: true
```

### 实例 E：隐藏/显示页头搜索框

编辑 `config/_default/params.yaml`：

```yaml
header:
  search: false   # true 显示搜索框
```

---

*本指南基于项目 2026-08 版本文件逐项核对整理；如升级 HugoBlox 模板，部分配置字段可能变化，以官方文档 https://docs.hugoblox.com 为准。*
