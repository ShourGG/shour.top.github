# 通知中心组件

## 项目简介

这是一个轻量级的通知中心组件，提供了动态通知展示、数据交互和响应式用户界面的解决方案。该项目支持多语言、动态数据加载、通知优先级展示，适用于任何需要通知功能的Web应用。

---

## 功能特点

- **通知图标**：右上角显示通知图标，支持徽标显示未读数量。
- **通知面板**：在页面右侧弹出，展示完整通知列表，支持按类型和优先级分类。
- **数据动态加载**：通过外部JSON文件动态加载通知内容。
- **通知优先级**：支持通知置顶功能。
- **多语言支持**：支持中英文通知内容，易于扩展至其他语言。
- **响应式UI**：兼容桌面端和移动端，具有现代设计风格。

---

## 快速开始

### 环境要求

- **Web服务器**：需要托管前端代码（如Nginx、Apache）。
- **现代浏览器**：支持JavaScript的执行。

### 文件结构

```plaintext
├── index.html         # 通知中心前端代码
├── 1.json             # 通知数据文件
├── assets/            # 图标等静态资源
```

### 部署步骤

1. 将`index.html`文件上传到Web服务器的根目录。
2. 将`1.json`（动态数据文件）存储到可访问的服务器路径或GitHub仓库。
3. 确保HTML文件中正确配置了数据文件路径：
   ```javascript
   const dataUrl = 'https://shourgg.github.io/-/1.json'; // JSON 数据地址
   ```
4. 启动服务器，访问部署的HTML文件，即可查看通知中心。

---

## 使用说明

### 数据格式
通知内容通过JSON文件配置，支持以下字段：

- **`id`**：通知ID（唯一标识）。
- **`type`**：通知类型，支持`update`（更新通知）和`bug`（修复通知）。
- **`pinned`**：是否置顶，`true`表示通知优先展示。
- **`version`**：通知适用版本。
- **`time`**：通知发布时间，UNIX时间戳格式。
- **`title`**：通知标题，支持多语言（如`zh`和`en`）。
- **`content`**：通知内容，包含`feature`（新特性）、`bug`（修复内容）、`opt`（优化内容）。
- **`author`**：通知发布者。
- **`icon`**：通知类型图标的链接。

#### 数据示例
```json
{
  "announce": [
    {
      "id": 2,
      "type": "update",
      "pinned": false,
      "version": "3.0",
      "time": 1739000000000,
      "title": {
        "zh": "3.0版本更新",
        "en": "3.0 Version Update"
      },
      "content": {
        "zh": {
          "feature": ["全新UI设计", "新增夜间模式"],
          "bug": ["修复了系统卡顿问题"],
          "opt": ["优化数据加载速度"]
        },
        "en": {
          "feature": ["New UI Design", "Added Dark Mode"],
          "bug": ["Fixed system lag issue"],
          "opt": ["Optimized data loading speed"]
        }
      },
      "author": "开发团队",
      "icon": "update-icon.png"
    }
  ]
}
```

### 通知图标
右上角通知图标显示未读通知数量，支持点击后打开通知面板。

### 通知面板
- 点击通知图标，面板从右侧弹出，展示完整的通知内容。
- 支持按通知类型（`bug`、`update`）和优先级（置顶）分类。
- 通知卡片显示发布时间、作者及详细内容。

---

## 开发者说明

### 核心逻辑

#### 数据加载
通过`fetch`方法从外部JSON文件加载通知数据：
```javascript
fetch(dataUrl)
  .then(res => res.json())
  .then(data => renderNotifications(data));
```

#### 渲染通知
函数`renderNotifications`实现以下功能：
- 按`pinned`优先级对通知排序。
- 动态生成HTML结构，支持多语言内容。
- 更新徽标显示未读数量。

#### 通知交互
- 点击通知图标，打开通知面板：
  ```javascript
  notificationIcon.addEventListener('click', () => {
    notificationPanel.classList.add('open');
  });
  ```
- 点击关闭按钮，关闭通知面板：
  ```javascript
  closePanelButton.addEventListener('click', () => {
    notificationPanel.classList.remove('open');
  });
  ```

### 样式说明
CSS采用现代设计风格，主要样式包括：
- **通知图标**：悬停放大效果，显示未读徽标。
- **通知面板**：从右侧平滑弹出，支持滚动查看。
- **通知卡片**：带有阴影和悬停提升效果的卡片式设计。

---

## 自定义指南

### 修改语言
可以通过扩展`uiText`对象实现更多语言支持：
```javascript
const uiText = {
  zh: {
    releaseTime: '发布时间',
    author: '作者',
    features: '新特性:',
    bugFixes: '修复内容:',
    optimizations: '优化内容:'
  },
  en: {
    releaseTime: 'Release Time',
    author: 'Author',
    features: 'Features:',
    bugFixes: 'Bug Fixes:',
    optimizations: 'Optimizations:'
  }
};
```

### 自定义图标
替换通知类型图标，修改JSON数据中的`icon`字段即可：
```json
"icon": "custom-icon.png"
```

---

## 许可证

该项目采用 [MIT License](LICENSE)。
