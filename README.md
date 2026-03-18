<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JINART FAQ</title>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: sans-serif;
}

body {
    background: #eaeaea;
    display: flex;
    justify-content: center;
}

/* 手機畫面 */
.app {
    width: 390px;
    height: 100vh;
    background: #f5f5f5;
    position: relative;
    overflow: hidden;
}

/* header */
.header {
    background: #ff4d4d;
    color: white;
    text-align: center;
    padding: 16px;
    border-radius: 0 0 20px 20px;
    font-weight: bold;
}

/* 頁面 */
.page {
    position: absolute;
    width: 100%;
    height: 100%;
    padding: 20px;
    transition: 0.3s;
    overflow-y: auto;
}

/* 初始 */
.home { left: 0; }
.detail { left: 100%; background: #fff; }

/* 按鈕 */
.menu-btn {
    background: #ddd;
    padding: 18px;
    margin: 12px 0;
    border-radius: 20px;
    text-align: center;
    font-weight: bold;
}

/* 上方紅色按鈕 */
.title-btn {
    background: #ff4d4d;
    color: white;
    padding: 12px;
    border-radius: 20px;
    text-align: center;
    margin-bottom: 20px;
    font-weight: bold;
}

/* 卡片 */
.card {
    background: #e5e5e5;
    padding: 20px;
    border-radius: 20px;
    margin-top: 10px;
    line-height: 1.6;
}

/* 返回 */
.back {
    text-align: center;
    margin-top: 20px;
    color: #888;
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
    "現貨商品，完成下單後 5-10 個工作天出貨。預購商品約 3-4 個月。",
    "若有訂單問題，請提供姓名、Email 並私訊 IG。",
    "預購出貨時間為預估，可能延遲。",
    "請於 15 天內聯繫客服，需完整開箱影片。",
    "Instagram：@jinart2018\n服務時間：09:30 - 17:00"
];

const detail = document.getElementById("detail");

function openPage(i) {
    document.getElementById("title").innerText = titles[i];
    document.getElementById("content").innerText = contents[i];
    detail.style.left = "0";
}

function goBack() {
    detail.style.left = "100%";
}

/* 滑動返回 */
let startX = 0;

detail.addEventListener("touchstart", e => {
    startX = e.touches[0].clientX;
});

detail.addEventListener("touchend", e => {
    let endX = e.changedTouches[0].clientX;
    if (endX - startX > 100) {
        goBack();
    }
});
</script>

</body>
</html>
</html>
