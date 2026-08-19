---
# Leave the homepage title empty to use the site title
title: ''
summary: ''
date: 2024-09-01
type: landing

sections:
  - block: resume-biography-3
    content:
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: me
      text: ''
      # Show a call-to-action button under your biography? (optional)
      button:
        text: 下载简历
        url: uploads/resume.pdf
      headings:
        about: '关于我'
        education: '教育背景'
        interests: '研究兴趣'
    design:
      # Use the new Gradient Mesh which automatically adapts to the selected theme colors
      background:
        gradient_mesh:
          enable: true

      # Name heading sizing to accommodate long or short names
      name:
        size: md # Options: xs, sm, md, lg (default), xl

      # Avatar customization
      avatar:
        size: medium # Options: small (150px), medium (200px, default), large (320px), xl (400px), xxl (500px)
        shape: circle # Options: circle (default), square, rounded
  - block: markdown
    content:
      title: '📚 研究方向'
      subtitle: ''
      text: |-
        我是一名金融专硕硕士研究生，专注于量化金融与金融工程领域的研究与实践。

        在量化研究方面，我基于DolphinDB高频数据开展订单流交易策略开发与因子挖掘，构建了多资产配置的风险平价改进模型（PCA风险平价策略年化收益6.29%、Sharpe 2.62），并完成了可转债多因子选券框架的研究。

        在市场微观结构方面，我在深圳证券交易所参与了ST股票涨跌幅限制改革的效果评估，以及最低订单停留时间制度的国际比较研究。

        在学术研究方面，我以第二作者在《财务管理研究》发表论文，实证检验了企业人工智能水平对非效率投资的影响。
    design:
      columns: 1

  - block: resume-experience
    content:
      username: me
    design:
      # Hugo date format
      date_format: '2006年1月'
      # Education or Experience section first?
      is_education_first: true
  - block: resume-skills
    content:
      title: 专业技能
      username: me
  - block: resume-awards
    content:
      title: 奖项与荣誉
      username: me
    design:

      columns: 2


    
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

  - block: collection
    id: papers
    content:
      title: 学术论文
      filters:
        folders:
          - publications
        featured_only: true
    design:
      view: article-grid
      columns: 1
  - block: collection
    content:
      title: 全部论文
      text: ''
      filters:
        folders:
          - publications
        exclude_featured: false
    design:
      view: citation      
---
