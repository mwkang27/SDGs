<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>지구 쓰담쓰담</title>
    <style>
        /* 앱 전체 디자인 스타일 */
        body {
            background-color: #f0f4f8;
            font-family: 'Apple SD Gothic Neo', 'Malgun Gothic', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .app-container {
            background-color: white;
            width: 360px;
            height: 640px; /* 스마트폰 비율 */
            border-radius: 25px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            box-sizing: border-box;
            position: relative;
            overflow: hidden;
            border: 8px solid #333; /* 폰 테두리 느낌 */
        }
        .header {
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
            color: #2E7D32;
        }
        .earth-character {
            font-size: 80px;
            margin: 30px 0;
            transition: transform 0.3s;
            cursor: pointer;
        }
        .earth-character:hover {
            transform: scale(1.1);
        }
        .question {
            font-size: 16px;
            color: #555;
            margin-bottom: 20px;
            text-align: center;
        }
        .btn-group {
            display: flex;
            flex-direction: column;
            width: 100%;
            gap: 10px;
        }
        .action-btn {
            background-color: #E8F5E9;
            border: 2px solid #C8E6C9;
            border-radius: 15px;
            padding: 15px;
            font-size: 16px;
            color: #2E7D32;
            cursor: pointer;
            transition: 0.2s;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .action-btn:hover {
            background-color: #C8E6C9;
            transform: translateY(-2px);
        }
        .result-screen {
            display: none; /* 평소엔 숨김 */
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(255, 255, 255, 0.95);
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            animation: fadeIn 0.5s;
        }
        .rice-bowls {
            font-size: 40px;
            margin: 20px 0;
        }
        .cheer-msg {
            font-size: 20px;
            font-weight: bold;
            color: #1565C0;
            margin: 10px 20px;
            line-height: 1.4;
        }
        .sub-msg {
            font-size: 14px;
            color: #666;
            margin-top: 10px;
        }
        .retry-btn {
            margin-top: 30px;
            padding: 10px 20px;
            background-color: #2E7D32;
            color: white;
            border: none;
            border-radius: 20px;
            cursor: pointer;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        @keyframes pop {
            0% { transform: scale(0.5); opacity: 0; }
            80% { transform: scale(1.2); }
            100% { transform: scale(1); opacity: 1; }
        }
    </style>
</head>
<body>

    <div class="app-container">
        <div class="header">지구 쓰담쓰담-"기아종식" 🌱</div>
        <div class="earth-character" id="earth">🌏</div>
        <div class="question">오늘 식사량을 얼마나 줄이셨나요?<br>작은 실천이 기적을 만듭니다.</div>

        <div class="btn-group">
            <button class="action-btn" onclick="calculate(0.5)">
                <span>🥄 한 숟가락 덜 먹기</span>
                <span>(50g)</span>
            </button>
            <button class="action-btn" onclick="calculate(1.5)">
                <span>🥣 밥 반 공기 남기기</span>
                <span>(150g)</span>
            </button>
            <button class="action-btn" onclick="calculate(3)">
                <span>🍔 인스턴트 대신 집밥</span>
                <span>(300g)</span>
            </button>
            <button class="action-btn" onclick="calculate(5)">
                <span>🥗 한 끼 소식하기</span>
                <span>(High)</span>
            </button>
        </div>

        <div class="result-screen" id="resultScreen">
            <div style="font-size: 60px;">🥰</div>
            <div class="rice-bowls" id="bowlDisplay"></div>
            <div class="cheer-msg" id="cheerMsg"></div>
            <div class="sub-msg">당신의 절약이 아이들의 한 끼가 됩니다.</div>
            <button class="retry-btn" onclick="resetApp()">내일 또 실천하기</button>
        </div>
    </div>

    <script>
        // 응원 문구 데이터베이스
        const messages = [
            "당신의 소식이<br>아이의 미소가 되었어요!",
            "지구도 가볍게,<br>마음도 가볍게! 화이팅!",
            "오늘 당신은<br>기적을 만들었습니다.",
            "선한 영향력!<br>정말 멋진 하루네요.",
            "지구를 쓰담쓰담~<br>당신 최고예요!"
        ];

        function calculate(amount) {
            const earth = document.getElementById('earth');
            const resultScreen = document.getElementById('resultScreen');
            const bowlDisplay = document.getElementById('bowlDisplay');
            const cheerMsg = document.getElementById('cheerMsg');

            // 1. 밥그릇 계산 (반올림)
            let bowlCount = Math.ceil(amount); 
            let bowls = "";
            for(let i=0; i<bowlCount; i++) {
                bowls += "🍚";
            }

            // 2. 문구 랜덤 선택
            const randomMsg = messages[Math.floor(Math.random() * messages.length)];

            // 3. 화면 표시
            bowlDisplay.innerHTML = bowls;
            cheerMsg.innerHTML = randomMsg;
            
            // 4. 결과창 띄우기
            resultScreen.style.display = 'flex';
        }

        function resetApp() {
            document.getElementById('resultScreen').style.display = 'none';
        }
    </script>
</body>
</html>
