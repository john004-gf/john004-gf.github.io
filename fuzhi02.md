<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- 引入图标库（可选，让按钮更美观） -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.2/font/bootstrap-icons.css">
    <title>可复制文本组件</title>
    <style>
        /* 文本容器样式 */
        .copy-card {
            width: 600px;
            margin: 20px auto;
            padding: 16px;
            border: 1px solid #e5e7eb;
            border-radius: 8px;
            background-color: #fff;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
            font-family: "PingFang SC", "Microsoft YaHei", sans-serif;
        }
        /* 文本标题 */
        .copy-card h3 {
            margin: 0 0 12px;
            font-size: 16px;
            color: #333;
        }
        /* 文本内容区域 */
        .copy-text {
            padding: 12px;
            border: 1px solid #eee;
            border-radius: 4px;
            background-color: #f9fafb;
            white-space: pre-wrap; /* 保留换行 */
            font-size: 14px;
            color: #555;
            overflow: auto; /* 超出自动滚动 */
            max-height: 200px; /* 限制高度 */
        }
        /* 操作按钮栏 */
        .action-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 12px;
        }
        /* 按钮通用样式 */
        .btn {
            display: inline-flex;
            align-items: center;
            padding: 6px 12px;
            border: 1px solid #ddd;
            border-radius: 4px;
            background-color: #fff;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .btn:hover {
            border-color: #007bff;
            color: #007bff;
        }
        /* 复制成功提示（可优化为动画） */
        .copy-tip {
            color: #28a745;
            font-size: 13px;
            margin-left: 8px;
            opacity: 0; /* 初始隐藏 */
            transition: opacity 0.3s;
        }
        .copy-tip.show {
            opacity: 1; /* 显示提示 */
        }
    </style>
</head>
<body>
    <!-- 可复制文本组件 -->
    <div class="copy-card">
        <h3>提示词内容</h3>
        <div class="copy-text" id="textContent">中国古代，迷你小人，远景，俯视角度，阳光明媚，高清画质，超高精度微缩模型渲染技术，热闹的古代集市上，多个身着古装的迷你小...</div>
        
        <div class="action-bar">
            <div>
                <button class="btn" id="copyBtn">
                    <i class="bi bi-clipboard"></i> 复制文本
                </button>
                <span class="copy-tip" id="copyTip">已复制！</span>
            </div>
            <button class="btn" id="expandBtn">展开完整内容</button>
        </div>
    </div>

    <script>
        // 复制功能
        const copyBtn = document.getElementById('copyBtn');
        const textContent = document.getElementById('textContent');
        const copyTip = document.getElementById('copyTip');
        
        copyBtn.addEventListener('click', () => {
            // 复制文本到剪贴板
            navigator.clipboard.writeText(textContent.innerText)
                .then(() => {
                    // 显示复制成功提示
                    copyTip.classList.add('show');
                    setTimeout(() => {
                        copyTip.classList.remove('show');
                    }, 2000); // 2秒后隐藏
                })
                .catch(err => {
                    console.error('复制失败:', err);
                    alert('复制失败，请手动复制');
                });
        });

        // 展开功能（示例：假设内容有截断，点击展开完整文本）
        const expandBtn = document.getElementById('expandBtn');
        expandBtn.addEventListener('click', () => {
            textContent.style.maxHeight = 'none'; // 取消高度限制
            expandBtn.style.display = 'none'; // 隐藏按钮
        });
    </script>
</body>
</html>
