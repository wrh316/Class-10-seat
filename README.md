<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>八年级十班座位随机分配系统</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #333;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            padding: 30px;
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
            background: linear-gradient(90deg, #ff6b6b, #4ecdc4, #45b7d1, #96ceb4);
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 2px dashed #eaeaea;
        }
        
        h1 {
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }
        
        .subtitle {
            color: #7f8c8d;
            font-size: 1.2rem;
            font-weight: 300;
        }
        
        .control-panel {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }
        
        button {
            padding: 14px 28px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            position: relative;
            overflow: hidden;
        }
        
        button::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transition: 0.5s;
        }
        
        button:hover::before {
            left: 100%;
        }
        
        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
        }
        
        button:active {
            transform: translateY(-1px);
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
        
        .info-panel {
            margin-top: 40px;
            padding: 25px;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border-radius: 12px;
            border-left: 5px solid #667eea;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
        }
        
        .info-panel h3 {
            margin-bottom: 15px;
            color: #2c3e50;
            font-size: 1.4rem;
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            text-align: center;
            transition: all 0.3s ease;
            border-top: 4px solid #667eea;
        }
        
        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
        }
        
        .stat-card h4 {
            color: #7f8c8d;
            margin-bottom: 10px;
            font-size: 1rem;
        }
        
        .stat-card p {
            font-size: 2rem;
            font-weight: bold;
            color: #2c3e50;
        }
        
        footer {
            margin-top: 50px;
            text-align: center;
            color: #7f8c8d;
            font-size: 1rem;
            padding-top: 25px;
            border-top: 2px dashed #eaeaea;
        }
        
        .output-console {
            background: #2c3e50;
            color: #ecf0f1;
            padding: 20px;
            border-radius: 10px;
            margin-top: 30px;
            font-family: 'Courier New', monospace;
            white-space: pre-wrap;
            box-shadow: inset 0 0 10px rgba(0,0,0,0.5);
            max-height: 400px;
            overflow-y: auto;
        }
        
        @media (max-width: 768px) {
            .desk {
                width: 160px;
                height: 75px;
                padding: 8px;
            }
            
            .student {
                font-size: 0.85rem;
            }
            
            .teacher-desk {
                width: 280px;
                font-size: 1.1rem;
            }
            
            h1 {
                font-size: 2rem;
            }
        }
        
        @media (max-width: 480px) {
            .desk {
                width: 140px;
                height: 65px;
            }
            
            .student {
                font-size: 0.75rem;
            }
            
            .teacher-desk {
                width: 220px;
                font-size: 1rem;
            }
            
            button {
                padding: 12px 20px;
                font-size: 1rem;
            }
            
            .row {
                gap: 10px;
            }
        }
        
        .loading {
            display: none;
            text-align: center;
            padding: 20px;
            color: #667eea;
            font-size: 1.2rem;
        }
        
        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #667eea;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>八年级十班座位随机分配系统</h1>
            <p class="subtitle">基于原C++程序实现的Web版本 - 完全相同的分配逻辑</p>
        </header>
        
        <div class="control-panel">
            <button id="generateBtn">🎲 生成随机座位表</button>
            <button id="consoleBtn">📋 显示控制台输出</button>
            <button id="resetBtn">🔄 重置系统</button>
        </div>
        
        <div class="loading" id="loading">
            <div class="spinner"></div>
            正在随机分配座位中...
        </div>
        
        <div class="classroom">
            <div class="teacher-desk">讲 台</div>
            <div class="rows" id="seatingPlan">
                <div style="text-align: center; padding: 40px; color: #7f8c8d; font-size: 1.2rem;">
                    点击"生成随机座位表"按钮开始分配座位
                </div>
            </div>
        </div>
        
        <div class="output-console" id="consoleOutput" style="display: none;">
            <!-- 控制台输出将在这里显示 -->
        </div>
        
        <div class="info-panel">
            <h3>📊 班级信息统计</h3>
            <p>本系统完全按照原C++程序的逻辑实现，确保座位分配的随机性和公平性。</p>
            
            <div class="stats">
                <div class="stat-card">
                    <h4>👦 男生人数</h4>
                    <p>31</p>
                </div>
                <div class="stat-card">
                    <h4>👧 女生人数</h4>
                    <p>23</p>
                </div>
                <div class="stat-card">
                    <h4>👥 总人数</h4>
                    <p>54</p>
                </div>
                <div class="stat-card">
                    <h4>💺 座位数</h4>
                    <p>27</p>
                </div>
            </div>
        </div>
        
        <footer>
            <p>© 2025 八年级十班座位分配系统 | 原程序作者: wrh316 | Web版本开发</p>
            <p style="margin-top: 10px; font-size: 0.9rem; color: #95a5a6;">
                版本 1.0 | 最后更新: 2025.9.28
            </p>
        </footer>
    </div>

    <script>
        // 学生名单数据 - 完全按照原C++程序
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
        
        // 获取DOM元素
        const generateBtn = document.getElementById('generateBtn');
        const consoleBtn = document.getElementById('consoleBtn');
        const resetBtn = document.getElementById('resetBtn');
        const seatingPlan = document.getElementById('seatingPlan');
        const consoleOutput = document.getElementById('consoleOutput');
        const loading = document.getElementById('loading');
        
        // Fisher-Yates 洗牌算法
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }
        
        // 生成座位表
        function generateSeatingPlan() {
            loading.style.display = 'block';
            
            // 模拟加载延迟
            setTimeout(() => {
                seatingPlan.innerHTML = '';
                let consoleText = '';
                
                // 创建男生和女生的卡片数组
                let boyCards = Array.from({length: 31}, (_, i) => i + 1);
                let girlCards = Array.from({length: 23}, (_, i) => i + 1);
                
                // 随机打乱数组 - 使用时间作为随机种子
                shuffleArray(boyCards);
                shuffleArray(girlCards);
                
                // 生成座位表 - 完全按照C++程序的逻辑
                for (let i = 1; i <= 27; i += 4) {
                    const row = document.createElement('div');
                    row.className = 'row';
                    let rowText = '| ';
                    
                    if (i < 21) {
                        // 前5行：每行4个桌子，根据行号决定男女顺序
                        if (Math.floor(i / 4) % 2 === 1) {
                            for (let j = 0; j < 4; j++) {
                                const desk = createDesk(
                                    boys[boyCards[i + j - 1]], 
                                    girls[girlCards[i + j - 1]]
                                );
                                row.appendChild(desk);
                                rowText += `${boys[boyCards[i + j - 1]]} ${girls[girlCards[i + j - 1]]} | `;
                            }
                        } else {
                            for (let j = 0; j < 4; j++) {
                                const desk = createDesk(
                                    girls[girlCards[i + j - 1]], 
                                    boys[boyCards[i + j - 1]]
                                );
                                row.appendChild(desk);
                                rowText += `${girls[girlCards[i + j - 1]]} ${boys[boyCards[i + j - 1]]} | `;
                            }
                        }
                    } else if (i === 21) {
                        // 第6行：3个男女混合桌 + 1个男生双人桌
                        for (let j = 0; j < 3; j++) {
                            const desk = createDesk(
                                boys[boyCards[i + j - 1]], 
                                girls[girlCards[i + j - 1]]
                            );
                            row.appendChild(desk);
                            rowText += `${boys[boyCards[i + j - 1]]} ${girls[girlCards[i + j - 1]]} | `;
                        }
                        
                        const desk = createDesk(
                            boys[boyCards[i + 3 - 1]], 
                            boys[boyCards[i + 7 - 1]]
                        );
                        row.appendChild(desk);
                        rowText += `${boys[boyCards[i + 3 - 1]]} ${boys[boyCards[i + 7 - 1]]} | `;
                    } else {
                        // 第7行：3个男生双人桌
                        for (let j = 0; j < 3; j++) {
                            const desk = createDesk(
                                boys[boyCards[i + j - 1]], 
                                boys[boyCards[i + j + 4 - 1]]
                            );
                            row.appendChild(desk);
                            rowText += `${boys[boyCards[i + j - 1]]} ${boys[boyCards[i + j + 4 - 1]]} | `;
                        }
                    }
                    
                    seatingPlan.appendChild(row);
                    consoleText += rowText + '\n';
                }
                
                consoleText += '讲 台\n';
                consoleOutput.textContent = consoleText;
                loading.style.display = 'none';
                
            }, 800); // 800ms延迟模拟加载
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
        
        // 判断学生是否为男生
        function isBoy(name) {
            return boys.includes(name);
        }
        
        // 显示/隐藏控制台输出
        function toggleConsole() {
            if (consoleOutput.style.display === 'none') {
                consoleOutput.style.display = 'block';
                consoleBtn.textContent = '📋 隐藏控制台输出';
            } else {
                consoleOutput.style.display = 'none';
                consoleBtn.textContent = '📋 显示控制台输出';
            }
        }
        
        // 重置系统
        function resetSystem() {
            seatingPlan.innerHTML = '<div style="text-align: center; padding: 40px; color: #7f8c8d; font-size: 1.2rem;">点击"生成随机座位表"按钮开始分配座位</div>';
            consoleOutput.style.display = 'none';
            consoleBtn.textContent = '📋 显示控制台输出';
            consoleOutput.textContent = '';
        }
        
        // 事件监听
        generateBtn.addEventListener('click', generateSeatingPlan);
        consoleBtn.addEventListener('click', toggleConsole);
        resetBtn.addEventListener('click', resetSystem);
        
        // 页面加载时显示一些信息
        window.addEventListener('DOMContentLoaded', () => {
            console.log('八年级十班座位分配系统已加载');
            console.log(`男生人数: ${boys.length - 1}, 女生人数: ${girls.length - 1}`);
        });
    </script>
</body>
</html>
