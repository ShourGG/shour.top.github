项目功能简介与使用说明
项目功能
该项目是一个通知中心组件，旨在提供动态通知展示、数据交互及UI响应的开箱即用解决方案。其核心功能包括：

通知图标：页面右上角显示通知图标，带有未读数量徽标，支持点击后打开通知面板。
通知面板：在页面右侧弹出，展示完整通知列表，支持分类（如Bug修复、功能更新等）。
数据动态加载：通过外部JSON文件动态加载通知内容。
通知优先级：支持通知置顶（pinned属性）。
多语言支持：支持中英文通知内容（在JSON中定义）。
响应式UI设计：兼容移动端与桌面端，设计风格现代。
使用步骤
1. 环境要求
需要Web服务器（如Nginx、Apache）托管前端代码，确保JSON数据文件可访问。
现代浏览器，支持JavaScript的执行。
2. 文件结构
index.html：主HTML文件，包含通知中心的前端代码。
1.json：通知数据文件，包含所有通知内容的动态配置。
图标资源（如notification-icon.png、bug-icon.png）：通知图标。
3. 部署说明
将index.html文件上传至服务器的Web目录。
将1.json（动态数据文件）存储到GitHub仓库或其他可访问的服务器路径。
确保HTML文件中正确配置了数据文件路径：
javascript
复制代码
const dataUrl = 'https://shourgg.github.io/-/1.json'; // JSON 数据地址
4. 自定义配置
JSON数据说明：

type：通知类型，支持update（更新通知）与bug（修复通知）。
pinned：是否置顶，true表示通知优先展示。
version：通知适用版本。
time：通知发布时间，UNIX时间戳格式。
title：通知标题，支持多语言。
content：通知内容，包含feature（新特性）、bug（修复内容）、opt（优化内容）。
author：通知发布者。
示例：
json
复制代码
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
语言切换：目前UI文字默认支持中文，可根据需要扩展到其他语言：

javascript
复制代码
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
图标自定义：更换通知类型图标，修改icon属性链接即可。
