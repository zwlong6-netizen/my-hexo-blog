# 响应式背景图片配置说明

## 功能说明
此功能允许Butterfly主题在桌面端和移动端显示不同的首页背景图片。

## 配置方法

### 1. 准备图片文件
- 桌面端背景图片：`/source/images/top_image.png` (已存在)
- 移动端背景图片：`/source/images/top_image_mobile.png` (需要添加)

### 2. 修改配置文件
在 `themes/butterfly/_config.yml` 中已添加以下配置：

```yaml
# Responsive background images for index page
index_img_responsive:
  desktop: /img/top_image.png
  mobile: /img/top_image_mobile.png
```

### 3. 自动注入CSS
主题会自动注入 `responsive_bg.css` 文件，无需手动添加。

## 断点说明
- **移动端**: ≤ 768px 显示移动端背景图片
- **桌面端**: > 768px 显示桌面端背景图片

## 自定义图片路径
如需修改图片路径，请同时更新：
1. `themes/butterfly/_config.yml` 中的 `index_img_responsive` 配置
2. `source/css/responsive_bg.css` 中的图片URL

## 注意事项
- 移动端图片建议使用竖屏比例 (9:16 或 3:4)
- 桌面端图片建议使用横屏比例 (16:9 或 4:3)
- 图片文件应放在 `/source/images/` 目录下
- 修改后需要重新生成站点：`hexo clean && hexo generate`
