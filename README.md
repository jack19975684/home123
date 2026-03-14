<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <title>家系圖產生器 - 支援 JPG 下載</title>
    <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        body { font-family: 'PingFang TC', sans-serif; background: #eceff1; display: flex; flex-direction: column; align-items: center; padding: 40px; }
        .card { background: white; padding: 30px; border-radius: 15px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); width: 100%; max-width: 900px; }
        textarea { width: 100%; height: 120px; border: 1px solid #cfd8dc; border-radius: 8px; padding: 12px; font-size: 14px; margin-bottom: 15px; box-sizing: border-box; }
        .btn-group { display: flex; gap: 10px; margin-bottom: 20px; }
        button { flex: 1; padding: 12px; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; transition: 0.3s; }
        .btn-draw { background: #2196F3; color: white; }
        .btn-download { background: #ff9800; color: white; }
        button:hover { opacity: 0.8; }
        #capture-area { background: white; padding: 40px; border: 1px solid #eee; min-height: 300px; display: flex; justify-content: center; align-items: center; border-radius: 8px; overflow: auto; }
    </style>
</head>
<body>

<div class="card">
    <h2>🌳 家族關係繪製工具</h2>
    <textarea id="inputData">
graph TD
    阿公 --- 阿嬤
    阿公 --> 爸爸
    爸爸 --- 媽媽
    爸爸 --> 我
    爸爸 --> 妹妹
    </textarea>

    <div class="btn-group">
        <button class="btn-draw" onclick="drawTree()">重新生成圖表</button>
        <button class="btn-download" onclick="downloadJPG()">下載為 JPG</button>
    </div>

    <div id="capture-area">
        <div class="mermaid" id="mermaid-output">
            graph TD
                阿公 --- 阿嬤
                阿公 --> 爸爸
                爸爸 --- 媽媽
                爸爸 --> 我
                爸爸 --> 妹妹
        </div>
    </div>
</div>

<script>
    mermaid.initialize({ startOnLoad: true, theme: 'forest' });

    function drawTree() {
        const input = document.getElementById('inputData').value;
        const container = document.getElementById('capture-area');
        container.innerHTML = `<div class="mermaid">${input}</div>`;
        mermaid.run();
    }

    function downloadJPG() {
        const target = document.getElementById('capture-area');
        html2canvas(target).then(canvas => {
            const link = document.createElement('a');
            link.download = 'family-tree.jpg';
            link.href = canvas.toDataURL('image/jpeg', 0.9); // 設定品質為 0.9
            link.click();
        });
    }
</script>

</body>
</html># home123
