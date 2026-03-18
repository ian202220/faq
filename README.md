<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>JINART FAQ</title>
    <style>
        /* 基礎設定：確保全螢幕且無邊距 */
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        
        body { 
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; 
            background: #ffffff; 
            margin: 0; 
            padding: 0;
            display: flex; 
            justify-content: center; 
            height: 100vh;
            overflow: hidden; 
        }

        /* 應用程式主容器：手機上 100% 填滿 */
        .app-container { 
            width: 100%; 
            max-width: 500px; /* 電腦版最大寬度限制 */
            height: 100vh;
            background: #f7f7f9; 
            position: relative;
            display: flex;
            flex-direction: column;
        }

        /* 標題列：簡約紅底白字 */
        .header { 
            background: #FF4D4D; 
            color: white; 
            text-align: center; 
            padding: 20px 0; 
            font-size: 1.25rem; 
            font-weight: bold; 
            letter-spacing: 1px;
            z-index: 10;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        /* 視窗包裝器 */
        .view-wrapper { flex: 1; position: relative; overflow: hidden; }

        /* 頁面通用樣式 */
        .view {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: #f7f7f9;
            transition: transform 0.3s cubic-bezier(0.1, 0.7, 0.1, 1);
            padding: 20px;
            overflow-y: auto;
        }

        /* 主選單 */
        #main-menu { z-index: 5; transform: translateX(0); }

        /* 詳情頁 (預設隱藏在右側) */
        #detail-page { z-index: 6; transform: translateX(100%); background: #ffffff; }

        /* 選單按鈕：符合手機點擊的大按鈕 */
        .menu-item { 
            background: white; 
            margin-bottom: 16px; 
            padding: 22px; 
            border-radius: 16px; 
            text-align: center; 
            cursor: pointer; 
            font-weight: 600;
            font-size: 1.1rem;
            color: #333;
            box-shadow: 0 4px 6px rgba(0,0,0,0.03);
            border: 1px solid rgba(0,0,0,0.05);
            transition: transform 0.1s, background 0.1s;
        }
        
        .menu-item:active { transform: scale(0.97); background: #f0f0f0; }

        /* 詳情內文卡片 */
        .content-card {
            background: white;
            padding: 25px;
            border-radius: 20px;
            min-height: 250px;
            color: #444;
            line-height: 1.8;
            font-size: 1.05rem;
            box-shadow: 0 2px 15px rgba(0,0,0,0.05);
            margin-top: 10px;
        }

        /* 返回按鈕 */
        .back-btn {
            display: block;
            margin: 30px auto;
            color: #FF4D4D;
            text-align: center;
            cursor: pointer;
            font-weight: bold;
            font-size: 1.1rem;
            padding: 15px;
            text-decoration: none;
        }

        .hint { text-align: center; font-size: 0.85rem; color: #bbb; margin-top: 15px; }
        
        a { color: #FF4D4D; text-decoration: underline; font-weight: bold; }
    </style>
</head>
<body>

    <div class="app-container">
        <div class="header" id="nav-title">常見問題</div>

        <div class="view-wrapper">
            <div id="main-menu" class="view">
                <div class="menu-item" onclick="openPage('出貨時間', '現貨商品，完成下單後將於 5-7 個工作天出貨。不是現貨商品則需 3-4 個月工作天製作（不含國定假日）。若同時購買訂製或預購商品，將待商品到齊後一起出貨。如想先收到現貨商品，麻煩請分開下單。')">出貨時間</div>
                <div class="menu-item" onclick="openPage('訂單問題', '您好～若您有訂單相關問題，歡迎提供訂購人姓名、Email 與訂單編號，並私訊我們的官方 IG，我們將協助您處理，謝謝您。')">訂單問題</div>
                <div class="menu-item" onclick="openPage('預購說明', '您好～預購出貨月為預估值，可能會因為生產/船運/品管/貨運等因素提早或延期發貨，不好意思造成您的不便，謝謝您的支持。')">預購說明</div>
                <div class="menu-item" onclick="openPage('退換貨政策', '【退換貨說明】請於出貨日起 15 天內聯繫客服。商品需保持完整包裝，非官方瑕疵或拆封損壞恕不退換。開箱請全程錄影，未提供完整影片不受理退換貨。個人取消訂單將扣手續費 2% 及保證金 5%。公仔／玩具塗裝問題 15 天內可依認證卡申請免費維修一次。')">退換貨政策</div>
                <div class="menu-item" onclick="openPage('客服聯絡方式', 'Instagram 客服：<br><a href=\'https://www.instagram.com/jinart2018/\' target=\'_blank\'>@jinart2018</a><br>服務時間：09:30 - 17:00')">客服聯絡方式</div>
            </div>

            <div id="detail-page" class="view">
                <div class="content-card" id="detail-content"></div>
                <div class="back-btn" onclick="goBack()">← 返回選單</div>
                <p class="hint">（也可向右滑動返回）</p>
            </div>
        </div>
    </div>

    <script>
        const navTitle = document.getElementById('nav-title');
        const detailPage = document.getElementById('detail-page');
        const detailContent = document.getElementById('detail-content');

        let startX = 0;
        let moveX = 0;

        function openPage(title, text) {
            navTitle.innerText = title;
            detailContent.innerHTML = `<strong>【${title}】</strong><br><br>${text}`;
            detailPage.style.transition = 'transform 0.3s cubic-bezier(0.1, 0.7, 0.1, 1)';
            detailPage.style.transform = 'translateX(0)';
        }

        function goBack() {
            navTitle.innerText = '常見問題';
            detailPage.style.transition = 'transform 0.3s cubic-bezier(0.1, 0.7, 0.1, 1)';
            detailPage.style.transform = 'translateX(100%)';
        }

        // 滑動返回邏輯
        detailPage.addEventListener('touchstart', (e) => {
            startX = e.touches[0].clientX;
        }, {passive: true});

        detailPage.addEventListener('touchmove', (e) => {
            moveX = e.touches[0].clientX;
            let diff = moveX - startX;
            if (diff > 0) {
                detailPage.style.transition = 'none';
                detailPage.style.transform = `translateX(${diff}px)`;
            }
        }, {passive: true});

        detailPage.addEventListener('touchend', (e) => {
            let diff = moveX - startX;
            detailPage.style.transition = 'transform 0.3s cubic-bezier(0.1, 0.7, 0.1, 1)';
            if (diff > 100) {
                goBack();
            } else {
                detailPage.style.transform = 'translateX(0)';
            }
            startX = 0; moveX = 0;
        });
    </script>

</body>
</html>
