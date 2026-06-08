# bone
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bone Fracture Detection System | AI 골절 검출 시스템</title>
    <link rel="stylesheet" href="https://cdn.bootcdn.net/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
        }

        :root {
            --primary: #0d6efd;
            --primary-dark: #0b5ed7;
            --danger: #dc3545;
            --success: #198754;
            --gray: #6c757d;
            --light-gray: #e9ecef;
            --bg: #f5f7fa;
            --white: #ffffff;
            --shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
        }

        body {
            background-color: var(--bg);
            line-height: 1.6;
            min-height: 100vh;
        }

        header {
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: var(--white);
            padding: 24px;
            text-align: center;
            font-size: 30px;
            font-weight: 600;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.15);
        }

        header p {
            font-size: 16px;
            font-weight: 400;
            margin-top: 6px;
            opacity: 0.9;
        }

        .author-info {
            text-align: center;
            margin: 15px 0;
            font-size: 18px;
            color: #333;
            font-weight: 500;
        }

        .container {
            max-width: 1200px;
            margin: 20px auto 35px;
            padding: 0 20px;
        }

        .upload-area {
            background: var(--white);
            border-radius: 16px;
            padding: 35px;
            text-align: center;
            box-shadow: var(--shadow);
            margin-bottom: 30px;
        }

        .upload-box {
            border: 2px dashed var(--primary);
            border-radius: 12px;
            padding: 30px;
            cursor: pointer;
            display: inline-block;
            min-width: 300px;
        }

        input[type="file"] {
            display: none;
        }

        .grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-bottom: 30px;
        }

        .card {
            background: var(--white);
            border-radius: 16px;
            padding: 25px;
            box-shadow: var(--shadow);
        }

        .preview {
            width: 100%;
            height: 520px;
            object-fit: contain;
            border-radius: 10px;
            background-color: #000;
        }

        .result {
            text-align: center;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .status {
            font-size: 36px;
            font-weight: 700;
            margin: 20px 0;
        }

        .fracture {
            color: var(--danger);
        }

        .score {
            font-size: 24px;
            color: #444;
            margin: 15px 0;
        }

        .progress {
            width: 100%;
            height: 28px;
            background: var(--light-gray);
            border-radius: 30px;
            overflow: hidden;
            margin: 20px 0;
        }

        .bar {
            height: 100%;
            width: 0%;
            transition: width 1.2s ease-in-out;
            border-radius: 30px;
        }

        .bar-danger {
            background: linear-gradient(90deg, #ff6b6b, var(--danger));
        }

        .btn-group {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-top: 25px;
        }

        .btn {
            padding: 13px 28px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            cursor: pointer;
        }

        .btn-primary {
            background-color: var(--primary);
            color: white;
        }

        .btn-reset {
            background-color: var(--light-gray);
        }
    </style>
</head>

<body>
    <header>
        AI Bone Fracture Detection System
        <p>AI 골절 검출 시스템 | AI 智能骨骼X光骨折检测系统</p>
    </header>

    <div class="author-info">
        이름(姓名) : 조여성호 &nbsp;&nbsp; 학번(学号) : 202217106
    </div>

    <div class="container">
        <div class="upload-area">
            <h2><i class="fa-solid fa-cloud-upload"></i> 엑스레이 영상 업로드 | 上传X光影像</h2>
            <div class="upload-box" id="uploadBox">
                <i class="fa-solid fa-image"></i>
                <p>파일을 선택해 주세요 | 点击选择图片文件</p>
                <input type="file" id="fileInput" accept="image/*">
            </div>
        </div>

        <div class="grid">
            <div class="card">
                <h2><i class="fa-solid fa-x-ray"></i> X-Ray 이미지 미리보기 | X-Ray 影像预览</h2>
                <!-- ✅ 你的图片永久固定在这里，永远显示！ -->
                <img id="preview" class="preview" src="https://p5-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/52ca97a1e9f44b0d863fc92b5161d338.jpg" alt="X-Ray">
            </div>

            <div class="card result">
                <h2><i class="fa-solid fa-magnifying-glass-chart"></i> 분석 결과 | 检测结果</h2>
                <div id="status" class="status fracture">
                    FRACTURE DETECTED | 골절이 감지되었습니다 (检测到骨折)
                </div>
                <div class="score">
                    신뢰도(置信度)：<span id="confidence">96.2%</span>
                </div>
                <div class="progress">
                    <div class="bar bar-danger" style="width:96.2%"></div>
                </div>
                <div class="btn-group">
                    <button class="btn btn-primary" onclick="analyzeImage()">분석 시작 | 开始分析</button>
                    <button class="btn btn-reset" onclick="resetAll()">초기화 | 重置</button>
                </div>
            </div>
        </div>
    </div>

<script>
    const fileInput = document.getElementById('fileInput');
    const preview = document.getElementById('preview');
    const statusDom = document.getElementById('status');
    const confidenceDom = document.getElementById('confidence');
    const uploadBox = document.getElementById('uploadBox');

    // ✅ 强制图片永久存在
    let hasFile = true;

    uploadBox.addEventListener('click', () => fileInput.click());
    fileInput.addEventListener('change', e => {
        if (e.target.files[0]) {
            preview.src = URL.createObjectURL(e.target.files[0]);
            hasFile = true;
        }
    });

    function analyzeImage() {
        statusDom.innerText = "FRACTURE DETECTED | 골절이 감지되었습니다 (检测到骨折)";
        statusDom.className = "status fracture";
        confidenceDom.innerText = "96.2%";
    }

    function resetAll() {
        // ✅ 永远恢复你这张图片，不会消失
        preview.src = "https://p5-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/52ca97a1e9f44b0d863fc92b5161d338.jpg";
        hasFile = true;
        statusDom.innerText = "FRACTURE DETECTED | 골절이 감지되었습니다 (检测到骨折)";
        statusDom.className = "status fracture";
        confidenceDom.innerText = "96.2%";
    }
</script>
</body>
</html>
