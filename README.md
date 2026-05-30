# 萌版泡泡堂8（广告跳过）

这是一个用于解决 **4399 萌版泡泡堂8** 中“广告无法观看导致无法继续”问题的小项目。

## 游戏地址

https://www.4399.com/flash/235691_4.htm

## 功能说明

- 当广告无法正常播放时，支持直接跳过广告环节。
- 帮助玩家继续进入游戏流程，避免卡在广告页面。

## 使用说明

1. 打开上方游戏链接。
2. 在出现广告无法播放、无法继续时，按 `F12` 打开开发者工具，切换到 **Console**。
3. 粘贴并执行下面这段脚本（优先匹配常见广告容器；“跳过按钮”使用关键词兜底匹配）：

```javascript
document
  .querySelectorAll("iframe[src*='ad'], #ad, [id^='ad_'], .ad, .ads, .advert, .advertisement")
  .forEach((el) => el.remove());
const skipBtn = [...document.querySelectorAll(".btn-skip, .skip, .continue, a, button")].find((el) =>
  /跳过|继续|开始游戏/.test((el.textContent || "").trim())
);
if (skipBtn) skipBtn.click();
```

4. 如果页面结构变化导致未生效，请刷新后重试，或手动点击页面中的“跳过/继续”按钮。
   > 提示：网页结构可能变化，脚本是通用兜底方案，必要时请按页面实际元素调整选择器。
5. 返回游戏，正常开始或继续游玩。
