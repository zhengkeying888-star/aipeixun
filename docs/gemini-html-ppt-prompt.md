# Gemini HTML PPT 生成提示词

> 适用工具：Gemini 3.1 Pro（或其他支持长文本+代码生成的 LLM）
> 输出要求：完整的、可直接保存为 `.html` 的独立页面代码

---

## 完整提示词（直接复制使用）

```
请为我生成一套HTML演示文稿的页面，基于以下严格的视觉规范和代码结构。

## 项目背景
- 用途：企业内部AI赋能培训PPT
- 面向：私域运营团队（中老年在线教育行业）
- 风格：温暖专业、信息密度适中、适合投影

## 核心技术规范

### 1. 基础HTML结构
每个页面必须是以下结构的 `.slide` div：

```html
<div class="slide">
  <div class="slide-inner">
    <!-- 页面内容区域 -->
    <div class="page-num">XX / XX</div>
  </div>
</div>
```

所有页面包裹在 `<div class="slideshow" id="slideshow">` 中。
导航脚本固定为：
```javascript
const slides = document.querySelectorAll('.slide');
let current = 0;
function showSlide(n) {
  slides.forEach(s => s.classList.remove('active'));
  current = (n + slides.length) % slides.length;
  slides[current].classList.add('active');
}
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight' || e.key === ' ') showSlide(current + 1);
  if (e.key === 'ArrowLeft') showSlide(current - 1);
});
```

### 2. CSS 样式规范（必须严格遵循）

已定义的全局样式类（直接使用，不要修改）：

| 类名 | 用途 | 样式特征 |
|:---|:---|:---|
| `.slide` | 单页容器 | `position:absolute; inset:0; display:none;` |
| `.slide.active` | 当前页 | `display:block;` |
| `.slide-inner` | 内容区 | `max-width:1600px; max-height:900px; padding:60px 80px;` |
| `h2` | 页面主标题 | `font-size:42px; color:#D32F2F;` |
| `.subtitle` | 副标题 | `font-size:22px; color:#8D6E63;` |
| `.card` | 通用卡片 | `background:#fff; border-radius:20px; padding:28px 32px; box-shadow:0 4px 20px rgba(0,0,0,0.06);` |
| `.card-pink` | 粉色卡片 | `background:#FFEBEE; border-color:#FFCDD2;` |
| `.card-green` | 绿色卡片 | `background:#E8F5E9; border-color:#C8E6C9;` |
| `.card-yellow` | 黄色卡片 | `background:#FFF8E1; border-color:#FFECB3;` |
| `.card-orange` | 橙色卡片 | `background:#FFF3E0; border-color:#FFE0B2;` |
| `.card-red` | 红色卡片 | `background:#FFEBEE; border-color:#EF9A9A;` |
| `.flex-row` | 横向布局 | `display:flex; gap:24px;` |
| `.col-2` | 双栏 | `flex:1; max-width:480px;` |
| `.col-3` | 三栏 | `flex:1; max-width:320px;` |
| `.col-4` | 四栏 | `flex:1; max-width:240px;` |
| `.icon-big` | 大图标 | `font-size:48px;` |
| `.icon-med` | 中图标 | `font-size:32px;` |
| `.page-num` | 页码 | 绝对定位右下角 |
| `.tag` | 标签 | `background:#D32F2F; color:#fff; padding:6px 18px; border-radius:20px;` |
| `.badge` | 徽章 | `padding:4px 12px; border-radius:12px; font-size:13px;` |
| `.badge-green` | 绿徽章 | `background:#E8F5E9; color:#2E7D32;` |
| `.badge-red` | 红徽章 | `background:#FFEBEE; color:#C62828;` |
| `.badge-orange` | 橙徽章 | `background:#FFF3E0; color:#EF6C00;` |
| `.formula-box` | 公式块 | `background:#fff; border-radius:12px; padding:12px 20px; border:2px solid #FFCDD2; font-size:18px; font-weight:700; color:#D32F2F;` |
| `.grid-3x2` | 3x2网格 | `display:grid; grid-template-columns:repeat(3, 1fr); gap:20px;` |
| `.chat-user` | 用户气泡 | `background:#FFEBEE; border-radius:16px 16px 4px 16px;` |
| `.chat-ai` | AI气泡 | `background:#fff; border-radius:16px 16px 16px 4px; border:2px solid #E0E0E0;` |
| `.chat-ai.bad` | AI错误输出 | `border-color:#EF9A9A; background:#FFEBEE;` |
| `.chat-ai.good` | AI正确输出 | `border-color:#C8E6C9; background:#E8F5E9;` |
| `.chat-label` | 气泡标签 | `font-size:12px; color:#8D6E63; font-weight:600;` |
| `.checklist` | 清单 | `list-style:none;` 带 ☐ 前缀 |
| `.arrow-right` | 箭头 | `font-size:32px; color:#FF7043;` |
| `.tag-row` | 标签行 | `display:flex; gap:12px; justify-content:center; flex-wrap:wrap;` |
| `.tag-item` | 标签项 | `background:#fff; border-radius:20px; padding:8px 20px; border:2px solid #FFCDD2;` |

