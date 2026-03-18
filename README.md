<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FAQ</title>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, sans-serif;
}

body {
    background: #e9e9eb;
    display: flex;
    justify-content: center;
}

/* 手機容器 */
.app {
    width: 390px;
    height: 100vh;
    background: #f2f2f7;
    border-radius: 30px;
    overflow: hidden;
    position: relative;
    box-shadow: 0 20px 50px rgba(0,0,0,0.15);
}

/* header */
.title-btn {
    background: linear-gradient(135deg, #ff4d4d, #ff6b6b);
    color: white;
    text-align: center;
    padding: 14px;
    border-radius: 20px;
    font-weight: 600;
    margin-bottom: 20px;
    box-shadow: 0 8px 20px rgba(255,77,77,0.3);
}

/* page */
.page {
    position: absolute;
    width: 100%;
    height: 100%;
    padding: 20px;
    transition: transform 0.35s ease;
    overflow-y: auto;
}

.home { transform: translateX(0); }
.detail { transform: translateX(100%); }

/* 按鈕 */
.menu-btn {
    background: #ffffff;
    padding: 18px;
    margin: 12px 0;
    border-radius: 20px;
    text-align: center;
    font-weight: 500;
    box-shadow: 0 5px 15px rgba(0,0,0,0.08);
    transition: 0.2s;
}

.menu-btn:active {
    transform: scale(0.96);
}

/* 卡片 */
.card {
    background: rgba(255,255,255,0.7);
    backdrop-filter: blur(10px);
    padding: 20px;
    border-radius: 20px;
    line-height: 1.8;
    font-size: 14px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.08);
    white-space: pre-line;
}

/* 返回 */
.back {
    text-align: center;
    margin-top: 20px;
    color: #999;
    font-size: 14px;
}
</style>
</head>

<body>

<div class="app">

    <!-- 首頁 -->
    <div class="page home" id="home">
        <div class="title-btn">常見問題</div>

        <div class="menu-btn" onclick="openPage(0)">出貨時間</div>
        <div class="menu-btn" onclick="openPage(1)">訂單問題</div>
        <div class="menu-btn" onclick="openPage(2)">預購說明</div>
        <div class="menu-btn" onclick="openPage(3)">退換貨政策</div>
        <div class="menu-btn" onclick="openPage(4)">客服聯絡方式</div>
    </div>

    <!-- 分頁 -->
    <div class="page detail" id="detail">
        <div class="title-btn" id="title"></div>
        <div class="card" id="content"></div>
        <div class="back" onclick="goBack()">← 返回首頁</div>
    </div>

</div>

<script>
const titles = [
"出貨時間",
"訂單問題",
"預購說明",
"退換貨政策",
"客服聯絡方式"
];

const contents = [

`現貨商品，完成下單後將於 5-10 個工作天出貨。非現貨商品則需 3-4 個月工作天製作（不含國定假日）。

若同時購買訂製或預購商品，將待商品到齊後一起出貨。如想先收到現貨商品，麻煩請分開下單。`,

`若有訂單相關問題，歡迎提供
訂購人姓名、Email 與訂單編號，

並私訊我們的官方Instagram 客服：@jinart2018，
我們將協助您處理，謝謝您。`,

`預購出貨月為預估值，可能會因為生產/船運/品管/貨運等因素提早或延期發貨，不好意思造成您的不便，謝謝您的支持。

若同時購買訂製或預購商品，將待商品到齊後一起出貨。如想先收到現貨商品，麻煩請分開下單。`,

`請於出貨日起 15 天內聯繫客服。商品需保持完整包裝，非官方瑕疵或拆封損壞恕不退換。

開箱請全程錄影，未提供完整影片不受理退換貨。

個人取消訂單將扣手續費 2% 及保證金 5%。

公仔／玩具塗裝問題 15 天內可依認證卡申請免費維修一次。`,

`Instagram 客服：
@jinart2018

服務時間：周一至周五09:30 - 17:00
國定假日不提供客服與出貨服務。`
];

const home = document.getElementById("home");
const detail = document.getElementById("detail");

function openPage(i) {
    document.getElementById("title").innerText = titles[i];
    document.getElementById("content").innerText = contents[i];
    home.style.transform = "translateX(-100%)";
    detail.style.transform = "translateX(0)";
}

function goBack() {
    home.style.transform = "translateX(0)";
    detail.style.transform = "translateX(100%)";
}

/* 滑動返回（升級版） */
let startX = 0;
let currentX = 0;
let dragging = false;

detail.addEventListener("touchstart", e => {
    startX = e.touches[0].clientX;
    dragging = true;
});

detail.addEventListener("touchmove", e => {
    if (!dragging) return;
    currentX = e.touches[0].clientX;
    let diff = currentX - startX;
    if (diff > 0) {
        detail.style.transform = `translateX(${diff}px)`;
    }
});

detail.addEventListener("touchend", () => {
    dragging = false;
    let diff = currentX - startX;

    if (diff > 120) {
        goBack();
    } else {
        detail.style.transform = "translateX(0)";
    }
});
</script>

</body>
</html>
