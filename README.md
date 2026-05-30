# 萌版泡泡堂8（广告跳过）

这是一个用于解决 **4399 萌版泡泡堂8** 中“广告无法观看导致无法继续”问题的小项目。

## 游戏地址

[点击此处进入 4399 萌版泡泡堂8](https://www.4399.com/flash/235691_4.htm)

> 该链接为 Flash 页面；若浏览器无法直接运行，请使用支持 Flash 模拟的环境或相关插件。

## 功能说明

- 当广告无法正常播放时，支持直接跳过广告环节。
- 帮助玩家继续进入游戏流程，避免卡在广告页面。

## 使用说明

1. 打开上方游戏链接。
2. 在出现广告无法播放、无法继续时，按 `F12` 打开开发者工具，切换到 **Console**。
3. 粘贴并执行下面这段脚本（优先匹配常见广告容器；“跳过按钮”使用关键词兜底匹配）：

```javascript
const AD_NODE_SELECTOR =
  "iframe[src*='ad'], [id*='ad'], [id*='gg'], [class*=' ad'], [class^='ad'], [class*='advert']";
const SKIP_BTN_SELECTOR = ".btn-skip, .skip, .continue, .next, .start-btn";
const SKIP_TEXT_PATTERN = /跳过|继续|开始游戏/i;

const adNodes = [...document.querySelectorAll(AD_NODE_SELECTOR)].filter((el) => {
  const text = `${el.id || ""} ${el.className || ""} ${el.getAttribute("src") || ""}`.toLowerCase();
  return /(^|[\s_-])(ad|ads|advert|advertisement|gg)([\s_-]|$)/.test(text);
});
adNodes.forEach((el) => el.remove());
const skipBtn = [...document.querySelectorAll(SKIP_BTN_SELECTOR)].find((el) =>
  SKIP_TEXT_PATTERN.test((el.textContent || "").trim())
);
if (skipBtn) skipBtn.click();
```

4. 如果页面结构变化导致未生效，请刷新后重试，或手动点击页面中的“跳过/继续”按钮。
   > 提示：网页结构可能变化，脚本是通用兜底方案，必要时请按页面实际元素调整选择器。
   > 注意：脚本会移除部分疑似广告元素，可能影响页面局部布局或功能。
   > 说明：按钮关键词基于中文界面（跳过/继续/开始游戏），其他语言版本请替换为对应关键词。
5. 返回游戏，正常开始或继续游玩。
