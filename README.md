<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Class 10's Seat Random Number Program</title>
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
            --bg-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --card-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            --hover-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
        }
        
        /* 深色主题变量 */
        .dark-theme {
            --primary: #5b6bf0;
            --secondary: #4c1d95;
            --accent: #60d9f0;
            --success: #5ae68a;
            --warning: #f7b955;
            --danger: #f87171;
            --light: #1e293b;
            --dark: #f1f5f9;
            --gray: #94a3b8;
            --bg-gradient: linear-gradient(135deg, #1e293b 0%, #334155 100%);
            --card-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            --hover-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
        }
        
        body {
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
            background: var(--bg-gradient);
            color: var(--dark);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            line-height: 1.6;
            transition: all 0.3s ease;
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
            animation: fadeIn 0.8s ease-out;
            transition: all 0.3s ease;
        }
        
        .dark-theme .container {
            background: rgba(30, 41, 59, 0.95);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
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
            animation: floating 3s ease-in-out infinite;
        }
        
        @keyframes floating {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
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
            box-shadow: var(--card-shadow);
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
            box-shadow: var(--hover-shadow);
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
            transition: all 0.3s ease;
        }
        
        .dark-theme .output-section {
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .output-section:hover {
            box-shadow: 
                inset 0 2px 4px rgba(0, 0, 0, 0.05),
                0 6px 25px rgba(0, 0, 0, 0.12);
        }
        
        .output-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid rgba(0, 0, 0, 0.1);
        }
        
        .dark-theme .output-header {
            border-bottom: 2px solid rgba(255, 255, 255, 0.1);
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
            transition: all 0.3s ease;
        }
        
        .dark-theme .output-container {
            background: #0f172a;
            border: 2px solid #475569;
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
            transition: all 0.3s ease;
        }
        
        .teacher-desk:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.2);
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
            box-shadow: var(--card-shadow);
            transition: all 0.3s ease;
            position: relative;
            animation: deskAppear 0.5s ease-out;
        }
        
        @keyframes deskAppear {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
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
            box-shadow: var(--hover-shadow);
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
            animation: studentAppear 0.5s ease-out;
        }
        
        @keyframes studentAppear {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
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
            box-shadow: var(--card-shadow);
            border: 1px solid rgba(255, 255, 255, 0.5);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            animation: fadeIn 0.6s ease-out;
        }
        
        .dark-theme .stat-card {
            background: linear-gradient(135deg, #1e293b, #334155);
            border: 1px solid rgba(255, 255, 255, 0.1);
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
            box-shadow: var(--hover-shadow);
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
        
        .dark-theme footer {
            border-top: 1px solid rgba(255, 255, 255, 0.1);
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
        
        .dark-theme .version {
            background: #334155;
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
            display: flex;
            align-items: center;
            gap: 10px;
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
        
        .dark-theme .tab-btn {
            background: #334155;
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
        
        /* 粒子背景效果 */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            overflow: hidden;
        }
        
        .particle {
            position: absolute;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            animation: float 15s infinite linear;
        }
        
        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
        }
        
        /* 个性化元素：班级徽章 */
        .class-badge {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #ffd700, #ffa500);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 5px 15px rgba(255, 165, 0, 0.3);
            animation: rotate 10s linear infinite;
        }
        
        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .class-badge i {
            font-size: 1.5rem;
            color: white;
        }
        
        /* 个性化元素：装饰性边框 */
        .decorative-border {
            position: absolute;
            top: 10px;
            left: 10px;
            right: 10px;
            bottom: 10px;
            border: 2px dashed rgba(67, 97, 238, 0.2);
            border-radius: 20px;
            pointer-events: none;
        }
        
        /* 个性化元素：动态背景图案 */
        .bg-pattern {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(67, 97, 238, 0.05) 0%, transparent 20%),
                radial-gradient(circle at 90% 80%, rgba(76, 201, 240, 0.05) 0%, transparent 20%),
                radial-gradient(circle at 50% 50%, rgba(74, 222, 128, 0.05) 0%, transparent 30%);
            z-index: -1;
        }
        
        /* 个性化元素：标题装饰 */
        .title-decoration {
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 4px;
            background: linear-gradient(90deg, transparent, var(--primary), transparent);
            border-radius: 2px;
        }
        
        /* 个性化元素：座位编号 */
        .desk-number {
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--primary);
            color: white;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
            font-weight: bold;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }
        
        /* 新增个性化元素：装饰性星星 */
        .decoration-star {
            position: absolute;
            color: rgba(255, 255, 255, 0.7);
            font-size: 1.2rem;
            animation: twinkle 3s infinite alternate;
        }
        
        @keyframes twinkle {
            0% { opacity: 0.3; transform: scale(0.8); }
            100% { opacity: 1; transform: scale(1.2); }
        }
        
        /* 新增个性化元素：时间显示 */
        .time-display {
            position: absolute;
            top: 20px;
            left: 20px;
            background: rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(10px);
            padding: 10px 15px;
            border-radius: 10px;
            font-size: 0.9rem;
            color: var(--dark);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        
        .dark-theme .time-display {
            background: rgba(30, 41, 59, 0.5);
            color: var(--dark);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        /* 新增个性化元素：班级标语 */
        .class-motto {
            text-align: center;
            margin-top: 10px;
            font-style: italic;
            color: var(--gray);
            font-size: 1rem;
            position: relative;
            padding: 0 20px;
        }
        
        .class-motto::before,
        .class-motto::after {
            content: '"';
            font-size: 1.5rem;
            color: var(--primary);
            position: absolute;
            top: -5px;
        }
        
        .class-motto::before {
            left: 0;
        }
        
        .class-motto::after {
            right: 0;
        }
        
        /* 新增个性化元素：进度条 */
        .progress-bar {
            height: 6px;
            background: rgba(67, 97, 238, 0.2);
            border-radius: 3px;
            overflow: hidden;
            margin-top: 15px;
            display: none;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--primary), var(--accent));
            width: 0%;
            transition: width 0.5s ease;
            border-radius: 3px;
        }
        
        /* 新增个性化元素：学生卡片翻转效果 */
        .student-card {
            perspective: 1000px;
            width: 48%;
        }
        
        .student-inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.6s;
            transform-style: preserve-3d;
        }
        
        .student-card:hover .student-inner {
            transform: rotateY(180deg);
        }
        
        .student-front, .student-back {
            position: absolute;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
            padding: 5px;
        }
        
        .student-front {
            color: white;
        }
        
        .student-back {
            background: linear-gradient(135deg, #f8fafc, #e2e8f0);
            color: var(--dark);
            transform: rotateY(180deg);
            font-size: 0.8rem;
        }
        
        .dark-theme .student-back {
            background: linear-gradient(135deg, #334155, #475569);
        }
        
        /* 新增个性化元素：教室背景 */
        .classroom-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                linear-gradient(90deg, transparent 49%, rgba(0,0,0,0.05) 50%, transparent 51%),
                linear-gradient(transparent 49%, rgba(0,0,0,0.05) 50%, transparent 51%);
            background-size: 50px 50px;
            opacity: 0.1;
            z-index: -1;
        }
        
        /* 新功能样式 */
        .top-controls {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .search-box {
            display: flex;
            align-items: center;
            background: var(--light);
            border-radius: 50px;
            padding: 10px 20px;
            box-shadow: var(--card-shadow);
            border: 1px solid rgba(255, 255, 255, 0.5);
            transition: all 0.3s ease;
        }
        
        .dark-theme .search-box {
            background: #334155;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .search-box:focus-within {
            box-shadow: var(--hover-shadow);
            transform: translateY(-2px);
        }
        
        .search-box input {
            border: none;
            background: transparent;
            padding: 8px 12px;
            font-size: 1rem;
            color: var(--dark);
            width: 200px;
            outline: none;
        }
        
        .search-box i {
            color: var(--gray);
        }
        
        .theme-toggle {
            display: flex;
            align-items: center;
            gap: 10px;
            background: var(--light);
            border-radius: 50px;
            padding: 10px 20px;
            box-shadow: var(--card-shadow);
            border: 1px solid rgba(255, 255, 255, 0.5);
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .dark-theme .theme-toggle {
            background: #334155;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .theme-toggle:hover {
            transform: translateY(-2px);
            box-shadow: var(--hover-shadow);
        }
        
        .theme-toggle i {
            color: var(--primary);
        }
        
        .history-panel {
            margin-top: 30px;
            background: var(--light);
            border-radius: 20px;
            padding: 25px;
            box-shadow: var(--card-shadow);
            border: 1px solid rgba(255, 255, 255, 0.5);
            display: none;
        }
        
        .dark-theme .history-panel {
            background: #1e293b;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .history-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid rgba(0, 0, 0, 0.1);
        }
        
        .dark-theme .history-header {
            border-bottom: 2px solid rgba(255, 255, 255, 0.1);
        }
        
        .history-title {
            font-size: 1.4rem;
            font-weight: 600;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .history-list {
            max-height: 300px;
            overflow-y: auto;
            padding-right: 10px;
        }
        
        .history-item {
            background: white;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            border-left: 4px solid var(--primary);
            transition: all 0.3s ease;
        }
        
        .dark-theme .history-item {
            background: #334155;
        }
        
        .history-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
        }
        
        .history-item-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
            font-weight: 600;
            color: var(--dark);
        }
        
        .history-item-content {
            font-family: 'Fira Code', 'Cascadia Code', 'Courier New', monospace;
            white-space: pre;
            overflow-x: auto;
            background: #f8fafc;
            padding: 12px;
            border-radius: 8px;
            font-size: 0.9rem;
            color: #1e293b;
        }
        
        .dark-theme .history-item-content {
            background: #0f172a;
            color: #e2e8f0;
        }
        
        .settings-panel {
            margin-top: 30px;
            background: var(--light);
            border-radius: 20px;
            padding: 25px;
            box-shadow: var(--card-shadow);
            border: 1px solid rgba(255, 255, 255, 0.5);
            display: none;
        }
        
        .dark-theme .settings-panel {
            background: #1e293b;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .settings-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid rgba(0, 0, 0, 0.1);
        }
        
        .dark-theme .settings-header {
            border-bottom: 2px solid rgba(255, 255, 255, 0.1);
        }
        
        .settings-title {
            font-size: 1.4rem;
            font-weight: 600;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .setting-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid rgba(0, 0, 0, 0.05);
        }
        
        .dark-theme .setting-item {
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
        }
        
        .setting-item:last-child {
            border-bottom: none;
        }
        
        .setting-label {
            font-weight: 500;
            color: var(--dark);
        }
        
        .setting-description {
            font-size: 0.9rem;
            color: var(--gray);
            margin-top: 5px;
        }
        
        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 24px;
        }
        
        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }
        
        .toggle-slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 24px;
        }
        
        .toggle-slider:before {
            position: absolute;
            content: "";
            height: 16px;
            width: 16px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }
        
        input:checked + .toggle-slider {
            background-color: var(--primary);
        }
        
        input:checked + .toggle-slider:before {
            transform: translateX(26px);
        }
        
        .highlight {
            background-color: rgba(255, 255, 0, 0.3);
            border-radius: 4px;
            padding: 2px 4px;
        }
        
        .student-result {
            margin-top: 20px;
            padding: 15px;
            background: var(--light);
            border-radius: 12px;
            box-shadow: var(--card-shadow);
            display: none;
        }
        
        .dark-theme .student-result {
            background: #1e293b;
        }
        
        .student-result-header {
            font-weight: 600;
            margin-bottom: 10px;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .student-details {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
        }
        
        .student-info {
            flex: 1;
            min-width: 200px;
        }
        
        .student-info p {
            margin-bottom: 8px;
            display: flex;
            justify-content: space-between;
        }
        
        .student-info span:first-child {
            font-weight: 500;
            color: var(--gray);
        }
        
        .student-info span:last-child {
            font-weight: 600;
            color: var(--dark);
        }
        
        .seat-info {
            background: var(--primary);
            color: white;
            padding: 8px 12px;
            border-radius: 8px;
            margin-top: 10px;
            font-weight: 500;
        }
        
        .student-seat-info {
            margin-top: 15px;
            padding: 15px;
            background: var(--light);
            border-radius: 12px;
            box-shadow: var(--card-shadow);
        }
        
        .dark-theme .student-seat-info {
            background: #1e293b;
        }
        
        .seat-position {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 10px;
        }
        
        .seat-position i {
            color: var(--primary);
        }
    </style>
</head>
<body>
    <!-- 粒子背景 -->
    <div class="particles" id="particles"></div>
    
    <!-- 动态背景图案 -->
    <div class="bg-pattern"></div>
    
    <!-- 装饰性星星 -->
    <div class="decoration-star" style="top: 10%; left: 5%;"><i class="fas fa-star"></i></div>
    <div class="decoration-star" style="top: 15%; right: 10%;"><i class="fas fa-star"></i></div>
    <div class="decoration-star" style="bottom: 20%; left: 15%;"><i class="fas fa-star"></i></div>
    <div class="decoration-star" style="bottom: 10%; right: 5%;"><i class="fas fa-star"></i></div>
    
    <div class="container">
        <!-- 时间显示 -->
        <div class="time-display" id="timeDisplay"></div>
        
        <!-- 班级徽章 -->
        <div class="class-badge">
            <i class="fas fa-graduation-cap"></i>
        </div>
        
        <!-- 装饰性边框 -->
        <div class="decorative-border"></div>
        
        <header>
            <div class="logo">
                <i class="fas fa-chalkboard-teacher"></i>
            </div>
            <h1>Class 10, Grade 2024</h1>
            <p class="subtitle">Seat Random Number Program</p>
            <div class="class-motto">十全十美，十班无畏，十战十胜，勇夺金杯。</div>
            <div class="title-decoration"></div>
        </header>
        
        <!-- 顶部控制栏 -->
        <div class="top-controls">
            <div class="search-box">
                <i class="fas fa-search"></i>
                <input type="text" id="searchInput" placeholder="Search for a student...">
            </div>
            <div class="theme-toggle" id="themeToggle">
                <i class="fas fa-moon"></i>
                <span>Dark Mode</span>
            </div>
        </div>
        
        <div class="control-panel">
            <button class="btn btn-primary" onclick="generateSeats()">
                <i class="fas fa-random"></i>
                🎲 Generate Random Seating Chart
            </button>
            <button class="btn btn-secondary" onclick="resetOutput()">
                <i class="fas fa-redo"></i>
                🔄 Reset System
            </button>
            <button class="btn btn-secondary" onclick="toggleHistory()">
                <i class="fas fa-history"></i>
                History
            </button>
            <button class="btn btn-secondary" onclick="toggleSettings()">
                <i class="fas fa-cog"></i>
                Settings
            </button>
        </div>
        
        <!-- 搜索结果 -->
        <div class="student-result" id="studentResult">
            <div class="student-result-header">
                <i class="fas fa-user-graduate"></i>
                Student Search Result
            </div>
            <div class="student-details" id="studentDetails">
                <!-- 搜索结果将在这里显示 -->
            </div>
        </div>
        
        <!-- 进度条 -->
        <div class="progress-bar" id="progressBar">
            <div class="progress-fill" id="progressFill"></div>
        </div>
        
        <div class="loading" id="loading">
            <div class="spinner"></div>
            <p>Seats are being randomly assigned...</p>
        </div>
        
        <div class="output-section">
            <div class="output-header">
                <div class="output-title">
                    <i class="fas fa-table"></i>
                    Seat Allocation Result
                </div>
                <div class="tab-buttons">
                    <button class="tab-btn active" onclick="switchTab('console')">Console View</button>
                    <button class="tab-btn" onclick="switchTab('visual')">Visual View</button>
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
                    <div class="classroom-bg"></div>
                    <div class="teacher-desk" id="teacherDesk">
                        <i class="fas fa-chalkboard"></i> Teacher's Desk
                    </div>
                    <div class="rows" id="seatingPlan">
                        <div style="text-align: center; padding: 40px; color: #7f8c8d; font-size: 1.2rem;">
                            Click the "Generate Random Seating Chart" button to start seat allocation.
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 历史记录面板 -->
        <div class="history-panel" id="historyPanel">
            <div class="history-header">
                <div class="history-title">
                    <i class="fas fa-history"></i>
                    Generation History
                </div>
                <button class="btn btn-secondary" onclick="clearHistory()">
                    <i class="fas fa-trash"></i>
                    Clear History
                </button>
            </div>
            <div class="history-list" id="historyList">
                <!-- 历史记录将在这里显示 -->
            </div>
        </div>
        
        <!-- 设置面板 -->
        <div class="settings-panel" id="settingsPanel">
            <div class="settings-header">
                <div class="settings-title">
                    <i class="fas fa-cog"></i>
                    System Settings
                </div>
                <button class="btn btn-secondary" onclick="toggleSettings()">
                    <i class="fas fa-times"></i>
                    Close
                </button>
            </div>
            <div class="settings-content">
                <div class="setting-item">
                    <div>
                        <div class="setting-label">Auto-save History</div>
                        <div class="setting-description">Automatically save each generation to history</div>
                    </div>
                    <label class="toggle-switch">
                        <input type="checkbox" id="autoSave" checked>
                        <span class="toggle-slider"></span>
                    </label>
                </div>
                <div class="setting-item">
                    <div>
                        <div class="setting-label">Show Animation Effects</div>
                        <div class="setting-description">Enable animations for a better user experience</div>
                    </div>
                    <label class="toggle-switch">
                        <input type="checkbox" id="showAnimations" checked>
                        <span class="toggle-slider"></span>
                    </label>
                </div>
                <div class="setting-item">
                    <div>
                        <div class="setting-label">Highlight Search Results</div>
                        <div class="setting-description">Highlight found students in the seating chart</div>
                    </div>
                    <label class="toggle-switch">
                        <input type="checkbox" id="highlightResults" checked>
                        <span class="toggle-slider"></span>
                    </label>
                </div>
            </div>
        </div>
        
        <div class="stats-grid">
            <div class="stat-card stat-boy">
                <div class="stat-icon">
                    <i class="fas fa-male"></i>
                </div>
                <h3>Boy Count</h3>
                <div class="number">31</div>
            </div>
            <div class="stat-card stat-girl">
                <div class="stat-icon">
                    <i class="fas fa-female"></i>
                </div>
                <h3>Girl Count</h3>
                <div class="number">23</div>
            </div>
            <div class="stat-card stat-total">
                <div class="stat-icon">
                    <i class="fas fa-users"></i>
                </div>
                <h3>All Count</h3>
                <div class="number">54</div>
            </div>
            <div class="stat-card stat-seat">
                <div class="stat-icon">
                    <i class="fas fa-chair"></i>
                </div>
                <h3>Seat Count</h3>
                <div class="number">27</div>
            </div>
        </div>
        
        <footer>
            <div class="footer-content">
                <div>
                    <p>© 2025 Class 10's Seat Random Number Program | Author by @wrh316 | Website</p>
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
        <i class="fas fa-check-circle"></i> The Code has Completed Successfully
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
        
        // 全局变量
        let currentSeating = null;
        let history = JSON.parse(localStorage.getItem('seatHistory')) || [];
        let isDarkTheme = localStorage.getItem('darkTheme') === 'true';
        
        // 初始化主题
        if (isDarkTheme) {
            document.body.classList.add('dark-theme');
            document.getElementById('themeToggle').innerHTML = '<i class="fas fa-sun"></i><span>Light Mode</span>';
        }
        
        // 创建粒子背景
        function createParticles() {
            const particlesContainer = document.getElementById('particles');
            const particleCount = 30;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.classList.add('particle');
                
                // 随机大小
                const size = Math.random() * 10 + 5;
                particle.style.width = `${size}px`;
                particle.style.height = `${size}px`;
                
                // 随机位置
                particle.style.left = `${Math.random() * 100}%`;
                
                // 随机动画延迟
                particle.style.animationDelay = `${Math.random() * 15}s`;
                
                // 随机动画时长
                const duration = Math.random() * 10 + 10;
                particle.style.animationDuration = `${duration}s`;
                
                particlesContainer.appendChild(particle);
            }
        }
        
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
        
        // 更新时钟显示
        function updateClock() {
            const now = new Date();
            const timeString = now.toLocaleString('zh-CN', {
                year: 'numeric',
                month: '2-digit',
                day: '2-digit',
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit',
                weekday: 'long'
            });
            document.getElementById('timeDisplay').textContent = timeString;
        }
        
        function createDesk(student1, student2, deskNumber) {
            const desk = document.createElement('div');
            desk.className = 'desk';
            
            // 添加座位编号
            const deskNumberElem = document.createElement('div');
            deskNumberElem.className = 'desk-number';
            deskNumberElem.textContent = deskNumber;
            desk.appendChild(deskNumberElem);
            
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
            const progressBar = document.getElementById('progressBar');
            const progressFill = document.getElementById('progressFill');
            
            // 显示加载动画和进度条
            loading.style.display = 'block';
            progressBar.style.display = 'block';
            output.textContent = 'Seats are being allocated. Please wait a moment...';
            
            // 模拟进度条
            let progress = 0;
            const progressInterval = setInterval(() => {
                progress += 5;
                progressFill.style.width = `${progress}%`;
                if (progress >= 100) {
                    clearInterval(progressInterval);
                }
            }, 100);
            
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
                
                // 存储当前座位分配
                currentSeating = {
                    boys: [...cardboy],
                    girls: [...cardgirl],
                    timestamp: new Date().toISOString()
                };
                
                // 生成座位表
                let deskCounter = 1;
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
                                    girls[cardgirl[i + j - 1]],
                                    deskCounter++
                                );
                                row.appendChild(desk);
                            }
                        } else {
                            for (let j = 0; j < 4; j++) {
                                line += setw(girls[cardgirl[i + j - 1]], 4) + ' ' + 
                                        setw(boys[cardboy[i + j - 1]], 4) + ' | ';
                                
                                const desk = createDesk(
                                    girls[cardgirl[i + j - 1]], 
                                    boys[cardboy[i + j - 1]],
                                    deskCounter++
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
                                girls[cardgirl[i + j - 1]],
                                deskCounter++
                            );
                            row.appendChild(desk);
                        }
                        line += setw(boys[cardboy[i + 3 - 1]], 4) + ' ' + 
                                setw(boys[cardboy[i + 7 - 1]], 4) + ' | ';
                        
                        const desk = createDesk(
                            boys[cardboy[i + 3 - 1]], 
                            boys[cardboy[i + 7 - 1]],
                            deskCounter++
                        );
                        row.appendChild(desk);
                    } else {
                        for (let j = 0; j < 3; j++) {
                            line += setw(boys[cardboy[i + j - 1]], 4) + ' ' + 
                                    setw(boys[cardboy[i + j + 4 - 1]], 4) + ' | ';
                            
                            const desk = createDesk(
                                boys[cardboy[i + j - 1]], 
                                boys[cardboy[i + j + 4 - 1]],
                                deskCounter++
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
                progressBar.style.display = 'none';
                progressFill.style.width = '0%';
                
                // 保存到历史记录
                if (document.getElementById('autoSave').checked) {
                    saveToHistory(outputText);
                }
                
                // 显示成功消息
                showSuccessMessage();
                
            }, 1500);
        }
        
        // 重置输出
        function resetOutput() {
            document.getElementById('output').textContent = 'Welcome to use the intelligent seat allocation system.\nClick the button above to start generating a random seating chart.\nThis system ensures the randomness and fairness of seat allocation, with a 3.2% probability of each person being assigned.';
            document.getElementById('seatingPlan').innerHTML = '<div style="text-align: center; padding: 40px; color: #7f8c8d; font-size: 1.2rem;">Click the "Generate Random Seating Chart" button to start seat allocation.</div>';
            document.getElementById('studentResult').style.display = 'none';
            currentSeating = null;
        }
        
        // 切换主题
        function toggleTheme() {
            isDarkTheme = !isDarkTheme;
            document.body.classList.toggle('dark-theme');
            
            const themeToggle = document.getElementById('themeToggle');
            if (isDarkTheme) {
                themeToggle.innerHTML = '<i class="fas fa-sun"></i><span>Light Mode</span>';
            } else {
                themeToggle.innerHTML = '<i class="fas fa-moon"></i><span>Dark Mode</span>';
            }
            
            localStorage.setItem('darkTheme', isDarkTheme);
        }
        
        // 切换历史记录面板
        function toggleHistory() {
            const historyPanel = document.getElementById('historyPanel');
            const settingsPanel = document.getElementById('settingsPanel');
            
            if (historyPanel.style.display === 'block') {
                historyPanel.style.display = 'none';
            } else {
                historyPanel.style.display = 'block';
                settingsPanel.style.display = 'none';
                renderHistory();
            }
        }
        
        // 切换设置面板
        function toggleSettings() {
            const settingsPanel = document.getElementById('settingsPanel');
            const historyPanel = document.getElementById('historyPanel');
            
            if (settingsPanel.style.display === 'block') {
                settingsPanel.style.display = 'none';
            } else {
                settingsPanel.style.display = 'block';
                historyPanel.style.display = 'none';
            }
        }
        
        // 保存到历史记录
        function saveToHistory(outputText) {
            const historyItem = {
                output: outputText,
                timestamp: new Date().toISOString(),
                date: new Date().toLocaleString()
            };
            
            history.unshift(historyItem);
            
            // 限制历史记录数量
            if (history.length > 10) {
                history = history.slice(0, 10);
            }
            
            localStorage.setItem('seatHistory', JSON.stringify(history));
        }
        
        // 渲染历史记录
        function renderHistory() {
            const historyList = document.getElementById('historyList');
            historyList.innerHTML = '';
            
            if (history.length === 0) {
                historyList.innerHTML = '<div style="text-align: center; padding: 20px; color: var(--gray);">No history records yet.</div>';
                return;
            }
            
            history.forEach((item, index) => {
                const historyItem = document.createElement('div');
                historyItem.className = 'history-item';
                
                const header = document.createElement('div');
                header.className = 'history-item-header';
                header.innerHTML = `
                    <span>Generation #${history.length - index}</span>
                    <span>${item.date}</span>
                `;
                
                const content = document.createElement('div');
                content.className = 'history-item-content';
                content.textContent = item.output;
                
                historyItem.appendChild(header);
                historyItem.appendChild(content);
                
                // 添加点击事件以加载历史记录
                historyItem.addEventListener('click', () => {
                    loadHistoryItem(item);
                });
                
                historyList.appendChild(historyItem);
            });
        }
        
        // 加载历史记录项
        function loadHistoryItem(item) {
            document.getElementById('output').textContent = item.output;
            document.getElementById('historyPanel').style.display = 'none';
            showSuccessMessage();
        }
        
        // 清空历史记录
        function clearHistory() {
            history = [];
            localStorage.setItem('seatHistory', JSON.stringify(history));
            renderHistory();
        }
        
        // 搜索学生
        function searchStudent() {
            const searchInput = document.getElementById('searchInput');
            const searchTerm = searchInput.value.trim();
            const studentResult = document.getElementById('studentResult');
            const studentDetails = document.getElementById('studentDetails');
            
            if (!searchTerm) {
                studentResult.style.display = 'none';
                return;
            }
            
            // 在所有学生中搜索
            const allStudents = [...boys.slice(1), ...girls.slice(1)];
            const foundStudents = allStudents.filter(student => 
                student.includes(searchTerm)
            );
            
            if (foundStudents.length === 0) {
                studentDetails.innerHTML = `<p>No student found with name: "${searchTerm}"</p>`;
                studentResult.style.display = 'block';
                return;
            }
            
            // 显示搜索结果
            let resultHTML = '';
            foundStudents.forEach(student => {
                const isMale = isBoy(student);
                const gender = isMale ? 'Male' : 'Female';
                const className = isMale ? 'boy' : 'girl';
                
                resultHTML += `
                    <div class="student-info">
                        <p><span>Name:</span> <span>${student}</span></p>
                        <p><span>Gender:</span> <span class="${className}">${gender}</span></p>
                        <p><span>Class:</span> <span>Class 10, Grade 2024</span></p>
                    </div>
                `;
                
                // 如果当前有座位分配，显示座位信息
                if (currentSeating) {
                    const seatInfo = findStudentSeat(student);
                    if (seatInfo) {
                        resultHTML += `
                            <div class="student-seat-info">
                                <div class="seat-info">
                                    <i class="fas fa-chair"></i> Seat Information
                                </div>
                                <div class="seat-position">
                                    <i class="fas fa-map-marker-alt"></i>
                                    <span>Desk ${seatInfo.deskNumber}, ${seatInfo.position}</span>
                                </div>
                                <div class="seat-position">
                                    <i class="fas fa-user-friends"></i>
                                    <span>Desk mate: ${seatInfo.deskMate}</span>
                                </div>
                            </div>
                        `;
                    }
                }
            });
            
            studentDetails.innerHTML = resultHTML;
            studentResult.style.display = 'block';
            
            // 高亮显示搜索结果
            if (document.getElementById('highlightResults').checked && currentSeating) {
                highlightStudentInSeating(foundStudents);
            }
        }
        
        // 查找学生座位信息
        function findStudentSeat(studentName) {
            if (!currentSeating) return null;
            
            const desks = document.querySelectorAll('.desk');
            for (let i = 0; i < desks.length; i++) {
                const desk = desks[i];
                const students = desk.querySelectorAll('.student');
                const deskNumber = desk.querySelector('.desk-number').textContent;
                
                for (let j = 0; j < students.length; j++) {
                    if (students[j].textContent === studentName) {
                        const deskMate = students[(j + 1) % 2].textContent;
                        const position = j === 0 ? 'Left' : 'Right';
                        
                        return {
                            deskNumber: deskNumber,
                            position: position,
                            deskMate: deskMate
                        };
                    }
                }
            }
            
            return null;
        }
        
        // 在座位表中高亮显示学生
        function highlightStudentInSeating(studentNames) {
            const desks = document.querySelectorAll('.desk');
            
            // 先移除所有高亮
            desks.forEach(desk => {
                const students = desk.querySelectorAll('.student');
                students.forEach(student => {
                    student.classList.remove('highlight');
                });
            });
            
            // 高亮匹配的学生
            desks.forEach(desk => {
                const students = desk.querySelectorAll('.student');
                students.forEach(student => {
                    if (studentNames.includes(student.textContent)) {
                        student.classList.add('highlight');
                    }
                });
            });
        }
        
        // 页面加载时显示初始信息
        window.addEventListener('DOMContentLoaded', () => {
            console.log('The intelligent seat allocation system has been loaded.');
            createParticles();
            updateClock();
            setInterval(updateClock, 1000);
            
            // 添加事件监听器
            document.getElementById('themeToggle').addEventListener('click', toggleTheme);
            document.getElementById('searchInput').addEventListener('input', searchStudent);
            
            // 从本地存储加载设置
            const autoSave = localStorage.getItem('autoSave');
            const showAnimations = localStorage.getItem('showAnimations');
            const highlightResults = localStorage.getItem('highlightResults');
            
            if (autoSave !== null) {
                document.getElementById('autoSave').checked = autoSave === 'true';
            }
            
            if (showAnimations !== null) {
                document.getElementById('showAnimations').checked = showAnimations === 'true';
            }
            
            if (highlightResults !== null) {
                document.getElementById('highlightResults').checked = highlightResults === 'true';
            }
            
            // 保存设置到本地存储
            document.getElementById('autoSave').addEventListener('change', function() {
                localStorage.setItem('autoSave', this.checked);
            });
            
            document.getElementById('showAnimations').addEventListener('change', function() {
                localStorage.setItem('showAnimations', this.checked);
            });
            
            document.getElementById('highlightResults').addEventListener('change', function() {
                localStorage.setItem('highlightResults', this.checked);
            });
        });
    </script>
</body>
</html>
