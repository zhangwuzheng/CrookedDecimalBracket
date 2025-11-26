## 使用这个文件作为背景

太棒了！您提供的视频素材完美契合了“藏境山水”的品牌形象以及“震撼的动态风景”的要求。这段**珠穆朗玛峰（可能是）的日落/日出延时视频**具有史诗级的视觉效果。

我现在将上一个版本的代码进行修改，把静态图片背景替换为**循环播放的视频背景**，并确保视频在移动端有良好的性能和体验。

### 关键修改点：

1.  **HTML结构：** 引入 `<video>` 标签，设置 `autoplay`（自动播放）、`loop`（循环）和 `muted`（静音，因为浏览器通常禁止自动播放带声音的视频）属性。
2.  **CSS层级：** 将视频放置在 `bg-layer` 中，并使用 `object-fit: cover` 确保视频始终填满整个屏幕，即使比例不同也不会出现黑边。
3.  **云雾效果：** 保留了上一个版本中的动态云雾特效，叠加在视频之上，进一步增加画面的纵深感和神秘感。

### 预览代码

请将下方代码保存为 `.html` 文件，并确保将您提供的视频文件（例如命名为 `background_video.mp4`）放置在与此 HTML 文件**相同的文件夹**内。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>藏境山水 - 秘境朝圣</title>
<style>
  /* --- 全局设置 --- */
  :root {
    --primary-color: #34568B; /* 藏蓝色，用于图标和文字点缀 */
    --accent-color-gold: #D4AF37; /* 藏式金色 */
    --card-bg: rgba(255, 255, 255, 0.9); /* 卡片背景色 */
    --text-color-dark: #333;
    --text-color-light: #666;
  }

  body, html {
    margin: 0;
    padding: 0;
    height: 100%;
    font-family: "PingFang SC", "Microsoft YaHei", sans-serif;
    overflow: hidden; /* 禁止滚动 */
    background-color: #000;
  }

  /* --- 视频背景层 (Video Background Layer) --- */
  .bg-layer {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    overflow: hidden;
  }

  /* 视频样式设置 */
  #background-video {
    width: 100%;
    height: 100%;
    object-fit: cover; /* 确保视频覆盖整个容器 */
    filter: brightness(0.95) contrast(1.1); /* 稍微提亮和对比度，让UI更清晰 */
  }

  /* 动态云雾效果 (叠加在视频之上) */
  .bg-layer::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 200%;
    height: 100%;
    background-image: url('https://png.pngtree.com/png-clipart/20220929/ourmid/pngtree-white-clouds-floating-fog-png-image_6234624.png'); /* 云雾素材 */
    background-size: cover;
    opacity: 0.3; /* 降低云雾透明度，更自然 */
    animation: moveClouds 60s linear infinite;
  }

  @keyframes moveClouds {
    from { transform: translateX(0); }
    to { transform: translateX(-50%); }
  }

  /* --- 内容容器 --- */
  .container {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 60px 20px 30px; 
    box-sizing: border-box;
  }

  /* --- 顶部文字 --- */
  .top-text {
    color: #fff;
    text-shadow: 0 2px 8px rgba(0,0,0,0.8); /* 增加阴影，确保在亮色雪山背景上清晰可见 */
  }
  .company-name {
    font-size: 36px;
    font-weight: 800;
    letter-spacing: 4px;
    margin-bottom: 10px;
    line-height: 1.2;
  }
  .slogan {
    font-size: 16px;
    font-weight: 300;
    opacity: 0.9;
    margin-bottom: 5px;
  }

  /* --- 底部悬浮白卡 (核心结构) --- */
  .bottom-card {
    background-color: var(--card-bg);
    border-radius: 24px;
    padding: 25px 15px 15px;
    box-shadow: 0 -10px 30px rgba(0,0,0,0.2);
    backdrop-filter: blur(15px); 
    -webkit-backdrop-filter: blur(15px);
    animation: slideUp 0.8s ease-out;
  }

  @keyframes slideUp {
    from { transform: translateY(100%); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
  }

  /* --- 上层：三大产品入口 --- */
  .products-row {
    display: flex;
    justify-content: space-around;
    margin-bottom: 25px;
    position: relative;
  }
  .products-row::after {
    content: '';
    position: absolute;
    bottom: -15px;
    left: 10%;
    width: 80%;
    height: 1px;
    background-color: rgba(0,0,0,0.08); 
  }

  .product-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    width: 30%;
  }

  /* 产品图标 (极简风格，透明背景) */
  .product-icon-box {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 8px;
    box-shadow: 0 4px 8px rgba(0,0,0,0.08);
    background-color: transparent; 
    border: 1px solid rgba(0,0,0,0.1); 
  }

  /* 虫草图标 - 极简 */
  .icon-cordyceps {
    width: 36px;
    height: 36px;
    background-color: var(--accent-color-gold);
    mask-image: url('data:image/svg+xml;utf8,<svg viewBox=\'0 0 24 24\' xmlns=\'http://www.w3.org/2000/svg\'><path fill=\'currentColor\' d=\'M12 2C6.477 2 2 6.477 2 12s4.477 10 10 10 10-4.477 10-10S17.523 2 12 2zm0 2a8 8 0 1 1 0 16 8 8 0 0 1 0-16zm-1 2v4a1 1 0 0 0 2 0V6a1 1 0 0 0-2 0zm0 6h2v6h-2z\'/></svg>');
    mask-size: contain;
    -webkit-mask-size: contain;
  }
  /* 7100水图标 - 极简 */
  .icon-water {
    width: 36px;
    height: 36px;
    background-color: #6CB4EE; /* 冰川蓝色 */
    mask-image: url('data:image/svg+xml;utf8,<svg viewBox=\'0 0 24 24\' xmlns=\'http://www.w3.org/2000/svg\'><path fill=\'currentColor\' d=\'M12 2c-.96 0-1.89.3-2.67.92L4 7.62V18c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V7.62l-5.33-4.7c-.78-.62-1.71-.92-2.67-.92zM6 18V9l6-5 6 5v9H6z\'/></svg>');
    mask-size: contain;
    -webkit-mask-size: contain;
  }
  /* 松茸图标 - 极简 */
  .icon-matsutake {
    width: 36px;
    height: 36px;
    background-color: #8B4513; /* 大地棕色 */
    mask-image: url('data:image/svg+xml;utf8,<svg viewBox=\'0 0 24 24\' xmlns=\'http://www.w3.org/2000/svg\'><path fill=\'currentColor\' d=\'M12 2c-3.31 0-6 2.69-6 6v7c0 1.66 1.34 3 3 3h6c1.66 0 3-1.34 3-3V8c0-3.31-2.69-6-6-6zm0 2c2.21 0 4 1.79 4 4v7c0 .55-.45 1-1 1h-6c-.55 0-1-.45-1-1V8c0-2.21 1.79-4 4-4zm-2 15h4v1H10z\'/></svg>');
    mask-size: contain;
    -webkit-mask-size: contain;
  }


  .product-title {
    font-size: 15px;
    font-weight: 600;
    color: var(--text-color-dark);
    margin-bottom: 2px;
  }
  .product-en {
    font-size: 10px;
    color: var(--text-color-light);
    text-transform: uppercase;
  }

  /* --- 下层：四大功能入口 --- */
  .functions-row {
    display: flex;
    justify-content: space-between;
    padding: 0 5px;
    margin-bottom: 15px;
  }

  .func-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    width: 22%;
  }

  /* 功能图标 (极简线性图标，颜色统一) */
  .func-icon {
    width: 28px;
    height: 28px;
    margin-bottom: 8px;
    background-color: var(--primary-color); 
    mask-size: contain;
    -webkit-mask-size: contain;
    mask-position: center;
    -webkit-mask-position: center;
    mask-repeat: no-repeat;
    -webkit-mask-repeat: no-repeat;
  }

  .func-text {
    font-size: 12px;
    color: var(--text-color-light);
    margin-bottom: 2px;
  }

  /* --- 底部横幅 --- */
  .banner {
    background: linear-gradient(to right, var(--primary-color), #5a7ea8); 
    color: #fff;
    text-align: center;
    padding: 12px 0;
    border-radius: 12px;
    font-size: 13px;
    font-weight: 500;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .banner::before, .banner::after {
    content: '—';
    opacity: 0.6;
    margin: 0 8px;
  }

</style>
</head>
<body>

  <div class="bg-layer">
    <video id="background-video" autoplay loop muted playsinline>
      <source src="潮点网_92548_720p.mp4" type="video/mp4">
      您的浏览器不支持视频背景。
    </video>
  </div>

  <div class="container">
    <div class="top-text">
      <div class="company-name">藏境山水</div>
      <div class="slogan">源自雪域高原的纯净馈赠</div>
      <div class="slogan">AUTHENTIC TIBETAN GIFTS</div>
    </div>

    <div class="bottom-card">
      <div class="products-row">
        <div class="product-item">
          <div class="product-icon-box">
            <div class="icon-cordyceps"></div>
          </div>
          <div class="product-title">臻选虫草</div>
          <div class="product-en">Cordyceps</div>
        </div>
        <div class="product-item">
          <div class="product-icon-box">
            <div class="icon-water"></div>
          </div>
          <div class="product-title">7100冰川水</div>
          <div class="product-en">Glacier Water</div>
        </div>
        <div class="product-item">
          <div class="product-icon-box">
            <div class="icon-matsutake"></div>
          </div>
          <div class="product-title">野生松茸</div>
          <div class="product-en">Matsutake</div>
        </div>
      </div>

      <div class="functions-row">
        <div class="func-item">
          <div class="func-icon" style="mask-image: url('data:image/svg+xml;utf8,<svg viewBox=\'0 0 24 24\' xmlns=\'http://www.w3.org/2000/svg\'><path d=\'M12 1L3 5v6c0 5.55 3.84 10.74 9 12 5.16-1.26 9-6.45 9-12V5l-9-4zm0 2.22l5.5 2.45-5.5 2.44-5.5-2.45L12 3.22zM12 19.12c-3.13-.91-5.5-4.57-5.5-8.12V7.18l5.5 2.44 5.5-2.44v3.82c0 3.55-2.37 7.21-5.5 8.12z\'/></svg>');"></div>
          <div class="func-text">品牌介绍</div>
          <div class="product-en">About Us</div>
        </div>
        <div class="func-item">
          <div class="func-icon" style="mask-image: url('data:image/svg+xml;utf8,<svg viewBox=\'0 0 24 24\' xmlns=\'http://www.w3.org/2000/svg\'><path d=\'M20 4H4c-1.11 0-1.99.89-1.99 2L2 18c0 1.11.89 2 2 2h16c1.11 0 2-.89 2-2V6c0-1.11-.89-2-2-2zm0 14H4V8h16v10zm-2-10h-6c-.55 0-1 .45-1 1s.45 1 1 1h6c.55 0 1-.45 1-1s-.45-1-1-1zM4 6h16v12H4V6z\'/></svg>');"></div>
          <div class="func-text">领券中心</div>
          <div class="product-en">Coupons</div>
        </div>
        <div class="func-item">
          <div class="func-icon" style="mask-image: url('data:image/svg+xml;utf8,<svg viewBox=\'0 0 24 24\' xmlns=\'http://www.w3.org/2000/svg\'><path d=\'M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 15h-2v-6h2v6zm0-8h-2V7h2v2z\'/></svg>');"></div>
          <div class="func-text">积分商城</div>
          <div class="product-en">Points Mall</div>
        </div>
        <div class="func-item">
          <div class="func-icon" style="mask-image: url('data:image/svg+xml;utf8,<svg viewBox=\'0 0 24 24\' xmlns=\'http://www.w3.org/2000/svg\'><path d=\'M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z\'/></svg>');"></div>
          <div class="func-text">个人中心</div>
          <div class="product-en">My Account</div>
        </div>
      </div>

      <div class="banner">
        探索藏地珍稀，开启纯净之旅~
      </div>
    </div>
  </div>

</body>
</html>
```

### ❗ 重要提示 (关于视频背景)

1.  **文件路径：** 我已将视频文件路径设置为 `src="潮点网_92548_720p.mp4"`。**您必须确保您的视频文件名称和此路径完全一致，并且位于同一个文件夹内。**
2.  **静音 (`muted`) 和自动播放 (`autoplay`):**
      * 绝大多数现代浏览器（包括微信小程序内置的WebView）都要求视频必须设置 `muted` 才能自动播放。
      * 我添加了 `playsinline` 属性，这对于 iOS 设备上的全屏播放体验非常重要。
3.  **性能：** 视频背景会消耗较多流量和电池。对于小程序，建议对视频进行压缩，以保证流畅的用户体验。您提供的 720P 分辨率是移动端比较合适的选择。

您现在可以查看这个融入了动态雪山背景的震撼页面效果了！