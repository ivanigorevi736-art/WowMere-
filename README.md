# WowMere-
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>WowMere - Мобильная нейросеть</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary: #6c63ff;
            --primary-dark: #554fd8;
            --secondary: #ff6584;
            --dark: #2d2b55;
            --light: #f8f9fa;
            --gray: #6c757d;
            --success: #28a745;
            --danger: #dc3545;
            --warning: #ffc107;
        }
        
        body {
            background-color: var(--dark);
            color: var(--light);
            overflow-x: hidden;
            height: 100vh;
        }
        
        /* Заставка */
        #splash-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            transition: opacity 0.5s ease;
        }
        
        .logo {
            font-size: 3rem;
            margin-bottom: 1rem;
            animation: pulse 2s infinite;
        }
        
        .app-name {
            font-size: 2rem;
            font-weight: bold;
            margin-bottom: 2rem;
        }
        
        .loading-bar {
            width: 200px;
            height: 4px;
            background-color: rgba(255, 255, 255, 0.3);
            border-radius: 2px;
            overflow: hidden;
        }
        
        .loading-progress {
            height: 100%;
            width: 0%;
            background-color: white;
            border-radius: 2px;
            animation: loading 2s forwards;
        }
        
        @keyframes loading {
            to { width: 100%; }
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        
        /* Основной контейнер */
        .container {
            max-width: 100%;
            margin: 0 auto;
            height: 100vh;
            display: flex;
            flex-direction: column;
            background-color: var(--dark);
            position: relative;
            overflow: hidden;
        }
        
        /* Шапка */
        .header {
            background-color: var(--primary);
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            position: relative;
            z-index: 10;
        }
        
        .header-left {
            display: flex;
            align-items: center;
        }
        
        .header-icon {
            font-size: 1.5rem;
            margin-right: 10px;
        }
        
        .app-title {
            font-size: 1.2rem;
            font-weight: bold;
        }
        
        .header-right {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .header-btn {
            background: none;
            border: none;
            color: var(--light);
            font-size: 1.2rem;
            cursor: pointer;
        }
        
        .avatar {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            background-color: var(--secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            cursor: pointer;
        }
        
        /* Чат */
        .chat-container {
            flex: 1;
            overflow-y: auto;
            padding: 15px;
            display: flex;
            flex-direction: column;
            background-color: var(--dark);
        }
        
        .message {
            max-width: 85%;
            padding: 12px 15px;
            margin-bottom: 15px;
            border-radius: 18px;
            position: relative;
            animation: fadeIn 0.3s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .user-message {
            align-self: flex-end;
            background-color: var(--primary);
            border-bottom-right-radius: 5px;
        }
        
        .ai-message {
            align-self: flex-start;
            background-color: #3a375e;
            border-bottom-left-radius: 5px;
        }
        
        .message-image {
            max-width: 100%;
            border-radius: 10px;
            margin-top: 8px;
            display: block;
        }
        
        .message-actions {
            display: flex;
            justify-content: flex-end;
            margin-top: 8px;
        }
        
        .action-btn {
            background: none;
            border: none;
            color: var(--gray);
            font-size: 0.9rem;
            margin-left: 10px;
            cursor: pointer;
            transition: color 0.2s;
        }
        
        .action-btn:hover {
            color: var(--light);
        }
        
        .like-btn.active {
            color: var(--success);
        }
        
        .dislike-btn.active {
            color: var(--danger);
        }
        
        /* Панель ввода */
        .input-container {
            padding: 15px;
            background-color: #3a375e;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .input-actions {
            display: flex;
            gap: 10px;
        }
        
        .input-action-btn {
            background: none;
            border: none;
            color: var(--light);
            font-size: 1.2rem;
            cursor: pointer;
            opacity: 0.7;
            transition: opacity 0.2s;
            padding: 8px;
        }
        
        .input-action-btn:hover {
            opacity: 1;
        }
        
        .message-input {
            flex: 1;
            padding: 12px 15px;
            border: none;
            border-radius: 24px;
            background-color: #2d2b55;
            color: var(--light);
            font-size: 1rem;
            outline: none;
        }
        
        .send-btn {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background-color: var(--primary);
            border: none;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: background-color 0.2s;
            flex-shrink: 0;
        }
        
        .send-btn:hover {
            background-color: var(--primary-dark);
        }
        
        .send-btn:disabled {
            background-color: var(--gray);
            cursor: not-allowed;
        }
        
        /* Модальные окна */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 100;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease;
        }
        
        .modal.active {
            opacity: 1;
            pointer-events: all;
        }
        
        .modal-content {
            background-color: #3a375e;
            width: 90%;
            max-width: 400px;
            max-height: 90vh;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
            transform: translateY(20px);
            transition: transform 0.3s ease;
            overflow-y: auto;
        }
        
        .modal.active .modal-content {
            transform: translateY(0);
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .modal-title {
            font-size: 1.3rem;
            font-weight: bold;
        }
        
        .close-btn {
            background: none;
            border: none;
            color: var(--light);
            font-size: 1.5rem;
            cursor: pointer;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-label {
            display: block;
            margin-bottom: 5px;
            font-size: 0.9rem;
            color: rgba(255, 255, 255, 0.8);
        }
        
        .form-input {
            width: 100%;
            padding: 12px 15px;
            border: none;
            border-radius: 8px;
            background-color: #2d2b55;
            color: var(--light);
            font-size: 1rem;
            outline: none;
        }
        
        .form-input:focus {
            box-shadow: 0 0 0 2px var(--primary);
        }
        
        .btn {
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .btn-primary {
            background-color: var(--primary);
            color: white;
            width: 100%;
        }
        
        .btn-primary:hover {
            background-color: var(--primary-dark);
        }
        
        .btn-secondary {
            background-color: transparent;
            color: var(--primary);
            border: 1px solid var(--primary);
            width: 100%;
            margin-top: 10px;
        }
        
        .btn-secondary:hover {
            background-color: rgba(108, 99, 255, 0.1);
        }
        
        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .tab {
            flex: 1;
            padding: 10px;
            text-align: center;
            cursor: pointer;
            border-bottom: 2px solid transparent;
        }
        
        .tab.active {
            color: var(--primary);
            border-bottom: 2px solid var(--primary);
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .profile-info {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .profile-avatar {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background-color: var(--secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            font-weight: bold;
            margin: 0 auto 15px;
            cursor: pointer;
        }
        
        .profile-name {
            font-size: 1.2rem;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .profile-email {
            color: rgba(255, 255, 255, 0.7);
            font-size: 0.9rem;
        }
        
        /* Настройки */
        .settings-group {
            margin-bottom: 25px;
        }
        
        .settings-title {
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 15px;
            color: var(--primary);
        }
        
        .setting-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .setting-info {
            flex: 1;
        }
        
        .setting-name {
            font-weight: 500;
            margin-bottom: 3px;
        }
        
        .setting-desc {
            font-size: 0.8rem;
            color: rgba(255, 255, 255, 0.6);
        }
        
        .toggle {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 24px;
        }
        
        .toggle input {
            opacity: 0;
            width: 0;
            height: 0;
        }
        
        .slider {
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
        
        .slider:before {
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
        
        input:checked + .slider {
            background-color: var(--primary);
        }
        
        input:checked + .slider:before {
            transform: translateX(26px);
        }
        
        .select {
            padding: 8px 12px;
            border-radius: 6px;
            background-color: #2d2b55;
            color: var(--light);
            border: none;
            outline: none;
        }
        
        /* Загрузка фото */
        .image-preview {
            max-width: 100%;
            max-height: 200px;
            border-radius: 10px;
            margin-top: 10px;
            display: none;
        }
        
        .remove-image {
            background-color: var(--danger);
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            margin-top: 5px;
            cursor: pointer;
            font-size: 0.8rem;
        }
        
        /* Языковой переключатель */
        .language-selector {
            position: relative;
            display: inline-block;
        }
        
        .language-btn {
            background: none;
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 20px;
            padding: 8px 15px;
            color: var(--light);
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            background-color: rgba(255, 255, 255, 0.1);
        }
        
        .language-dropdown {
            position: absolute;
            top: 100%;
            right: 0;
            background-color: #3a375e;
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            padding: 10px;
            min-width: 150px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            display: none;
            z-index: 10;
        }
        
        .language-dropdown.active {
            display: block;
        }
        
        .language-option {
            padding: 8px 12px;
            cursor: pointer;
            border-radius: 4px;
            transition: background-color 0.2s;
        }
        
        .language-option:hover {
            background-color: var(--primary);
        }
        
        /* Уведомления */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 20px;
            background-color: var(--success);
            color: white;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            z-index: 200;
            transform: translateX(150%);
            transition: transform 0.3s ease;
        }
        
        .notification.active {
            transform: translateX(0);
        }
        
        .notification.error {
            background-color: var(--danger);
        }
        
        .notification.warning {
            background-color: var(--warning);
            color: #000;
        }
        
        /* Адаптивность */
        @media (max-width: 480px) {
            .message {
                max-width: 90%;
            }
            
            .modal-content {
                width: 95%;
                padding: 20px;
            }
            
            .header-right {
                gap: 10px;
            }
        }
    </style>
</head>
<body>
    <!-- Заставка -->
    <div id="splash-screen">
        <div class="logo">
            <i class="fas fa-brain"></i>
        </div>
        <div class="app-name">WowMere</div>
        <div class="loading-bar">
            <div class="loading-progress"></div>
        </div>
    </div>

    <!-- Основной контейнер -->
    <div class="container">
        <!-- Шапка -->
        <div class="header">
            <div class="header-left">
                <div class="header-icon">
                    <i class="fas fa-brain"></i>
                </div>
                <div class="app-title">WowMere</div>
            </div>
            <div class="header-right">
                <div class="language-selector">
                    <button class="language-btn" id="language-btn">
                        <i class="fas fa-globe"></i>
                        <span id="current-lang">RU</span>
                    </button>
                    <div class="language-dropdown" id="language-dropdown">
                        <div class="language-option" data-lang="ru">Русский</div>
                        <div class="language-option" data-lang="en">English</div>
                        <div class="language-option" data-lang="es">Español</div>
                        <div class="language-option" data-lang="fr">Français</div>
                    </div>
                </div>
                <button class="header-btn" id="settings-btn">
                    <i class="fas fa-cog"></i>
                </button>
                <div class="avatar" id="profile-btn">
                    <i class="fas fa-user"></i>
                </div>
            </div>
        </div>

        <!-- Чат -->
        <div class="chat-container" id="chat-container">
            <!-- Сообщения будут добавляться здесь -->
        </div>

        <!-- Панель ввода с кнопкой отправки -->
        <div class="input-container">
            <div class="input-actions">
                <button class="input-action-btn" id="camera-btn">
                    <i class="fas fa-camera"></i>
                </button>
                <button class="input-action-btn" id="gallery-btn">
                    <i class="fas fa-image"></i>
                </button>
            </div>
            <input type="text" class="message-input" id="message-input" placeholder="Введите ваше сообщение...">
            <button class="send-btn" id="send-btn">
                <i class="fas fa-paper-plane"></i>
            </button>
        </div>
    </div>

    <!-- Модальное окно входа/регистрации -->
    <div class="modal" id="auth-modal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">Вход в WowMere</div>
                <button class="close-btn" id="close-auth-modal">&times;</button>
            </div>
            
            <div class="tabs">
                <div class="tab active" data-tab="login">Вход</div>
                <div class="tab" data-tab="register">Регистрация</div>
            </div>
            
            <div class="tab-content active" id="login-tab">
                <div class="form-group">
                    <label class="form-label">Email</label>
                    <input type="email" class="form-input" id="login-email" placeholder="Ваш email">
                </div>
                <div class="form-group">
                    <label class="form-label">Пароль</label>
                    <input type="password" class="form-input" id="login-password" placeholder="Ваш пароль">
                </div>
                <button class="btn btn-primary" id="login-btn">Войти</button>
            </div>
            
            <div class="tab-content" id="register-tab">
                <div class="form-group">
                    <label class="form-label">Имя</label>
                    <input type="text" class="form-input" id="register-name" placeholder="Ваше имя">
                </div>
                <div class="form-group">
                    <label class="form-label">Email</label>
                    <input type="email" class="form-input" id="register-email" placeholder="Ваш email">
                </div>
                <div class="form-group">
                    <label class="form-label">Пароль</label>
                    <input type="password" class="form-input" id="register-password" placeholder="Придумайте пароль">
                </div>
                <button class="btn btn-primary" id="register-btn">Зарегистрироваться</button>
            </div>
        </div>
    </div>

    <!-- Модальное окно профиля -->
    <div class="modal" id="profile-modal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">Профиль</div>
                <button class="close-btn" id="close-profile-modal">&times;</button>
            </div>
            
            <div class="profile-info">
                <div class="profile-avatar" id="profile-avatar">
                    <i class="fas fa-user"></i>
                </div>
                <div class="profile-name" id="profile-name">Пользователь</div>
                <div class="profile-email" id="profile-email">user@example.com</div>
            </div>
            
            <div class="form-group">
                <label class="form-label">Имя</label>
                <input type="text" class="form-input" id="edit-name" placeholder="Ваше имя">
            </div>
            <div class="form-group">
                <label class="form-label">Email</label>
                <input type="email" class="form-input" id="edit-email" placeholder="Ваш email">
            </div>
            <div class="form-group">
                <label class="form-label">Новый пароль</label>
                <input type="password" class="form-input" id="edit-password" placeholder="Оставьте пустым, если не меняете">
            </div>
            
            <button class="btn btn-primary" id="save-profile-btn">Сохранить изменения</button>
            <button class="btn btn-secondary" id="logout-btn">Выйти</button>
        </div>
    </div>

    <!-- Модальное окно настроек -->
    <div class="modal" id="settings-modal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">Настройки</div>
                <button class="close-btn" id="close-settings-modal">&times;</button>
            </div>
            
            <div class="settings-group">
                <div class="settings-title">Внешний вид</div>
                
                <div class="setting-item">
                    <div class="setting-info">
                        <div class="setting-name">Темная тема</div>
                        <div class="setting-desc">Использовать темную цветовую схему</div>
                    </div>
                    <label class="toggle">
                        <input type="checkbox" id="dark-theme" checked>
                        <span class="slider"></span>
                    </label>
                </div>
                
                <div class="setting-item">
                    <div class="setting-info">
                        <div class="setting-name">Размер текста</div>
                        <div class="setting-desc">Настройте размер текста в чате</div>
                    </div>
                    <select class="select" id="font-size">
                        <option value="small">Маленький</option>
                        <option value="medium" selected>Средний</option>
                        <option value="large">Большой</option>
                    </select>
                </div>
            </div>
            
            <div class="settings-group">
                <div class="settings-title">Уведомления</div>
                
                <div class="setting-item">
                    <div class="setting-info">
                        <div class="setting-name">Push-уведомления</div>
                        <div class="setting-desc">Получать уведомления о новых ответах</div>
                    </div>
                    <label class="toggle">
                        <input type="checkbox" id="push-notifications" checked>
                        <span class="slider"></span>
                    </label>
                </div>
                
                <div class="setting-item">
                    <div class="setting-info">
                        <div class="setting-name">Звуковые уведомления</div>
                        <div class="setting-desc">Воспроизводить звук при новом сообщении</div>
                    </div>
                    <label class="toggle">
                        <input type="checkbox" id="sound-notifications">
                        <span class="slider"></span>
                    </label>
                </div>
            </div>
            
            <button class="btn btn-secondary" id="reset-settings-btn">Сбросить настройки</button>
        </div>
    </div>

    <!-- Модальное окно загрузки фото -->
    <div class="modal" id="image-modal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">Отправить изображение</div>
                <button class="close-btn" id="close-image-modal">&times;</button>
            </div>
            
            <div class="form-group">
                <label class="form-label">Выберите изображение</label>
                <input type="file" class="form-input" id="image-upload" accept="image/*">
            </div>
            
            <div id="image-preview-container">
                <img id="image-preview" class="image-preview" src="" alt="Предпросмотр">
                <button class="remove-image" id="remove-image">Удалить изображение</button>
            </div>
            
            <div class="form-group">
                <label class="form-label">Описание (необязательно)</label>
                <input type="text" class="form-input" id="image-caption" placeholder="Добавьте описание к изображению...">
            </div>
            
            <button class="btn btn-primary" id="send-image-btn" disabled>Отправить изображение</button>
        </div>
    </div>

    <!-- Уведомление -->
    <div class="notification" id="notification">Сообщение скопировано!</div>

    <script>
        // Данные приложения
        let currentUser = null;
        let messages = [];
        let currentLanguage = 'ru';
        let settings = {
            darkTheme: true,
            fontSize: 'medium',
            pushNotifications: true,
            soundNotifications: false
        };
        
        // DOM элементы
        const splashScreen = document.getElementById('splash-screen');
        const chatContainer = document.getElementById('chat-container');
        const messageInput = document.getElementById('message-input');
        const sendBtn = document.getElementById('send-btn');
        const authModal = document.getElementById('auth-modal');
        const profileModal = document.getElementById('profile-modal');
        const settingsModal = document.getElementById('settings-modal');
        const imageModal = document.getElementById('image-modal');
        const profileBtn = document.getElementById('profile-btn');
        const settingsBtn = document.getElementById('settings-btn');
        const cameraBtn = document.getElementById('camera-btn');
        const galleryBtn = document.getElementById('gallery-btn');
        const closeAuthModal = document.getElementById('close-auth-modal');
        const closeProfileModal = document.getElementById('close-profile-modal');
        const closeSettingsModal = document.getElementById('close-settings-modal');
        const closeImageModal = document.getElementById('close-image-modal');
        const loginBtn = document.getElementById('login-btn');
        const registerBtn = document.getElementById('register-btn');
        const saveProfileBtn = document.getElementById('save-profile-btn');
        const logoutBtn = document.getElementById('logout-btn');
        const sendImageBtn = document.getElementById('send-image-btn');
        const removeImageBtn = document.getElementById('remove-image');
        const imageUpload = document.getElementById('image-upload');
        const imagePreview = document.getElementById('image-preview');
        const resetSettingsBtn = document.getElementById('reset-settings-btn');
        const notification = document.getElementById('notification');
        const languageBtn = document.getElementById('language-btn');
        const languageDropdown = document.getElementById('language-dropdown');
        const currentLangElement = document.getElementById('current-lang');
        const tabs = document.querySelectorAll('.tab');
        const tabContents = document.querySelectorAll('.tab-content');
        
        // Имитация загрузки приложения
        setTimeout(() => {
            splashScreen.style.opacity = '0';
            setTimeout(() => {
                splashScreen.style.display = 'none';
                // Показываем окно авторизации после загрузки
                authModal.classList.add('active');
            }, 500);
        }, 2500);
        
        // Обработчики событий
        sendBtn.addEventListener('click', sendMessage);
        messageInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') sendMessage();
        });
        
        profileBtn.addEventListener('click', () => {
            if (currentUser) {
                openProfileModal();
            } else {
                authModal.classList.add('active');
            }
        });
        
        settingsBtn.addEventListener('click', () => {
            settingsModal.classList.add('active');
        });
        
        cameraBtn.addEventListener('click', () => {
            openImageModal('camera');
        });
        
        galleryBtn.addEventListener('click', () => {
            openImageModal('gallery');
        });
        
        closeAuthModal.addEventListener('click', () => {
            authModal.classList.remove('active');
        });
        
        closeProfileModal.addEventListener('click', () => {
            profileModal.classList.remove('active');
        });
        
        closeSettingsModal.addEventListener('click', () => {
            settingsModal.classList.remove('active');
        });
        
        closeImageModal.addEventListener('click', () => {
            imageModal.classList.remove('active');
            resetImageModal();
        });
        
        loginBtn.addEventListener('click', login);
        registerBtn.addEventListener('click', register);
        saveProfileBtn.addEventListener('click', saveProfile);
        logoutBtn.addEventListener('click', logout);
        sendImageBtn.addEventListener('click', sendImage);
        removeImageBtn.addEventListener('click', resetImageModal);
        resetSettingsBtn.addEventListener('click', resetSettings);
        
        // Языковой переключатель
        languageBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            languageDropdown.classList.toggle('active');
        });
        
        document.querySelectorAll('.language-option').forEach(option => {
            option.addEventListener('click', () => {
                const lang = option.getAttribute('data-lang');
                setLanguage(lang);
                languageDropdown.classList.remove('active');
                showNotification(`Язык изменен на ${lang.toUpperCase()}`);
            });
        });
        
        // Закрытие языкового меню при клике вне его
        document.addEventListener('click', () => {
            languageDropdown.classList.remove('active');
        });
        
        // Обработчики для настроек
        document.getElementById('dark-theme').addEventListener('change', function() {
            settings.darkTheme = this.checked;
            saveSettings();
        });
        
        document.getElementById('push-notifications').addEventListener('change', function() {
            settings.pushNotifications = this.checked;
            saveSettings();
        });
        
        document.getElementById('sound-notifications').addEventListener('change', function() {
            settings.soundNotifications = this.checked;
            saveSettings();
        });
        
        document.getElementById('font-size').addEventListener('change', function() {
            settings.fontSize = this.value;
            saveSettings();
        });
        
        // Обработчик загрузки изображения
        imageUpload.addEventListener('change', function() {
            if (this.files && this.files[0]) {
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    imagePreview.src = e.target.result;
                    imagePreview.style.display = 'block';
                    document.getElementById('remove-image').style.display = 'block';
                    sendImageBtn.disabled = false;
                }
                
                reader.readAsDataURL(this.files[0]);
            }
        });
        
        // Переключение между вкладками входа и регистрации
        tabs.forEach(tab => {
            tab.addEventListener('click', () => {
                const tabId = tab.getAttribute('data-tab');
                
                tabs.forEach(t => t.classList.remove('active'));
                tabContents.forEach(tc => tc.classList.remove('active'));
                
                tab.classList.add('active');
                document.getElementById(`${tabId}-tab`).classList.add('active');
            });
        });
        
        // Функции приложения
        function sendMessage() {
            const messageText = messageInput.value.trim();
            if (!messageText) return;
            
            if (!currentUser) {
                showNotification('Сначала войдите в систему', true);
                authModal.classList.add('active');
                return;
            }
            
            // Добавляем сообщение пользователя
            addMessage(messageText, 'user');
            messageInput.value = '';
            
            // Имитируем ответ ИИ
            setTimeout(() => {
                const aiResponse = generateAIResponse(messageText);
                addMessage(aiResponse, 'ai');
            }, 1000);
        }
        
        function addMessage(text, sender, imageUrl = null) {
            const messageDiv = document.createElement('div');
            messageDiv.classList.add('message', `${sender}-message`);
            
            const messageText = document.createElement('div');
            messageText.textContent = text;
            messageDiv.appendChild(messageText);
            
            // Добавляем изображение, если есть
            if (imageUrl) {
                const messageImage = document.createElement('img');
                messageImage.classList.add('message-image');
                messageImage.src = imageUrl;
                messageDiv.appendChild(messageImage);
            }
            
            // Добавляем действия для сообщений ИИ
            if (sender === 'ai') {
                const actionsDiv = document.createElement('div');
                actionsDiv.classList.add('message-actions');
                
                const likeBtn = document.createElement('button');
                likeBtn.classList.add('action-btn', 'like-btn');
                likeBtn.innerHTML = '<i class="fas fa-thumbs-up"></i>';
                likeBtn.addEventListener('click', () => toggleReaction(likeBtn, 'like'));
                
                const dislikeBtn = document.createElement('button');
                dislikeBtn.classList.add('action-btn', 'dislike-btn');
                dislikeBtn.innerHTML = '<i class="fas fa-thumbs-down"></i>';
                dislikeBtn.addEventListener('click', () => toggleReaction(dislikeBtn, 'dislike'));
                
                const copyBtn = document.createElement('button');
                copyBtn.classList.add('action-btn', 'copy-btn');
                copyBtn.innerHTML = '<i class="fas fa-copy"></i>';
                copyBtn.addEventListener('click', () => copyToClipboard(text));
                
                actionsDiv.appendChild(likeBtn);
                actionsDiv.appendChild(dislikeBtn);
                actionsDiv.appendChild(copyBtn);
                messageDiv.appendChild(actionsDiv);
            }
            
            chatContainer.appendChild(messageDiv);
            chatContainer.scrollTop = chatContainer.scrollHeight;
            
            // Сохраняем сообщение
            messages.push({ text, sender, imageUrl, timestamp: new Date() });
        }
        
        function generateAIResponse(userMessage) {
            const lowerMessage = userMessage.toLowerCase();
            
            if (lowerMessage.includes('привет') || lowerMessage.includes('здравствуй')) {
                return "Привет! Я WowMere - ваша умная нейросеть. Рада вас видеть! 😊";
            } else if (lowerMessage.includes('как дела')) {
                return "У меня всё отлично! Я всегда готова помочь вам с любыми вопросами. А как ваши дела?";
            } else if (lowerMessage.includes('погода')) {
                return "К сожалению, я не имею доступа к актуальным данным о погоде. Но могу предложить проверить погоду в вашем любимом погодном приложении!";
            } else if (lowerMessage.includes('технологи') || lowerMessage.includes('ai')) {
                return "Технологии - это увлекательно! 🤖 Искусственный интеллект - это будущее, которое уже наступило.";
            } else {
                const responses = [
                    `Интересный вопрос! "${userMessage}" - это многогранная тема. Что именно вас интересует?`,
                    `Спасибо за ваш вопрос! Давайте разберем "${userMessage}" подробнее.`,
                    `Отличный вопрос! У меня есть много информации по теме "${userMessage}".`
                ];
                return responses[Math.floor(Math.random() * responses.length)];
            }
        }
        
        function setLanguage(lang) {
            currentLanguage = lang;
            currentLangElement.textContent = lang.toUpperCase();
        }
        
        function openImageModal(source) {
            if (!currentUser) {
                showNotification('Сначала войдите в систему', true);
                authModal.classList.add('active');
                return;
            }
            
            imageModal.classList.add('active');
            
            if (source === 'camera') {
                showNotification('В демо-версии используйте загрузку из галереи', false, 'warning');
            }
        }
        
        function resetImageModal() {
            imageUpload.value = '';
            imagePreview.src = '';
            imagePreview.style.display = 'none';
            document.getElementById('remove-image').style.display = 'none';
            document.getElementById('image-caption').value = '';
            sendImageBtn.disabled = true;
        }
        
        function sendImage() {
            const imageUrl = imagePreview.src;
            const caption = document.getElementById('image-caption').value.trim();
            
            if (!imageUrl) return;
            
            // Добавляем сообщение с изображением
            addMessage(caption || 'Изображение', 'user', imageUrl);
            
            // Закрываем модальное окно и сбрасываем его
            imageModal.classList.remove('active');
            resetImageModal();
            
            // Имитируем ответ ИИ
            setTimeout(() => {
                const aiResponse = "Интересное изображение! К сожалению, в демо-версии я не могу анализировать изображения.";
                addMessage(aiResponse, 'ai');
            }, 1500);
        }
        
        function toggleReaction(button, type) {
            const isActive = button.classList.contains('active');
            
            // Сбрасываем все реакции
            document.querySelectorAll('.like-btn, .dislike-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Устанавливаем новую реакцию, если она не была активна
            if (!isActive) {
                button.classList.add('active');
                showNotification(`Вы ${type === 'like' ? 'оценили' : 'не оценили'} ответ`);
            } else {
                showNotification('Реакция удалена');
            }
        }
        
        function copyToClipboard(text) {
            navigator.clipboard.writeText(text)
                .then(() => {
                    showNotification('Сообщение скопировано!');
                })
                .catch(err => {
                    console.error('Ошибка копирования: ', err);
                    showNotification('Не удалось скопировать', true);
                });
        }
        
        function login() {
            const email = document.getElementById('login-email').value;
            const password = document.getElementById('login-password').value;
            
            if (!email || !password) {
                showNotification('Заполните все поля', true);
                return;
            }
            
            // Имитация входа
            currentUser = {
                id: 1,
                name: 'Пользователь',
                email: email
            };
            
            showNotification('Вход выполнен успешно!');
            authModal.classList.remove('active');
            
            // Добавляем приветственное сообщение
            setTimeout(() => {
                addMessage('Привет! Я WowMere - ваша умная нейросеть. Рада вас видеть! 😊', 'ai');
            }, 500);
        }
        
        function register() {
            const name = document.getElementById('register-name').value;
            const email = document.getElementById('register-email').value;
            const password = document.getElementById('register-password').value;
            
            if (!name || !email || !password) {
                showNotification('Заполните все поля', true);
                return;
            }
            
            if (password.length < 6) {
                showNotification('Пароль должен содержать не менее 6 символов', true);
                return;
            }
            
            // Имитация регистрации
            currentUser = {
                id: Date.now(),
                name: name,
                email: email
            };
            
            showNotification('Регистрация прошла успешно!');
            authModal.classList.remove('active');
            
            // Добавляем приветственное сообщение
            setTimeout(() => {
                addMessage(`Привет, ${name}! Добро пожаловать в WowMere! 🎉`, 'ai');
            }, 500);
        }
        
        function openProfileModal() {
            if (currentUser) {
                document.getElementById('edit-name').value = currentUser.name;
                document.getElementById('edit-email').value = currentUser.email;
                document.getElementById('profile-name').textContent = currentUser.name;
                document.getElementById('profile-email').textContent = currentUser.email;
                profileModal.classList.add('active');
            }
        }
        
        function saveProfile() {
            const name = document.getElementById('edit-name').value;
            const email = document.getElementById('edit-email').value;
            const password = document.getElementById('edit-password').value;
            
            if (!name || !email) {
                showNotification('Заполните обязательные поля', true);
                return;
            }
            
            // Обновляем данные пользователя
            currentUser.name = name;
            currentUser.email = email;
            
            if (password) {
                showNotification('Профиль и пароль успешно обновлены!');
            } else {
                showNotification('Профиль успешно обновлен!');
            }
            
            profileModal.classList.remove('active');
        }
        
        function logout() {
            currentUser = null;
            messages = [];
            chatContainer.innerHTML = '';
            profileModal.classList.remove('active');
            authModal.classList.add('active');
            showNotification('Вы вышли из системы');
        }
        
        function saveSettings() {
            // Сохранение настроек
            showNotification('Настройки сохранены');
        }
        
        function resetSettings() {
            if (confirm('Вы уверены, что хотите сбросить все настройки к значениям по умолчанию?')) {
                showNotification('Настройки сброшены к значениям по умолчанию');
            }
        }
        
        function showNotification(text, isError = false, type = '') {
            notification.textContent = text;
            notification.className = 'notification';
            notification.classList.add('active');
            
            if (isError) {
                notification.classList.add('error');
            } else if (type === 'warning') {
                notification.classList.add('warning');
            }
            
            setTimeout(() => {
                notification.classList.remove('active');
            }, 3000);
        }
        
        // Инициализация приложения
        document.addEventListener('DOMContentLoaded', () => {
            // Добавляем начальное сообщение
            setTimeout(() => {
                if (chatContainer.children.length === 0) {
                    addMessage('Добро пожаловать в WowMere! Пожалуйста, войдите или зарегистрируйтесь, чтобы начать общение.', 'ai');
                }
            }, 3000);
        });
    </script>
</body>
</html>
