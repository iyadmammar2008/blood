<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تبادل الدم (التبرع)</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #fff;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }
        h1 {
            text-align: center;
            margin-bottom: 20px;
            font-size: 2.5em;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        .transfusion {
            text-align: center;
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            max-width: 600px;
            width: 100%;
        }
        .transfusion select {
            padding: 10px;
            font-size: 1em;
            border-radius: 5px;
            border: none;
            margin: 10px;
            width: 200px;
        }
        .transfusion button {
            background: #4CAF50;
            color: #fff;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1em;
            margin-top: 20px;
            transition: background 0.3s;
        }
        .transfusion button:hover {
            background: #45A049;
        }
        .feedback {
            margin-top: 20px;
            font-size: 1.2em;
            font-weight: bold;
        }
        .info {
            margin-top: 20px;
            font-size: 1.1em;
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <h1>تبادل الدم (التبرع)</h1>
    <div class="transfusion">

        <label>اختر المتبرع:</label>
        <select id="donor-select">
            <option value="">اختر...</option>
            <option value="iyad">إياد (A+)</option>
            <option value="youssf">يوسف (B-)</option>
            <option value="taybi">طيبي (O+)</option>
            <option value="mohamed">محمد (AB-)</option>
            <option value="badr">بدر الدين (O-)</option>
            <option value="walid">وليد (A-)</option>
            <option value="yassin">ياسين (B+)</option>
            <option value="israa">إسراء (A-)</option>
            <option value="sirin">سيرين (B+)</option>
            <option value="juhaina">جهينة (AB+)</option>
            <option value="hala">هالا (O+)</option>
            <option value="fatna">فاطنة (A+)</option>
            <option value="ihssan">إحسان (B-)</option>
            <option value="roufayda">رفيدة (AB-)</option>
            <option value="amal">أمال (O-)</option>
        </select>
        <br>

        <label>اختر المتلقي:</label>
        <select id="recipient-select">
            <option value="">اختر...</option>
            <option value="iyad">إياد (A+)</option>
            <option value="youssf">يوسف (B-)</option>
            <option value="taybi">طيبي (O+)</option>
            <option value="mohamed">محمد (AB-)</option>
            <option value="badr">بدر الدين (O-)</option>
            <option value="walid">وليد (A-)</option>
            <option value="yassin">ياسين (B+)</option>
            <option value="israa">إسراء (A-)</option>
            <option value="sirin">سيرين (B+)</option>
            <option value="juhaina">جهينة (AB+)</option>
            <option value="hala">هالا (O+)</option>
            <option value="fatna">فاطنة (A+)</option>
            <option value="ihssan">إحسان (B-)</option>
            <option value="roufayda">رفيدة (AB-)</option>
            <option value="amal">أمال (O-)</option>
        </select>
        <br>

        <button onclick="checkTransfusion()">تحقق التوافق</button>
        <div class="feedback" id="transfusion-feedback"></div>

        <div class="info">
            <strong>معلومة:</strong>  
            A- يمكنه التبرع لـ A+ و A- و AB+ و AB-  
            O- يمكنه التبرع للجميع  
            AB+ يمكنه استقبال من الجميع  
        </div>
    </div>

    <script>
        const persons = {
            iyad: 'A+',
            youssf: 'B-',
            taybi: 'O+',
            mohamed: 'AB-',
            badr: 'O-',
            walid: 'A-',
            yassin: 'B+',
            israa: 'A-',
            sirin: 'B+',
            juhaina: 'AB+',
            hala: 'O+',
            fatna: 'A+',
            ihssan: 'B-',
            roufayda: 'AB-',
            amal: 'O-'
        };

        const compatibility = {
            'O-': ['O-', 'O+', 'A-', 'A+', 'B-', 'B+', 'AB-', 'AB+'],
            'O+': ['O+', 'A+', 'B+', 'AB+'],
            'A-': ['A-', 'A+', 'AB-', 'AB+'],
            'A+': ['A+', 'AB+'],
            'B-': ['B-', 'B+', 'AB-', 'AB+'],
            'B+': ['B+', 'AB+'],
            'AB-': ['AB-', 'AB+'],
            'AB+': ['AB+']
        };

        function checkTransfusion() {
            const donor = document.getElementById("donor-select").value;
            const recipient = document.getElementById("recipient-select").value;
            const result = document.getElementById("transfusion-feedback");

            if (!donor || !recipient) {
                result.textContent = "يرجى اختيار المتبرع والمتلقي.";
                result.style.color = "#FFEB3B";
                return;
            }

            if (donor === recipient) {
                result.textContent = "لا يمكن للشخص التبرع لنفسه.";
                result.style.color = "#F44336";
                return;
            }

            const donorType = persons[donor];
            const recipientType = persons[recipient];

            const allowed = compatibility[donorType].includes(recipientType);

            if (allowed) {
                result.textContent = `✔ نعم، ${donorType} يمكنه التبرع لـ ${recipientType}.`;
                result.style.color = "#4CAF50";
            } else {
                result.textContent = `✖ لا، ${donorType} لا يمكنه التبرع لـ ${recipientType}.`;
                result.style.color = "#F44336";
            }
        }
    </script>

</body>
</html>
