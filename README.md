<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Rodina Market СПБ</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&family=Orbitron:wght@400;500;600;700;800;900&display=swap');

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
  }

  :root {
    --bg-primary: #0A0E17;
    --bg-secondary: #111827;
    --bg-card: rgba(17, 24, 39, 0.85);
    --accent: #00D4AA;
    --accent-glow: rgba(0, 212, 170, 0.3);
    --warning: #FF6B6B;
    --purple: #9D73FF;
    --gold: #FFD700;
    --text-primary: #FFFFFF;
    --text-secondary: #B8C1D1;
    --text-muted: #6B7280;
    --border: rgba(255,255,255,0.08);
    --radius: 16px;
    --radius-sm: 10px;
    --radius-xs: 6px;
  }

  body {
    font-family: 'Inter', -apple-system, sans-serif;
    background: var(--bg-primary);
    color: var(--text-primary);
    min-height: 100vh;
    overflow-x: hidden;
    position: relative;
  }

  /* ===== ANIMATED BACKGROUND ===== */
  .bg-animation {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    pointer-events: none;
    overflow: hidden;
  }

  .bg-animation::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: 
      radial-gradient(ellipse at 20% 50%, rgba(0,212,170,0.06) 0%, transparent 50%),
      radial-gradient(ellipse at 80% 20%, rgba(157,115,255,0.05) 0%, transparent 50%),
      radial-gradient(ellipse at 50% 80%, rgba(255,107,107,0.04) 0%, transparent 50%);
    animation: bgFloat 20s ease-in-out infinite;
  }

  @keyframes bgFloat {
    0%, 100% { transform: translate(0, 0) rotate(0deg); }
    33% { transform: translate(30px, -30px) rotate(1deg); }
    66% { transform: translate(-20px, 20px) rotate(-1deg); }
  }

  .grid-overlay {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    pointer-events: none;
    background-image: 
      linear-gradient(rgba(0,212,170,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,212,170,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
  }

  /* ===== APP CONTAINER ===== */
  .app {
    position: relative;
    z-index: 1;
    max-width: 430px;
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  /* ===== SCREENS ===== */
  .screen {
    display: none;
    flex: 1;
    flex-direction: column;
    padding-bottom: 80px;
    animation: screenIn 0.35s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .screen.active {
    display: flex;
  }

  @keyframes screenIn {
    from { opacity: 0; transform: translateY(15px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ===== HEADER ===== */
  .header {
    position: sticky;
    top: 0;
    z-index: 100;
    background: rgba(10, 14, 23, 0.9);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
    padding: 12px 16px;
  }

  .header-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 10px;
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .logo-icon {
    width: 32px;
    height: 32px;
    background: linear-gradient(135deg, var(--accent), #00a888);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    box-shadow: 0 0 15px var(--accent-glow);
  }

  .logo-text {
    font-family: 'Orbitron', sans-serif;
    font-weight: 700;
    font-size: 15px;
    background: linear-gradient(135deg, var(--accent), #ffffff);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .logo-sub {
    font-size: 9px;
    color: var(--text-muted);
    letter-spacing: 2px;
    text-transform: uppercase;
  }

  .header-actions {
    display: flex;
    gap: 8px;
  }

  .header-btn {
    width: 36px;
    height: 36px;
    border-radius: 10px;
    border: 1px solid var(--border);
    background: var(--bg-card);
    color: var(--text-secondary);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    cursor: pointer;
    transition: all 0.2s;
    position: relative;
  }

  .header-btn:active {
    transform: scale(0.92);
  }

  .header-btn .badge {
    position: absolute;
    top: -4px;
    right: -4px;
    width: 16px;
    height: 16px;
    background: var(--warning);
    border-radius: 50%;
    font-size: 9px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
  }

  /* ===== SEARCH BAR ===== */
  .search-bar {
    position: relative;
  }

  .search-bar input {
    width: 100%;
    padding: 10px 16px 10px 40px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border);
    background: rgba(255,255,255,0.04);
    color: var(--text-primary);
    font-size: 14px;
    outline: none;
    transition: all 0.2s;
  }

  .search-bar input::placeholder {
    color: var(--text-muted);
  }

  .search-bar input:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px var(--accent-glow);
  }

  .search-bar .search-icon {
    position: absolute;
    left: 12px;
    top: 50%;
    transform: translateY(-50%);
    color: var(--text-muted);
    font-size: 15px;
  }

  /* ===== CATEGORIES ===== */
  .categories {
    display: flex;
    gap: 8px;
    padding: 12px 16px;
    overflow-x: auto;
    scrollbar-width: none;
    -ms-overflow-style: none;
  }

  .categories::-webkit-scrollbar { display: none; }

  .cat-chip {
    flex-shrink: 0;
    padding: 7px 14px;
    border-radius: 20px;
    border: 1px solid var(--border);
    background: var(--bg-card);
    color: var(--text-secondary);
    font-size: 12px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.2s;
    white-space: nowrap;
  }

  .cat-chip.active {
    background: linear-gradient(135deg, var(--accent), #00a888);
    color: var(--bg-primary);
    border-color: transparent;
    font-weight: 600;
    box-shadow: 0 0 15px var(--accent-glow);
  }

  .cat-chip:active { transform: scale(0.95); }

  /* ===== SECTION HEADER ===== */
  .section-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 8px 16px 12px;
  }

  .section-title {
    font-size: 17px;
    font-weight: 700;
  }

  .section-link {
    font-size: 12px;
    color: var(--accent);
    cursor: pointer;
  }

  /* ===== PRODUCT CARDS ===== */
  .products-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    padding: 0 16px;
  }

  .product-card {
    background: var(--bg-card);
    backdrop-filter: blur(10px);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    overflow: hidden;
    cursor: pointer;
    transition: all 0.25s;
    position: relative;
  }

  .product-card:active {
    transform: scale(0.97);
    border-color: var(--accent);
  }

  .product-img {
    width: 100%;
    aspect-ratio: 1;
    background: var(--bg-secondary);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 48px;
    position: relative;
    overflow: hidden;
  }

  .product-img::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 40px;
    background: linear-gradient(transparent, var(--bg-card));
  }

  .rarity-badge {
    position: absolute;
    top: 6px;
    left: 6px;
    padding: 3px 8px;
    border-radius: 6px;
    font-size: 9px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    z-index: 2;
  }

  .rarity-legendary {
    background: linear-gradient(135deg, #FFD700, #FFA500);
    color: #000;
    animation: legendaryPulse 2s ease-in-out infinite;
  }

  .rarity-epic {
    background: linear-gradient(135deg, #9D73FF, #7C3AED);
    color: #fff;
  }

  .rarity-rare {
    background: linear-gradient(135deg, #3B82F6, #2563EB);
    color: #fff;
  }

  .rarity-common {
    background: rgba(255,255,255,0.15);
    color: var(--text-secondary);
  }

  @keyframes legendaryPulse {
    0%, 100% { box-shadow: 0 0 8px rgba(255,215,0,0.3); }
    50% { box-shadow: 0 0 16px rgba(255,215,0,0.6); }
  }

  .product-info {
    padding: 10px;
  }

  .product-name {
    font-size: 12px;
    font-weight: 600;
    margin-bottom: 4px;
    line-height: 1.3;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  .product-stats {
    display: flex;
    gap: 6px;
    margin-bottom: 8px;
  }

  .stat-tag {
    font-size: 9px;
    padding: 2px 6px;
    border-radius: 4px;
    background: rgba(255,255,255,0.06);
    color: var(--text-muted);
  }

  .product-footer {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .product-price {
    font-size: 14px;
    font-weight: 800;
    color: var(--accent);
    font-family: 'Orbitron', sans-serif;
  }

  .product-seller {
    display: flex;
    align-items: center;
    gap: 4px;
    font-size: 10px;
    color: var(--text-muted);
  }

  .seller-avatar {
    width: 16px;
    height: 16px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--purple), var(--accent));
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 8px;
  }

  .online-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #22C55E;
    box-shadow: 0 0 6px rgba(34,197,94,0.5);
  }

  .urgent-tag {
    position: absolute;
    top: 6px;
    right: 6px;
    padding: 3px 8px;
    border-radius: 6px;
    font-size: 9px;
    font-weight: 700;
    background: var(--warning);
    color: #fff;
    z-index: 2;
    animation: urgentBlink 1.5s ease-in-out infinite;
  }

  @keyframes urgentBlink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.7; }
  }

  /* ===== BANNER ===== */
  .promo-banner {
    margin: 8px 16px 16px;
    padding: 16px;
    border-radius: var(--radius);
    background: linear-gradient(135deg, rgba(157,115,255,0.2), rgba(0,212,170,0.15));
    border: 1px solid rgba(157,115,255,0.3);
    position: relative;
    overflow: hidden;
  }

  .promo-banner::before {
    content: '';
    position: absolute;
    top: -50%;
    right: -20%;
    width: 120px;
    height: 120px;
    background: radial-gradient(circle, rgba(157,115,255,0.2), transparent 70%);
  }

  .promo-title {
    font-size: 14px;
    font-weight: 700;
    margin-bottom: 4px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .promo-text {
    font-size: 11px;
    color: var(--text-secondary);
    line-height: 1.4;
  }

  .promo-btn {
    margin-top: 10px;
    padding: 7px 16px;
    border-radius: 8px;
    border: none;
    background: linear-gradient(135deg, var(--purple), #7C3AED);
    color: #fff;
    font-size: 11px;
    font-weight: 600;
    cursor: pointer;
  }

  /* ===== BOTTOM NAV ===== */
  .bottom-nav {
    position: fixed;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 100%;
    max-width: 430px;
    background: rgba(10, 14, 23, 0.95);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-around;
    padding: 8px 0;
    padding-bottom: max(8px, env(safe-area-inset-bottom));
    z-index: 1000;
  }

  .nav-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 3px;
    cursor: pointer;
    padding: 4px 12px;
    border-radius: 12px;
    transition: all 0.2s;
    position: relative;
  }

  .nav-item:active { transform: scale(0.9); }

  .nav-icon {
    font-size: 22px;
    transition: all 0.2s;
  }

  .nav-label {
    font-size: 10px;
    color: var(--text-muted);
    font-weight: 500;
    transition: all 0.2s;
  }

  .nav-item.active .nav-icon {
    color: var(--accent);
    filter: drop-shadow(0 0 8px var(--accent-glow));
  }

  .nav-item.active .nav-label {
    color: var(--accent);
    font-weight: 600;
  }

  .nav-item.active::before {
    content: '';
    position: absolute;
    top: -8px;
    left: 50%;
    transform: translateX(-50%);
    width: 20px;
    height: 3px;
    border-radius: 0 0 3px 3px;
    background: var(--accent);
    box-shadow: 0 0 10px var(--accent-glow);
  }

  .nav-add {
    width: 48px;
    height: 48px;
    border-radius: 14px;
    background: linear-gradient(135deg, var(--accent), #00a888);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 26px;
    color: var(--bg-primary);
    margin-top: -20px;
    box-shadow: 0 0 20px var(--accent-glow), 0 4px 15px rgba(0,0,0,0.3);
    border: none;
    cursor: pointer;
    transition: all 0.2s;
  }

  .nav-add:active { transform: scale(0.9); }

  /* ===== LOGIN SCREEN ===== */
  .login-screen {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 30px 24px;
    text-align: center;
  }

  .login-logo {
    width: 80px;
    height: 80px;
    background: linear-gradient(135deg, var(--accent), #00a888);
    border-radius: 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 40px;
    margin-bottom: 20px;
    box-shadow: 0 0 40px var(--accent-glow);
    animation: logoFloat 3s ease-in-out infinite;
  }

  @keyframes logoFloat {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
  }

  .login-title {
    font-family: 'Orbitron', sans-serif;
    font-size: 22px;
    font-weight: 800;
    margin-bottom: 6px;
    background: linear-gradient(135deg, var(--accent), #fff);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .login-subtitle {
    font-size: 13px;
    color: var(--text-muted);
    margin-bottom: 30px;
  }

  .login-form {
    width: 100%;
    max-width: 340px;
  }

  .input-group {
    margin-bottom: 14px;
    text-align: left;
  }

  .input-group label {
    display: block;
    font-size: 12px;
    font-weight: 600;
    color: var(--text-secondary);
    margin-bottom: 6px;
  }

  .input-group input {
    width: 100%;
    padding: 12px 16px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border);
    background: rgba(255,255,255,0.04);
    color: var(--text-primary);
    font-size: 14px;
    outline: none;
    transition: all 0.2s;
  }

  .input-group input:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px var(--accent-glow);
  }

  .login-btn {
    width: 100%;
    padding: 14px;
    border-radius: var(--radius-sm);
    border: none;
    background: linear-gradient(135deg, var(--accent), #00a888);
    color: var(--bg-primary);
    font-size: 15px;
    font-weight: 700;
    cursor: pointer;
    margin-top: 8px;
    transition: all 0.2s;
    box-shadow: 0 0 20px var(--accent-glow);
  }

  .login-btn:active { transform: scale(0.97); }

  .divider {
    display: flex;
    align-items: center;
    gap: 12px;
    margin: 20px 0;
    color: var(--text-muted);
    font-size: 12px;
  }

  .divider::before, .divider::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .social-btns {
    display: flex;
    gap: 10px;
  }

  .social-btn {
    flex: 1;
    padding: 12px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border);
    background: var(--bg-card);
    color: var(--text-secondary);
    font-size: 13px;
    font-weight: 500;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    transition: all 0.2s;
  }

  .social-btn:active { transform: scale(0.97); }

  .social-btn.vk { border-color: rgba(39, 135, 245, 0.3); }
  .social-btn.google { border-color: rgba(234, 67, 53, 0.3); }

  /* ===== PROFILE SCREEN ===== */
  .profile-header {
    padding: 20px 16px;
    text-align: center;
    position: relative;
  }

  .profile-avatar {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), var(--purple));
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 32px;
    margin: 0 auto 12px;
    border: 3px solid var(--accent);
    box-shadow: 0 0 20px var(--accent-glow);
    position: relative;
  }

  .profile-verify {
    position: absolute;
    bottom: -2px;
    right: -2px;
    width: 24px;
    height: 24px;
    background: var(--accent);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    border: 2px solid var(--bg-primary);
  }

  .profile-name {
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 4px;
  }

  .profile-server {
    font-size: 12px;
    color: var(--text-muted);
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 4px;
  }

  .profile-rating {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    margin-top: 8px;
    padding: 4px 12px;
    border-radius: 20px;
    background: rgba(255,215,0,0.1);
    border: 1px solid rgba(255,215,0,0.2);
  }

  .profile-rating .stars {
    color: var(--gold);
    font-size: 12px;
  }

  .profile-rating .score {
    font-size: 13px;
    font-weight: 700;
    color: var(--gold);
  }

  .profile-rating .count {
    font-size: 11px;
    color: var(--text-muted);
  }

  .profile-stats {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 10px;
    padding: 0 16px 16px;
  }

  .stat-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    padding: 12px 8px;
    text-align: center;
  }

  .stat-value {
    font-size: 20px;
    font-weight: 800;
    color: var(--accent);
    font-family: 'Orbitron', sans-serif;
  }

  .stat-label {
    font-size: 10px;
    color: var(--text-muted);
    margin-top: 2px;
  }

  .profile-tabs {
    display: flex;
    border-bottom: 1px solid var(--border);
    padding: 0 16px;
  }

  .profile-tab {
    flex: 1;
    padding: 12px 0;
    text-align: center;
    font-size: 13px;
    font-weight: 500;
    color: var(--text-muted);
    cursor: pointer;
    position: relative;
    transition: all 0.2s;
  }

  .profile-tab.active {
    color: var(--accent);
    font-weight: 600;
  }

  .profile-tab.active::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 20%;
    width: 60%;
    height: 2px;
    background: var(--accent);
    border-radius: 2px 2px 0 0;
    box-shadow: 0 0 8px var(--accent-glow);
  }

  .profile-content {
    padding: 12px 16px;
  }

  .deal-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    margin-bottom: 8px;
  }

  .deal-icon {
    width: 44px;
    height: 44px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 22px;
    flex-shrink: 0;
  }

  .deal-info { flex: 1; }

  .deal-name {
    font-size: 13px;
    font-weight: 600;
    margin-bottom: 2px;
  }

  .deal-meta {
    font-size: 11px;
    color: var(--text-muted);
  }

  .deal-price {
    font-size: 14px;
    font-weight: 700;
    font-family: 'Orbitron', sans-serif;
  }

  .deal-price.sold { color: #22C55E; }
  .deal-price.bought { color: var(--accent); }

  /* ===== ADD ITEM SCREEN ===== */
  .add-screen {
    padding: 16px;
  }

  .add-title {
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 20px;
  }

  .form-group {
    margin-bottom: 16px;
  }

  .form-label {
    display: block;
    font-size: 12px;
    font-weight: 600;
    color: var(--text-secondary);
    margin-bottom: 8px;
  }

  .form-input {
    width: 100%;
    padding: 12px 14px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border);
    background: rgba(255,255,255,0.04);
    color: var(--text-primary);
    font-size: 14px;
    outline: none;
    transition: all 0.2s;
    font-family: 'Inter', sans-serif;
  }

  .form-input:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px var(--accent-glow);
  }

  .form-select {
    width: 100%;
    padding: 12px 14px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border);
    background: var(--bg-secondary);
    color: var(--text-primary);
    font-size: 14px;
    outline: none;
    appearance: none;
    cursor: pointer;
    font-family: 'Inter', sans-serif;
  }

  .photo-upload {
    border: 2px dashed var(--border);
    border-radius: var(--radius);
    padding: 30px;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s;
  }

  .photo-upload:active {
    border-color: var(--accent);
    background: rgba(0,212,170,0.05);
  }

  .photo-upload-icon {
    font-size: 36px;
    margin-bottom: 8px;
  }

  .photo-upload-text {
    font-size: 13px;
    color: var(--text-muted);
  }

  .stat-sliders {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .stat-row {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .stat-name {
    font-size: 12px;
    color: var(--text-secondary);
    width: 40px;
    font-weight: 500;
  }

  .stat-slider {
    flex: 1;
    -webkit-appearance: none;
    height: 6px;
    border-radius: 3px;
    background: var(--bg-secondary);
    outline: none;
  }

  .stat-slider::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background: var(--accent);
    cursor: pointer;
    box-shadow: 0 0 10px var(--accent-glow);
  }

  .stat-val {
    font-size: 12px;
    font-weight: 700;
    color: var(--accent);
    width: 30px;
    text-align: right;
    font-family: 'Orbitron', sans-serif;
  }

  .submit-btn {
    width: 100%;
    padding: 14px;
    border-radius: var(--radius-sm);
    border: none;
    background: linear-gradient(135deg, var(--accent), #00a888);
    color: var(--bg-primary);
    font-size: 15px;
    font-weight: 700;
    cursor: pointer;
    margin-top: 8px;
    transition: all 0.2s;
    box-shadow: 0 0 20px var(--accent-glow);
  }

  .submit-btn:active { transform: scale(0.97); }

  /* ===== CHAT SCREEN ===== */
  .chat-list {
    padding: 8px 16px;
  }

  .chat-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px;
    border-radius: var(--radius-sm);
    cursor: pointer;
    transition: all 0.2s;
    margin-bottom: 4px;
  }

  .chat-item:active {
    background: rgba(255,255,255,0.04);
  }

  .chat-avatar {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    flex-shrink: 0;
    position: relative;
  }

  .chat-avatar.online::after {
    content: '';
    position: absolute;
    bottom: 1px;
    right: 1px;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background: #22C55E;
    border: 2px solid var(--bg-primary);
  }

  .chat-info { flex: 1; min-width: 0; }

  .chat-name {
    font-size: 14px;
    font-weight: 600;
    margin-bottom: 2px;
  }

  .chat-last {
    font-size: 12px;
    color: var(--text-muted);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .chat-meta {
    text-align: right;
    flex-shrink: 0;
  }

  .chat-time {
    font-size: 11px;
    color: var(--text-muted);
    margin-bottom: 4px;
  }

  .chat-unread {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: var(--accent);
    color: var(--bg-primary);
    font-size: 11px;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: auto;
  }

  /* ===== CHAT DETAIL (modal) ===== */
  .chat-modal {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: var(--bg-primary);
    z-index: 2000;
    display: none;
    flex-direction: column;
    max-width: 430px;
    left: 50%;
    transform: translateX(-50%);
  }

  .chat-modal.active {
    display: flex;
  }

  .chat-modal-header {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 16px;
    background: rgba(10,14,23,0.95);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
  }

  .chat-back {
    width: 36px;
    height: 36px;
    border-radius: 10px;
    border: 1px solid var(--border);
    background: var(--bg-card);
    color: var(--text-secondary);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    cursor: pointer;
  }

  .chat-modal-user {
    flex: 1;
  }

  .chat-modal-name {
    font-size: 15px;
    font-weight: 600;
  }

  .chat-modal-status {
    font-size: 11px;
    color: #22C55E;
  }

  .chat-messages {
    flex: 1;
    overflow-y: auto;
    padding: 16px;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .message {
    max-width: 80%;
    padding: 10px 14px;
    border-radius: 16px;
    font-size: 13px;
    line-height: 1.4;
    animation: msgIn 0.3s ease;
  }

  @keyframes msgIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .message.incoming {
    background: var(--bg-card);
    border: 1px solid var(--border);
    align-self: flex-start;
    border-bottom-left-radius: 4px;
  }

  .message.outgoing {
    background: linear-gradient(135deg, rgba(0,212,170,0.2), rgba(0,212,170,0.1));
    border: 1px solid rgba(0,212,170,0.2);
    align-self: flex-end;
    border-bottom-right-radius: 4px;
  }

  .message-time {
    font-size: 10px;
    color: var(--text-muted);
    margin-top: 4px;
  }

  .system-msg {
    text-align: center;
    font-size: 11px;
    color: var(--text-muted);
    padding: 8px 16px;
    background: rgba(255,107,107,0.08);
    border-radius: 8px;
    border: 1px solid rgba(255,107,107,0.15);
  }

  .chat-input-area {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 12px 16px;
    background: rgba(10,14,23,0.95);
    border-top: 1px solid var(--border);
  }

  .chat-input {
    flex: 1;
    padding: 10px 14px;
    border-radius: 20px;
    border: 1px solid var(--border);
    background: rgba(255,255,255,0.04);
    color: var(--text-primary);
    font-size: 13px;
    outline: none;
    font-family: 'Inter', sans-serif;
  }

  .chat-input:focus {
    border-color: var(--accent);
  }

  .chat-send {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: none;
    background: linear-gradient(135deg, var(--accent), #00a888);
    color: var(--bg-primary);
    font-size: 18px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
  }

  .chat-send:active { transform: scale(0.9); }

  .chat-templates {
    display: flex;
    gap: 6px;
    padding: 8px 16px;
    overflow-x: auto;
    scrollbar-width: none;
  }

  .chat-templates::-webkit-scrollbar { display: none; }

  .template-btn {
    flex-shrink: 0;
    padding: 6px 12px;
    border-radius: 16px;
    border: 1px solid var(--border);
    background: var(--bg-card);
    color: var(--text-secondary);
    font-size: 11px;
    cursor: pointer;
    transition: all 0.2s;
  }

  .template-btn:active {
    border-color: var(--accent);
    color: var(--accent);
  }

  /* ===== PRODUCT DETAIL MODAL ===== */
  .product-modal {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: var(--bg-primary);
    z-index: 2000;
    display: none;
    flex-direction: column;
    max-width: 430px;
    left: 50%;
    transform: translateX(-50%);
    overflow-y: auto;
  }

  .product-modal.active { display: flex; }

  .pm-header {
    position: sticky;
    top: 0;
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 12px 16px;
    background: rgba(10,14,23,0.95);
    backdrop-filter: blur(20px);
  }

  .pm-back {
    width: 36px;
    height: 36px;
    border-radius: 10px;
    border: 1px solid var(--border);
    background: var(--bg-card);
    color: var(--text-secondary);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    cursor: pointer;
  }

  .pm-image {
    width: 100%;
    aspect-ratio: 4/3;
    background: var(--bg-secondary);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 80px;
    position: relative;
  }

  .pm-content {
    padding: 20px 16px;
  }

  .pm-rarity {
    display: inline-block;
    padding: 4px 10px;
    border-radius: 6px;
    font-size: 10px;
    font-weight: 700;
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .pm-name {
    font-size: 22px;
    font-weight: 800;
    margin-bottom: 8px;
    line-height: 1.2;
  }

  .pm-stats {
    display: flex;
    gap: 10px;
    margin-bottom: 16px;
  }

  .pm-stat {
    padding: 8px 14px;
    border-radius: var(--radius-sm);
    background: var(--bg-card);
    border: 1px solid var(--border);
    text-align: center;
  }

  .pm-stat-val {
    font-size: 16px;
    font-weight: 800;
    color: var(--accent);
    font-family: 'Orbitron', sans-serif;
  }

  .pm-stat-label {
    font-size: 10px;
    color: var(--text-muted);
    margin-top: 2px;
  }

  .pm-desc {
    font-size: 13px;
    color: var(--text-secondary);
    line-height: 1.5;
    margin-bottom: 16px;
  }

  .pm-seller {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 14px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    margin-bottom: 16px;
  }

  .pm-seller-avatar {
    width: 44px;
    height: 44px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--purple), var(--accent));
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
  }

  .pm-seller-info { flex: 1; }

  .pm-seller-name {
    font-size: 14px;
    font-weight: 600;
  }

  .pm-seller-rating {
    font-size: 11px;
    color: var(--gold);
  }

  .pm-price-block {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 16px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    margin-bottom: 16px;
  }

  .pm-price {
    font-size: 24px;
    font-weight: 900;
    color: var(--accent);
    font-family: 'Orbitron', sans-serif;
  }

  .pm-price-sub {
    font-size: 11px;
    color: var(--text-muted);
  }

  .pm-actions {
    display: flex;
    gap: 10px;
  }

  .pm-buy-btn {
    flex: 1;
    padding: 14px;
    border-radius: var(--radius-sm);
    border: none;
    background: linear-gradient(135deg, var(--accent), #00a888);
    color: var(--bg-primary);
    font-size: 15px;
    font-weight: 700;
    cursor: pointer;
    box-shadow: 0 0 20px var(--accent-glow);
  }

  .pm-chat-btn {
    width: 52px;
    height: 52px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border);
    background: var(--bg-card);
    color: var(--text-secondary);
    font-size: 22px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  /* ===== NOTIFICATION TOAST ===== */
  .toast {
    position: fixed;
    top: 20px;
    left: 50%;
    transform: translateX(-50%) translateY(-100px);
    max-width: 380px;
    width: calc(100% - 32px);
    padding: 12px 16px;
    border-radius: var(--radius-sm);
    background: var(--bg-card);
    border: 1px solid var(--accent);
    box-shadow: 0 10px 30px rgba(0,0,0,0.5), 0 0 20px var(--accent-glow);
    z-index: 9999;
    display: flex;
    align-items: center;
    gap: 10px;
    transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    font-size: 13px;
    font-weight: 500;
  }

  .toast.show {
    transform: translateX(-50%) translateY(0);
  }

  .toast-icon {
    font-size: 20px;
    flex-shrink: 0;
  }

  /* ===== SCROLLBAR ===== */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }

  /* ===== RESPONSIVE ===== */
  @media (min-width: 431px) {
    .app { border-left: 1px solid var(--border); border-right: 1px solid var(--border); }
  }

  /* ===== GUARANTEE CHECK ===== */
  .guarantee-card {
    margin: 0 16px 16px;
    padding: 14px;
    border-radius: var(--radius-sm);
    background: linear-gradient(135deg, rgba(0,212,170,0.1), rgba(157,115,255,0.08));
    border: 1px solid rgba(0,212,170,0.2);
  }

  .guarantee-title {
    font-size: 13px;
    font-weight: 700;
    margin-bottom: 8px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .guarantee-steps {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  .guarantee-step {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 11px;
    color: var(--text-secondary);
  }

  .guarantee-num {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: var(--accent);
    color: var(--bg-primary);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 10px;
    font-weight: 700;
    flex-shrink: 0;
  }

  /* ===== SETTINGS ===== */
  .settings-group {
    padding: 0 16px;
    margin-bottom: 16px;
  }

  .settings-group-title {
    font-size: 12px;
    font-weight: 600;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 1px;
    padding: 8px 0;
  }

  .settings-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 14px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    margin-bottom: 4px;
    cursor: pointer;
    transition: all 0.2s;
  }

  .settings-item:active {
    background: rgba(255,255,255,0.06);
  }

  .settings-left {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .settings-icon {
    width: 36px;
    height: 36px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
  }

  .settings-label {
    font-size: 14px;
    font-weight: 500;
  }

  .toggle {
    width: 44px;
    height: 24px;
    border-radius: 12px;
    background: var(--bg-secondary);
    border: 1px solid var(--border);
    position: relative;
    cursor: pointer;
    transition: all 0.3s;
  }

  .toggle.on {
    background: var(--accent);
    border-color: var(--accent);
  }

  .toggle::after {
    content: '';
    position: absolute;
    top: 2px;
    left: 2px;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background: #fff;
    transition: all 0.3s;
  }

  .toggle.on::after {
    left: 22px;
  }

  .settings-arrow {
    color: var(--text-muted);
    font-size: 14px;
  }

  .logout-btn {
    margin: 16px;
    padding: 14px;
    border-radius: var(--radius-sm);
    border: 1px solid rgba(255,107,107,0.3);
    background: rgba(255,107,107,0.08);
    color: var(--warning);
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    text-align: center;
    transition: all 0.2s;
  }

  .logout-btn:active { transform: scale(0.97); }

  /* ===== LOADING ===== */
  .loading-screen {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    gap: 16px;
  }

  .loader {
    width: 50px;
    height: 50px;
    border: 3px solid var(--border);
    border-top-color: var(--accent);
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
  }

  @keyframes spin {
    to { transform: rotate(360deg); }
  }

  .loading-text {
    font-size: 14px;
    color: var(--text-muted);
    font-family: 'Orbitron', sans-serif;
    letter-spacing: 2px;
  }

  /* ===== EMPTY STATE ===== */
  .empty-state {
    text-align: center;
    padding: 40px 20px;
  }

  .empty-icon {
    font-size: 48px;
    margin-bottom: 12px;
  }

  .empty-title {
    font-size: 16px;
    font-weight: 600;
    margin-bottom: 4px;
  }

  .empty-text {
    font-size: 13px;
    color: var(--text-muted);
  }
</style>
</head>
<body>

<div class="bg-animation"></div>
<div class="grid-overlay"></div>

<div class="app" id="app">

  <!-- ===== LOADING SCREEN ===== -->
  <div class="screen active" id="screen-loading">
    <div class="loading-screen">
      <div class="loader"></div>
      <div class="loading-text">RODINA MARKET</div>
      <div style="font-size:11px;color:var(--text-muted);">Загрузка сервера СПБ...</div>
    </div>
  </div>

  <!-- ===== LOGIN SCREEN ===== -->
  <div class="screen" id="screen-login">
    <div class="login-screen">
      <div class="login-logo">🏪</div>
      <div class="login-title">RODINA MARKET</div>
      <div class="login-subtitle">Торговая площадка сервера СПБ</div>
      
      <div class="login-form">
        <div class="input-group">
          <label>🎮 Игровой никнейм</label>
          <input type="text" id="login-nick" placeholder="Nick_Name" value="Shadow_Hunter">
        </div>
        <div class="input-group">
          <label>🔑 Пароль от аккаунта</label>
          <input type="password" id="login-pass" placeholder="••••••••" value="password">
        </div>
        <button class="login-btn" onclick="doLogin()">🚀 Войти в аккаунт</button>
        
        <div class="divider">или войти через</div>
        
        <div class="social-btns">
          <button class="social-btn vk" onclick="doLogin()">
            <span>🔵</span> ВКонтакте
          </button>
          <button class="social-btn google" onclick="doLogin()">
            <span>🔴</span> Google
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- ===== MARKET SCREEN ===== -->
  <div class="screen" id="screen-market">
    <div class="header">
      <div class="header-top">
        <div class="logo">
          <div class="logo-icon">🏪</div>
          <div>
            <div class="logo-text">RODINA MARKET</div>
            <div class="logo-sub">САНКТ-ПЕТЕРБУРГ</div>
          </div>
        </div>
        <div class="header-actions">
          <div class="header-btn" onclick="showToast('🔔', 'Нет новых уведомлений')">
            🔔
            <div class="badge">3</div>
          </div>
          <div class="header-btn" onclick="switchTab('profile')">👤</div>
        </div>
      </div>
      <div class="search-bar">
        <span class="search-icon">🔍</span>
        <input type="text" placeholder="Поиск предметов, продавцов..." id="search-input" oninput="filterProducts()">
      </div>
    </div>

    <div class="categories" id="categories">
      <div class="cat-chip active" data-cat="all" onclick="setCategory(this)">🔥 Все</div>
      <div class="cat-chip" data-cat="axs" onclick="setCategory(this)">🎒 Аксы</div>
      <div class="cat-chip" data-cat="shards" onclick="setCategory(this)">💎 Осколки</div>
      <div class="cat-chip" data-cat="certs" onclick="setCategory(this)">📜 Сертификаты</div>
      <div class="cat-chip" data-cat="tuning" onclick="setCategory(this)">🚗 Тюнинг</div>
      <div class="cat-chip" data-cat="skins" onclick="setCategory(this)">🎨 Скины</div>
      <div class="cat-chip" data-cat="resources" onclick="setCategory(this)">📦 Ресурсы</div>
    </div>

    <div class="promo-banner">
      <div class="promo-title">🎉 Сезонная распродажа!</div>
      <div class="promo-text">Скидки до 30% на аксессуары до конца недели. Успей купить!</div>
      <button class="promo-btn">Смотреть предложения →</button>
    </div>

    <div class="section-header">
      <div class="section-title">🔥 Актуальные лоты</div>
      <div class="section-link">Фильтры ⚙️</div>
    </div>

    <div class="products-grid" id="products-grid">
      <!-- Products will be injected by JS -->
    </div>

    <div style="height:20px"></div>
  </div>

  <!-- ===== ADD ITEM SCREEN ===== -->
  <div class="screen" id="screen-add">
    <div class="header">
      <div class="header-top">
        <div class="logo">
          <div class="logo-icon">➕</div>
          <div>
            <div class="logo-text">НОВЫЙ ЛОТ</div>
            <div class="logo-sub">Разместить товар</div>
          </div>
        </div>
      </div>
    </div>

    <div class="add-screen">
      <div class="form-group">
        <div class="photo-upload" onclick="document.getElementById('file-input').click()">
          <div class="photo-upload-icon">📸</div>
          <div class="photo-upload-text">Нажмите для загрузки скриншота<br>или перетащите изображение</div>
        </div>
        <input type="file" id="file-input" style="display:none" accept="image/*">
      </div>

      <div class="form-group">
        <label class="form-label">🏷️ Название предмета</label>
        <input class="form-input" placeholder="Например: Космический кроссовок" value="Легендарный Космический кроссовок">
      </div>

      <div class="form-group">
        <label class="form-label">📂 Категория</label>
        <select class="form-select">
          <option>🎒 Аксессуары (аксы)</option>
          <option>💎 Осколки / Крафт</option>
          <option>📜 Сертификаты</option>
          <option>🚗 Тюнинг авто</option>
          <option>🎨 Скины / Косметика</option>
          <option>📦 Ресурсы / Валюта</option>
        </select>
      </div>

      <div class="form-group">
        <label class="form-label">📊 Характеристики</label>
        <div class="stat-sliders">
          <div class="stat-row">
            <span class="stat-name">HP</span>
            <input type="range" class="stat-slider" min="0" max="200" value="150" oninput="this.nextElementSibling.textContent=this.value">
            <span class="stat-val">150</span>
          </div>
          <div class="stat-row">
            <span class="stat-name">ЗАЩ</span>
            <input type="range" class="stat-slider" min="0" max="200" value="80" oninput="this.nextElementSibling.textContent=this.value">
            <span class="stat-val">80</span>
          </div>
          <div class="stat-row">
            <span class="stat-name">УРН</span>
            <input type="range" class="stat-slider" min="0" max="200" value="120" oninput="this.nextElementSibling.textContent=this.value">
            <span class="stat-val">120</span>
          </div>
        </div>
      </div>

      <div class="form-group">
        <label class="form-label">💵 Цена (вирт. ₽)</label>
        <input class="form-input" type="number" placeholder="2450000" value="2450000" style="font-family:'Orbitron',sans-serif;font-weight:700;">
      </div>

      <div class="form-group">
        <label class="form-label">📢 Описание</label>
        <textarea class="form-input" rows="3" placeholder="Опишите предмет, условия обмена..." style="resize:none;">Топовый акс для PvP, полный комплект. Обмен возможен. Срочная продажа!</textarea>
      </div>

      <div class="form-group" style="display:flex;align-items:center;justify-content:space-between;">
        <span class="form-label" style="margin:0;">🔄 Разрешить обмен</span>
        <div class="toggle on" onclick="this.classList.toggle('on')"></div>
      </div>

      <div class="form-group" style="display:flex;align-items:center;justify-content:space-between;">
        <span class="form-label" style="margin:0;">⚡ Срочная продажа</span>
        <div class="toggle" onclick="this.classList.toggle('on')"></div>
      </div>

      <button class="submit-btn" onclick="submitProduct()">📢 Опубликовать лот</button>
    </div>
  </div>

  <!-- ===== CHAT SCREEN ===== -->
  <div class="screen" id="screen-chats">
    <div class="header">
      <div class="header-top">
        <div class="logo">
          <div class="logo-icon">💬</div>
          <div>
            <div class="logo-text">СООБЩЕНИЯ</div>
            <div class="logo-sub">Безопасный чат</div>
          </div>
        </div>
        <div class="header-actions">
          <div class="header-btn" onclick="showToast('🛡️','Правила безопасной торговли в чате')">🛡️</div>
        </div>
      </div>
    </div>

    <div class="chat-list" id="chat-list">
      <!-- Chats injected by JS -->
    </div>
  </div>

  <!-- ===== PROFILE SCREEN ===== -->
  <div class="screen" id="screen-profile">
    <div class="header">
      <div class="header-top">
        <div class="logo">
          <div class="logo-icon">👤</div>
          <div>
            <div class="logo-text">ПРОФИЛЬ</div>
            <div class="logo-sub">Shadow_Hunter</div>
          </div>
        </div>
        <div class="header-actions">
          <div class="header-btn" onclick="showToast('⚙️','Настройки')">⚙️</div>
        </div>
      </div>
    </div>

    <div class="profile-header">
      <div class="profile-avatar">
        🦊
        <div class="profile-verify">✓</div>
      </div>
      <div class="profile-name">Shadow_Hunter</div>
      <div class="profile-server">📍 Сервер: Санкт-Петербург</div>
      <div class="profile-rating">
        <span class="stars">★★★★★</span>
        <span class="score">4.8</span>
        <span class="count">(127 сделок)</span>
      </div>
    </div>

    <div class="profile-stats">
      <div class="stat-card">
        <div class="stat-value">43</div>
        <div class="stat-label">Продано</div>
      </div>
      <div class="stat-card">
        <div class="stat-value">31</div>
        <div class="stat-label">Куплено</div>
      </div>
      <div class="stat-card">
        <div class="stat-value">7</div>
        <div class="stat-label">В продаже</div>
      </div>
    </div>

    <div class="profile-tabs">
      <div class="profile-tab active" onclick="switchProfileTab(this, 'my-lots')">🛍️ Мои товары</div>
      <div class="profile-tab" onclick="switchProfileTab(this, 'history')">📜 История</div>
      <div class="profile-tab" onclick="switchProfileTab(this, 'settings')">⚙️ Настройки</div>
    </div>

    <div class="profile-content" id="profile-content">
      <!-- Content injected by JS -->
    </div>
  </div>

  <!-- ===== BOTTOM NAV ===== -->
  <nav class="bottom-nav" id="bottom-nav" style="display:none;">
    <div class="nav-item active" data-screen="market" onclick="switchTab('market')">
      <span class="nav-icon">🏪</span>
      <span class="nav-label">Маркет</span>
    </div>
    <div class="nav-item" data-screen="chats" onclick="switchTab('chats')">
      <span class="nav-icon">💬</span>
      <span class="nav-label">Чаты</span>
    </div>
    <button class="nav-add" onclick="switchTab('add')">➕</button>
    <div class="nav-item" data-screen="profile" onclick="switchTab('profile')">
      <span class="nav-icon">👤</span>
      <span class="nav-label">Профиль</span>
    </div>
    <div class="nav-item" data-screen="more" onclick="showToast('📋','Раздел в разработке')">
      <span class="nav-icon">☰</span>
      <span class="nav-label">Ещё</span>
    </div>
  </nav>
</div>

<!-- ===== CHAT MODAL ===== -->
<div class="chat-modal" id="chat-modal">
  <div class="chat-modal-header">
    <div class="chat-back" onclick="closeChatModal()">←</div>
    <div class="chat-avatar online" style="width:36px;height:36px;font-size:16px;border-radius:50%;background:linear-gradient(135deg,#9D73FF,#00D4AA);display:flex;align-items:center;justify-content:center;" id="cm-avatar">🐺</div>
    <div class="chat-modal-user">
      <div class="chat-modal-name" id="cm-name">White_Wolf</div>
      <div class="chat-modal-status">🟢 Онлайн в игре</div>
    </div>
    <div class="header-btn" onclick="showToast('⚠️','Жалоба отправлена модераторам')">⚠️</div>
  </div>
  <div class="system-msg">
    🔒 Безопасный чат • Не переводите деньги вне игры!
  </div>
  <div class="chat-templates">
    <button class="template-btn" onclick="sendTemplate('Готов купить, какой способ обмена?')">💰 Готов купить</button>
    <button class="template-btn" onclick="sendTemplate('Можете сделать скриншот предмета в инвентаре?')">📸 Скриншот</button>
    <button class="template-btn" onclick="sendTemplate('Договорились, встречаемся в игре: площадь Восстания')">📍 Встреча</button>
    <button class="template-btn" onclick="sendTemplate('Цена окончательная?')">🤔 Торг</button>
  </div>
  <div class="chat-messages" id="chat-messages">
    <!-- Messages injected by JS -->
  </div>
  <div class="chat-input-area">
    <input class="chat-input" id="chat-input" placeholder="Введите сообщение..." onkeydown="if(event.key==='Enter')sendMessage()">
    <button class="chat-send" onclick="sendMessage()">➤</button>
  </div>
</div>

<!-- ===== PRODUCT DETAIL MODAL ===== -->
<div class="product-modal" id="product-modal">
  <div class="pm-header">
    <div class="pm-back" onclick="closeProductModal()">←</div>
    <div style="font-size:14px;font-weight:600;">Детали лота</div>
    <div class="header-btn" onclick="showToast('❤️','Добавлено в избранное')">❤️</div>
  </div>
  <div class="pm-image" id="pm-image">👟</div>
  <div class="pm-content">
    <div class="pm-rarity" id="pm-rarity">ЛЕГЕНДАРНЫЙ</div>
    <div class="pm-name" id="pm-name">Легендарный Космический кроссовок</div>
    <div class="pm-stats" id="pm-stats">
      <div class="pm-stat"><div class="pm-stat-val">150</div><div class="pm-stat-label">HP</div></div>
      <div class="pm-stat"><div class="pm-stat-val">80</div><div class="pm-stat-label">ЗАЩ</div></div>
      <div class="pm-stat"><div class="pm-stat-val">120</div><div class="pm-stat-label">УРН</div></div>
    </div>
    <div class="pm-desc" id="pm-desc">Топовый акс для PvP, полный комплект. Обмен возможен. Срочная продажа!</div>
    
    <div class="pm-seller">
      <div class="pm-seller-avatar" id="pm-seller-avatar">🐺</div>
      <div class="pm-seller-info">
        <div class="pm-seller-name" id="pm-seller-name">White_Wolf</div>
        <div class="pm-seller-rating">⭐ 4.9 • 89 сделок • 🟢 Онлайн</div>
      </div>
    </div>

    <div class="guarantee-card">
      <div class="guarantee-title">🛡️ Гарант-чек сделки</div>
      <div class="guarantee-steps">
        <div class="guarantee-step"><div class="guarantee-num">1</div> Обсудите детали в чате</div>
        <div class="guarantee-step"><div class="guarantee-num">2</div> Продавец создаёт оферту</div>
        <div class="guarantee-step"><div class="guarantee-num">3</div> Обмен в игре по инструкции</div>
        <div class="guarantee-step"><div class="guarantee-num">4</div> Подтвердите сделку</div>
      </div>
    </div>

    <div class="pm-price-block">
      <div>
        <div class="pm-price" id="pm-price">2 450 000 ₽</div>
        <div class="pm-price-sub">виртуальные рубли</div>
      </div>
    </div>

    <div class="pm-actions">
      <button class="pm-buy-btn" onclick="showToast('✅','Оферта отправлена продавцу!');closeProductModal();">🤝 Купить</button>
      <button class="pm-chat-btn" onclick="openChatFromProduct();">💬</button>
    </div>
  </div>
</div>

<!-- ===== TOAST ===== -->
<div class="toast" id="toast">
  <span class="toast-icon" id="toast-icon">✅</span>
  <span id="toast-text">Уведомление</span>
</div>

<script>
// ===== DATA =====
const products = [
  { id:1, name:"Космический кроссовок", icon:"👟", rarity:"legendary", rarityLabel:"ЛЕГЕНДА", hp:150, def:80, atk:120, price:2450000, seller:"White_Wolf", sellerIcon:"🐺", online:true, cat:"axs", desc:"Топовый акс для PvP, полный комплект. Обмен возможен.", urgent:true },
  { id:2, name:"Осколки хаоса x50", icon:"💎", rarity:"epic", rarityLabel:"ЭПИК", hp:0, def:0, atk:0, price:890000, seller:"DarkMage_SPB", sellerIcon:"🧙", online:false, cat:"shards", desc:"Полный стак осколков для крафта легендарного оружия." },
  { id:3, name:"Сертификат на BMW M5", icon:"📜", rarity:"epic", rarityLabel:"ЭПИК", hp:0, def:0, atk:0, price:5200000, seller:"AutoTrader", sellerIcon:"🏎️", online:true, cat:"certs", desc:"Сертификат на получение BMW M5 F90 с полным тюнингом." },
  { id:4, name:"Неоновый обвес GT-R", icon:"🚗", rarity:"rare", rarityLabel:"РЕДКИЙ", hp:0, def:0, atk:0, price:1750000, seller:"TuningMaster", sellerIcon:"🔧", online:true, cat:"tuning", desc:"Полный неоновый обвес для Nissan GT-R R35. Включает спойлер, бампер, капот." },
  { id:5, name:"Скин «Призрак»", icon:"👻", rarity:"rare", rarityLabel:"РЕДКИЙ", hp:0, def:0, atk:0, price:650000, seller:"GhostRider", sellerIcon:"💀", online:false, cat:"skins", desc:"Эксклюзивный скин персонажа «Призрак». Лимитированная серия." },
  { id:6, name:"Ресурсы: Сталь x200", icon:"📦", rarity:"common", rarityLabel:"ОБЫЧНЫЙ", hp:0, def:0, atk:0, price:320000, seller:"FarmerPro", sellerIcon:"⛏️", online:true, cat:"resources", desc:"Большой стак стали для крафта. Быстрая доставка." },
  { id:7, name:"Золотая цепь «Император»", icon:"📿", rarity:"legendary", rarityLabel:"ЛЕГЕНДА", hp:50, def:30, atk:10, price:3100000, seller:"KingPin_SPB", sellerIcon:"👑", online:true, cat:"axs", desc:"Уникальная золотая цепь. Статы: HP+50, Защита+30." },
  { id:8, name:"Осколки стихий x100", icon:"🔮", rarity:"epic", rarityLabel:"ЭПИК", hp:0, def:0, atk:0, price:1200000, seller:"Elementalist", sellerIcon:"🌟", online:false, cat:"shards", desc:"Осколки всех стихий для крафта мифического оружия." },
];

const chats = [
  { id:1, name:"White_Wolf", icon:"🐺", bg:"linear-gradient(135deg,#9D73FF,#00D4AA)", online:true, lastMsg:"Да, цена окончательная. Встречаемся на площади?", time:"19:42", unread:2,
    messages:[
      {type:'system', text:'🔒 Безопасный чат активирован. Не переводите деньги вне игры!'},
      {type:'incoming', text:'Привет! Вижу ты выставил космический кроссовок', time:'19:30'},
      {type:'outgoing', text:'Привет! Да, он ещё в продаже. Интересует?', time:'19:32'},
      {type:'incoming', text:'Да, хочу купить. Можешь сделать скриншот статов?', time:'19:35'},
      {type:'outgoing', text:'Конечно, сейчас скину. Цена 2.45кк, торг уместен', time:'19:38'},
      {type:'incoming', text:'Да, цена окончательная. Встречаемся на площади?', time:'19:42'},
    ]
  },
  { id:2, name:"DarkMage_SPB", icon:"🧙", bg:"linear-gradient(135deg,#7C3AED,#EC4899)", online:false, lastMsg:"Отправил осколки, проверь инвентарь", time:"18:15", unread:0,
    messages:[
      {type:'system', text:'🔒 Безопасный чат активирован'},
      {type:'incoming', text:'Привет, продаю осколки хаоса, 50 штук', time:'17:50'},
      {type:'outgoing', text:'Сколько за весь стак?', time:'17:55'},
      {type:'incoming', text:'890к, цена фиксированная', time:'18:00'},
      {type:'outgoing', text:'Договорились, кидай обмен', time:'18:10'},
      {type:'incoming', text:'Отправил осколки, проверь инвентарь', time:'18:15'},
    ]
  },
  { id:3, name:"AutoTrader", icon:"🏎️", bg:"linear-gradient(135deg,#F59E0B,#EF4444)", online:true, lastMsg:"Сертификат ещё актуален", time:"16:30", unread:1,
    messages:[
      {type:'system', text:'🔒 Безопасный чат активирован'},
      {type:'outgoing', text:'Привет, сертификат на BMW ещё в продаже?', time:'16:20'},
      {type:'incoming', text:'Сертификат ещё актуален', time:'16:30'},
    ]
  },
  { id:4, name:"TuningMaster", icon:"🔧", bg:"linear-gradient(135deg,#10B981,#3B82F6)", online:true, lastMsg:"Обвес в отличном состоянии", time:"вчера", unread:0,
    messages:[
      {type:'system', text:'🔒 Безопасный чат активирован'},
      {type:'incoming', text:'Продаю неоновый обвес на GT-R', time:'вчера'},
    ]
  }
];

// ===== SCREEN MANAGEMENT =====
let currentScreen = 'loading';

function showScreen(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById('screen-' + id).classList.add('active');
  currentScreen = id;
  
  const nav = document.getElementById('bottom-nav');
  nav.style.display = (id === 'loading' || id === 'login') ? 'none' : 'flex';
  
  // Update nav active state
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  const navItem = document.querySelector(`.nav-item[data-screen="${id}"]`);
  if (navItem) navItem.classList.add('active');
}

function switchTab(tab) {
  showScreen(tab);
  if (tab === 'profile') renderProfileContent('my-lots');
}

// ===== INIT =====
window.addEventListener('load', () => {
  setTimeout(() => {
    showScreen('login');
  }, 1500);
});

function doLogin() {
  showScreen('market');
  renderProducts(products);
  renderChats();
  renderProfileContent('my-lots');
  showToast('🎮', 'Добро пожаловать, Shadow_Hunter!');
}

// ===== PRODUCTS =====
let currentCategory = 'all';

function setCategory(el) {
  document.querySelectorAll('.cat-chip').forEach(c => c.classList.remove('active'));
  el.classList.add('active');
  currentCategory = el.dataset.cat;
  renderProducts(products);
}

function renderProducts(list) {
  const grid = document.getElementById('products-grid');
  const search = (document.getElementById('search-input')?.value || '').toLowerCase();
  
  let filtered = list;
  if (currentCategory !== 'all') {
    filtered = filtered.filter(p => p.cat === currentCategory);
  }
  if (search) {
    filtered = filtered.filter(p => p.name.toLowerCase().includes(search) || p.seller.toLowerCase().includes(search));
  }

  grid.innerHTML = filtered.map(p => `
    <div class="product-card" onclick="openProduct(${p.id})">
      <div class="product-img">
        ${p.icon}
        <div class="rarity-badge rarity-${p.rarity}">${p.rarityLabel}</div>
        ${p.urgent ? '<div class="urgent-tag">🔥 СРОЧНО</div>' : ''}
      </div>
      <div class="product-info">
        <div class="product-name">${p.name}</div>
        <div class="product-stats">
          ${p.hp ? `<span class="stat-tag">HP ${p.hp}</span>` : ''}
          ${p.def ? `<span class="stat-tag">ЗАЩ ${p.def}</span>` : ''}
          ${p.atk ? `<span class="stat-tag">УРН ${p.atk}</span>` : ''}
        </div>
        <div class="product-footer">
          <div class="product-price">${(p.price/1000).toFixed(0)}к</div>
          <div class="product-seller">
            <div class="seller-avatar">${p.sellerIcon}</div>
            ${p.seller.split('_')[0]}
            ${p.online ? '<div class="online-dot"></div>' : ''}
          </div>
        </div>
      </div>
    </div>
  `).join('');

  if (filtered.length === 0) {
    grid.innerHTML = `
      <div class="empty-state" style="grid-column:1/-1;">
        <div class="empty-icon">🔍</div>
        <div class="empty-title">Ничего не найдено</div>
        <div class="empty-text">Попробуйте изменить фильтры или поисковый запрос</div>
      </div>
    `;
  }
}

function filterProducts() {
  renderProducts(products);
}

function openProduct(id) {
  const p = products.find(x => x.id === id);
  if (!p) return;
  
  document.getElementById('pm-image').textContent = p.icon;
  document.getElementById('pm-rarity').textContent = p.rarityLabel;
  document.getElementById('pm-rarity').className = 'pm-rarity rarity-' + p.rarity;
  document.getElementById('pm-name').textContent = p.name;
  document.getElementById('pm-desc').textContent = p.desc;
  document.getElementById('pm-price').textContent = p.price.toLocaleString('ru-RU') + ' ₽';
  document.getElementById('pm-seller-avatar').textContent = p.sellerIcon;
  document.getElementById('pm-seller-name').textContent = p.seller;
  
  const statsEl = document.getElementById('pm-stats');
  if (p.hp) {
    statsEl.innerHTML = `
      <div class="pm-stat"><div class="pm-stat-val">${p.hp}</div><div class="pm-stat-label">HP</div></div>
      <div class="pm-stat"><div class="pm-stat-val">${p.def}</div><div class="pm-stat-label">ЗАЩ</div></div>
      <div class="pm-stat"><div class="pm-stat-val">${p.atk}</div><div class="pm-stat-label">УРН</div></div>
    `;
    statsEl.style.display = 'flex';
  } else {
    statsEl.style.display = 'none';
  }

  // Store current product for chat
  window._currentProduct = p;
  
  document.getElementById('product-modal').classList.add('active');
  document.body.style.overflow = 'hidden';
}

function closeProductModal() {
  document.getElementById('product-modal').classList.remove('active');
  document.body.style.overflow = '';
}

function openChatFromProduct() {
  const p = window._currentProduct;
  closeProductModal();
  
  // Find or create chat
  let chat = chats.find(c => c.name === p.seller);
  if (!chat) {
    chat = {
      id: chats.length + 1,
      name: p.seller,
      icon: p.sellerIcon,
      bg: "linear-gradient(135deg,#00D4AA,#9D73FF)",
      online: p.online,
      lastMsg: "Новый чат",
      time: "сейчас",
      unread: 0,
      messages: [
        {type:'system', text:'🔒 Безопасный чат активирован. Не переводите деньги вне игры!'},
        {type:'outgoing', text:`Привет! Интересует "${p.name}" за ${p.price.toLocaleString('ru-RU')}₽`, time:'сейчас'}
      ]
    };
    chats.unshift(chat);
  }
  
  openChat(chat.id);
}

// ===== CHATS =====
function renderChats() {
  const list = document.getElementById('chat-list');
  list.innerHTML = chats.map(c => `
    <div class="chat-item" onclick="openChat(${c.id})">
      <div class="chat-avatar ${c.online ? 'online' : ''}" style="background:${c.bg};font-size:20px;">${c.icon}</div>
      <div class="chat-info">
        <div class="chat-name">${c.name}</div>
        <div class="chat-last">${c.lastMsg}</div>
      </div>
      <div class="chat-meta">
        <div class="chat-time">${c.time}</div>
        ${c.unread > 0 ? `<div class="chat-unread">${c.unread}</div>` : ''}
      </div>
    </div>
  `).join('');
}

function openChat(id) {
  const chat = chats.find(c => c.id === id);
  if (!chat) return;
  
  chat.unread = 0;
  
  document.getElementById('cm-avatar').textContent = chat.icon;
  document.getElementById('cm-avatar').style.background = chat.bg;
  document.getElementById('cm-name').textContent = chat.name;
  
  renderMessages(chat);
  document.getElementById('chat-modal').classList.add('active');
  document.body.style.overflow = 'hidden';
  
  window._currentChat = chat;
}

function renderMessages(chat) {
  const container = document.getElementById('chat-messages');
  container.innerHTML = chat.messages.map(m => {
    if (m.type === 'system') {
      return `<div class="system-msg">${m.text}</div>`;
    }
    return `
      <div class="message ${m.type}">
        ${m.text}
        <div class="message-time">${m.time}</div>
      </div>
    `;
  }).join('');
  container.scrollTop = container.scrollHeight;
}

function closeChatModal() {
  document.getElementById('chat-modal').classList.remove('active');
  document.body.style.overflow = '';
  renderChats();
}

function sendMessage() {
  const input = document.getElementById('chat-input');
  const text = input.value.trim();
  if (!text) return;
  
  const chat = window._currentChat;
  const now = new Date();
  const time = now.getHours().toString().padStart(2,'0') + ':' + now.getMinutes().toString().padStart(2,'0');
  
  chat.messages.push({ type: 'outgoing', text, time });
  chat.lastMsg = text.substring(0, 40);
  chat.time = time;
  
  input.value = '';
  renderMessages(chat);
  
  // Simulate reply
  setTimeout(() => {
    const replies = [
      'Хорошо, давай обсудим детали',
      'Сейчас в игре, могу через 5 минут',
      'Цена окончательная, без торга',
      'Отправил предмет, проверяй инвентарь!',
      'Давай на площади Восстания встретимся',
      'Скриншот статов сейчас сделаю',
      'Договорились! Создаю оферту 🔒'
    ];
    const reply = replies[Math.floor(Math.random() * replies.length)];
    chat.messages.push({ type: 'incoming', text: reply, time });
    chat.lastMsg = reply.substring(0, 40);
    chat.time = time;
    renderMessages(chat);
    showToast('💬', `${chat.name}: ${reply}`);
  }, 1500 + Math.random() * 2000);
}

function sendTemplate(text) {
  document.getElementById('chat-input').value = text;
  sendMessage();
}

// ===== PROFILE =====
function switchProfileTab(el, tab) {
  document.querySelectorAll('.profile-tab').forEach(t => t.classList.remove('active'));
  el.classList.add('active');
  renderProfileContent(tab);
}

function renderProfileContent(tab) {
  const container = document.getElementById('profile-content');
  
  if (tab === 'my-lots') {
    container.innerHTML = products.filter(p => p.seller === 'Shadow_Hunter').map(p => `
      <div class="deal-item" onclick="openProduct(${p.id})">
        <div class="deal-icon" style="background:var(--bg-secondary);font-size:28px;">${p.icon}</div>
        <div class="deal-info">
          <div class="deal-name">${p.name}</div>
          <div class="deal-meta">Размещён сегодня • 👁 47 просмотров</div>
        </div>
        <div class="deal-price" style="color:var(--accent);">${(p.price/1000).toFixed(0)}к ₽</div>
      </div>
    `).join('') || `
      <div class="empty-state">
        <div class="empty-icon">📦</div>
        <div class="empty-title">Нет активных лотов</div>
        <div class="empty-text">Нажмите ➕ чтобы добавить первый товар</div>
      </div>
    `;
  } else if (tab === 'history') {
    container.innerHTML = `
      <div class="deal-item">
        <div class="deal-icon" style="background:rgba(34,197,94,0.1);">✅</div>
        <div class="deal-info">
          <div class="deal-name">Продажа: Кроссовки HP+100</div>
          <div class="deal-meta">15.04.2026 • Покупатель: White_Wolf • ★★★★★</div>
        </div>
        <div class="deal-price sold">+1 800 000 ₽</div>
      </div>
      <div class="deal-item">
        <div class="deal-icon" style="background:rgba(0,212,170,0.1);">🛒</div>
        <div class="deal-info">
          <div class="deal-name">Покупка: Осколки хаоса x30</div>
          <div class="deal-meta">14.04.2026 • Продавец: DarkMage_SPB</div>
        </div>
        <div class="deal-price bought">-540 000 ₽</div>
      </div>
      <div class="deal-item">
        <div class="deal-icon" style="background:rgba(34,197,94,0.1);">✅</div>
        <div class="deal-info">
          <div class="deal-name">Продажа: Скин «Дракон»</div>
          <div class="deal-meta">12.04.2026 • Покупатель: KingPin_SPB • ★★★★☆</div>
        </div>
        <div class="deal-price sold">+920 000 ₽</div>
      </div>
      <div class="deal-item">
        <div class="deal-icon" style="background:rgba(157,115,255,0.1);">🔄</div>
        <div class="deal-info">
          <div class="deal-name">Обмен: Тюнинг GT-R ↔ Обвес BMW</div>
          <div class="deal-meta">10.04.2026 • С: TuningMaster</div>
        </div>
        <div class="deal-price" style="color:var(--purple);">Обмен</div>
      </div>
    `;
  } else if (tab === 'settings') {
    container.innerHTML = `
      <div class="settings-group">
        <div class="settings-group-title">Аккаунт</div>
        <div class="settings-item" onclick="showToast('👤','Редактирование профиля')">
          <div class="settings-left">
            <div class="settings-icon" style="background:rgba(0,212,170,0.1);">👤</div>
            <div class="settings-label">Редактировать профиль</div>
          </div>
          <span class="settings-arrow">›</span>
        </div>
        <div class="settings-item" onclick="showToast('🔗','Привязка ВК')">
          <div class="settings-left">
            <div class="settings-icon" style="background:rgba(39,135,245,0.1);">🔗</div>
            <div class="settings-label">Привязать ВКонтакте</div>
          </div>
          <span style="font-size:11px;color:var(--accent);">Привязано</span>
        </div>
      </div>
      <div class="settings-group">
        <div class="settings-group-title">Уведомления</div>
        <div class="settings-item">
          <div class="settings-left">
            <div class="settings-icon" style="background:rgba(157,115,255,0.1);">🔔</div>
            <div class="settings-label">Push-уведомления</div>
          </div>
          <div class="toggle on" onclick="this.classList.toggle('on')"></div>
        </div>
        <div class="settings-item">
          <div class="settings-left">
            <div class="settings-icon" style="background:rgba(255,215,0,0.1);">💰</div>
            <div class="settings-label">Уведомления о ценах</div>
          </div>
          <div class="toggle on" onclick="this.classList.toggle('on')"></div>
        </div>
        <div class="settings-item">
          <div class="settings-left">
            <div class="settings-icon" style="background:rgba(34,197,94,0.1);">💬</div>
            <div class="settings-label">Звук сообщений</div>
          </div>
          <div class="toggle" onclick="this.classList.toggle('on')"></div>
        </div>
      </div>
      <div class="settings-group">
        <div class="settings-group-title">Безопасность</div>
        <div class="settings-item" onclick="showToast('🔒','Двухфакторная аутентификация')">
          <div class="settings-left">
            <div class="settings-icon" style="background:rgba(255,107,107,0.1);">🔒</div>
            <div class="settings-label">2FA авторизация</div>
          </div>
          <div class="toggle on" onclick="this.classList.toggle('on')"></div>
        </div>
        <div class="settings-item" onclick="showToast('📋','Журнал действий открыт')">
          <div class="settings-left">
            <div class="settings-icon" style="background:rgba(107,114,128,0.1);">📋</div>
            <div class="settings-label">Журнал действий</div>
          </div>
          <span class="settings-arrow">›</span>
        </div>
      </div>
      <div class="logout-btn" onclick="doLogout()">🚪 Выйти из аккаунта</div>
    `;
  }
}

function doLogout() {
  showScreen('login');
  showToast('👋', 'Вы вышли из аккаунта');
}

function submitProduct() {
  showToast('✅', 'Лот успешно опубликован!');
  setTimeout(() => switchTab('market'), 800);
}

// ===== TOAST =====
function showToast(icon, text) {
  const toast = document.getElementById('toast');
  document.getElementById('toast-icon').textContent = icon;
  document.getElementById('toast-text').textContent = text;
  toast.classList.add('show');
  setTimeout(() => toast.classList.remove('show'), 3000);
}

// ===== KEYBOARD HANDLING =====
document.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') {
    closeProductModal();
    closeChatModal();
  }
});
</script>

</body>
</html>
