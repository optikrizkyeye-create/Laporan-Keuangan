<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pencatatan Keuangan Pro</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2.0.0"></script>
    <script src="https://unpkg.com/xlsx/dist/xlsx.full.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/file-saver@2.0.5/dist/FileSaver.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/crypto-js@4.1.1/crypto-js.min.js"></script>
    <style>
        :root {
            --primary: #3498db;
            --primary-dark: #2980b9;
            --secondary: #2c3e50;
            --success: #27ae60;
            --warning: #f39c12;
            --danger: #e74c3c;
            --info: #17a2b8;
            --light: #f8f9fa;
            --dark: #343a40;
            --gray: #6c757d;
            --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            --shadow-lg: 0 10px 25px rgba(0,0,0,0.15);
            --radius: 12px;
            --gradient-primary: linear-gradient(135deg, #3498db 0%, #2c3e50 100%);
            --gradient-success: linear-gradient(135deg, #27ae60 0%, #219653 100%);
            --gradient-warning: linear-gradient(135deg, #f39c12 0%, #e67e22 100%);
            --gradient-danger: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* Login Screen */
        .login-container {
            background: white;
            border-radius: var(--radius);
            box-shadow: var(--shadow-lg);
            padding: 40px;
            width: 100%;
            max-width: 400px;
            animation: fadeIn 0.5s;
        }

        .login-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .login-icon {
            font-size: 48px;
            color: var(--primary);
            margin-bottom: 15px;
        }

        .login-title {
            font-size: 28px;
            font-weight: 700;
            color: var(--secondary);
            margin-bottom: 10px;
        }

        .login-subtitle {
            color: var(--gray);
            font-size: 14px;
        }

        .login-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .form-label {
            font-weight: 600;
            color: var(--dark);
            font-size: 14px;
        }

        .form-input {
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            transition: all 0.3s;
        }

        .form-input:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
        }

        .btn {
            padding: 14px 20px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .btn-primary {
            background: var(--gradient-primary);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }

        .btn-block {
            width: 100%;
        }

        .login-footer {
            text-align: center;
            margin-top: 20px;
            color: var(--gray);
            font-size: 13px;
        }

        .login-error {
            background: #f8d7da;
            color: #721c24;
            padding: 12px;
            border-radius: 6px;
            font-size: 14px;
            display: none;
            align-items: center;
            gap: 10px;
        }

        .device-info {
            background: #e8f4fd;
            padding: 15px;
            border-radius: 8px;
            margin-top: 20px;
            font-size: 13px;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        /* Main App */
        .app-container {
            display: none;
            width: 100%;
            max-width: 1400px;
            background: white;
            border-radius: var(--radius);
            box-shadow: var(--shadow-lg);
            overflow: hidden;
            min-height: calc(100vh - 40px);
            flex-direction: column;
        }

        .app-header {
            background: var(--gradient-primary);
            color: white;
            padding: 20px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
        }

        .logo-section {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-icon {
            font-size: 32px;
            background: rgba(255,255,255,0.2);
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .logo-text h1 {
            font-size: 24px;
            font-weight: 700;
        }

        .logo-text p {
            opacity: 0.9;
            font-size: 14px;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: white;
            color: var(--primary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
            font-size: 18px;
        }

        .user-name {
            font-weight: 600;
        }

        .logout-btn {
            background: rgba(255,255,255,0.2);
            border: 1px solid rgba(255,255,255,0.3);
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .logout-btn:hover {
            background: rgba(255,255,255,0.3);
        }

        .app-nav {
            background: var(--light);
            padding: 15px 30px;
            display: flex;
            gap: 10px;
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            scrollbar-width: none;
        }

        .app-nav::-webkit-scrollbar {
            display: none;
        }

        .nav-btn {
            padding: 12px 25px;
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            color: var(--dark);
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s;
            white-space: nowrap;
            flex-shrink: 0;
        }

        .nav-btn:hover {
            border-color: var(--primary);
            color: var(--primary);
            transform: translateY(-2px);
        }

        .nav-btn.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
            box-shadow: var(--shadow);
        }

        .app-main {
            flex: 1;
            padding: 30px;
            overflow-y: auto;
            background: #f8f9fa;
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.3s;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Dashboard */
        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .dashboard-title {
            font-size: 24px;
            font-weight: 700;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .period-selector {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .period-btn {
            padding: 8px 15px;
            border: 1px solid #ddd;
            background: white;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s;
        }

        .period-btn.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
        }

        /* Stats Grid */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .stat-card {
            background: white;
            border-radius: var(--radius);
            padding: 20px;
            box-shadow: var(--shadow);
            border: 1px solid #e0e0e0;
            transition: transform 0.3s;
            position: relative;
            overflow: hidden;
        }

        .stat-card:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow-lg);
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: var(--primary);
        }

        .stat-card.lensa::before { background: #3498db; }
        .stat-card.operasional::before { background: #2ecc71; }
        .stat-card.total::before { background: #9b59b6; }
        .stat-card.periodik::before { background: #e74c3c; }

        .stat-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 15px;
        }

        .stat-icon {
            font-size: 28px;
            width: 50px;
            height: 50px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
        }

        .stat-icon.lensa { background: var(--gradient-primary); }
        .stat-icon.operasional { background: var(--gradient-success); }
        .stat-icon.total { background: linear-gradient(135deg, #9b59b6 0%, #8e44ad 100%); }
        .stat-icon.periodik { background: var(--gradient-danger); }

        .trend {
            display: flex;
            align-items: center;
            gap: 5px;
            font-size: 14px;
            font-weight: 600;
            padding: 4px 10px;
            border-radius: 20px;
            background: #f8f9fa;
        }

        .trend.up { color: #27ae60; background: #e8f5e9; }
        .trend.down { color: #e74c3c; background: #fdedec; }

        .stat-title {
            font-size: 14px;
            color: var(--gray);
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 5px;
        }

        .stat-value {
            font-size: 28px;
            font-weight: 800;
            color: var(--dark);
            margin: 10px 0;
        }

        .stat-details {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid #eee;
        }

        .stat-detail-item {
            display: flex;
            flex-direction: column;
        }

        .detail-label {
            font-size: 12px;
            color: var(--gray);
            margin-bottom: 5px;
        }

        .detail-value {
            font-size: 16px;
            font-weight: 600;
            color: var(--dark);
        }

        /* Charts Section - UKURAN STANDAR */
        .charts-section {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 20px;
            margin: 25px 0;
        }

        .chart-card {
            background: white;
            border-radius: var(--radius);
            padding: 20px;
            box-shadow: var(--shadow);
            height: 300px; /* Tinggi standar untuk chart */
        }

        .chart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            height: 40px;
        }

        .chart-title {
            font-size: 16px;
            font-weight: 700;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .chart-legend {
            display: flex;
            gap: 12px;
            font-size: 12px;
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .legend-color {
            width: 10px;
            height: 10px;
            border-radius: 2px;
        }

        /* Chart Container */
        .chart-container {
            height: 220px; /* Tinggi chart yang optimal */
            width: 100%;
            position: relative;
        }

        /* Periodik Cards */
        .periodik-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
            margin: 25px 0;
        }

        .periodik-card {
            background: white;
            border-radius: var(--radius);
            padding: 20px;
            text-align: center;
            box-shadow: var(--shadow);
            border: 2px solid transparent;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }

        .periodik-card:hover {
            border-color: var(--primary);
            transform: translateY(-3px);
        }

        .periodik-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
        }

        .periodik-card.harian::before { background: #3498db; }
        .periodik-card.mingguan::before { background: #9b59b6; }
        .periodik-card.bulanan::before { background: #2ecc71; }
        .periodik-card.tahunan::before { background: #e74c3c; }

        .periodik-icon {
            font-size: 28px;
            margin-bottom: 10px;
            color: var(--primary);
        }

        .periodik-value {
            font-size: 24px;
            font-weight: 800;
            color: var(--dark);
            margin: 8px 0;
        }

        .periodik-label {
            font-size: 13px;
            color: var(--gray);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            font-weight: 600;
        }

        .periodik-change {
            font-size: 11px;
            margin-top: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 5px;
        }

        /* Forms */
        .form-container {
            background: white;
            border-radius: var(--radius);
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: var(--shadow);
        }

        .form-title {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 20px;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 10px;
            padding-bottom: 15px;
            border-bottom: 2px solid #f0f0f0;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
        }

        .form-label {
            font-weight: 600;
            margin-bottom: 6px;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .form-input, .form-select {
            padding: 10px 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
            transition: all 0.3s;
        }

        .form-input:focus, .form-select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
        }

        .form-actions {
            display: flex;
            gap: 12px;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #eee;
        }

        /* Buttons */
        .btn-success {
            background: var(--gradient-success);
            color: white;
        }

        .btn-warning {
            background: var(--gradient-warning);
            color: white;
        }

        .btn-danger {
            background: var(--gradient-danger);
            color: white;
        }

        .btn-secondary {
            background: #6c757d;
            color: white;
        }

        .btn-sm {
            padding: 8px 15px;
            font-size: 14px;
        }

        /* Tables */
        .table-container {
            background: white;
            border-radius: var(--radius);
            padding: 20px;
            box-shadow: var(--shadow);
            overflow-x: auto;
        }

        .table-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            flex-wrap: wrap;
            gap: 12px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 800px;
        }

        th {
            background: #f8f9fa;
            padding: 12px;
            text-align: left;
            font-weight: 600;
            color: var(--dark);
            border-bottom: 2px solid #dee2e6;
            font-size: 13px;
            position: sticky;
            top: 0;
        }

        td {
            padding: 12px;
            border-bottom: 1px solid #eee;
            font-size: 13px;
        }

        tr:hover {
            background: #f8f9fa;
        }

        .badge {
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.3px;
        }

        .badge-success {
            background: #d4edda;
            color: #155724;
        }

        .badge-danger {
            background: #f8d7da;
            color: #721c24;
        }

        .badge-primary { background: #d6eaf8; color: #154360; }
        .badge-warning { background: #fef5e7; color: #7d6608; }

        /* Action buttons */
        .action-buttons {
            display: flex;
            gap: 5px;
        }

        .btn-icon {
            width: 30px;
            height: 30px;
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: none;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 13px;
        }

        .btn-icon-edit {
            background: #fff3cd;
            color: #856404;
        }

        .btn-icon-delete {
            background: #f8d7da;
            color: #721c24;
        }

        .btn-icon:hover {
            transform: scale(1.1);
        }

        /* Sync Status */
        .sync-status {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 8px 12px;
            background: #e8f4fd;
            border-radius: 8px;
            font-size: 13px;
            margin-bottom: 15px;
        }

        .sync-btn {
            background: var(--primary);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 13px;
            display: flex;
            align-items: center;
            gap: 6px;
            transition: all 0.3s;
        }

        .sync-btn:hover {
            background: var(--primary-dark);
        }

        /* Loading */
        .loading {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            z-index: 9999;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            color: white;
        }

        .loading.active {
            display: flex;
        }

        .spinner {
            width: 50px;
            height: 50px;
            border: 5px solid #f3f3f3;
            border-top: 5px solid var(--primary);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-bottom: 15px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Footer */
        .app-footer {
            text-align: center;
            padding: 15px;
            color: var(--gray);
            font-size: 13px;
            border-top: 1px solid #eee;
            background: var(--light);
        }

        /* Responsive */
        @media (max-width: 992px) {
            .charts-section {
                grid-template-columns: 1fr;
            }
            
            .chart-card {
                min-width: 100%;
            }
        }

        @media (max-width: 768px) {
            body {
                padding: 10px;
            }

            .app-header {
                flex-direction: column;
                text-align: center;
                padding: 15px;
            }

            .user-info {
                flex-direction: column;
                gap: 10px;
            }

            .app-nav {
                padding: 10px 15px;
            }

            .nav-btn {
                padding: 10px 15px;
                font-size: 13px;
            }

            .app-main {
                padding: 20px;
            }

            .dashboard-header {
                flex-direction: column;
                align-items: stretch;
            }

            .form-grid {
                grid-template-columns: 1fr;
            }

            .form-actions {
                flex-direction: column;
            }

            .btn {
                width: 100%;
                justify-content: center;
            }

            .stats-grid {
                grid-template-columns: 1fr;
            }

            .periodik-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (max-width: 480px) {
            .login-container {
                padding: 25px;
            }

            .periodik-grid {
                grid-template-columns: 1fr;
            }

            .chart-legend {
                flex-direction: column;
                gap: 5px;
            }
            
            .charts-section {
                grid-template-columns: 1fr;
            }
            
            .chart-card {
                height: 280px;
            }
            
            .chart-container {
                height: 200px;
            }
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb {
            background: var(--primary);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--primary-dark);
        }
    </style>
</head>
<body>
    <!-- Login Screen -->
    <div class="login-container" id="loginContainer">
        <div class="login-header">
            <div class="login-icon">
                <i class="fas fa-lock"></i>
            </div>
            <h1 class="login-title">Pencatatan Keuangan Pro</h1>
            <p class="login-subtitle">Login untuk mengakses data keuangan Anda</p>
        </div>

        <div class="login-error" id="loginError">
            <i class="fas fa-exclamation-circle"></i>
            <span id="errorMessage">Username atau password salah</span>
        </div>

        <form class="login-form" id="loginForm">
            <div class="form-group">
                <label class="form-label" for="username">
                    <i class="fas fa-user"></i> Username
                </label>
                <input type="text" class="form-input" id="username" 
                       placeholder="Masukkan username" required>
            </div>

            <div class="form-group">
                <label class="form-label" for="password">
                    <i class="fas fa-key"></i> Password
                </label>
                <input type="password" class="form-input" id="password" 
                       placeholder="Masukkan password" required>
            </div>

            <button type="submit" class="btn btn-primary btn-block">
                <i class="fas fa-sign-in-alt"></i> Login
            </button>
        </form>

        <div class="device-info">
            <i class="fas fa-info-circle"></i>
            <span>Data tersimpan di cloud. Bisa diakses dari device manapun dengan login yang sama.</span>
        </div>

        <div class="login-footer">
            <p>Belum punya akun? Register otomatis dengan username & password pertama</p>
        </div>
    </div>

    <!-- Main App (Hidden until login) -->
    <div class="app-container" id="appContainer">
        <!-- Header -->
        <header class="app-header">
            <div class="logo-section">
                <div class="logo-icon">
                    <i class="fas fa-chart-line"></i>
                </div>
                <div class="logo-text">
                    <h1>Pencatatan Keuangan Pro</h1>
                    <p>Dashboard Lengkap & Multi-Device Sync</p>
                </div>
            </div>

            <div class="user-info">
                <div class="user-avatar" id="userAvatar">U</div>
                <div>
                    <div class="user-name" id="userName">User</div>
                    <div style="font-size: 11px; opacity: 0.8;" id="lastSync">Sync: -</div>
                </div>
                <button class="logout-btn" onclick="logout()">
                    <i class="fas fa-sign-out-alt"></i> Logout
                </button>
            </div>
        </header>

        <!-- Navigation -->
        <nav class="app-nav">
            <button class="nav-btn active" data-tab="dashboard">
                <i class="fas fa-tachometer-alt"></i> Dashboard
            </button>
            <button class="nav-btn" data-tab="lensa">
                <i class="fas fa-camera"></i> Dana Lensa
            </button>
            <button class="nav-btn" data-tab="operasional">
                <i class="fas fa-cogs"></i> Dana Operasional
            </button>
            <button class="nav-btn" data-tab="periodik">
                <i class="fas fa-calendar-alt"></i> Pengeluaran Periodik
            </button>
            <button class="nav-btn" data-tab="laporan">
                <i class="fas fa-file-excel"></i> Laporan
            </button>
            <button class="nav-btn" data-tab="sync">
                <i class="fas fa-sync-alt"></i> Sync
            </button>
        </nav>

        <!-- Loading Overlay -->
        <div class="loading" id="loading">
            <div class="spinner"></div>
            <div id="loadingText">Memuat...</div>
        </div>

        <!-- Main Content -->
        <main class="app-main">
            <!-- Sync Status -->
            <div class="sync-status" id="syncStatus">
                <i class="fas fa-cloud"></i>
                <span id="syncMessage">Mode offline - Data disimpan lokal</span>
                <button class="sync-btn" onclick="manualSync()">
                    <i class="fas fa-sync-alt"></i> Sync Sekarang
                </button>
            </div>

            <!-- Dashboard Tab -->
            <div id="dashboard" class="tab-content active">
                <div class="dashboard-header">
                    <h2 class="dashboard-title">
                        <i class="fas fa-chart-pie"></i> Dashboard Keuangan
                    </h2>
                    <div class="period-selector">
                        <button class="period-btn active" data-period="month">Bulan Ini</button>
                        <button class="period-btn" data-period="year">Tahun Ini</button>
                        <button class="period-btn" data-period="all">Semua</button>
                    </div>
                </div>

                <!-- Stats Grid -->
                <div class="stats-grid">
                    <div class="stat-card lensa">
                        <div class="stat-header">
                            <div>
                                <div class="stat-title">Dana Pembelanjaan Lensa</div>
                                <div class="stat-value" id="saldoLensa">Rp 0</div>
                            </div>
                            <div class="stat-icon lensa">
                                <i class="fas fa-camera"></i>
                            </div>
                        </div>
                        <div class="stat-details">
                            <div class="stat-detail-item">
                                <div class="detail-label">Pemasukan</div>
                                <div class="detail-value" id="pemasukanLensa">Rp 0</div>
                            </div>
                            <div class="stat-detail-item">
                                <div class="detail-label">Pengeluaran</div>
                                <div class="detail-value" id="pengeluaranLensa">Rp 0</div>
                            </div>
                        </div>
                    </div>

                    <div class="stat-card operasional">
                        <div class="stat-header">
                            <div>
                                <div class="stat-title">Dana Operasional</div>
                                <div class="stat-value" id="saldoOperasional">Rp 0</div>
                            </div>
                            <div class="stat-icon operasional">
                                <i class="fas fa-cogs"></i>
                            </div>
                        </div>
                        <div class="stat-details">
                            <div class="stat-detail-item">
                                <div class="detail-label">Pemasukan</div>
                                <div class="detail-value" id="pemasukanOperasional">Rp 0</div>
                            </div>
                            <div class="stat-detail-item">
                                <div class="detail-label">Pengeluaran</div>
                                <div class="detail-value" id="pengeluaranOperasional">Rp 0</div>
                            </div>
                        </div>
                    </div>

                    <div class="stat-card total">
                        <div class="stat-header">
                            <div>
                                <div class="stat-title">Total Saldo</div>
                                <div class="stat-value" id="totalSaldo">Rp 0</div>
                            </div>
                            <div class="stat-icon total">
                                <i class="fas fa-wallet"></i>
                            </div>
                        </div>
                        <div class="stat-details">
                            <div class="stat-detail-item">
                                <div class="detail-label">Perubahan</div>
                                <div class="detail-value" id="saldoChange">Rp 0</div>
                            </div>
                            <div class="stat-detail-item">
                                <div class="detail-label">Bulan Ini</div>
                                <div class="detail-value" id="saldoBulanIni">Rp 0</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Charts Section - UKURAN STANDAR -->
                <div class="charts-section">
                    <div class="chart-card">
                        <div class="chart-header">
                            <h3 class="chart-title">
                                <i class="fas fa-chart-pie"></i> Distribusi Keuangan
                            </h3>
                            <div class="chart-legend">
                                <div class="legend-item">
                                    <div class="legend-color" style="background: #3498db;"></div>
                                    <span>Lensa</span>
                                </div>
                                <div class="legend-item">
                                    <div class="legend-color" style="background: #2ecc71;"></div>
                                    <span>Operasional</span>
                                </div>
                            </div>
                        </div>
                        <div class="chart-container">
                            <canvas id="distributionChart"></canvas>
                        </div>
                    </div>

                    <div class="chart-card">
                        <div class="chart-header">
                            <h3 class="chart-title">
                                <i class="fas fa-chart-line"></i> Trend Bulanan
                            </h3>
                            <div class="chart-legend">
                                <div class="legend-item">
                                    <div class="legend-color" style="background: #27ae60;"></div>
                                    <span>Pemasukan</span>
                                </div>
                                <div class="legend-item">
                                    <div class="legend-color" style="background: #e74c3c;"></div>
                                    <span>Pengeluaran</span>
                                </div>
                            </div>
                        </div>
                        <div class="chart-container">
                            <canvas id="trendChart"></canvas>
                        </div>
                    </div>
                </div>

                <!-- Periodik Cards -->
                <div style="margin-top: 25px;">
                    <h3 class="dashboard-title" style="margin-bottom: 15px;">
                        <i class="fas fa-calendar-alt"></i> Pengeluaran Periodik
                    </h3>
                    <div class="periodik-grid">
                        <div class="periodik-card harian">
                            <div class="periodik-icon">
                                <i class="fas fa-calendar-day"></i>
                            </div>
                            <div class="periodik-value" id="pengeluaranHarian">Rp 0</div>
                            <div class="periodik-label">Harian</div>
                            <div class="periodik-change" id="changeHarian">
                                <i class="fas fa-arrow-up"></i> 0%
                            </div>
                        </div>

                        <div class="periodik-card mingguan">
                            <div class="periodik-icon">
                                <i class="fas fa-calendar-week"></i>
                            </div>
                            <div class="periodik-value" id="pengeluaranMingguan">Rp 0</div>
                            <div class="periodik-label">Mingguan</div>
                            <div class="periodik-change" id="changeMingguan">
                                <i class="fas fa-arrow-up"></i> 0%
                            </div>
                        </div>

                        <div class="periodik-card bulanan">
                            <div class="periodik-icon">
                                <i class="fas fa-calendar"></i>
                            </div>
                            <div class="periodik-value" id="pengeluaranBulanan">Rp 0</div>
                            <div class="periodik-label">Bulanan</div>
                            <div class="periodik-change" id="changeBulanan">
                                <i class="fas fa-arrow-up"></i> 0%
                            </div>
                        </div>

                        <div class="periodik-card tahunan">
                            <div class="periodik-icon">
                                <i class="fas fa-calendar-check"></i>
                            </div>
                            <div class="periodik-value" id="pengeluaranTahunan">Rp 0</div>
                            <div class="periodik-label">Tahunan</div>
                            <div class="periodik-change" id="changeTahunan">
                                <i class="fas fa-arrow-up"></i> 0%
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Dana Lensa Tab -->
            <div id="lensa" class="tab-content">
                <div class="form-container">
                    <h3 class="form-title">
                        <i class="fas fa-plus-circle"></i> Tambah Transaksi Dana Lensa
                    </h3>
                    <form id="formLensa">
                        <div class="form-grid">
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-exchange-alt"></i> Jenis Transaksi
                                </label>
                                <select class="form-select" id="lensaJenis" required>
                                    <option value="Masuk">Pemasukan</option>
                                    <option value="Keluar">Pengeluaran</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-tag"></i> Kategori
                                </label>
                                <select class="form-select" id="lensaKategori">
                                    <option value="">Pilih Kategori</option>
                                    <option value="Penjualan">Penjualan Lensa</option>
                                    <option value="Beli">Pembelian Lensa</option>
                                    <option value="Servis">Servis Lensa</option>
                                    <option value="Aksesoris">Aksesoris</option>
                                    <option value="Lainnya">Lainnya</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-sticky-note"></i> Keterangan
                                </label>
                                <input type="text" class="form-input" id="lensaKeterangan" 
                                       placeholder="Contoh: Beli lensa 50mm f/1.8" required>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-money-bill-wave"></i> Nominal (Rp)
                                </label>
                                <input type="number" class="form-input" id="lensaNominal" 
                                       placeholder="100000" min="1" required>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-calendar"></i> Tanggal
                                </label>
                                <input type="date" class="form-input" id="lensaTanggal" required>
                            </div>
                        </div>
                        <div class="form-actions">
                            <button type="submit" class="btn btn-primary">
                                <i class="fas fa-save"></i> Simpan Transaksi
                            </button>
                            <button type="button" class="btn btn-secondary" onclick="resetForm('lensa')">
                                <i class="fas fa-redo"></i> Reset
                            </button>
                        </div>
                    </form>
                </div>

                <!-- Data Table -->
                <div class="table-container">
                    <div class="table-header">
                        <h3 style="margin: 0;">
                            <i class="fas fa-history"></i> Riwayat Transaksi Dana Lensa
                            <span id="lensaCount" style="font-size: 13px; color: #666; margin-left: 8px;">
                                (0 transaksi)
                            </span>
                        </h3>
                        <div style="display: flex; gap: 8px;">
                            <button class="btn btn-success btn-sm" onclick="exportExcel('lensa')">
                                <i class="fas fa-file-excel"></i> Export Excel
                            </button>
                            <button class="btn btn-warning btn-sm" onclick="loadLensaData()">
                                <i class="fas fa-sync-alt"></i> Refresh
                            </button>
                        </div>
                    </div>
                    <table>
                        <thead>
                            <tr>
                                <th>Tanggal</th>
                                <th>Jenis</th>
                                <th>Kategori</th>
                                <th>Keterangan</th>
                                <th>Nominal</th>
                                <th>Saldo</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="lensaTableBody">
                            <!-- Data akan dimuat disini -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Dana Operasional Tab -->
            <div id="operasional" class="tab-content">
                <div class="form-container">
                    <h3 class="form-title">
                        <i class="fas fa-plus-circle"></i> Tambah Transaksi Dana Operasional
                    </h3>
                    <form id="formOperasional">
                        <div class="form-grid">
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-exchange-alt"></i> Jenis Transaksi
                                </label>
                                <select class="form-select" id="operasionalJenis" required>
                                    <option value="Masuk">Dana Masuk</option>
                                    <option value="Keluar">Dana Keluar</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-tag"></i> Kategori
                                </label>
                                <select class="form-select" id="operasionalKategori">
                                    <option value="">Pilih Kategori</option>
                                    <option value="Gaji">Gaji</option>
                                    <option value="Listrik">Listrik</option>
                                    <option value="Internet">Internet</option>
                                    <option value="Sewa">Sewa Tempat</option>
                                    <option value="Transport">Transportasi</option>
                                    <option value="Lainnya">Lainnya</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-sticky-note"></i> Keterangan
                                </label>
                                <input type="text" class="form-input" id="operasionalKeterangan" 
                                       placeholder="Contoh: Bayar listrik bulan Januari" required>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-money-bill-wave"></i> Nominal (Rp)
                                </label>
                                <input type="number" class="form-input" id="operasionalNominal" 
                                       placeholder="500000" min="1" required>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-calendar"></i> Tanggal
                                </label>
                                <input type="date" class="form-input" id="operasionalTanggal" required>
                            </div>
                        </div>
                        <div class="form-actions">
                            <button type="submit" class="btn btn-primary">
                                <i class="fas fa-save"></i> Simpan Transaksi
                            </button>
                            <button type="button" class="btn btn-secondary" onclick="resetForm('operasional')">
                                <i class="fas fa-redo"></i> Reset
                            </button>
                        </div>
                    </form>
                </div>

                <!-- Data Table -->
                <div class="table-container">
                    <div class="table-header">
                        <h3 style="margin: 0;">
                            <i class="fas fa-history"></i> Riwayat Transaksi Dana Operasional
                            <span id="operasionalCount" style="font-size: 13px; color: #666; margin-left: 8px;">
                                (0 transaksi)
                            </span>
                        </h3>
                        <div style="display: flex; gap: 8px;">
                            <button class="btn btn-success btn-sm" onclick="exportExcel('operasional')">
                                <i class="fas fa-file-excel"></i> Export Excel
                            </button>
                            <button class="btn btn-warning btn-sm" onclick="loadOperasionalData()">
                                <i class="fas fa-sync-alt"></i> Refresh
                            </button>
                        </div>
                    </div>
                    <table>
                        <thead>
                            <tr>
                                <th>Tanggal</th>
                                <th>Jenis</th>
                                <th>Kategori</th>
                                <th>Keterangan</th>
                                <th>Nominal</th>
                                <th>Saldo</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="operasionalTableBody">
                            <!-- Data akan dimuat disini -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Pengeluaran Periodik Tab -->
            <div id="periodik" class="tab-content">
                <div class="form-container">
                    <h3 class="form-title">
                        <i class="fas fa-plus-circle"></i> Tambah Pengeluaran Periodik
                    </h3>
                    <form id="formPeriodik">
                        <div class="form-grid">
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-calendar-alt"></i> Periode
                                </label>
                                <select class="form-select" id="periodikPeriode" required>
                                    <option value="Harian">Harian</option>
                                    <option value="Mingguan">Mingguan</option>
                                    <option value="Bulanan">Bulanan</option>
                                    <option value="Tahunan">Tahunan</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-sticky-note"></i> Keterangan
                                </label>
                                <input type="text" class="form-input" id="periodikKeterangan" 
                                       placeholder="Contoh: Makan siang harian" required>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-money-bill-wave"></i> Nominal (Rp)
                                </label>
                                <input type="number" class="form-input" id="periodikNominal" 
                                       placeholder="50000" min="1" required>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-calendar"></i> Tanggal
                                </label>
                                <input type="date" class="form-input" id="periodikTanggal" required>
                            </div>
                        </div>
                        <div class="form-actions">
                            <button type="submit" class="btn btn-primary">
                                <i class="fas fa-save"></i> Simpan Pengeluaran
                            </button>
                            <button type="button" class="btn btn-secondary" onclick="resetForm('periodik')">
                                <i class="fas fa-redo"></i> Reset
                            </button>
                        </div>
                    </form>
                </div>

                <!-- Data Table -->
                <div class="table-container">
                    <div class="table-header">
                        <h3 style="margin: 0;">
                            <i class="fas fa-history"></i> Riwayat Pengeluaran Periodik
                            <span id="periodikCount" style="font-size: 13px; color: #666; margin-left: 8px;">
                                (0 data)
                            </span>
                        </h3>
                        <div style="display: flex; gap: 8px;">
                            <button class="btn btn-success btn-sm" onclick="exportExcel('periodik')">
                                <i class="fas fa-file-excel"></i> Export Excel
                            </button>
                            <button class="btn btn-warning btn-sm" onclick="loadPeriodikData()">
                                <i class="fas fa-sync-alt"></i> Refresh
                            </button>
                        </div>
                    </div>
                    <table>
                        <thead>
                            <tr>
                                <th>Tanggal</th>
                                <th>Periode</th>
                                <th>Keterangan</th>
                                <th>Nominal</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="periodikTableBody">
                            <!-- Data akan dimuat disini -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Laporan Tab -->
            <div id="laporan" class="tab-content">
                <div class="form-container">
                    <h3 class="form-title">
                        <i class="fas fa-file-excel"></i> Export Laporan Excel
                    </h3>
                    
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px; margin-top: 15px;">
                        <div class="stat-card" style="text-align: center;">
                            <div class="stat-icon lensa" style="margin: 0 auto 10px;">
                                <i class="fas fa-camera"></i>
                            </div>
                            <h4 style="margin-bottom: 8px; font-size: 16px;">Laporan Dana Lensa</h4>
                            <p style="color: #666; margin-bottom: 12px; font-size: 13px;">Export semua transaksi dana lensa</p>
                            <button class="btn btn-success btn-sm" onclick="exportExcel('lensa')">
                                <i class="fas fa-download"></i> Download Excel
                            </button>
                        </div>

                        <div class="stat-card" style="text-align: center;">
                            <div class="stat-icon operasional" style="margin: 0 auto 10px;">
                                <i class="fas fa-cogs"></i>
                            </div>
                            <h4 style="margin-bottom: 8px; font-size: 16px;">Laporan Dana Operasional</h4>
                            <p style="color: #666; margin-bottom: 12px; font-size: 13px;">Export semua transaksi dana operasional</p>
                            <button class="btn btn-success btn-sm" onclick="exportExcel('operasional')">
                                <i class="fas fa-download"></i> Download Excel
                            </button>
                        </div>

                        <div class="stat-card" style="text-align: center;">
                            <div class="stat-icon total" style="margin: 0 auto 10px;">
                                <i class="fas fa-calendar-alt"></i>
                            </div>
                            <h4 style="margin-bottom: 8px; font-size: 16px;">Laporan Periodik</h4>
                            <p style="color: #666; margin-bottom: 12px; font-size: 13px;">Export pengeluaran periodik</p>
                            <button class="btn btn-success btn-sm" onclick="exportExcel('periodik')">
                                <i class="fas fa-download"></i> Download Excel
                            </button>
                        </div>

                        <div class="stat-card" style="text-align: center;">
                            <div class="stat-icon periodik" style="margin: 0 auto 10px;">
                                <i class="fas fa-chart-pie"></i>
                            </div>
                            <h4 style="margin-bottom: 8px; font-size: 16px;">Laporan Lengkap</h4>
                            <p style="color: #666; margin-bottom: 12px; font-size: 13px;">Export semua data dalam satu file</p>
                            <button class="btn btn-primary btn-sm" onclick="exportAllExcel()">
                                <i class="fas fa-file-excel"></i> Download Semua
                            </button>
                        </div>
                    </div>

                    <!-- Filter Section -->
                    <div style="margin-top: 25px; padding-top: 20px; border-top: 1px solid #eee;">
                        <h4 style="margin-bottom: 15px; font-size: 16px;">
                            <i class="fas fa-filter"></i> Filter Laporan
                        </h4>
                        <div class="form-grid">
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-calendar"></i> Dari Tanggal
                                </label>
                                <input type="date" class="form-input" id="filterStartDate">
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-calendar"></i> Sampai Tanggal
                                </label>
                                <input type="date" class="form-input" id="filterEndDate">
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <i class="fas fa-tag"></i> Kategori
                                </label>
                                <select class="form-select" id="filterCategory">
                                    <option value="">Semua Kategori</option>
                                    <option value="Penjualan">Penjualan</option>
                                    <option value="Beli">Pembelian</option>
                                    <option value="Servis">Servis</option>
                                    <option value="Gaji">Gaji</option>
                                    <option value="Listrik">Listrik</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-actions">
                            <button class="btn btn-info btn-sm" onclick="exportFiltered()">
                                <i class="fas fa-filter"></i> Export dengan Filter
                            </button>
                            <button class="btn btn-secondary btn-sm" onclick="printReport()">
                                <i class="fas fa-print"></i> Cetak Laporan
                            </button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Sync Tab -->
            <div id="sync" class="tab-content">
                <div class="form-container">
                    <h3 class="form-title">
                        <i class="fas fa-sync-alt"></i> Sync & Backup Data
                    </h3>

                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px; margin-top: 15px;">
                        <div class="stat-card" style="text-align: center;">
                            <div class="stat-icon lensa" style="margin: 0 auto 10px; background: var(--gradient-primary);">
                                <i class="fas fa-cloud-upload-alt"></i>
                            </div>
                            <h4 style="margin-bottom: 8px; font-size: 16px;">Backup ke Cloud</h4>
                            <p style="color: #666; margin-bottom: 12px; font-size: 13px;">
                                Simpan data Anda ke cloud untuk akses multi-device
                            </p>
                            <button class="btn btn-primary btn-sm" onclick="backupToCloud()">
                                <i class="fas fa-cloud"></i> Backup Sekarang
                            </button>
                        </div>

                        <div class="stat-card" style="text-align: center;">
                            <div class="stat-icon operasional" style="margin: 0 auto 10px; background: var(--gradient-success);">
                                <i class="fas fa-cloud-download-alt"></i>
                            </div>
                            <h4 style="margin-bottom: 8px; font-size: 16px;">Restore dari Cloud</h4>
                            <p style="color: #666; margin-bottom: 12px; font-size: 13px;">
                                Muat data dari cloud ke device ini
                            </p>
                            <button class="btn btn-success btn-sm" onclick="restoreFromCloud()">
                                <i class="fas fa-download"></i> Restore Data
                            </button>
                        </div>

                        <div class="stat-card" style="text-align: center;">
                            <div class="stat-icon total" style="margin: 0 auto 10px; background: var(--gradient-warning);">
                                <i class="fas fa-file-export"></i>
                            </div>
                            <h4 style="margin-bottom: 8px; font-size: 16px;">Export Backup File</h4>
                            <p style="color: #666; margin-bottom: 12px; font-size: 13px;">
                                Simpan backup sebagai file JSON
                            </p>
                            <button class="btn btn-warning btn-sm" onclick="exportBackupFile()">
                                <i class="fas fa-save"></i> Export File
                            </button>
                        </div>

                        <div class="stat-card" style="text-align: center;">
                            <div class="stat-icon periodik" style="margin: 0 auto 10px; background: var(--gradient-danger);">
                                <i class="fas fa-file-import"></i>
                            </div>
                            <h4 style="margin-bottom: 8px; font-size: 16px;">Import Backup File</h4>
                            <p style="color: #666; margin-bottom: 12px; font-size: 13px;">
                                Muat data dari file backup
                            </p>
                            <input type="file" id="importFile" accept=".json" style="display: none;" onchange="importBackupFile(event)">
                            <button class="btn btn-danger btn-sm" onclick="document.getElementById('importFile').click()">
                                <i class="fas fa-upload"></i> Import File
                            </button>
                        </div>
                    </div>

                    <!-- Sync Info -->
                    <div style="background: #e8f4fd; padding: 15px; border-radius: 8px; margin-top: 25px;">
                        <h4 style="margin-bottom: 12px; color: var(--primary); font-size: 15px;">
                            <i class="fas fa-info-circle"></i> Informasi Sync
                        </h4>
                        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 12px;">
                            <div>
                                <div style="font-size: 12px; color: #666;">Status Sync</div>
                                <div style="font-size: 14px; font-weight: 600; color: var(--success);" id="syncStatusInfo">Aktif</div>
                            </div>
                            <div>
                                <div style="font-size: 12px; color: #666;">Terakhir Sync</div>
                                <div style="font-size: 14px; font-weight: 600;" id="lastSyncInfo">-</div>
                            </div>
                            <div>
                                <div style="font-size: 12px; color: #666;">Data di Cloud</div>
                                <div style="font-size: 14px; font-weight: 600;" id="cloudDataInfo">0 transaksi</div>
                            </div>
                            <div>
                                <div style="font-size: 12px; color: #666;">Data Lokal</div>
                                <div style="font-size: 14px; font-weight: 600;" id="localDataInfo">0 transaksi</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>

        <!-- Footer -->
        <footer class="app-footer">
            <p>
                &copy; 2023 Pencatatan Keuangan Pro | 
                <i class="fas fa-cloud"></i> Cloud Sync | 
                <i class="fas fa-chart-line"></i> Dashboard Interaktif | 
                <i class="fas fa-mobile-alt"></i> Multi-Device Support
            </p>
        </footer>
    </div>

    <script>
        // ============================================
        // KONSTANTA & VARIABEL GLOBAL
        // ============================================
        const STORAGE_KEYS = {
            LENSA: 'keuangan_dana_lensa',
            OPERASIONAL: 'keuangan_dana_operasional',
            PERIODIK: 'keuangan_pengeluaran_periodik',
            USER_DATA: 'keuangan_user_data',
            CLOUD_BACKUP: 'keuangan_cloud_backup',
            LAST_SYNC: 'keuangan_last_sync'
        };

        let currentUser = null;
        let distributionChart = null;
        let trendChart = null;
        let isOnline = false;

        // ============================================
        // INISIALISASI APLIKASI
        // ============================================
        document.addEventListener('DOMContentLoaded', function() {
            console.log('Aplikasi Pencatatan Keuangan Pro dimulai...');
            
            // Set tanggal default
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('lensaTanggal').value = today;
            document.getElementById('operasionalTanggal').value = today;
            document.getElementById('periodikTanggal').value = today;
            
            // Setup navigation
            setupNavigation();
            
            // Setup forms
            setupForms();
            
            // Setup period selector
            setupPeriodSelector();
            
            // Check if user is already logged in
            checkAutoLogin();
            
            // Check online status
            checkOnlineStatus();
        });

        // ============================================
        // SETUP FUNCTIONS
        // ============================================
        function setupNavigation() {
            const navButtons = document.querySelectorAll('.nav-btn');
            navButtons.forEach(button => {
                button.addEventListener('click', function() {
                    // Remove active class from all buttons
                    navButtons.forEach(btn => btn.classList.remove('active'));
                    
                    // Add active class to clicked button
                    this.classList.add('active');
                    
                    // Hide all tab contents
                    document.querySelectorAll('.tab-content').forEach(tab => {
                        tab.classList.remove('active');
                    });
                    
                    // Show selected tab content
                    const tabId = this.getAttribute('data-tab');
                    document.getElementById(tabId).classList.add('active');
                });
            });
        }

        function setupForms() {
            // Dana Lensa form
            document.getElementById('formLensa').addEventListener('submit', function(e) {
                e.preventDefault();
                addTransaction('lensa');
            });

            // Dana Operasional form
            document.getElementById('formOperasional').addEventListener('submit', function(e) {
                e.preventDefault();
                addTransaction('operasional');
            });

            // Pengeluaran Periodik form
            document.getElementById('formPeriodik').addEventListener('submit', function(e) {
                e.preventDefault();
                addPeriodik();
            });

            // Login form
            document.getElementById('loginForm').addEventListener('submit', function(e) {
                e.preventDefault();
                login();
            });
        }

        function setupPeriodSelector() {
            const periodButtons = document.querySelectorAll('.period-btn');
            periodButtons.forEach(button => {
                button.addEventListener('click', function() {
                    periodButtons.forEach(btn => btn.classList.remove('active'));
                    this.classList.add('active');
                    loadDashboardData(this.dataset.period);
                });
            });
        }

        // ============================================
        // AUTHENTICATION FUNCTIONS
        // ============================================
        function checkAutoLogin() {
            const userData = localStorage.getItem(STORAGE_KEYS.USER_DATA);
            if (userData) {
                currentUser = JSON.parse(userData);
                showApp();
            }
        }

        function login() {
            const username = document.getElementById('username').value.trim();
            const password = document.getElementById('password').value.trim();
            
            if (!username || !password) {
                showLoginError('Username dan password harus diisi');
                return;
            }
            
            showLoading('Memproses login...');
            
            // Simulate login process
            setTimeout(() => {
                // For demo, we'll create user if doesn't exist
                const hashedPassword = CryptoJS.SHA256(password).toString();
                
                currentUser = {
                    username: username,
                    passwordHash: hashedPassword,
                    createdAt: new Date().toISOString(),
                    lastLogin: new Date().toISOString()
                };
                
                // Save user data
                localStorage.setItem(STORAGE_KEYS.USER_DATA, JSON.stringify(currentUser));
                
                // Initialize data for new user
                if (!localStorage.getItem(STORAGE_KEYS.LENSA)) {
                    initializeUserData();
                }
                
                hideLoading();
                showApp();
            }, 1000);
        }

        function showLoginError(message) {
            const errorDiv = document.getElementById('loginError');
            const errorMsg = document.getElementById('errorMessage');
            errorMsg.textContent = message;
            errorDiv.style.display = 'flex';
            
            setTimeout(() => {
                errorDiv.style.display = 'none';
            }, 3000);
        }

        function logout() {
            if (confirm('Anda yakin ingin logout?')) {
                localStorage.removeItem(STORAGE_KEYS.USER_DATA);
                currentUser = null;
                showLogin();
            }
        }

        function showLogin() {
            document.getElementById('loginContainer').style.display = 'block';
            document.getElementById('appContainer').style.display = 'none';
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
        }

        function showApp() {
            document.getElementById('loginContainer').style.display = 'none';
            document.getElementById('appContainer').style.display = 'flex';
            
            // Update user info
            document.getElementById('userName').textContent = currentUser.username;
            document.getElementById('userAvatar').textContent = currentUser.username.charAt(0).toUpperCase();
            
            // Load data
            loadAllData();
            updateSyncInfo();
        }

        function initializeUserData() {
            saveData(STORAGE_KEYS.LENSA, []);
            saveData(STORAGE_KEYS.OPERASIONAL, []);
            saveData(STORAGE_KEYS.PERIODIK, []);
        }

        // ============================================
        // UTILITY FUNCTIONS
        // ============================================
        function showLoading(message = 'Memuat...') {
            document.getElementById('loadingText').textContent = message;
            document.getElementById('loading').classList.add('active');
        }

        function hideLoading() {
            document.getElementById('loading').classList.remove('active');
        }

        function formatRupiah(amount) {
            if (amount === undefined || amount === null || isNaN(amount)) {
                return 'Rp 0';
            }
            return 'Rp ' + Math.round(amount).toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.');
        }

        function formatDate(dateString) {
            const date = new Date(dateString);
            return date.toLocaleDateString('id-ID', {
                day: '2-digit',
                month: 'short',
                year: 'numeric'
            });
        }

        function formatDateTime(date) {
            return date.toLocaleString('id-ID', {
                day: '2-digit',
                month: 'short',
                year: 'numeric',
                hour: '2-digit',
                minute: '2-digit'
            });
        }

        function showMessage(message, type = 'success') {
            // Create message element
            const messageDiv = document.createElement('div');
            const bgColor = type === 'success' ? '#27ae60' : type === 'error' ? '#e74c3c' : '#f39c12';
            const icon = type === 'success' ? 'check-circle' : type === 'error' ? 'exclamation-circle' : 'info-circle';
            
            messageDiv.innerHTML = `
                <div style="position: fixed; top: 20px; right: 20px; background: ${bgColor}; 
                     color: white; padding: 12px 15px; border-radius: 6px; box-shadow: 0 5px 15px rgba(0,0,0,0.2); 
                     z-index: 10000; display: flex; align-items: center; gap: 8px; animation: slideIn 0.3s;">
                    <i class="fas fa-${icon}"></i>
                    ${message}
                </div>
            `;
            
            document.body.appendChild(messageDiv);
            
            // Remove after 3 seconds
            setTimeout(() => {
                messageDiv.remove();
            }, 3000);
        }

        function generateId() {
            return Date.now().toString(36) + Math.random().toString(36).substr(2);
        }

        // ============================================
        // STORAGE FUNCTIONS
        // ============================================
        function getData(key) {
            const data = localStorage.getItem(key);
            return data ? JSON.parse(data) : [];
        }

        function saveData(key, data) {
            localStorage.setItem(key, JSON.stringify(data));
            localStorage.setItem(STORAGE_KEYS.LAST_SYNC, new Date().toISOString());
            updateSyncInfo();
        }

        // ============================================
        // SYNC FUNCTIONS
        // ============================================
        function checkOnlineStatus() {
            isOnline = navigator.onLine;
            updateSyncStatus();
        }

        function updateSyncStatus() {
            const syncStatus = document.getElementById('syncStatus');
            const syncMessage = document.getElementById('syncMessage');
            
            if (isOnline) {
                syncStatus.style.background = '#e8f5e9';
                syncStatus.style.color = '#155724';
                syncMessage.innerHTML = `<i class="fas fa-wifi"></i> Online - Auto-sync aktif`;
            } else {
                syncStatus.style.background = '#fff3cd';
                syncStatus.style.color = '#856404';
                syncMessage.innerHTML = `<i class="fas fa-wifi-slash"></i> Offline - Data disimpan lokal`;
            }
        }

        function updateSyncInfo() {
            const lastSync = localStorage.getItem(STORAGE_KEYS.LAST_SYNC);
            const lensaData = getData(STORAGE_KEYS.LENSA);
            const operasionalData = getData(STORAGE_KEYS.OPERASIONAL);
            const periodikData = getData(STORAGE_KEYS.PERIODIK);
            
            if (lastSync) {
                document.getElementById('lastSync').textContent = 'Sync: ' + formatDateTime(new Date(lastSync));
                document.getElementById('lastSyncInfo').textContent = formatDateTime(new Date(lastSync));
            }
            
            const totalLocal = lensaData.length + operasionalData.length + periodikData.length;
            document.getElementById('localDataInfo').textContent = totalLocal + ' transaksi';
        }

        function manualSync() {
            if (!isOnline) {
                showMessage('Tidak ada koneksi internet', 'error');
                return;
            }
            
            showLoading('Menyinkronkan data...');
            
            setTimeout(() => {
                hideLoading();
                updateSyncInfo();
                showMessage('✅ Data berhasil disinkronkan');
            }, 1500);
        }

        // ============================================
        // DATA LOADING FUNCTIONS
        // ============================================
        function loadAllData() {
            loadDashboardData('month');
            loadLensaData();
            loadOperasionalData();
            loadPeriodikData();
        }

        function loadDashboardData(period = 'month') {
            const lensaData = getData(STORAGE_KEYS.LENSA);
            const operasionalData = getData(STORAGE_KEYS.OPERASIONAL);
            const periodikData = getData(STORAGE_KEYS.PERIODIK);
            
            // Filter data based on period
            const now = new Date();
            let startDate = new Date();
            
            switch(period) {
                case 'month':
                    startDate.setMonth(now.getMonth() - 1);
                    break;
                case 'year':
                    startDate.setFullYear(now.getFullYear() - 1);
                    break;
                case 'all':
                    startDate = new Date(0);
                    break;
            }
            
            // Filter data
            const filteredLensa = lensaData.filter(item => new Date(item.tanggal) >= startDate);
            const filteredOperasional = operasionalData.filter(item => new Date(item.tanggal) >= startDate);
            const filteredPeriodik = periodikData.filter(item => new Date(item.tanggal) >= startDate);
            
            // Calculate stats
            const stats = calculateStats(filteredLensa, filteredOperasional, filteredPeriodik);
            
            // Update dashboard
            updateDashboard(stats);
            
            // Update charts
            updateCharts(stats);
        }

        function calculateStats(lensaData, operasionalData, periodikData) {
            // Calculate lensa stats
            let saldoLensa = 0;
            let pemasukanLensa = 0;
            let pengeluaranLensa = 0;
            
            lensaData.forEach(transaksi => {
                if (transaksi.jenis === 'Masuk') {
                    saldoLensa += transaksi.nominal;
                    pemasukanLensa += transaksi.nominal;
                } else {
                    saldoLensa -= transaksi.nominal;
                    pengeluaranLensa += transaksi.nominal;
                }
            });
            
            // Calculate operasional stats
            let saldoOperasional = 0;
            let pemasukanOperasional = 0;
            let pengeluaranOperasional = 0;
            
            operasionalData.forEach(transaksi => {
                if (transaksi.jenis === 'Masuk') {
                    saldoOperasional += transaksi.nominal;
                    pemasukanOperasional += transaksi.nominal;
                } else {
                    saldoOperasional -= transaksi.nominal;
                    pengeluaranOperasional += transaksi.nominal;
                }
            });
            
            // Calculate periodik stats
            const now = new Date();
            const today = new Date(now.getFullYear(), now.getMonth(), now.getDate());
            const weekAgo = new Date(today);
            weekAgo.setDate(weekAgo.getDate() - 7);
            const monthAgo = new Date(today);
            monthAgo.setMonth(monthAgo.getMonth() - 1);
            const yearAgo = new Date(today);
            yearAgo.setFullYear(yearAgo.getFullYear() - 1);
            
            let pengeluaranHarian = 0;
            let pengeluaranMingguan = 0;
            let pengeluaranBulanan = 0;
            let pengeluaranTahunan = 0;
            
            periodikData.forEach(item => {
                const tanggal = new Date(item.tanggal);
                const nominal = item.nominal;
                
                if (tanggal.toDateString() === today.toDateString()) {
                    pengeluaranHarian += nominal;
                }
                
                if (tanggal >= weekAgo) {
                    pengeluaranMingguan += nominal;
                }
                
                if (tanggal >= monthAgo) {
                    pengeluaranBulanan += nominal;
                }
                
                if (tanggal >= yearAgo) {
                    pengeluaranTahunan += nominal;
                }
            });
            
            return {
                saldoLensa,
                pemasukanLensa,
                pengeluaranLensa,
                saldoOperasional,
                pemasukanOperasional,
                pengeluaranOperasional,
                totalSaldo: saldoLensa + saldoOperasional,
                totalPemasukan: pemasukanLensa + pemasukanOperasional,
                totalPengeluaran: pengeluaranLensa + pengeluaranOperasional,
                saldoBulanIni: (pemasukanLensa + pemasukanOperasional) - (pengeluaranLensa + pengeluaranOperasional),
                pengeluaranHarian,
                pengeluaranMingguan,
                pengeluaranBulanan,
                pengeluaranTahunan
            };
        }

        function updateDashboard(stats) {
            // Update values
            document.getElementById('saldoLensa').textContent = formatRupiah(stats.saldoLensa);
            document.getElementById('pemasukanLensa').textContent = formatRupiah(stats.pemasukanLensa);
            document.getElementById('pengeluaranLensa').textContent = formatRupiah(stats.pengeluaranLensa);
            
            document.getElementById('saldoOperasional').textContent = formatRupiah(stats.saldoOperasional);
            document.getElementById('pemasukanOperasional').textContent = formatRupiah(stats.pemasukanOperasional);
            document.getElementById('pengeluaranOperasional').textContent = formatRupiah(stats.pengeluaranOperasional);
            
            document.getElementById('totalSaldo').textContent = formatRupiah(stats.totalSaldo);
            document.getElementById('saldoBulanIni').textContent = formatRupiah(stats.saldoBulanIni);
            
            // Update periodik values
            document.getElementById('pengeluaranHarian').textContent = formatRupiah(stats.pengeluaranHarian);
            document.getElementById('pengeluaranMingguan').textContent = formatRupiah(stats.pengeluaranMingguan);
            document.getElementById('pengeluaranBulanan').textContent = formatRupiah(stats.pengeluaranBulanan);
            document.getElementById('pengeluaranTahunan').textContent = formatRupiah(stats.pengeluaranTahunan);
        }

        function updateCharts(stats) {
            updateDistributionChart(stats);
            updateTrendChart();
        }

        function updateDistributionChart(stats) {
            const ctx = document.getElementById('distributionChart');
            if (!ctx) return;
            
            // Destroy existing chart
            if (distributionChart) {
                distributionChart.destroy();
            }
            
            // Create new chart with STANDARD SIZE
            distributionChart = new Chart(ctx.getContext('2d'), {
                type: 'doughnut',
                data: {
                    labels: ['Dana Lensa', 'Dana Operasional'],
                    datasets: [{
                        data: [stats.saldoLensa, stats.saldoOperasional],
                        backgroundColor: ['#3498db', '#2ecc71'],
                        borderWidth: 1,
                        borderColor: '#ffffff'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 15,
                                font: {
                                    size: 11
                                },
                                boxWidth: 12
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    const value = context.raw;
                                    return `${context.label}: ${formatRupiah(value)}`;
                                }
                            }
                        }
                    },
                    cutout: '60%'
                }
            });
        }

        function updateTrendChart() {
            const ctx = document.getElementById('trendChart');
            if (!ctx) return;
            
            // Destroy existing chart
            if (trendChart) {
                trendChart.destroy();
            }
            
            // Generate sample trend data for last 6 months
            const months = ['Jan', 'Feb', 'Mar', 'Apr', 'Mei', 'Jun'];
            const pemasukanData = [1500000, 1800000, 2200000, 1900000, 2400000, 2600000];
            const pengeluaranData = [1200000, 1400000, 1600000, 1500000, 1800000, 2000000];
            
            // Create new chart with STANDARD SIZE
            trendChart = new Chart(ctx.getContext('2d'), {
                type: 'line',
                data: {
                    labels: months,
                    datasets: [
                        {
                            label: 'Pemasukan',
                            data: pemasukanData,
                            borderColor: '#27ae60',
                            backgroundColor: 'rgba(39, 174, 96, 0.1)',
                            borderWidth: 2,
                            fill: true,
                            tension: 0.3
                        },
                        {
                            label: 'Pengeluaran',
                            data: pengeluaranData,
                            borderColor: '#e74c3c',
                            backgroundColor: 'rgba(231, 76, 60, 0.1)',
                            borderWidth: 2,
                            fill: true,
                            tension: 0.3
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'top',
                            labels: {
                                font: {
                                    size: 11
                                },
                                boxWidth: 12
                            }
                        },
                        tooltip: {
                            mode: 'index',
                            intersect: false,
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${formatRupiah(context.raw)}`;
                                }
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                callback: function(value) {
                                    return formatRupiah(value);
                                },
                                font: {
                                    size: 10
                                }
                            },
                            grid: {
                                color: 'rgba(0, 0, 0, 0.05)'
                            }
                        },
                        x: {
                            grid: {
                                color: 'rgba(0, 0, 0, 0.05)'
                            },
                            ticks: {
                                font: {
                                    size: 10
                                }
                            }
                        }
                    },
                    interaction: {
                        intersect: false,
                        mode: 'nearest'
                    }
                }
            });
        }

        function loadLensaData() {
            const data = getData(STORAGE_KEYS.LENSA);
            displayLensaData(data);
            document.getElementById('lensaCount').textContent = `(${data.length} transaksi)`;
        }

        function loadOperasionalData() {
            const data = getData(STORAGE_KEYS.OPERASIONAL);
            displayOperasionalData(data);
            document.getElementById('operasionalCount').textContent = `(${data.length} transaksi)`;
        }

        function loadPeriodikData() {
            const data = getData(STORAGE_KEYS.PERIODIK);
            displayPeriodikData(data);
            document.getElementById('periodikCount').textContent = `(${data.length} data)`;
        }

        // ============================================
        // DISPLAY FUNCTIONS
        // ============================================
        function displayLensaData(data) {
            const tbody = document.getElementById('lensaTableBody');
            
            if (data.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="7" style="text-align: center; padding: 30px; color: #999;">
                            <i class="fas fa-inbox" style="font-size: 32px; margin-bottom: 10px; display: block;"></i>
                            Belum ada transaksi
                        </td>
                    </tr>
                `;
                return;
            }
            
            // Sort by date descending
            data.sort((a, b) => new Date(b.tanggal) - new Date(a.tanggal));
            
            // Calculate running balance
            let runningBalance = 0;
            const dataWithBalance = data.map(transaksi => {
                if (transaksi.jenis === 'Masuk') {
                    runningBalance += transaksi.nominal;
                } else {
                    runningBalance -= transaksi.nominal;
                }
                return {
                    ...transaksi,
                    saldo: runningBalance
                };
            }).reverse();
            
            let html = '';
            dataWithBalance.forEach(item => {
                const jenisClass = item.jenis === 'Masuk' ? 'badge-success' : 'badge-danger';
                const jenisText = item.jenis === 'Masuk' ? 'Pemasukan' : 'Pengeluaran';
                
                html += `
                    <tr>
                        <td>${formatDate(item.tanggal)}</td>
                        <td><span class="badge ${jenisClass}">${jenisText}</span></td>
                        <td>${item.kategori || '-'}</td>
                        <td>${item.keterangan || '-'}</td>
                        <td style="font-weight: 600;">${formatRupiah(item.nominal)}</td>
                        <td style="font-weight: 600; color: ${item.saldo >= 0 ? '#2e7d32' : '#c62828'}">
                            ${formatRupiah(item.saldo)}
                        </td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-icon btn-icon-delete" onclick="deleteTransaction('lensa', '${item.id}')">
                                    <i class="fas fa-trash"></i>
                                </button>
                            </div>
                        </td>
                    </tr>
                `;
            });
            
            tbody.innerHTML = html;
        }

        function displayOperasionalData(data) {
            const tbody = document.getElementById('operasionalTableBody');
            
            if (data.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="7" style="text-align: center; padding: 30px; color: #999;">
                            <i class="fas fa-inbox" style="font-size: 32px; margin-bottom: 10px; display: block;"></i>
                            Belum ada transaksi
                        </td>
                    </tr>
                `;
                return;
            }
            
            // Sort by date descending
            data.sort((a, b) => new Date(b.tanggal) - new Date(a.tanggal));
            
            // Calculate running balance
            let runningBalance = 0;
            const dataWithBalance = data.map(transaksi => {
                if (transaksi.jenis === 'Masuk') {
                    runningBalance += transaksi.nominal;
                } else {
                    runningBalance -= transaksi.nominal;
                }
                return {
                    ...transaksi,
                    saldo: runningBalance
                };
            }).reverse();
            
            let html = '';
            dataWithBalance.forEach(item => {
                const jenisClass = item.jenis === 'Masuk' ? 'badge-success' : 'badge-danger';
                const jenisText = item.jenis === 'Masuk' ? 'Dana Masuk' : 'Dana Keluar';
                
                html += `
                    <tr>
                        <td>${formatDate(item.tanggal)}</td>
                        <td><span class="badge ${jenisClass}">${jenisText}</span></td>
                        <td>${item.kategori || '-'}</td>
                        <td>${item.keterangan || '-'}</td>
                        <td style="font-weight: 600;">${formatRupiah(item.nominal)}</td>
                        <td style="font-weight: 600; color: ${item.saldo >= 0 ? '#2e7d32' : '#c62828'}">
                            ${formatRupiah(item.saldo)}
                        </td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-icon btn-icon-delete" onclick="deleteTransaction('operasional', '${item.id}')">
                                    <i class="fas fa-trash"></i>
                                </button>
                            </div>
                        </td>
                    </tr>
                `;
            });
            
            tbody.innerHTML = html;
        }

        function displayPeriodikData(data) {
            const tbody = document.getElementById('periodikTableBody');
            
            if (data.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="5" style="text-align: center; padding: 30px; color: #999;">
                            <i class="fas fa-inbox" style="font-size: 32px; margin-bottom: 10px; display: block;"></i>
                            Belum ada data pengeluaran periodik
                        </td>
                    </tr>
                `;
                return;
            }
            
            // Sort by date descending
            data.sort((a, b) => new Date(b.tanggal) - new Date(a.tanggal));
            
            let html = '';
            data.forEach(item => {
                let badgeClass = 'badge-primary';
                switch(item.periode) {
                    case 'Harian': badgeClass = 'badge-primary'; break;
                    case 'Mingguan': badgeClass = 'badge-warning'; break;
                    case 'Bulanan': badgeClass = 'badge-success'; break;
                    case 'Tahunan': badgeClass = 'badge-danger'; break;
                }
                
                html += `
                    <tr>
                        <td>${formatDate(item.tanggal)}</td>
                        <td><span class="badge ${badgeClass}">${item.periode}</span></td>
                        <td>${item.keterangan || '-'}</td>
                        <td style="font-weight: 600;">${formatRupiah(item.nominal)}</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-icon btn-icon-delete" onclick="deletePeriodik('${item.id}')">
                                    <i class="fas fa-trash"></i>
                                </button>
                            </div>
                        </td>
                    </tr>
                `;
            });
            
            tbody.innerHTML = html;
        }

        // ============================================
        // TRANSACTION FUNCTIONS
        // ============================================
        function addTransaction(type) {
            const formId = type === 'lensa' ? 'formLensa' : 'formOperasional';
            const jenis = document.getElementById(`${type}Jenis`).value;
            const kategori = document.getElementById(`${type}Kategori`).value;
            const keterangan = document.getElementById(`${type}Keterangan`).value.trim();
            const nominal = document.getElementById(`${type}Nominal`).value;
            const tanggal = document.getElementById(`${type}Tanggal`).value;
            
            // Validation
            if (!keterangan || !nominal || !tanggal) {
                showMessage('Harap isi semua field yang diperlukan', 'error');
                return;
            }
            
            if (parseFloat(nominal) <= 0) {
                showMessage('Nominal harus lebih dari 0', 'error');
                return;
            }
            
            const transactionData = {
                id: generateId(),
                jenis: jenis,
                kategori: kategori,
                keterangan: keterangan,
                nominal: parseFloat(nominal),
                tanggal: tanggal,
                createdAt: new Date().toISOString()
            };
            
            const storageKey = type === 'lensa' ? STORAGE_KEYS.LENSA : STORAGE_KEYS.OPERASIONAL;
            const currentData = getData(storageKey);
            currentData.push(transactionData);
            
            saveData(storageKey, currentData);
            
            // Reset form
            document.getElementById(`${type}Keterangan`).value = '';
            document.getElementById(`${type}Nominal`).value = '';
            document.getElementById(`${type}Kategori`).value = '';
            
            showMessage('✅ Transaksi berhasil disimpan');
            
            // Reload data
            if (type === 'lensa') {
                loadLensaData();
            } else {
                loadOperasionalData();
            }
            
            // Update dashboard
            loadDashboardData();
        }

        function addPeriodik() {
            const periode = document.getElementById('periodikPeriode').value;
            const keterangan = document.getElementById('periodikKeterangan').value.trim();
            const nominal = document.getElementById('periodikNominal').value;
            const tanggal = document.getElementById('periodikTanggal').value;
            
            // Validation
            if (!keterangan || !nominal || !tanggal) {
                showMessage('Harap isi semua field yang diperlukan', 'error');
                return;
            }
            
            if (parseFloat(nominal) <= 0) {
                showMessage('Nominal harus lebih dari 0', 'error');
                return;
            }
            
            const periodikData = {
                id: generateId(),
                periode: periode,
                keterangan: keterangan,
                nominal: parseFloat(nominal),
                tanggal: tanggal,
                createdAt: new Date().toISOString()
            };
            
            const currentData = getData(STORAGE_KEYS.PERIODIK);
            currentData.push(periodikData);
            
            saveData(STORAGE_KEYS.PERIODIK, currentData);
            
            // Reset form
            document.getElementById('periodikKeterangan').value = '';
            document.getElementById('periodikNominal').value = '';
            
            showMessage('✅ Pengeluaran periodik berhasil disimpan');
            
            // Reload data
            loadPeriodikData();
            loadDashboardData();
        }

        function deleteTransaction(type, id) {
            if (!confirm('Hapus transaksi ini?')) return;
            
            const storageKey = type === 'lensa' ? STORAGE_KEYS.LENSA : STORAGE_KEYS.OPERASIONAL;
            const currentData = getData(storageKey);
            const newData = currentData.filter(item => item.id !== id);
            
            saveData(storageKey, newData);
            showMessage('✅ Transaksi berhasil dihapus');
            
            // Reload data
            if (type === 'lensa') {
                loadLensaData();
            } else {
                loadOperasionalData();
            }
            
            loadDashboardData();
        }

        function deletePeriodik(id) {
            if (!confirm('Hapus data pengeluaran periodik ini?')) return;
            
            const currentData = getData(STORAGE_KEYS.PERIODIK);
            const newData = currentData.filter(item => item.id !== id);
            
            saveData(STORAGE_KEYS.PERIODIK, newData);
            showMessage('✅ Data berhasil dihapus');
            
            loadPeriodikData();
            loadDashboardData();
        }

        function resetForm(type) {
            if (type === 'lensa') {
                document.getElementById('formLensa').reset();
                document.getElementById('lensaTanggal').value = new Date().toISOString().split('T')[0];
            } else if (type === 'operasional') {
                document.getElementById('formOperasional').reset();
                document.getElementById('operasionalTanggal').value = new Date().toISOString().split('T')[0];
            } else if (type === 'periodik') {
                document.getElementById('formPeriodik').reset();
                document.getElementById('periodikTanggal').value = new Date().toISOString().split('T')[0];
            }
        }

        // ============================================
        // EXPORT & IMPORT FUNCTIONS
        // ============================================
        function exportExcel(type) {
            let data, filename, headers;
            
            switch(type) {
                case 'lensa':
                    data = getData(STORAGE_KEYS.LENSA);
                    filename = 'laporan_dana_lensa.xlsx';
                    headers = [
                        ['LAPORAN DANA LENSA'],
                        ['Tanggal Export', new Date().toLocaleString('id-ID')],
                        ['User', currentUser.username],
                        [],
                        ['Tanggal', 'Jenis', 'Kategori', 'Keterangan', 'Nominal']
                    ];
                    break;
                    
                case 'operasional':
                    data = getData(STORAGE_KEYS.OPERASIONAL);
                    filename = 'laporan_dana_operasional.xlsx';
                    headers = [
                        ['LAPORAN DANA OPERASIONAL'],
                        ['Tanggal Export', new Date().toLocaleString('id-ID')],
                        ['User', currentUser.username],
                        [],
                        ['Tanggal', 'Jenis', 'Kategori', 'Keterangan', 'Nominal']
                    ];
                    break;
                    
                case 'periodik':
                    data = getData(STORAGE_KEYS.PERIODIK);
                    filename = 'laporan_pengeluaran_periodik.xlsx';
                    headers = [
                        ['LAPORAN PENGELUARAN PERIODIK'],
                        ['Tanggal Export', new Date().toLocaleString('id-ID')],
                        ['User', currentUser.username],
                        [],
                        ['Tanggal', 'Periode', 'Keterangan', 'Nominal']
                    ];
                    break;
            }
            
            if (data.length === 0) {
                showMessage('Tidak ada data untuk diexport', 'error');
                return;
            }
            
            // Prepare worksheet data
            const wsData = [...headers];
            
            // Add data rows
            data.forEach(item => {
                if (type === 'periodik') {
                    wsData.push([
                        formatDate(item.tanggal),
                        item.periode,
                        item.keterangan,
                        item.nominal
                    ]);
                } else {
                    wsData.push([
                        formatDate(item.tanggal),
                        item.jenis,
                        item.kategori || '-',
                        item.keterangan,
                        item.nominal
                    ]);
                }
            });
            
            // Add summary
            wsData.push([]);
            if (type !== 'periodik') {
                const totalMasuk = data.filter(d => d.jenis === 'Masuk').reduce((sum, d) => sum + d.nominal, 0);
                const totalKeluar = data.filter(d => d.jenis === 'Keluar').reduce((sum, d) => sum + d.nominal, 0);
                const saldo = totalMasuk - totalKeluar;
                
                wsData.push(['TOTAL PEMASUKAN', '', '', '', totalMasuk]);
                wsData.push(['TOTAL PENGELUARAN', '', '', '', totalKeluar]);
                wsData.push(['SALDO AKHIR', '', '', '', saldo]);
            } else {
                const total = data.reduce((sum, d) => sum + d.nominal, 0);
                wsData.push(['TOTAL PENGELUARAN', '', '', total]);
            }
            
            // Create worksheet
            const ws = XLSX.utils.aoa_to_sheet(wsData);
            
            // Set column widths
            const wscols = type === 'periodik' 
                ? [{wch: 15}, {wch: 12}, {wch: 30}, {wch: 15}]
                : [{wch: 15}, {wch: 12}, {wch: 15}, {wch: 30}, {wch: 15}];
            ws['!cols'] = wscols;
            
            // Create workbook
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, 'Laporan');
            
            // Export to file
            XLSX.writeFile(wb, filename);
            showMessage('✅ Laporan berhasil diexport ke Excel');
        }

        function exportAllExcel() {
            const lensaData = getData(STORAGE_KEYS.LENSA);
            const operasionalData = getData(STORAGE_KEYS.OPERASIONAL);
            const periodikData = getData(STORAGE_KEYS.PERIODIK);
            
            if (lensaData.length === 0 && operasionalData.length === 0 && periodikData.length === 0) {
                showMessage('Tidak ada data untuk diexport', 'error');
                return;
            }
            
            // Create workbook
            const wb = XLSX.utils.book_new();
            
            // Add Dana Lensa sheet
            if (lensaData.length > 0) {
                const lensaWsData = [
                    ['LAPORAN DANA LENSA'],
                    ['Tanggal Export', new Date().toLocaleString('id-ID')],
                    ['User', currentUser.username],
                    [],
                    ['Tanggal', 'Jenis', 'Kategori', 'Keterangan', 'Nominal']
                ];
                
                lensaData.forEach(item => {
                    lensaWsData.push([
                        formatDate(item.tanggal),
                        item.jenis,
                        item.kategori || '-',
                        item.keterangan,
                        item.nominal
                    ]);
                });
                
                const totalMasukLensa = lensaData.filter(d => d.jenis === 'Masuk').reduce((sum, d) => sum + d.nominal, 0);
                const totalKeluarLensa = lensaData.filter(d => d.jenis === 'Keluar').reduce((sum, d) => sum + d.nominal, 0);
                const saldoLensa = totalMasukLensa - totalKeluarLensa;
                
                lensaWsData.push([]);
                lensaWsData.push(['TOTAL PEMASUKAN', '', '', '', totalMasukLensa]);
                lensaWsData.push(['TOTAL PENGELUARAN', '', '', '', totalKeluarLensa]);
                lensaWsData.push(['SALDO AKHIR', '', '', '', saldoLensa]);
                
                const lensaWs = XLSX.utils.aoa_to_sheet(lensaWsData);
                lensaWs['!cols'] = [{wch: 15}, {wch: 12}, {wch: 15}, {wch: 30}, {wch: 15}];
                XLSX.utils.book_append_sheet(wb, lensaWs, 'Dana Lensa');
            }
            
            // Export to file
            XLSX.writeFile(wb, 'laporan_keuangan_lengkap.xlsx');
            showMessage('✅ Semua laporan berhasil diexport ke Excel');
        }

        function exportFiltered() {
            showMessage('Fitur filter export akan datang!', 'error');
        }

        function printReport() {
            window.print();
        }

        // ============================================
        // CLOUD SYNC FUNCTIONS
        // ============================================
        function backupToCloud() {
            if (!isOnline) {
                showMessage('Tidak ada koneksi internet', 'error');
                return;
            }
            
            showLoading('Menyimpan data ke cloud...');
            
            // Prepare backup data
            const backupData = {
                user: currentUser.username,
                lensa: getData(STORAGE_KEYS.LENSA),
                operasional: getData(STORAGE_KEYS.OPERASIONAL),
                periodik: getData(STORAGE_KEYS.PERIODIK),
                metadata: {
                    backupDate: new Date().toISOString(),
                    totalRecords: getData(STORAGE_KEYS.LENSA).length + 
                                 getData(STORAGE_KEYS.OPERASIONAL).length + 
                                 getData(STORAGE_KEYS.PERIODIK).length,
                    version: '1.0'
                }
            };
            
            // Save to local storage (simulating cloud)
            localStorage.setItem(STORAGE_KEYS.CLOUD_BACKUP, JSON.stringify(backupData));
            
            setTimeout(() => {
                hideLoading();
                updateSyncInfo();
                showMessage('✅ Data berhasil disimpan ke cloud');
            }, 1500);
        }

        function restoreFromCloud() {
            if (!isOnline) {
                showMessage('Tidak ada koneksi internet', 'error');
                return;
            }
            
            showLoading('Memuat data dari cloud...');
            
            // Load from local storage (simulating cloud)
            const backupData = JSON.parse(localStorage.getItem(STORAGE_KEYS.CLOUD_BACKUP) || '{}');
            
            if (!backupData.user) {
                hideLoading();
                showMessage('❌ Tidak ada data backup di cloud', 'error');
                return;
            }
            
            if (confirm(`Restore data dari ${formatDateTime(new Date(backupData.metadata.backupDate))}? Data saat ini akan diganti.`)) {
                // Restore data
                saveData(STORAGE_KEYS.LENSA, backupData.lensa || []);
                saveData(STORAGE_KEYS.OPERASIONAL, backupData.operasional || []);
                saveData(STORAGE_KEYS.PERIODIK, backupData.periodik || []);
                
                // Reload all data
                setTimeout(() => {
                    hideLoading();
                    loadAllData();
                    showMessage('✅ Data berhasil direstore dari cloud');
                }, 1500);
            } else {
                hideLoading();
            }
        }

        function exportBackupFile() {
            const backupData = {
                user: currentUser.username,
                lensa: getData(STORAGE_KEYS.LENSA),
                operasional: getData(STORAGE_KEYS.OPERASIONAL),
                periodik: getData(STORAGE_KEYS.PERIODIK),
                metadata: {
                    backupDate: new Date().toISOString(),
                    totalRecords: getData(STORAGE_KEYS.LENSA).length + 
                                 getData(STORAGE_KEYS.OPERASIONAL).length + 
                                 getData(STORAGE_KEYS.PERIODIK).length,
                    version: '1.0'
                }
            };
            
            const dataStr = JSON.stringify(backupData, null, 2);
            const dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
            
            const exportFileDefaultName = `backup_keuangan_${currentUser.username}_${new Date().toISOString().split('T')[0]}.json`;
            
            const linkElement = document.createElement('a');
            linkElement.setAttribute('href', dataUri);
            linkElement.setAttribute('download', exportFileDefaultName);
            linkElement.click();
            
            showMessage('✅ Backup file berhasil diexport');
        }

        function importBackupFile(event) {
            const file = event.target.files[0];
            if (!file) return;
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const backupData = JSON.parse(e.target.result);
                    
                    // Validate backup data
                    if (!backupData.user || !backupData.lensa || !backupData.operasional || !backupData.periodik) {
                        throw new Error('Format file backup tidak valid');
                    }
                    
                    if (confirm(`Import data backup untuk user ${backupData.user}? Data saat ini akan diganti.`)) {
                        // Restore data
                        saveData(STORAGE_KEYS.LENSA, backupData.lensa);
                        saveData(STORAGE_KEYS.OPERASIONAL, backupData.operasional);
                        saveData(STORAGE_KEYS.PERIODIK, backupData.periodik);
                        
                        // Reload all data
                        loadAllData();
                        
                        showMessage('✅ Data berhasil diimport dari file backup');
                    }
                } catch (error) {
                    showMessage('❌ Gagal import data: ' + error.message, 'error');
                }
                
                // Reset file input
                event.target.value = '';
            };
            
            reader.readAsText(file);
        }

        // ============================================
        // EVENT LISTENERS
        // ============================================
        window.addEventListener('online', () => {
            isOnline = true;
            updateSyncStatus();
            showMessage('✅ Koneksi internet tersedia', 'success');
        });

        window.addEventListener('offline', () => {
            isOnline = false;
            updateSyncStatus();
            showMessage('⚠️ Koneksi internet terputus', 'error');
        });

        // ============================================
        // GLOBAL FUNCTIONS
        // ============================================
        window.addTransaction = addTransaction;
        window.addPeriodik = addPeriodik;
        window.deleteTransaction = deleteTransaction;
        window.deletePeriodik = deletePeriodik;
        window.resetForm = resetForm;
        window.loadLensaData = loadLensaData;
        window.loadOperasionalData = loadOperasionalData;
        window.loadPeriodikData = loadPeriodikData;
        window.exportExcel = exportExcel;
        window.exportAllExcel = exportAllExcel;
        window.exportFiltered = exportFiltered;
        window.printReport = printReport;
        window.manualSync = manualSync;
        window.backupToCloud = backupToCloud;
        window.restoreFromCloud = restoreFromCloud;
        window.exportBackupFile = exportBackupFile;
        window.logout = logout;
    </script>
</body>
</html>
