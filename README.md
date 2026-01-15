<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>กิจกรรม 501 เลือกตั้ง’69</title>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        :root {
            /* Palette สีพาสเทล */
            --bg-color: #FDFBF7; /* ครีมอ่อน */
            --card-bg: #FFFFFF;
            --primary-pastel: #A0C4FF; /* ฟ้าพาสเทล */
            --primary-hover: #8AB6F9;
            --success-pastel: #B9FBC0; /* เขียวพาสเทล */
            --success-text: #2D6A4F;
            --error-pastel: #FFC6FF; /* ชมพู/แดงพาสเทล */
            --error-text: #880E4F;
            --text-main: #5D5D5D;
            --shadow: 0 10px 30px rgba(0,0,0,0.05);
        }

        body {
            font-family: 'Kanit', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
        }

        .container {
            background-color: var(--card-bg);
            padding: 3rem;
            border-radius: 20px;
            box-shadow: var(--shadow);
            text-align: center;
            width: 100%;
            max-width: 450px;
            transition: transform 0.3s ease;
        }

        h1 {
            font-weight: 600;
            color: #779ECB; /* ฟ้าหม่น */
            margin-bottom: 0.5rem;
            font-size: 2rem;
        }

        p.subtitle {
            color: #999;
            margin-bottom: 2rem;
            font-weight: 300;
        }

        .input-group {
            margin-bottom: 1.5rem;
            text-align: left;
        }

        label {
            display: block;
            margin-bottom: 0.5rem;
            font-size: 1rem;
            color: var(--text-main);
        }

        input[type="text"] {
            width: 100%;
            padding: 15px;
            border: 2px solid #EEE;
            border-radius: 12px;
            font-size: 1.1rem;
            font-family: 'Kanit', sans-serif;
            box-sizing: border-box; /* สำคัญเพื่อให้ padding ไม่ดัน layout */
            transition: all 0.3s;
            outline: none;
            color: var(--text-main);
        }

        input[type="text"]:focus {
            border-color: var(--primary-pastel);
            box-shadow: 0 0 0 4px rgba(160, 196, 255, 0.2);
        }

        button {
            width: 100%;
            padding: 15px;
            background-color: var(--primary-pastel);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 1.2rem;
            font-family: 'Kanit', sans-serif;
            cursor: pointer;
            transition: background 0.3s;
            font-weight: 400;
        }

        button:hover {
            background-color: var(--primary-hover);
        }

        /* Result Area */
        #result-area {
            margin-top: 2rem;
            padding: 20px;
            border-radius: 15px;
            display: none; /* ซ่อนไว้ก่อน */
            animation: fadeIn 0.5s ease;
        }

        .result-icon {
            font-size: 3rem;
            margin-bottom: 10px;
            display: block;
        }

        .result-title {
            font-size: 1.5rem;
            font-weight: 600;
            margin: 0;
        }

        .result-desc {
            margin-top: 5px;
            font-size: 1rem;
        }

        /* States */
        .status-success {
            background-color: var(--success-pastel);
            color: var(--success-text);
        }

        .status-error {
            background-color: var(--error-pastel);
            color: var(--error-text);
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Footer */
        .footer {
            margin-top: 2rem;
            font-size: 0.8rem;
            color: #CCC;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>กิจกรรม 501 เลือกตั้ง’69</h1>
        <p class="subtitle">ระบบตรวจสอบสิทธิ์การเลือกตั้ง</p>

        <div class="input-group">
            <label for="id-input">กรอกเลขประจำตัวของท่าน</label>
            <input type="text" id="id-input" placeholder="ระบุตัวเลข..." onkeypress="handleEnter(event)">
        </div>

        <button onclick="checkRights()">ตรวจสอบสิทธิ์</button>

        <div id="result-area">
            <i id="result-icon" class="result-icon fas"></i>
            <h2 id="result-title" class="result-title"></h2>
            <p id="result-desc" class="result-desc"></p>
        </div>

        <div class="footer">
            © 501 Election '69 System
        </div>
    </div>

    <script>
        // ฐานข้อมูลจากไฟล์ที่แนบมา
        const validIds = [
            "123692", "223693", "323694", "423695", "523696", 
            "623697", "723698", "823699", "923700", "1023702", 
            "1123838", "1224463", "1325079", "1425080", "1525081", 
            "1612769", "1723517", "1823554", "1923704", "2023705", 
            "2123708", "2223709", "2325083", "2425084", 
            "112233123", "212233123", "222233123", "223233123", 
            "223333123", "223343223", "223344233", "223344234", 
            "323344234", "334344234", "334444234", "334454234", 
            "334455234", "334455334", "334455344", "334455345", 
            "434455345", "444455345", "445455345"
        ];

        function checkRights() {
            const inputVal = document.getElementById('id-input').value.trim();
            const resultArea = document.getElementById('result-area');
            const resultIcon = document.getElementById('result-icon');
            const resultTitle = document.getElementById('result-title');
            const resultDesc = document.getElementById('result-desc');

            if (!inputVal) {
                alert("กรุณากรอกข้อมูลก่อนตรวจสอบ");
                return;
            }

            // Reset Classes
            resultArea.className = ''; 
            resultArea.style.display = 'block';

            if (validIds.includes(inputVal)) {
                // กรณี: มีสิทธิ์ (สีเขียวพาสเทล)
                resultArea.classList.add('status-success');
                resultIcon.className = 'result-icon fas fa-check-circle';
                resultTitle.innerText = 'คุณมีสิทธิ์เลือกตั้ง';
                resultDesc.innerText = 'ข้อมูลของคุณถูกต้องและอยู่ในระบบ';
            } else {
                // กรณี: ไม่มีสิทธิ์ (สีแดง/ชมพูพาสเทล)
                resultArea.classList.add('status-error');
                resultIcon.className = 'result-icon fas fa-times-circle';
                resultTitle.innerText = 'ไม่พบข้อมูลในระบบ';
                resultDesc.innerText = 'กรุณาตรวจสอบเลขใหม่อีกครั้ง หรือติดต่อเจ้าหน้าที่';
            }
        }

        // ฟังก์ชันเพื่อให้กด Enter แล้วตรวจสอบได้เลย
        function handleEnter(e) {
            if(e.key === 'Enter'){
                checkRights();
            }
        }
    </script>
</body>
</html>
