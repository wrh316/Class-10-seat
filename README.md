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
            --primary-light: #6c8aff;
            --primary-dark: #3a0ca3;
            --secondary: #7209b7;
            --accent: #4cc9f0;
            --success: #4ade80;
            --warning: #f59e0b;
            --danger: #ef4444;
            --light: #f8fafc;
            --dark: #1e293b;
            --gray: #64748b;
            --bg-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --card-gradient: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(255, 255, 255, 0.85));
            --card-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            --hover-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
            --glass-bg: rgba(255, 255, 255, 0.25);
            --glass-border: rgba(255, 255, 255, 0.18);
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
            overflow-x: hidden;
        }
        
        .container {
            background: var(--card-gradient);
            backdrop-filter: blur(20px);
            border-radius: 24px;
            box-shadow: 
                0 25px 50px -12px rgba(0, 0, 0, 0.25),
                inset 0 1px 0 rgba(255, 255, 255, 0.3);
            padding: 40px;
            max-width: 1200px;
            width: 100%;
            border: 1px solid var(--glass-border);
            position: relative;
            overflow: hidden;
            animation: fadeIn 0.8s ease-out;
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
            position: relative;
            z-index: 1;
        }
        
        .logo::after {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary-light), var(--primary-dark));
            opacity: 0.7;
            z-index: -1;
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); opacity: 0.7; }
            50% { transform: scale(1.1); opacity: 0.4; }
            100% { transform: scale(1); opacity: 0.7; }
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
            position: relative;
            display: inline-block;
        }
        
        h1::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--primary), transparent);
            border-radius: 2px;
        }
        
        .subtitle {
            color: var(--gray);
            font-size: 1.2rem;
            font-weight: 400;
            margin-bottom: 10px;
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
            min-width: 240px;
            justify-content: center;
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
        
        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
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
            position: relative;
            overflow: hidden;
        }
        
        .output-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(67, 97, 238, 0.03), rgba(76, 201, 240, 0.03));
            z-index: 0;
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
            position: relative;
            z-index: 1;
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
            z-index: 1;
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
            position: relative;
            z-index: 1;
        }
        
        .teacher-desk::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.2), transparent);
            border-radius: 10px;
            z-index: -1;
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
            overflow: hidden;
        }
        
        .desk::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.3), transparent);
            z-index: 0;
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
            border-color: var(--primary);
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
            position: relative;
            z-index: 1;
            cursor: pointer;
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
        
        .student::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.2), transparent);
            border-radius: 6px;
            z-index: -1;
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
            position: relative;
            z-index: 1;
        }
        
        .stat-icon::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.2), transparent);
            z-index: -1;
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
            position: relative;
            z-index: 1;
        }
        
        .spinner {
            width: 60px;
            height: 60px;
            border: 4px solid rgba(67, 97, 238, 0.2);
            border-top: 4px solid var(--primary);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
            position: relative;
        }
        
        .spinner::after {
            content: '';
            position: absolute;
            top: -4px;
            left: -4px;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            border: 4px solid transparent;
            border-bottom: 4px solid var(--accent);
            animation: spin 0.5s linear infinite reverse;
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
            position: relative;
            z-index: 1;
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
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
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
            position: relative;
            z-index: 1;
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
            position: relative;
            overflow: hidden;
        }
        
        .tab-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(67, 97, 238, 0.1), transparent);
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .tab-btn.active {
            background: var(--primary);
            color: white;
        }
        
        .tab-btn:hover::before {
            opacity: 1;
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
            z-index: 1;
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
            z-index: 1;
        }
        
        /* 新增个性化元素：装饰性星星 */
        .decoration-star {
            position: absolute;
            color: rgba(255, 255, 255, 0.7);
            font-size: 1.2rem;
            animation: twinkle 3s infinite alternate;
            z-index: -1;
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
            z-index: 1;
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
            position: relative;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--primary), var(--accent));
            width: 0%;
            transition: width 0.5s ease;
            border-radius: 3px;
            position: relative;
            overflow: hidden;
        }
        
        .progress-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
            animation: shimmer 2s infinite;
        }
        
        @keyframes shimmer {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
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
        
        /* 新增：学生信息提示 */
        .student-tooltip {
            position: absolute;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            padding: 8px 12px;
            border-radius: 6px;
            font-size: 0.8rem;
            z-index: 100;
            pointer-events: none;
            opacity: 0;
            transition: opacity 0.3s;
            white-space: nowrap;
        }
        
        .student-tooltip.show {
            opacity: 1;
        }
        
        /* 新增：按钮涟漪效果 */
        .ripple {
            position: absolute;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.6);
            transform: scale(0);
            animation: ripple 0.6s linear;
            pointer-events: none;
        }
        
        @keyframes ripple {
            to {
                transform: scale(4);
                opacity: 0;
            }
        }
        
        /* 新增：卡片悬停效果 */
        .card-hover {
            transition: all 0.3s ease;
        }
        
        .card-hover:hover {
            transform: translateY(-5px);
        }
        
        /* 新增：输入框样式 */
        .input-group {
            margin-bottom: 20px;
            position: relative;
        }
        
        .input-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark);
        }
        
        .input-field {
            width: 100%;
            padding: 12px 16px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.3s ease;
            background: white;
        }
        
        .input-field:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.1);
            outline: none;
        }
        
        /* 新增：通知系统 */
        .notification {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: var(--dark);
            color: white;
            padding: 15px 25px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            z-index: 1000;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: transform 0.3s ease;
        }
        
        .notification.show {
            transform: translateX(-50%) translateY(0);
        }
        
        .notification.success {
            background: var(--success);
        }
        
        .notification.warning {
            background: var(--warning);
        }
        
        .notification.error {
            background: var(--danger);
        }
        
        /* 新增：设置面板 */
        .settings-panel {
            background: var(--light);
            border-radius: 16px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: var(--card-shadow);
            border: 1px solid rgba(255, 255, 255, 0.5);
            display: none;
        }
        
        .settings-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .settings-title {
            font-size: 1.3rem;
            font-weight: 600;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .settings-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }
        
        .setting-item {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        
        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 60px;
            height: 30px;
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
            border-radius: 34px;
        }
        
        .toggle-slider:before {
            position: absolute;
            content: "";
            height: 22px;
            width: 22px;
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
            transform: translateX(30px);
        }
        
        /* 新增：搜索功能 */
        .search-container {
            position: relative;
            margin-bottom: 20px;
        }
        
        .search-input {
            width: 100%;
            padding: 12px 45px 12px 16px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.3s ease;
            background: white;
        }
        
        .search-input:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.1);
            outline: none;
        }
        
        .search-icon {
            position: absolute;
            right: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--gray);
        }
        
        /* 新增：学生详情弹窗 */
        .student-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 2000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }
        
        .student-modal.show {
            opacity: 1;
            visibility: visible;
        }
        
        .student-modal-content {
            background: white;
            border-radius: 16px;
            padding: 30px;
            max-width: 500px;
            width: 90%;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
            position: relative;
            transform: translateY(20px);
            transition: transform 0.3s ease;
        }
        
        .student-modal.show .student-modal-content {
            transform: translateY(0);
        }
        
        .student-modal-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--gray);
        }
        
        .student-modal-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .student-avatar {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            color: white;
        }
        
        .student-avatar.boy {
            background: linear-gradient(135deg, #3b82f6, #1d4ed8);
        }
        
        .student-avatar.girl {
            background: linear-gradient(135deg, #ec4899, #be185d);
        }
        
        .student-info {
            flex: 1;
        }
        
        .student-name {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 5px;
        }
        
        .student-gender {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
        }
        
        .student-gender.boy {
            background: rgba(59, 130, 246, 0.1);
            color: #1d4ed8;
        }
        
        .student-gender.girl {
            background: rgba(236, 72, 153, 0.1);
            color: #be185d;
        }
        
        .student-details {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }
        
        .detail-item {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }
        
        .detail-label {
            font-size: 0.9rem;
            color: var(--gray);
        }
        
        .detail-value {
            font-weight: 600;
        }
        
        /* 新增：打印样式 */
        @media print {
            body * {
                visibility: hidden;
            }
            
            .container, .container * {
                visibility: visible;
            }
            
            .container {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                box-shadow: none;
            }
            
            .btn, .tab-buttons, .settings-panel, footer, .class-badge, .time-display {
                display: none !important;
            }
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
        
        <div class="control-panel">
            <button class="btn btn-primary" id="generateBtn" onclick="generateSeats()">
                <i class="fas fa-random"></i>
                🎲 Generate Random Seating Chart
            </button>
            <button class="btn btn-secondary" onclick="resetOutput()">
                <i class="fas fa-redo"></i>
                🔄 Reset System
            </button>
            <button class="btn btn-secondary" onclick="toggleSettings()">
                <i class="fas fa-cog"></i>
                ⚙️ Settings
            </button>
            <button class="btn btn-secondary" onclick="printSeatingChart()">
                <i class="fas fa-print"></i>
                🖨️ Print Chart
            </button>
        </div>
        
        <!-- 设置面板 -->
        <div class="settings-panel" id="settingsPanel">
            <div class="settings-header">
                <div class="settings-title">
                    <i class="fas fa-sliders-h"></i>
                    System Settings
                </div>
                <button class="btn btn-secondary" onclick="toggleSettings()">
                    <i class="fas fa-times"></i>
                    Close
                </button>
            </div>
            <div class="settings-grid">
                <div class="setting-item">
                    <label class="input-label">Animation Speed</label>
                    <select class="input-field" id="animationSpeed">
                        <option value="fast">Fast</option>
                        <option value="normal" selected>Normal</option>
                        <option value="slow">Slow</option>
                    </select>
                </div>
                <div class="setting-item">
                    <label class="input-label">Show Student Details</label>
                    <label class="toggle-switch">
                        <input type="checkbox" id="showDetails" checked>
                        <span class="toggle-slider"></span>
                    </label>
                </div>
                <div class="setting-item">
                    <label class="input-label">Auto-switch to Visual View</label>
                    <label class="toggle-switch">
                        <input type="checkbox" id="autoSwitchView" checked>
                        <span class="toggle-slider"></span>
                    </label>
                </div>
                <div class="setting-item">
                    <label class="input-label">Sound Effects</label>
                    <label class="toggle-switch">
                        <input type="checkbox" id="soundEffects">
                        <span class="toggle-slider"></span>
                    </label>
                </div>
            </div>
        </div>
        
        <!-- 搜索功能 -->
        <div class="search-container">
            <input type="text" class="search-input" id="searchInput" placeholder="Search for a student...">
            <i class="fas fa-search search-icon"></i>
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
            <div class="stat-card stat-boy card-hover">
                <div class="stat-icon">
                    <i class="fas fa-male"></i>
                </div>
                <h3>Boy Count</h3>
                <div class="number">31</div>
            </div>
            <div class="stat-card stat-girl card-hover">
                <div class="stat-icon">
                    <i class="fas fa-female"></i>
                </div>
                <h3>Girl Count</h3>
                <div class="number">23</div>
            </div>
            <div class="stat-card stat-total card-hover">
                <div class="stat-icon">
                    <i class="fas fa-users"></i>
                </div>
                <h3>All Count</h3>
                <div class="number">54</div>
            </div>
            <div class="stat-card stat-seat card-hover">
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

    <!-- 学生详情弹窗 -->
    <div class="student-modal" id="studentModal">
        <div class="student-modal-content">
            <button class="student-modal-close" onclick="closeStudentModal()">
                <i class="fas fa-times"></i>
            </button>
            <div class="student-modal-header">
                <div class="student-avatar" id="studentAvatar">
                    <i class="fas fa-user"></i>
                </div>
                <div class="student-info">
                    <div class="student-name" id="studentName">Student Name</div>
                    <div class="student-gender" id="studentGender">Gender</div>
                </div>
            </div>
            <div class="student-details">
                <div class="detail-item">
                    <span class="detail-label">Seat Number</span>
                    <span class="detail-value" id="studentSeat">-</span>
                </div>
                <div class="detail-item">
                    <span class="detail-label">Row</span>
                    <span class="detail-value" id="studentRow">-</span>
                </div>
                <div class="detail-item">
                    <span class="detail-label">Desk Partner</span>
                    <span class="detail-value" id="studentPartner">-</span>
                </div>
                <div class="detail-item">
                    <span class="detail-label">Position</span>
                    <span class="detail-value" id="studentPosition">-</span>
                </div>
            </div>
        </div>
    </div>

    <div class="success-message" id="successMessage">
        <i class="fas fa-check-circle"></i> The Code has Completed Successfully
    </div>
    
    <!-- 通知系统 -->
    <div class="notification" id="notification">
        <i class="fas fa-info-circle"></i>
        <span id="notificationText">This is a notification</span>
    </div>
    
    <!-- 学生信息提示 -->
    <div class="student-tooltip" id="studentTooltip"></div>

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
        
        // 当前座位分配数据
        let currentSeatingData = null;
        
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
        
        // 创建涟漪效果
        function createRipple(event) {
            const button = event.currentTarget;
            const circle = document.createElement('span');
            const diameter = Math.max(button.clientWidth, button.clientHeight);
            const radius = diameter / 2;
            
            circle.style.width = circle.style.height = `${diameter}px`;
            circle.style.left = `${event.clientX - button.getBoundingClientRect().left - radius}px`;
            circle.style.top = `${event.clientY - button.getBoundingClientRect().top - radius}px`;
            circle.classList.add('ripple');
            
            const ripple = button.getElementsByClassName('ripple')[0];
            if (ripple) {
                ripple.remove();
            }
            
            button.appendChild(circle);
        }
        
        // 添加按钮涟漪效果
        document.querySelectorAll('.btn').forEach(button => {
            button.addEventListener('click', createRipple);
        });
        
        // 显示通知
        function showNotification(message, type = 'info') {
            const notification = document.getElementById('notification');
            const notificationText = document.getElementById('notificationText');
            
            notificationText.textContent = message;
            notification.className = 'notification';
            notification.classList.add(type);
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
        
        // 显示学生信息提示
        function showStudentTooltip(event, studentName) {
            const tooltip = document.getElementById('studentTooltip');
            tooltip.textContent = studentName;
            tooltip.style.left = `${event.pageX + 10}px`;
            tooltip.style.top = `${event.pageY + 10}px`;
            tooltip.classList.add('show');
        }
        
        // 隐藏学生信息提示
        function hideStudentTooltip() {
            const tooltip = document.getElementById('studentTooltip');
            tooltip.classList.remove('show');
        }
        
        // 切换设置面板
        function toggleSettings() {
            const settingsPanel = document.getElementById('settingsPanel');
            if (settingsPanel.style.display === 'block') {
                settingsPanel.style.display = 'none';
            } else {
                settingsPanel.style.display = 'block';
            }
        }
        
        // 打印座位表
        function printSeatingChart() {
            if (!currentSeatingData) {
                showNotification('Please make the seating chart.', 'warning');
                return;
            }
            window.print();
        }
        
        // 打开学生详情弹窗
        function openStudentModal(studentName, seatNumber, row, partner, position) {
            const modal = document.getElementById('studentModal');
            const avatar = document.getElementById('studentAvatar');
            const nameElem = document.getElementById('studentName');
            const genderElem = document.getElementById('studentGender');
            const seatElem = document.getElementById('studentSeat');
            const rowElem = document.getElementById('studentRow');
            const partnerElem = document.getElementById('studentPartner');
            const positionElem = document.getElementById('studentPosition');
            
            // 设置学生信息
            nameElem.textContent = studentName;
            const isMale = isBoy(studentName);
            genderElem.textContent = isMale ? 'Boy.' : 'Girl.';
            genderElem.className = isMale ? 'student-gender boy' : 'student-gender girl';
            avatar.className = isMale ? 'student-avatar boy' : 'student-avatar girl';
            avatar.innerHTML = isMale ? '<i class="fas fa-male"></i>' : '<i class="fas fa-female"></i>';
            
            seatElem.textContent = seatNumber;
            rowElem.textContent = row;
            partnerElem.textContent = partner;
            positionElem.textContent = position;
            
            // 显示弹窗
            modal.classList.add('show');
        }
        
        // 关闭学生详情弹窗
        function closeStudentModal() {
            const modal = document.getElementById('studentModal');
            modal.classList.remove('show');
        }
        
        // 搜索学生
        function searchStudent() {
            const searchTerm = document.getElementById('searchInput').value.trim().toLowerCase();
            if (!searchTerm) return;
            
            if (!currentSeatingData) {
                showNotification('Please make the seating chart.', 'warning');
                return;
            }
            
            // 在所有学生中搜索
            const allStudents = [...boys.slice(1), ...girls.slice(1)];
            const foundStudent = allStudents.find(student => 
                student.toLowerCase().includes(searchTerm)
            );
            
            if (foundStudent) {
                // 查找学生在座位表中的位置
                let studentInfo = null;
                for (let i = 0; i < currentSeatingData.length; i++) {
                    const row = currentSeatingData[i];
                    for (let j = 0; j < row.length; j++) {
                        const desk = row[j];
                        if (desk.student1 === foundStudent || desk.student2 === foundStudent) {
                            studentInfo = {
                                name: foundStudent,
                                seatNumber: desk.deskNumber,
                                row: i + 1,
                                partner: desk.student1 === foundStudent ? desk.student2 : desk.student1,
                                position: desk.student1 === foundStudent ? 'Left Side.' : 'Right Side.'
                            };
                            break;
                        }
                    }
                    if (studentInfo) break;
                }
                
                if (studentInfo) {
                    openStudentModal(
                        studentInfo.name,
                        studentInfo.seatNumber,
                        studentInfo.row,
                        studentInfo.partner,
                        studentInfo.position
                    );
                    // 切换到可视化视图
                    switchTab('visual');
                } else {
                    showNotification(`The seat information of Student "${foundStudent}" was not found.`, 'error');
                }
            } else {
                showNotification(`Students not found. "${searchTerm}"`, 'error');
            }
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
            student1Elem.addEventListener('mouseenter', (e) => showStudentTooltip(e, student1));
            student1Elem.addEventListener('mouseleave', hideStudentTooltip);
            student1Elem.addEventListener('click', () => {
                openStudentModal(
                    student1,
                    deskNumber,
                    Math.ceil(deskNumber / 4),
                    student2,
                    'Left Side.'
                );
            });
            
            const student2Elem = document.createElement('div');
            student2Elem.className = `student ${isBoy(student2) ? 'boy' : 'girl'}`;
            student2Elem.textContent = student2;
            student2Elem.addEventListener('mouseenter', (e) => showStudentTooltip(e, student2));
            student2Elem.addEventListener('mouseleave', hideStudentTooltip);
            student2Elem.addEventListener('click', () => {
                openStudentModal(
                    student2,
                    deskNumber,
                    Math.ceil(deskNumber / 4),
                    student1,
                    'Right Side.'
                );
            });
            
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
            const generateBtn = document.getElementById('generateBtn');
            
            // 禁用生成按钮
            generateBtn.disabled = true;
            
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
                
                // 存储座位数据
                currentSeatingData = [];
                
                // 生成座位表
                let deskCounter = 1;
                for (let i = 1; i <= 27; i += 4) {
                    let line = '| ';
                    const row = document.createElement('div');
                    row.className = 'row';
                    
                    const rowData = [];
                    
                    if (i < 21) {
                        if (Math.floor(i / 4) % 2 === 1) {
                            for (let j = 0; j < 4; j++) {
                                const student1 = boys[cardboy[i + j - 1]];
                                const student2 = girls[cardgirl[i + j - 1]];
                                
                                line += setw(student1, 4) + ' ' + setw(student2, 4) + ' | ';
                                
                                const desk = createDesk(student1, student2, deskCounter);
                                row.appendChild(desk);
                                
                                rowData.push({
                                    deskNumber: deskCounter,
                                    student1: student1,
                                    student2: student2
                                });
                                
                                deskCounter++;
                            }
                        } else {
                            for (let j = 0; j < 4; j++) {
                                const student1 = girls[cardgirl[i + j - 1]];
                                const student2 = boys[cardboy[i + j - 1]];
                                
                                line += setw(student1, 4) + ' ' + setw(student2, 4) + ' | ';
                                
                                const desk = createDesk(student1, student2, deskCounter);
                                row.appendChild(desk);
                                
                                rowData.push({
                                    deskNumber: deskCounter,
                                    student1: student1,
                                    student2: student2
                                });
                                
                                deskCounter++;
                            }
                        }
                    } else if (i === 21) {
                        for (let j = 0; j < 3; j++) {
                            const student1 = boys[cardboy[i + j - 1]];
                            const student2 = girls[cardgirl[i + j - 1]];
                            
                            line += setw(student1, 4) + ' ' + setw(student2, 4) + ' | ';
                            
                            const desk = createDesk(student1, student2, deskCounter);
                            row.appendChild(desk);
                            
                            rowData.push({
                                deskNumber: deskCounter,
                                student1: student1,
                                student2: student2
                            });
                            
                            deskCounter++;
                        }
                        
                        const student1 = boys[cardboy[i + 3 - 1]];
                        const student2 = boys[cardboy[i + 7 - 1]];
                        
                        line += setw(student1, 4) + ' ' + setw(student2, 4) + ' | ';
                        
                        const desk = createDesk(student1, student2, deskCounter);
                        row.appendChild(desk);
                        
                        rowData.push({
                            deskNumber: deskCounter,
                            student1: student1,
                            student2: student2
                        });
                        
                        deskCounter++;
                    } else {
                        for (let j = 0; j < 3; j++) {
                            const student1 = boys[cardboy[i + j - 1]];
                            const student2 = boys[cardboy[i + j + 4 - 1]];
                            
                            line += setw(student1, 4) + ' ' + setw(student2, 4) + ' | ';
                            
                            const desk = createDesk(student1, student2, deskCounter);
                            row.appendChild(desk);
                            
                            rowData.push({
                                deskNumber: deskCounter,
                                student1: student1,
                                student2: student2
                            });
                            
                            deskCounter++;
                        }
                    }
                    
                    outputText += line + '\n';
                    seatingPlan.appendChild(row);
                    currentSeatingData.push(rowData);
                }
                
                // 设置输出
                output.textContent = outputText;
                loading.style.display = 'none';
                progressBar.style.display = 'none';
                progressFill.style.width = '0%';
                
                // 启用生成按钮
                generateBtn.disabled = false;
                
                // 显示成功消息
                showSuccessMessage();
                
                // 自动切换到可视化视图
                const autoSwitchView = document.getElementById('autoSwitchView').checked;
                if (autoSwitchView) {
                    switchTab('visual');
                }
                
            }, 1500);
        }
        
        // 重置输出
        function resetOutput() {
            document.getElementById('output').textContent = 'Welcome to use the intelligent seat allocation system.\nClick the button above to start generating a random seating chart.\nThis system ensures the randomness and fairness of seat allocation, with a 3.2% probability of each person being assigned.';
            document.getElementById('seatingPlan').innerHTML = '<div style="text-align: center; padding: 40px; color: #7f8c8d; font-size: 1.2rem;">Click the "Generate Random Seating Chart" button to start seat allocation.</div>';
            document.getElementById('searchInput').value = '';
            currentSeatingData = null;
            showNotification('The system has been reset.', 'info');
        }
        
        // 页面加载时显示初始信息
        window.addEventListener('DOMContentLoaded', () => {
            console.log('The intelligent seat allocation system has been loaded.');
            createParticles();
            updateClock();
            setInterval(updateClock, 1000);
            
            // 添加卡片悬停效果
            document.querySelectorAll('.stat-card').forEach(card => {
                card.classList.add('card-hover');
            });
            
            // 添加搜索功能
            document.getElementById('searchInput').addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    searchStudent();
                }
            });
            
            // 点击弹窗外部关闭弹窗
            document.getElementById('studentModal').addEventListener('click', (e) => {
                if (e.target === document.getElementById('studentModal')) {
                    closeStudentModal();
                }
            });
        });
    </script>
</body>
</html>
