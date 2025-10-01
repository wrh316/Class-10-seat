<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Class 10's Seat Random Number Program.</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        :root {
            --primary: #4361ee;
            --secondary: #3a0ca3;
            --accent: #4cc9f0;
            --success: #4ade80;
            --warning: #f59e0b;
            --danger: #ef4444;
            --light: #f8fafc;
            --dark: #1e293b;
            --gray: #64748b;
        }
        
        body {
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: var(--dark);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            line-height: 1.6;
        }
        
        .container {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 24px;
            box-shadow: 
                0 25px 50px -12px rgba(0, 0, 0, 0.25),
                inset 0 1px 0 rgba(255, 255, 255, 0.3);
            padding: 40px;
            max-width: 1200px;
            width: 100%;
            border: 1px solid rgba(255, 255, 255, 0.2);
            position: relative;
            overflow: hidden;
        }
        
        .container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, 
                var(--primary), 
                var(--accent), 
                var(--success), 
                var(--warning));
            border-radius: 24px 24px 0 0;
        }
        
        header {
            text-align: center;
            margin-bottom: 40px;
            position: relative;
        }
        
        .logo {
            width: 80px;
            height: 80px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border-radius: 50%;
            margin: 0 auto 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 8px 25px rgba(67, 97, 238, 0.3);
        }
        
        .logo i {
            font-size: 2rem;
            color: white;
        }
        
        h1 {
            color: var(--dark);
            font-size: 2.8rem;
            font-weight: 700;
            margin-bottom: 10px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .subtitle {
            color: var(--gray);
            font-size: 1.2rem;
            font-weight: 400;
        }
        
        .control-panel {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 40px;
            flex-wrap: wrap;
        }
        
        .btn {
            padding: 16px 32px;
            border: none;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            align-items: center;
            gap: 12px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }
        
        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
            transition: 0.5s;
        }
        
        .btn:hover::before {
            left: 100%;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
        }
        
        .btn-secondary {
            background: linear-gradient(135deg, var(--gray), #475569);
            color: white;
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
        }
        
        .btn:active {
            transform: translateY(-1px);
        }
        
        .output-section {
            background: var(--light);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 
                inset 0 2px 4px rgba(0, 0, 0, 0.05),
                0 4px 20px rgba(0, 0, 0, 0.08);
            border: 1px solid rgba(255, 255, 255, 0.5);
        }
        
        .output-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid rgba(0, 0, 0, 0.1);
        }
        
        .output-title {
            font-size: 1.4rem;
            font-weight: 600;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .output-container {
            background: #1e293b;
            color: #e2e8f0;
            padding: 25px;
            border-radius: 15px;
            font-family: 'Fira Code', 'Cascadia Code', 'Courier New', monospace;
            white-space: pre;
            overflow-x: auto;
            border: 2px solid #334155;
            box-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.5);
            line-height: 1.8;
            font-size: 15px;
            font-weight: 500;
            min-height: 300px;
            position: relative;
        }
        
        .visualization {
            display: none;
            margin-top: 30px;
        }
        
        .classroom {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 30px;
            position: relative;
        }
        
        .teacher-desk {
            width: 350px;
            height: 50px;
            background: linear-gradient(135deg, #8e9eab, #eef2f3);
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 50px;
            border-radius: 10px;
            font-weight: bold;
            font-size: 1.3rem;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
            border: 3px solid #bdc3c7;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        }
        
        .rows {
            display: flex;
            flex-direction: column;
            gap: 20px;
            width: 100%;
        }
        
        .row {
            display: flex;
            justify-content: center;
            gap: 20px;
        }
        
        .desk {
            width: 200px;
            height: 90px;
            background: linear-gradient(135deg, #f5f7fa, #c3cfe2);
            border: 3px solid #a5b1c2;
            border-radius: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            position: relative;
        }
        
        .desk::after {
            content: '';
            position: absolute;
            top: 5px;
            left: 5px;
            right: 5px;
            bottom: 5px;
            border: 1px solid rgba(255,255,255,0.5);
            border-radius: 8px;
            pointer-events: none;
        }
        
        .desk:hover {
            transform: translateY(-5px) scale(1.02);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.2);
            border-color: #667eea;
        }
        
        .student {
            text-align: center;
            width: 48%;
            font-size: 1rem;
            font-weight: 600;
            padding: 5px;
            border-radius: 6px;
            transition: all 0.3s ease;
        }
        
        .student.boy {
            background: linear-gradient(135deg, #74b9ff, #0984e3);
            color: white;
            box-shadow: 0 3px 10px rgba(116, 185, 255, 0.3);
        }
        
        .student.girl {
            background: linear-gradient(135deg, #fd79a8, #e84393);
            color: white;
            box-shadow: 0 3px 10px rgba(253, 121, 168, 0.3);
        }
        
        .student:hover {
            transform: scale(1.05);
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        
        .stat-card {
            background: linear-gradient(135deg, var(--light), white);
            padding: 25px;
            border-radius: 16px;
            text-align: center;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
            border: 1px solid rgba(255, 255, 255, 0.5);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 4px;
            height: 100%;
            background: linear-gradient(to bottom, var(--primary), var(--accent));
        }
        
        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
        }
        
        .stat-icon {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 15px;
            font-size: 1.5rem;
            color: white;
        }
        
        .stat-boy .stat-icon { background: linear-gradient(135deg, #3b82f6, #1d4ed8); }
        .stat-girl .stat-icon { background: linear-gradient(135deg, #ec4899, #be185d); }
        .stat-total .stat-icon { background: linear-gradient(135deg, #10b981, #047857); }
        .stat-seat .stat-icon { background: linear-gradient(135deg, #f59e0b, #d97706); }
        
        .stat-card h3 {
            color: var(--gray);
            font-size: 0.95rem;
            margin-bottom: 8px;
            font-weight: 500;
        }
        
        .stat-card .number {
            font-size: 2.2rem;
            font-weight: 700;
            color: var(--dark);
        }
        
        .loading {
            display: none;
            text-align: center;
            padding: 30px;
        }
        
        .spinner {
            width: 60px;
            height: 60px;
            border: 4px solid rgba(67, 97, 238, 0.2);
            border-top: 4px solid var(--primary);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }
        
        footer {
            margin-top: 40px;
            text-align: center;
            color: var(--gray);
            padding-top: 25px;
            border-top: 1px solid rgba(0, 0, 0, 0.1);
        }
        
        .footer-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .version {
            background: var(--light);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 500;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 25px;
            }
            
            h1 {
                font-size: 2.2rem;
            }
            
            .control-panel {
                flex-direction: column;
                align-items: center;
            }
            
            .btn {
                width: 100%;
                max-width: 300px;
                justify-content: center;
            }
            
            .output-container {
                font-size: 13px;
                padding: 20px;
            }
            
            .teacher-desk {
                width: 280px;
                font-size: 1.1rem;
            }
            
            .desk {
                width: 160px;
                height: 75px;
                padding: 8px;
            }
            
            .student {
                font-size: 0.85rem;
            }
            
            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .footer-content {
                flex-direction: column;
                text-align: center;
            }
        }
        
        @media (max-width: 480px) {
            .container {
                padding: 20px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .teacher-desk {
                width: 220px;
                font-size: 1rem;
            }
            
            .desk {
                width: 140px;
                height: 65px;
            }
            
            .student {
                font-size: 0.75rem;
            }
            
            .stats-grid {
                grid-template-columns: 1fr;
            }
            
            .output-container {
                font-size: 12px;
            }
        }
        
        .floating {
            animation: floating 3s ease-in-out infinite;
        }
        
        @keyframes floating {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        
        .success-message {
            position: fixed;
            top: 20px;
            right: 20px;
            background: var(--success);
            color: white;
            padding: 15px 25px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            transform: translateX(400px);
            transition: transform 0.3s ease;
            z-index: 1000;
        }
        
        .success-message.show {
            transform: translateX(0);
        }
        
        .tab-buttons {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
            gap: 10px;
        }
        
        .tab-btn {
            padding: 12px 24px;
            background: var(--light);
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            color: var(--gray);
        }
        
        .tab-btn.active {
            background: var(--primary);
            color: white;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo floating">
                <i class="fas fa-chalkboard-teacher"></i>
            </div>
            <h1>Class 10,Grade 2024</h1>
            <p class="subtitle">Seat Random Number Program.</p>
        </header>
        
        <div class="control-panel">
            <button class="btn btn-primary" onclick="generateSeats()">
                <i class="fas fa-random"></i>
                🎲 Generate Random Seating Chart.
            </button>
            <button class="btn btn-secondary" onclick="resetOutput()">
                <i class="fas fa-redo"></i>
                🔄 Reset System.
            </button>
        </div>
        
        <div class="loading" id="loading">
            <div class="spinner"></div>
            <p>Seats are being randomly assigned...</p>
        </div>
        
        <div class="output-section">
            <div class="output-header">
                <div class="output-title">
                    <i class="fas fa-table"></i>
                    Seat Allocation Result.
                </div>
                <div class="tab-buttons">
                    <button class="tab-btn active" onclick="switchTab('console')">Console View.</button>
                    <button class="tab-btn" onclick="switchTab('visual')">Visual View.</button>
                </div>
            </div>
            
            <div class="tab-content active" id="console-tab">
                <div class="output-container" id="output">
Welcome to use the intelligent seat allocation system.
Click the button above to start generating a random seating chart.
This system ensures the randomness and fairness of seat allocation, with a 3.2% probability of each person being assigned.
                </div>
            </div>
            
            <div class="tab-content" id="visual-tab">
                <div class="classroom">
                    <div class="teacher-desk" id="teacherDesk">
                        <i class="fas fa-chalkboard"></i> 讲台
                    </div>
                    <div class="rows" id="seatingPlan">
                        <div style="text-align: center; padding: 40px; color: #7f8c8d; font-size: 1.2rem;">
                            Click the "Generate Random Seating Chart" button to start seat allocation.
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="stats-grid">
            <div class="stat-card stat-boy">
                <div class="stat-icon">
                    <i class="fas fa-male"></i>
                </div>
                <h3>Boy Count.</h3>
                <div class="number">31</div>
            </div>
            <div class="stat-card stat-girl">
                <div class="stat-icon">
                    <i class="fas fa-female"></i>
                </div>
                <h3>Girl Count.</h3>
                <div class="number">23</div>
            </div>
            <div class="stat-card stat-total">
                <div class="stat-icon">
                    <i class="fas fa-users"></i>
                </div>
                <h3>All Count.</h3>
                <div class="number">54</div>
            </div>
            <div class="stat-card stat-seat">
                <div class="stat-icon">
                    <i class="fas fa-chair"></i>
                </div>
                <h3>Seat Count.</h3>
                <div class="number">27</div>
            </div>
        </div>
        
        <footer>
            <div class="footer-content">
                <div>
                    <p>© 2025 Class 10's Seat Random Number Program. | Author by @wrh316 | Website</p>
                    <p style="margin-top: 5px; font-size: 0.9rem; color: #94a3b8;">
                        <i class="fas fa-code"></i> Website Versions，C++ Versions：https://note.ms/class10seat
                    </p>
                </div>
                <div class="version">
                    <i class="fas fa-star"></i> Version 3.16.7 | Last Update: 2025.10.1
                </div>
            </div>
        </footer>
    </div>

    <div class="success-message" id="successMessage">
        <i class="fas fa-check-circle"></i> The Code has Completed Successfully.
    </div>

    <script>
        // 学生名单
        const boys = [
            "", "张逸轩", "张庐焜", "黄月童", "吴弘宇", "张涵睿", "余浩玮", "许正涛",
            "王若鸿", "张炜承", "郭辰睿", "闻泽", "高竟翔", "吴进宇", "章津跃", "辛伯辰",
            "昌靖茗", "高伟宸", "柯源", "徐浩中", "王海骁", "张欣成", "范洪鑫", "杨颜旗",
            "李元昊", "刘柯汉", "章横溢", "陈思友", "李浚玮", "李承志", "孙家腾", "李辰熙"
        ];
        
        const girls = [
            "", "毕思妍", "万金慧", "王泽予", "闫可欣", "袁灏亓", "王璟瑜", "周依冉",
            "魏可晗", "陈晓希", "汪嘉彦", "沈傲然", "刘洋东", "余正月", "王泺辰", "杨渃馨",
            "余正秋", "张瀛嘉", "汪悦桐", "陈雨谦", "孙天佑", "黄焱熔", "肖雅祺", "常昕妤"
        ];
        
        // Fisher-Yates 洗牌算法
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }
        
        // 生成固定宽度的字符串
        function setw(text, width) {
            let str = text.toString();
            while (str.length < width) {
                str = ' ' + str;
            }
            return str;
        }
        
        // 显示成功消息
        function showSuccessMessage() {
            const message = document.getElementById('successMessage');
            message.classList.add('show');
            setTimeout(() => {
                message.classList.remove('show');
            }, 3000);
        }
        
        // 切换标签页
        function switchTab(tabName) {
            // 移除所有标签页的active类
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // 激活选中的标签页
            document.getElementById(`${tabName}-tab`).classList.add('active');
            event.target.classList.add('active');
        }
        
        // 判断学生是否为男生
        function isBoy(name) {
            return boys.includes(name);
        }
        
        // 创建单个桌子元素
        function createDesk(student1, student2) {
            const desk = document.createElement('div');
            desk.className = 'desk';
            
            const student1Elem = document.createElement('div');
            student1Elem.className = `student ${isBoy(student1) ? 'boy' : 'girl'}`;
            student1Elem.textContent = student1;
            
            const student2Elem = document.createElement('div');
            student2Elem.className = `student ${isBoy(student2) ? 'boy' : 'girl'}`;
            student2Elem.textContent = student2;
            
            desk.appendChild(student1Elem);
            desk.appendChild(student2Elem);
            
            return desk;
        }
        
        // 生成座位表
        function generateSeats() {
            const output = document.getElementById('output');
            const seatingPlan = document.getElementById('seatingPlan');
            const loading = document.getElementById('loading');
            
            // 显示加载动画
            loading.style.display = 'block';
            output.textContent = 'Seats are being allocated. Please wait a moment...';
            
            setTimeout(() => {
                let outputText = '';
                
                // 创建卡片数组
                let cardboy = Array.from({length: 31}, (_, i) => i + 1);
                let cardgirl = Array.from({length: 23}, (_, i) => i + 1);
                
                // 随机打乱
                shuffleArray(cardboy);
                shuffleArray(cardgirl);
                
                // 清空可视化座位表
                seatingPlan.innerHTML = '';
                
                // 生成座位表
                for (let i = 1; i <= 27; i += 4) {
                    let line = '| ';
                    const row = document.createElement('div');
                    row.className = 'row';
                    
                    if (i < 21) {
                        if (Math.floor(i / 4) % 2 === 1) {
                            for (let j = 0; j < 4; j++) {
                                line += setw(boys[cardboy[i + j - 1]], 4) + ' ' + 
                                        setw(girls[cardgirl[i + j - 1]], 4) + ' | ';
                                
                                const desk = createDesk(
                                    boys[cardboy[i + j - 1]], 
                                    girls[cardgirl[i + j - 1]]
                                );
                                row.appendChild(desk);
                            }
                        } else {
                            for (let j = 0; j < 4; j++) {
                                line += setw(girls[cardgirl[i + j - 1]], 4) + ' ' + 
                                        setw(boys[cardboy[i + j - 1]], 4) + ' | ';
                                
                                const desk = createDesk(
                                    girls[cardgirl[i + j - 1]], 
                                    boys[cardboy[i + j - 1]]
                                );
                                row.appendChild(desk);
                            }
                        }
                    } else if (i === 21) {
                        for (let j = 0; j < 3; j++) {
                            line += setw(boys[cardboy[i + j - 1]], 4) + ' ' + 
                                    setw(girls[cardgirl[i + j - 1]], 4) + ' | ';
                            
                            const desk = createDesk(
                                boys[cardboy[i + j - 1]], 
                                girls[cardgirl[i + j - 1]]
                            );
                            row.appendChild(desk);
                        }
                        line += setw(boys[cardboy[i + 3 - 1]], 4) + ' ' + 
                                setw(boys[cardboy[i + 7 - 1]], 4) + ' | ';
                        
                        const desk = createDesk(
                            boys[cardboy[i + 3 - 1]], 
                            boys[cardboy[i + 7 - 1]]
                        );
                        row.appendChild(desk);
                    } else {
                        for (let j = 0; j < 3; j++) {
                            line += setw(boys[cardboy[i + j - 1]], 4) + ' ' + 
                                    setw(boys[cardboy[i + j + 4 - 1]], 4) + ' | ';
                            
                            const desk = createDesk(
                                boys[cardboy[i + j - 1]], 
                                boys[cardboy[i + j + 4 - 1]]
                            );
                            row.appendChild(desk);
                        }
                    }
                    
                    outputText += line + '\n';
                    seatingPlan.appendChild(row);
                }
                
                // 设置输出
                output.textContent = outputText;
                loading.style.display = 'none';
                
                // 显示成功消息
                showSuccessMessage();
                
            }, 1500);
        }
        
        // 重置输出
        function resetOutput() {
            document.getElementById('output').textContent = 'Welcome to use the intelligent seat allocation system.\nClick the button above to start generating a random seating chart.\nThis system ensures the randomness and fairness of seat allocation, with a 3.2% probability of each person being assigned.';
            document.getElementById('seatingPlan').innerHTML = '<div style="text-align: center; padding: 40px; color: #7f8c8d; font-size: 1.2rem;">Click the "Generate Random Seating Chart" button to start seat allocation.</div>';
        }
        
        // 页面加载时显示初始信息
        window.addEventListener('DOMContentLoaded', () => {
            console.log('The intelligent seat allocation system has been loaded.');
        });
    </script>
</body>
</html>
