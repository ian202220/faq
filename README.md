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
            border-left: 1px solid #eee;
            border-right: 1px solid #eee;
        }

        /* LOGO Header 區塊 */
        .logo-header { 
            width: 100%;
            background: #e60012; /* JINART 品牌紅 */
            padding: 0;
            margin: 0;
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
            transition: transform 0.3s cubic-bezier(0.1, 0.7, 0.1, 1);
            padding: 20px;
            overflow-y: auto;
        }

        #main-menu { z-index: 5; transform: translateX(0); }
        #detail-view { z-index: 6; transform: translateX(100%); background: #fcfcfc; }

        /* 按鈕樣式優化 */
        .menu-item { 
            background: #f5f5f7; 
            margin-bottom: 15px; 
            padding: 18px; 
            border-radius: 40px; 
            text-align: center; 
            cursor: pointer; 
            font-weight: bold;
            font-size: 1.05rem;
            color: #1d1d1f;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            width: 100%;
            border: none;
            display: block;
        }
        
        .menu-item:active { transform: scale(0.97); background: #e8e8ed; }

        .content-card {
            background: white;
            padding: 25px;
            border-radius: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.06);
            line-height: 1.8;
            color: #333;
            font-size: 1rem;
            margin-top: 10px;
        }

        .back-btn {
            display: block;
            margin: 30px auto;
            color: #e60012;
            font-weight: bold;
            text-align: center;
            padding: 15px;
            cursor: pointer;
            text-decoration: none;
        }

        a { color: #e60012; text-decoration: underline; font-weight: bold; }
        .hint { text-align: center; font-size: 0.8rem; color: #999; margin-top: 15px; }
    </style>
</head>
<body>

<div class="app-container">
    <div class="logo-header">
        <img src="https://raw.githubusercontent.com/ZOSeTzzMg34WY9qe7UQbun/Untitled/main/JINART%20%E5%93%81%E7%89%8C%E9%A0%AD%E5%83%8F886x425px.jpg" 
             onerror="this.src='https://placehold.co/886x425/e60012/white?text=JINART+LOGO'" 
             alt="JINART Logo">
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
    let isMoving = false;

    function openDetail(title, text) {
        detailContent.innerHTML = `<strong>【${title}】</strong><br><br>${text}`;
        detailView.style.transition = 'transform 0.3s cubic-bezier(0.1, 0.7, 0.1, 1)';
        detailView.style.transform = 'translateX(0)';
    }

    function closeDetail() {
        detailView.style.transition = 'transform 0.3s cubic-bezier(0.1, 0.7, 0.1, 1)';
        detailView.style.transform = 'translateX(100%)';
    }

    detailView.addEventListener('touchstart', e => {
        startX = e.touches[0].clientX;
        isMoving = true;
    }, {passive: true});

    detailView.addEventListener('touchmove', e => {
        if (!isMoving) return;
        moveX = e.touches[0].clientX;
        let diff = moveX - startX;
        if (diff > 0) {
            detailView.style.transition = 'none';
            detailView.style.transform = `translateX(${diff}px)`;
        }
    }, {passive: true});

    detailView.addEventListener('touchend', e => {
        isMoving = false;
        detailView.style.transition = 'transform 0.3s cubic-bezier(0.1, 0.7, 0.1, 1)';
        if (moveX - startX > 100) {
            closeDetail();
        } else {
            detailView.style.transform = 'translateX(0)';
        }
        startX = 0; 
        moveX = 0;
    });
</script>

</body>
</html>
