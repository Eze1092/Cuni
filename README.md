<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>SmartCam Pro - Editor Optimizado</title>
    <style>
        /* ===== VARIABLES Y RESET ===== */
        :root {
            --bg-primary: #0a0a12;
            --bg-secondary: #161622;
            --bg-tertiary: #222235;
            --bg-card: #1a1a2a;
            --accent-primary: #5a67d8;
            --accent-secondary: #8c9eff;
            --accent-gradient: linear-gradient(135deg, var(--accent-primary), var(--accent-secondary));
            --text-primary: #eef2ff;
            --text-secondary: #a1a1c2;
            --success: #48bb78;
            --warning: #ed8936;
            --danger: #f56565;
            --border-radius: 16px;
            --transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
            --shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            --inner-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.4);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        body {
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            display: flex;
            overflow: hidden;
            position: relative;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, sans-serif;
            touch-action: manipulation;
        }

        body::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at top right, rgba(90, 103, 216, 0.1), transparent 70%);
            z-index: -1;
        }

        /* ===== LAYOUT PRINCIPAL ===== */
        .app-container {
            display: flex;
            flex-direction: column;
            width: 100%;
            height: 100vh;
            position: relative;
        }

        /* ===== SIDEBAR ===== */
        .sidebar {
            width: 100%;
            background: var(--bg-secondary);
            padding: 12px 0;
            display: flex;
            flex-wrap: wrap;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            z-index: 10;
            box-shadow: var(--shadow);
            gap: 8px;
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
        }

        .sidebar-header {
            padding: 0 15px 10px;
            margin-bottom: 5px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            width: 100%;
        }

        .logo {
            font-size: 22px;
            font-weight: 800;
            background: var(--accent-gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 3px;
            letter-spacing: -0.5px;
            text-align: center;
        }

        .tagline {
            font-size: 10px;
            color: var(--text-secondary);
            font-weight: 500;
            text-align: center;
        }

        .tools-category {
            padding: 0 10px;
            margin-bottom: 12px;
            width: 140px;
            min-width: 140px;
        }

        .category-title {
            font-size: 11px;
            font-weight: 600;
            color: var(--text-secondary);
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
            display: flex;
            align-items: center;
        }

        .category-title::after {
            content: '';
            flex: 1;
            height: 1px;
            background: rgba(255, 255, 255, 0.05);
            margin-left: 8px;
        }

        .tool-btn {
            width: 100%;
            background: transparent;
            border: none;
            color: var(--text-primary);
            padding: 10px 12px;
            margin-bottom: 6px;
            border-radius: 10px;
            text-align: left;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            font-size: 13px;
            font-weight: 500;
            position: relative;
            overflow: hidden;
        }

        .tool-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 3px;
            height: 100%;
            background: var(--accent-gradient);
            transform: translateX(-10px);
            transition: var(--transition);
            opacity: 0;
        }

        .tool-btn:active {
            background: rgba(255, 255, 255, 0.03);
            padding-left: 15px;
        }

        .tool-btn:active::before {
            transform: translateX(0);
            opacity: 1;
        }

        .tool-btn i {
            margin-right: 8px;
            font-size: 14px;
            width: 20px;
            text-align: center;
            color: var(--text-secondary);
            transition: var(--transition);
        }

        .tool-btn:active i {
            color: var(--accent-primary);
        }

        .tool-btn.active {
            background: rgba(90, 103, 216, 0.1);
            color: var(--accent-secondary);
        }

        .tool-btn.active i {
            color: var(--accent-primary);
        }

        /* ===== CONTENIDO PRINCIPAL ===== */
        .main-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            padding: 12px;
            overflow: hidden;
            position: relative;
        }

        .top-bar {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 12px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            gap: 12px;
        }

        .app-title {
            font-size: 18px;
            font-weight: 700;
            background: var(--accent-gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            display: flex;
            align-items: center;
            gap: 8px;
            flex: 1;
            min-width: 200px;
        }

        .app-title i {
            font-size: 16px;
        }

        .action-buttons {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 10px 16px;
            border-radius: 12px;
            border: none;
            font-weight: 600;
            font-size: 13px;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 6px;
            box-shadow: var(--shadow);
        }

        .btn-primary {
            background: var(--accent-gradient);
            color: white;
        }

        .btn-outline {
            background: transparent;
            border: 1px solid var(--accent-primary);
            color: var(--accent-primary);
        }

        .btn:active {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(90, 103, 216, 0.25);
        }

        .btn-outline:active {
            background: rgba(90, 103, 216, 0.1);
        }

        /* ===== ÁREA DE TRABAJO ===== */
        .workspace {
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: 15px;
            overflow: hidden;
        }

        .image-container {
            flex: 1;
            background: var(--bg-card);
            border-radius: var(--border-radius);
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
            box-shadow: var(--shadow);
            border: 1px solid rgba(255, 255, 255, 0.05);
            min-height: 300px;
        }

        .image-placeholder {
            text-align: center;
            padding: 20px;
            color: var(--text-secondary);
            max-width: 100%;
        }

        .image-placeholder i {
            font-size: 50px;
            margin-bottom: 12px;
            color: rgba(255, 255, 255, 0.07);
        }

        .image-placeholder h3 {
            font-size: 16px;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--text-primary);
        }

        .image-placeholder p {
            font-size: 12px;
            margin-bottom: 15px;
            line-height: 1.5;
        }

        .upload-btn {
            background: var(--accent-gradient);
            color: white;
            padding: 10px 25px;
            border-radius: 10px;
            border: none;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: var(--shadow);
            font-size: 14px;
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }

        .upload-btn:active {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(90, 103, 216, 0.35);
        }

        .drag-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(90, 103, 216, 0.2);
            border: 2px dashed var(--accent-primary);
            border-radius: var(--border-radius);
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 18px;
            font-weight: 700;
            color: white;
            opacity: 0;
            pointer-events: none;
            transition: var(--transition);
            z-index: 20;
            text-align: center;
            padding: 15px;
        }

        .image-container.drag-over .drag-overlay {
            opacity: 1;
        }

        #preview-image {
            max-width: 100%;
            max-height: 100%;
            display: none;
            border-radius: var(--border-radius);
            box-shadow: 0 8px 40px rgba(0, 0, 0, 0.4);
            transition: all 0.3s ease;
        }

        /* ===== PANEL DE EDICIÓN ===== */
        .edit-panel {
            width: 100%;
            background: var(--bg-card);
            border-radius: var(--border-radius);
            padding: 15px;
            overflow-y: auto;
            box-shadow: var(--shadow);
            border: 1px solid rgba(255, 255, 255, 0.05);
            max-height: 350px;
            -webkit-overflow-scrolling: touch;
        }

        .panel-title {
            font-size: 15px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
            font-weight: 600;
            color: var(--accent-secondary);
        }

        .panel-title i {
            background: var(--accent-gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            font-size: 16px;
        }

        .controls-group {
            margin-bottom: 20px;
            background: rgba(255, 255, 255, 0.03);
            padding: 12px;
            border-radius: var(--border-radius);
        }

        .control-label {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
            font-size: 12px;
            color: var(--text-secondary);
            font-weight: 500;
        }

        .control-label span:last-child {
            color: var(--text-primary);
            font-weight: 600;
        }

        .slider-container {
            position: relative;
        }

        .slider {
            width: 100%;
            height: 6px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 4px;
            outline: none;
            -webkit-appearance: none;
            position: relative;
            overflow: hidden;
        }

        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 16px;
            height: 16px;
            border-radius: 50%;
            background: white;
            cursor: pointer;
            box-shadow: 0 0 10px rgba(90, 103, 216, 0.8);
            border: 2px solid var(--accent-primary);
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }

        .slider:active::-webkit-slider-thumb {
            transform: scale(1.2);
        }

        .slider-fill {
            position: absolute;
            top: 0;
            left: 0;
            height: 100%;
            background: var(--accent-gradient);
            border-radius: 4px;
            pointer-events: none;
        }

        .color-palette {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(28px, 1fr));
            gap: 8px;
            margin-top: 12px;
        }

        .color-option {
            width: 100%;
            height: 32px;
            border-radius: 8px;
            cursor: pointer;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
            box-shadow: var(--inner-shadow);
            border: 1px solid transparent;
        }

        .color-option:active {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
        }

        .color-option.active {
            border-color: white;
            transform: scale(1.05);
        }

        .color-option.active::after {
            content: '\2713';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
            font-size: 12px;
        }

        .phone-presets {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
            gap: 10px;
            margin-top: 12px;
        }

        .preset-btn {
            background: var(--bg-tertiary);
            border: none;
            color: var(--text-primary);
            padding: 10px 6px;
            border-radius: 10px;
            cursor: pointer;
            transition: var(--transition);
            text-align: center;
            font-size: 11px;
            font-weight: 500;
            box-shadow: var(--inner-shadow);
            border: 1px solid rgba(255, 255, 255, 0.05);
            position: relative;
            overflow: hidden;
        }

        .preset-btn:active {
            background: rgba(255, 255, 255, 0.05);
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
        }

        .preset-btn i {
            display: block;
            font-size: 18px;
            margin-bottom: 6px;
        }

        .iphone { color: #a6a6a6; }
        .samsung { color: #1428a0; }
        .xiaomi { color: #ff6700; }
        .pixel { color: #4285f4; }
        .huawei { color: #ff0000; }
        .sony { color: #0066cc; }
        .oppo { color: #008000; }
        .vivo { color: #415fff; }
        .oneplus { color: #eb0029; }

        /* ===== FOOTER ===== */
        .footer {
            padding: 12px 0 5px;
            text-align: center;
            color: var(--text-secondary);
            font-size: 10px;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
            margin-top: 12px;
            font-weight: 500;
        }

        /* ===== NOTIFICACIONES ===== */
        .notification {
            position: fixed;
            bottom: 12px;
            right: 12px;
            background: var(--bg-card);
            color: var(--text-primary);
            padding: 12px 18px;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            display: flex;
            align-items: center;
            gap: 8px;
            z-index: 1000;
            transform: translateY(100px);
            opacity: 0;
            border-left: 4px solid var(--accent-primary);
            animation: slideIn 0.5s forwards, fadeOut 0.5s forwards 2.5s;
            font-size: 13px;
            max-width: 90%;
        }

        .notification i {
            font-size: 14px;
            color: var(--accent-primary);
        }

        /* ===== RESPONSIVE ===== */
        @media (min-width: 768px) {
            .app-container {
                flex-direction: row;
            }
            
            .sidebar {
                width: 240px;
                flex-direction: column;
                flex-wrap: nowrap;
                padding: 15px 0;
                border-right: 1px solid rgba(255, 255, 255, 0.05);
                border-bottom: none;
                gap: 0;
            }
            
            .sidebar-header {
                padding: 0 15px 15px;
                margin-bottom: 10px;
            }
            
            .logo {
                font-size: 24px;
                text-align: left;
            }
            
            .tagline {
                font-size: 11px;
                text-align: left;
            }
            
            .tools-category {
                padding: 0 12px;
                margin-bottom: 20px;
                width: 100%;
            }
            
            .tool-btn {
                padding: 10px 15px;
                margin-bottom: 6px;
                font-size: 13px;
            }
            
            .main-content {
                padding: 20px;
            }
            
            .top-bar {
                margin-bottom: 20px;
                padding-bottom: 15px;
            }
            
            .app-title {
                font-size: 20px;
            }
            
            .btn {
                padding: 10px 20px;
                font-size: 13px;
            }
            
            .workspace {
                flex-direction: row;
                gap: 20px;
            }
            
            .edit-panel {
                width: 300px;
                max-height: none;
                padding: 20px;
            }
            
            .image-placeholder {
                padding: 30px;
            }
            
            .image-placeholder i {
                font-size: 60px;
            }
            
            .image-placeholder h3 {
                font-size: 18px;
            }
            
            .image-placeholder p {
                font-size: 13px;
            }
            
            .upload-btn {
                padding: 12px 30px;
                font-size: 14px;
            }
            
            .drag-overlay {
                font-size: 20px;
            }
            
            .panel-title {
                font-size: 16px;
            }
            
            .controls-group {
                padding: 15px;
            }
            
            .color-palette {
                grid-template-columns: repeat(5, 1fr);
            }
            
            .phone-presets {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .preset-btn {
                padding: 12px 8px;
                font-size: 12px;
            }
            
            .preset-btn i {
                font-size: 22px;
            }
            
            .footer {
                font-size: 11px;
            }
        }

        /* ===== ANIMACIONES ===== */
        @keyframes slideIn {
            to {
                transform: translateY(0);
                opacity: 1;
            }
   