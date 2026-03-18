<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>JINART FAQ</title>
    <style>
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        
        body { 
            font-family: -apple-system, "Helvetica Neue", sans-serif; 
            background: #ffffff; 
            margin: 0; 
            display: flex; 
            justify-content: center; 
            height: 100vh;
            overflow: hidden; 
        }

        .app-container { 
            width: 100%; 
            max-width: 450px; 
            background: white; 
            position: relative;
            display: flex;
            flex-direction: column;
        }

        /* 使用官方 LOGO 作為 Header */
        .logo-header { 
            width: 100%;
            background: #ff0000; /* 官方紅底色 */
            display: block;
        }
        
        .logo-header img {
            width: 100%;
            height: auto;
            display: block;
        }

        .view-wrapper { flex: 1; position: relative; overflow: hidden; }

        .view {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: white;
            transition: transform 0.3s ease-out;
            padding: 25px;
            overflow-y: auto;
        }

        #main-menu { z-index: 5; transform: translateX(0); }
        #detail-view { z-index: 6; transform: translateX(100%); background: #fcfcfc; }

        /* 按鈕尺寸修復：符合手機寬度 */
        .menu-item { 
            background: #f2f2f2; 
            margin-bottom: 20px; 
            padding: 20px; 
            border-radius: 40px; 
            text-align: center; 
            cursor: pointer; 
            font-weight: bold;
            font-size: 1.1rem;
            color: #333;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            width: 100%; /* 撐開寬度 */
        }
        
        .menu-item:active { transform: scale(0.96); background: #e0e0e0; }

        .content-card {
            background: white;
            padding: 25px;
            border-radius: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
            line-height: 1.8;
            color: #444;
            font-size: 1rem;
        }

        .back-btn {
            display: block;
            margin: 30px auto;
            color: #ff0000;
            font-weight: bold;
            text-align: center;
            padding: 10px;
            cursor: pointer;
        }

        a { color: #ff0000; text-decoration: underline; }
        .hint { text-align: center; font-size: 0.85rem; color: #bbb; margin-top: 10px; }
    </style>
</head>
<body>

<div class="app-container">
    <div class="logo-header">
        <img src="https://raw.githubusercontent.com/ZOSeTzzMg34WY9qe7UQbun/Untitled/main/JINART%20%E5%93%81%E7%89%8C%E9%A0%AD%E5%83%8F886x425px.jpg" alt="JINART Logo">
    </div>

    <div class="view-wrapper">
        <div id="main-menu" class="view">
            <div class="menu-item" onclick="openDetail('出貨時間', '現貨商品，完成下單後將於 5-7 個工作天出貨。不是現貨商品則需 3-4 個月工作天製作（不含國定假日）。若同時購買訂製或預購商品，將待商品到齊後一起出貨。如想先收到現貨商品，麻煩請分開下單。')">出貨時間</div>
            <div class="menu-item" onclick="openDetail('訂單問題', '您好～若您有訂單相關問題，歡迎提供訂購人姓名、Email 與訂單編號，並私訊我們的官方 IG，我們將協助您處理，謝謝您。')">訂單問題</div>
            <div class="menu-item" onclick="openDetail('預購說明', '您好～預購出貨月為預估值，可能會因為生產/船運/品管/貨運等因素提早或延期發貨，不好意思造成您的不便，謝謝您的支持。')">預購說明</div>
            <div class="menu-item" onclick="openDetail('退換貨政策', '【退換貨說明】請於出貨日起 15 天內聯繫客服。商品需保持完整包裝，非官方瑕疵或拆封損壞恕不退換。開箱請全程錄影，未提供完整影片不受理退換貨。個人取消訂單將扣手續費 2% 及保證金 5%。公仔／玩具塗裝問題 15 天內可依認證卡申請免費維修一次。')">退換貨政策</div>
            <div class="menu-item" onclick="openDetail('客服聯絡方式', 'Instagram 客服：<br><a href=\'https://www.instagram.com/jinart2018/\' target=\'_blank\'>@jinart2018</a><br>服務時間：09:30 - 17:00')">客服聯絡方式</div>
        </div>

        <div id="detail-view" class="view">
            <div class="content-card" id="detail-content"></div>
            <div class="back-btn" onclick="closeDetail()">← 返回常見問題</div>
            <p class="hint">（也可向右滑動返回）</p>
        </div>
    </div>
</div>

<script>
    const detailView = document.getElementById('detail-view');
    const detailContent = document.getElementById('detail-content');
    
    let startX = 0;
    let moveX = 0;

    function openDetail(title, text) {
        detailContent.innerHTML = `<strong>【${title}】</strong><br><br>${text}`;
        detailView.style.transform = 'translateX(0)';
    }

    function closeDetail() {
        detailView.style.transform = 'translateX(100%)';
    }

    // 滑動返回
    detailView.addEventListener('touchstart', e => startX = e.touches[0].clientX);
    detailView.addEventListener('touchmove', e => {
        moveX = e.touches[0].clientX;
        let diff = moveX - startX;
        if (diff > 0) {
            detailView.style.transition = 'none';
            detailView.style.transform = `translateX(${diff}px)`;
        }
    });
    detailView.addEventListener('touchend', () => {
        detailView.style.transition = 'transform 0.3s ease-out';
        if (moveX - startX > 100) closeDetail();
        else detailView.style.transform = 'translateX(0)';
        startX = 0; moveX = 0;
    });
</script>

</body>
</html>
