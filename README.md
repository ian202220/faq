<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>JINART FAQ</title>
    <style>
        /* 基礎設定 - 確保畫面乾淨 */
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        body { 
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; 
            background: #f0f2f5; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            height: 100vh; 
            margin: 0; 
            overflow: hidden; /* 防止手機整頁晃動 */
        }

        /* 模擬手機容器 */
        .phone-container { 
            width: 100%;
            max-width: 414px; 
            height: 100vh; /* 在手機上全螢幕，在電腦上限制寬度 */
            background: white; 
            overflow: hidden; 
            position: relative;
            display: flex;
            flex-direction: column;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
        }

        @media (min-height: 700px) {
            .phone-container { height: 667px; border-radius: 30px; }
        }

        /* 紅色標題列 */
        .header { 
            background: #ff5252; 
            color: white; 
            text-align: center; 
            padding: 20px 0; 
            font-size: 1.2rem; 
            font-weight: bold; 
            z-index: 10;
        }

        /* 視窗包裝器 */
        .view-wrapper { flex: 1; position: relative; overflow: hidden; }

        /* 頁面通用樣式 */
        .view {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: white;
            transition: transform 0.3s ease-out;
            padding: 20px;
            overflow-y: auto;
        }

        /* 主選單 */
        #main-menu { z-index: 5; transform: translateX(0); }

        /* 詳情頁 (預設隱藏在右側) */
        #detail-page { z-index: 6; transform: translateX(100%); background: #f9f9f9; }

        /* 選單按鈕 */
        .menu-item { 
            background: #f1f1f1; 
            margin-bottom: 15px; 
            padding: 16px; 
            border-radius: 50px; 
            text-align: center; 
            cursor: pointer; 
            font-weight: 500;
            color: #333;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
            transition: transform 0.1s;
        }
        .menu-item:active { transform: scale(0.97); }

        /* 詳情內文卡片 */
        .content-card {
            background: white;
            padding: 20px;
            border-radius: 15px;
            min-height: 200px;
            color: #444;
            line-height: 1.7;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }

        /* 返回按鈕 */
        .back-btn {
            display: block;
            margin: 20px auto;
            color: #ff5252;
            text-align: center;
            cursor: pointer;
            font-weight: bold;
            padding: 10px;
        }

        .hint { text-align: center; font-size: 0.8rem; color: #bbb; margin-top: 10px; }
        
        a { color: #ff5252; text-decoration: underline; font-weight: bold; }
    </style>
</head>
<body>

    <div class="phone-container">
        <div class="header" id="nav-title">常見問題</div>

        <div class="view-wrapper">
            <div id="main-menu" class="view">
                <div class="menu-item" onclick="openPage('出貨時間', '現貨商品，完成下單後將於 5-7 個工作天出貨。不是現貨商品則需 3-4 個月工作天製作（不含國定假日）。若同時購買訂製或預購商品，將待商品到齊後一起出貨。如想先收到現貨商品，麻煩請分開下單。')">出貨時間</div>
                <div class="menu-item" onclick="openPage('訂單問題', '您好～若您有訂單相關問題，歡迎提供訂購人姓名、Email 與訂單編號，並私訊我們的官方 IG，我們將協助您處理，謝謝您。')">訂單問題</div>
                <div class="menu-item" onclick="openPage('預購說明', '您好～預購出貨月為預估值，可能會因為生產/船運/品管/貨運等因素提早或延期發貨，不好意思造成您的不便，謝謝您的支持。')">預購說明</div>
                <div class="menu-item" onclick="openPage('退換貨政策', '【退換貨說明】請於出貨日起 15 天內聯繫客服。商品需保持完整包裝，非官方瑕疵或拆封損壞恕不退換。開箱請全程錄影，未提供完整影片不受理退換貨。個人取消訂單將扣手續費 2% 及保證金 5%。公仔／玩具塗裝問題 15 天內可依認證卡申請免費維修一次（寄回運費由消費者先付，若官方瑕疵則退回）。盲盒中盒重複屬廠商裝盒問題。')">退換貨政策</div>
                <div class="menu-item" onclick="openPage('客服聯絡方式', 'Instagram 客服：<br><a href=\'https://www.instagram.com/jinart2018/\' target=\'_blank\'>@jinart2018</a><br>服務時間：09:30 - 17:00')">客服聯絡方式</div>
            </div>

            <div id="detail-page" class="view">
                <div class="content-card" id="detail-content"></div>
                <div class="back-btn" onclick="goBack()">← 返回選單</div>
                <p class="hint">（也可從左側向右滑動返回）</p>
            </div>
        </div>
    </div>

    <script>
        const navTitle = document.getElementById('nav-title');
        const detailPage = document.getElementById('detail-page');
        const detailContent = document.getElementById('detail-content');

        let startX = 0;
        let moveX = 0;

        // 開啟頁面
        function openPage(title, text) {
            navTitle.innerText = title;
            detailContent.innerHTML = text;
            detailPage.style.transition = 'transform 0.3s ease-out';
            detailPage.style.transform = 'translateX(0)';
        }

        // 返回首頁
        function goBack() {
            navTitle.innerText = '常見問題';
            detailPage.style.transition = 'transform 0.3s ease-out';
            detailPage.style.transform = 'translateX(100%)';
        }

        // 滑動返回監聽
        detailPage.addEventListener('touchstart', (e) => {
            startX = e.touches[0].clientX;
        });

        detailPage.addEventListener('touchmove', (e) => {
            moveX = e.touches[0].clientX;
            let diff = moveX - startX;
            if (diff > 0) {
                detailPage.style.transition = 'none';
                detailPage.style.transform = `translateX(${diff}px)`;
            }
        });

        detailPage.addEventListener('touchend', (e) => {
            let diff = moveX - startX;
            detailPage.style.transition = 'transform 0.3s ease-out';
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
