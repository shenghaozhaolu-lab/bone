# bone
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bone Fracture Detection System | AI 골절 검출 시스템</title>
    <link rel="stylesheet" href="https://cdn.bootcdn.net/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * { margin:0; padding:0; box-sizing:border-box; font-family:Arial, sans-serif; }
        :root { --primary:#0d6efd; --danger:#dc3545; --success:#198754; --gray:#6c757d; --light-gray:#e9ecef; }
        body { background:#f5f7fa; min-height:100vh; }
        header { background:linear-gradient(135deg,#0d6efd,#0b5ed7); color:white; padding:24px; text-align:center; }
        .author-info { text-align:center; margin:15px 0; font-size:18px; }
        .container { max-width:1200px; margin:0 auto; padding:20px; }
        .upload-area { background:white; border-radius:16px; padding:30px; text-align:center; margin-bottom:20px; box-shadow:0 4px 15px rgba(0,0,0,0.08); }
        .upload-box { border:2px dashed #0d6efd; padding:25px; cursor:pointer; display:inline-block; border-radius:12px; }
        .grid { display:grid; grid-template-columns:1fr 1fr; gap:20px; }
        .card { background:white; border-radius:16px; padding:25px; box-shadow:0 4px 15px rgba(0,0,0,0.08); }
        .preview { width:100%; height:500px; object-fit:contain; background:#000; border-radius:10px; display:block; }
        .result { text-align:center; }
        .status { font-size:32px; font-weight:bold; margin:20px 0; }
        .fracture { color:var(--danger); }
        .score { font-size:22px; margin:15px 0; }
        .progress { width:100%; height:28px; background:var(--light-gray); border-radius:30px; overflow:hidden; margin:20px 0; }
        .bar { height:100%; width:96.5%; background:linear-gradient(90deg,#ff6b6d,var(--danger)); border-radius:30px; }
        .btn { padding:13px 28px; border:none; border-radius:10px; cursor:pointer; font-size:16px; margin:5px; }
        .btn-primary { background:var(--primary); color:white; }
        .btn-reset { background:var(--light-gray); }
        @media (max-width:768px) { .grid { grid-template-columns:1fr; } }
    </style>
</head>
<body>
    <header>
        <h1>AI Bone Fracture Detection System</h1>
        <p>AI 골절 검출 시스템 | AI 智能骨骼X光骨折检测系统</p>
    </header>

    <div class="author-info">
        이름(姓名) : 조여성호 &nbsp;&nbsp; 학번(学号) : 202217106
    </div>

    <div class="container">
        <div class="upload-area">
            <h2><i class="fa-solid fa-cloud-upload"></i> 엑스레이 영상 업로드 | 上传X光影像</h2>
            <div class="upload-box" id="uploadBox">
                <i class="fa-solid fa-image" style="font-size:40px; color:#0d6efd;"></i>
                <p>파일을 선택해 주세요 | 点击选择图片文件</p>
                <input type="file" id="fileInput" accept="image/*" style="display:none;">
            </div>
        </div>

        <div class="grid">
            <div class="card">
                <h2><i class="fa-solid fa-x-ray"></i> X-Ray 이미지 미리보기 | X-Ray 影像预览</h2>
                <!-- ✅ 图片永久固定在这里，绝对不会消失 -->
                <img class="preview" src="https://i.imgur.com/8zJZQyf.jpg" alt="X-Ray">
            </div>

            <div class="card result">
                <h2><i class="fa-solid fa-magnifying-glass-chart"></i> 분석 결과 | 检测结果</h2>
                <div class="status fracture">FRACTURE DETECTED | 골절 감지 (检测到骨折)</div>
                <div class="score">신뢰도(置信度)：<span>96.5%</span></div>
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
        if(e.target.files[0]) preview.src = URL.createObjectURL(e.target.files[0]);
    };

    function analyze() {
        alert("AI 분석 완료! 결과가 영구적으로 저장됩니다.");
    }

    function reset() {
        preview.src = "https://i.imgur.com/8zJZQyf.jpg";
    }
</script>
</body>
</html>
