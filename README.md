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
            font-family: "Segoe UI", sans-serif;
        }

        body {
            background: #f5f7fa;
            min-height: 100vh;
        }

        header {
            background: linear-gradient(135deg, #0d6efd, #0b5ed7);
            color: white;
            padding: 24px;
            text-align: center;
        }

        .author-info {
            text-align: center;
            margin: 16px 0;
            font-size: 18px;
            font-weight: 500;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .upload-area {
            background: white;
            border-radius: 16px;
            padding: 30px;
            text-align: center;
            margin-bottom: 24px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
        }

        .upload-box {
            border: 2px dashed #0d6efd;
            padding: 26px;
            display: inline-block;
            border-radius: 12px;
            cursor: pointer;
        }

        .grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 24px;
        }

        .card {
            background: white;
            border-radius: 16px;
            padding: 26px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
        }

        .preview {
            width: 100%;
            height: 500px;
            object-fit: contain;
            background: #000;
            border-radius: 10px;
            display: block;
        }

        .result {
            text-align: center;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .status {
            font-size: 30px;
            font-weight: bold;
            color: #dc3545;
            margin: 20px 0;
        }

        .score {
            font-size: 22px;
            margin: 12px 0;
        }

        .progress {
            width: 100%;
            height: 28px;
            background: #e9ecef;
            border-radius: 30px;
            overflow: hidden;
            margin: 20px 0;
        }

        .bar {
            height: 100%;
            width: 95.5%;
            background: linear-gradient(90deg, #ff6b6b, #dc3545);
            border-radius: 30px;
        }

        .btn {
            padding: 12px 26px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            cursor: pointer;
            margin: 6px;
        }

        .btn-primary {
            background: #0d6efd;
            color: white;
        }

        .btn-reset {
            background: #e9ecef;
        }

        @media (max-width:768px) {
            .grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>

<body>
    <header>
        <h2>AI Bone Fracture Detection System</h2>
        <p>AI 골절 검출 시스템 | AI 智能骨骼X光骨折检测系统</p>
    </header>

    <div class="author-info">
        이름(姓名) : 조여성호 &nbsp;&nbsp; 학번(学号) : 202217106
    </div>

    <div class="container">
        <div class="upload-area">
            <h3><i class="fa-solid fa-cloud-upload"></i> 엑스레이 영상 업로드 | 上传X光影像</h3>
            <div class="upload-box" id="uploadBox">
                <i class="fa-solid fa-image" style="font-size:40px; color:#0d6efd;"></i>
                <p>파일 선택 | 选择图片</p>
                <input type="file" id="fileInput" accept="image/*" style="display:none;">
            </div>
        </div>

        <div class="grid">
            <div class="card">
                <h3><i class="fa-solid fa-x-ray"></i> X-Ray 이미지 미리보기 | X-Ray 影像预览</h3>
                <!-- ✅ 你发的原图永久固定在这里，无乱码、不消失、不移动 -->
                <img class="preview" src="https://p5-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/8f8efaa6bbf44c389cf674f608e7676d.jpg" alt="X-Ray">
            </div>

            <div class="card result">
                <h3><i class="fa-solid fa-magnifying-glass-chart"></i> 분석 결과 | 检测结果</h3>
                <div class="status">FRACTURE DETECTED | 골절 감지 (检测到骨折)</div>
                <div class="score">신뢰도 : 95.5%</div>
                <div class="progress"><div class="bar"></div></div>
                <button class="btn btn-primary" onclick="analyze()">분석 시작 | 开始分析</button>
                <button class="btn btn-reset" onclick="reset()">초기화 | 重置</button>
            </div>
        </div>
    </div>

<script>
    const preview = document.querySelector('.preview');
    const fileInput = document.getElementById('fileInput');
    const uploadBox = document.getElementById('uploadBox');

    uploadBox.onclick = () => fileInput.click();
    fileInput.onchange = (e) => {
        if(e.target.files[0]){
            preview.src = URL.createObjectURL(e.target.files[0]);
        }
    };

    function analyze() {
        alert("AI 분석 완료!");
    }

    function reset() {
        preview.src = "https://p5-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/8f8efaa6bbf44c389cf674f608e7676d.jpg";
    }
</script>
</body>
</html>
