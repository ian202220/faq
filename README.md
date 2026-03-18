<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>常見問題 FAQ</title>
    <style>
        /* 基礎樣式 */
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        body { 
            font-family: -apple-system, "Helvetica Neue", sans-serif; 
            background: #f2f2f7; 
            margin: 0; 
            display: flex; 
            justify-content: center; 
            height: 100vh;
            overflow: hidden; /* 防止整頁捲動影響手勢 */
        }

        /* 模擬手機容器 */
        .app-container { 
            width: 100%; 
            max-width: 414px; 
            background: white; 
            position: relative;
            display: flex;
            flex-direction: column;
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
        }

        /* 紅色標題列 */
        .header { 
            background: #FF4D4D; 
            color: white; 
            text-align: center; 
            padding: 18px 0; 
            font-size: 1.1rem; 
            font-weight: 600; 
            z-index: 10;
        }

        /* 內容區塊控制 */
        .view-wrapper {
            flex: 1;
            position: relative;
            overflow: hidden;
        }

        /* 頁面共同樣式 */
        .view {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: white;
            transition: transform 0.3s ease-out;
            padding: 20px;
            overflow-y: auto;
        }

        /* 主選單頁面 */
        #main-menu { transform: translateX(0); z-index: 5; }
        
        /* 詳情頁面 (預設在右側外面) */
        #detail-view { transform: translateX(100%); z-index: 6; background: #f9f9f9; }

        /* 選單按鈕 */
        .menu-item { 
            background: #EFEFEF; 
            margin-bottom: 16px; 
            padding: 16px; 
            border-radius: 30px; 
            text-align: center; 
            cursor: pointer; 
            font-weight: 500;
            color: #333;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
            transition: transform 0.1s;
        }
        .menu-item:active { transform: scale(0.98); background: #e5e5e5; }

        /* 詳情內文 */
        .content-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            min-height: 200px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            line-height: 1.8;
            color: #444;
        }

        .hint {
            text-align: center;
            font-size: 0.8rem;
            color: #999;
            margin-top: 20px;
        }
    </style>
</head>
<body>

<div class="app-container">
    <div class="header" id="nav-title">常見問題</div>

    <div class="view-wrapper">
        <div id="main-menu" class="view">
            <div class="menu-item" onclick="openDetail('出貨時間', '本商店商品皆為現貨，下單後約 2-3 個工作天出貨。如有急單請先連繫客服。')">出貨時間</div>
            <div class="menu-item" onclick="openDetail('訂單問題', '您可以透過「我的訂單」查詢最新進度。若顯示「處理中」代表已進入包裝流程。')">訂單問題</div>
            <div class="menu-item" onclick="openDetail('預購說明', '預購商品追加期為 14-21 天（不含假日），商品到齊後會依序發貨。')">預購說明</div>
            <div class="menu-item" onclick="openDetail('退換貨政策', '我們提供 7 天鑑賞期。退貨需保持商品全新、包裝完整，請連繫客服取得退貨代碼。')">退換貨政策</div>
            <div class="menu-item" onclick="openDetail('客服聯絡方式', '官方 LINE：@your_shop<br>服務時間：週一至週五 10:00 - 18:00')">客服聯絡方式</div>
        </div>

        <div id="detail-view" class="view">
            <div class="content-card" id="detail-content"></div>
            <p class="hint">← 向右滑動返回選單</p>
        </div>
    </div>
</div>

<script>
    const mainMenu = document.getElementById('main-menu');
    const detailView = document.getElementById('detail-view');
    const detailContent = document.getElementById('detail-content');
    const navTitle = document.getElementById('nav-title');

    let startX = 0;
    let currentX = 0;

    // 開啟詳情
    function openDetail(title, text) {
        navTitle.innerText = title;
        detailContent.innerHTML = text;
        detailView.style.transform = 'translateX(0)';
    }

    // 關閉詳情 (返回)
    function closeDetail() {
        navTitle.innerText = '常見問題';
        detailView.style.transform = 'translateX(100%)';
    }

    // 滑動返回邏輯
    detailView.addEventListener('touchstart', (e) => {
        startX = e.touches[0].clientX;
    });

    detailView.addEventListener('touchmove', (e) => {
        currentX = e.touches[0].clientX;
        let diff = currentX - startX;
        if (diff > 0) {
            // 跟隨手指滑動
            detailView.style.transition = 'none';
            detailView.style.transform = `translateX(${diff}px)`;
        }
    });

    detailView.addEventListener('touchend', (e) => {
        detailView.style.transition = 'transform 0.3s ease-out';
        let diff = currentX - startX;
        
        if (diff > 100) { // 滑動超過 100px 就返回
            closeDetail();
        } else {
            detailView.style.transform = 'translateX(0)';
        }
        startX = 0;
        currentX = 0;
    });
</script>

</body>
</html>