### 3. 全局颜色规范
- 背景色：`#FFF5F0`
- 标题色：`#D32F2F`
- 正文色：`#5D4037`
- 副标题/注释：`#8D6E63`
- 强调红：`#C62828`
- 强调绿：`#2E7D32`
- 强调橙：`#EF6C00`

### 4. 布局原则
- 每页信息密度适中，投影清晰可读
- 大量留白，每页不超过6个核心要点
- 优先使用 `.card` + `.flex-row` 组合
- 对话场景使用 `.chat-user` + `.chat-ai` 气泡
- 对比场景使用左右双栏（灰色 vs 粉色背景）

## 本次生成要求

请生成以下页面的完整HTML代码：

【在这里描述你要生成的页面内容】

要求：
1. 输出完整的、独立的HTML文件（包含style和script）
2. 只输出我要求的页面，不要包含其他已有页面
3. 严格使用上述CSS类名，不要自定义新样式
4. 确保 `.slide` 第一个有 `.active` 类
5. 页面内容要具体、有业务场景，不要泛泛而谈
```

---

## 使用示例

### 示例1：生成单页新内容

```
请生成1页HTML：

标题：LLM vs AGENT 的本质区别
内容：
- 用左右双栏对比 LLM（大脑）和 AGENT（大脑+手脚）
- 左栏：LLM 只做一件事——你输入文字，它生成文字
- 右栏：AGENT 做一串事——你描述目标，它自动操作文件/写代码/执行流程
- 底部用一个卡片总结：关键不是工具贵不贵，是你要知道自己在用什么维度的工具

要求用对话气泡形式展示一个场景：运营说"帮我写文案"，LLM 生成文字；运营说"帮我自动整理本周数据并生成报告"，AGENT 执行一系列操作。
```

### 示例2：修改现有页面风格

```
基于以下已有页面结构，帮我生成一个相同主题但不同案例的页面：

【粘贴现有页面的HTML代码片段】

要求：
- 保持完全相同的CSS类名和结构
- 把案例从"唱歌宋"改为"手机摄影"
- 把数据替换为：进量8000人，预约率6.2%，到课率65%，转化率18%
```

---

## 输出格式检查清单

Gemini 生成后，请自检以下项目：

- [ ] 是否使用了已定义的CSS类名（没有自定义新样式）
- [ ] 第一个 `.slide` 是否有 `.active` 类
- [ ] `page-num` 是否正确编号
- [ ] 背景色是否为 `#FFF5F0`
- [ ] 标题色是否为 `#D32F2F`
- [ ] 卡片是否有 `border-radius:20px` 和阴影
- [ ] 键盘导航脚本是否完整

---

## 注意事项

1. **不要自定义新CSS**：所有样式必须用上述预定义的类。如需特殊布局，用内联style写在HTML元素上。
2. **保持独立**：每页HTML可以独立运行，包含完整的 `<html><head><style><body><script>` 结构。
3. **中文优先**：所有内容中文，英文术语后加中文注释。
4. **业务具体**：案例要具体到品类、数据、场景，不要抽象描述。
