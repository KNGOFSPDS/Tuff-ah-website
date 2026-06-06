# Tuff-ah-website
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ClimbTrack - Track Your Ascent</title>
    <link rel="stylesheet" href="css/styles.css">
    <link rel="stylesheet" href="[cdnjs.cloudflare.com](https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css)">
</head>
<body>
    <div id="app">
        <!-- Splash Screen -->
        <div id="splash-screen" class="screen active">
            <div class="splash-content">
                <div class="logo">
                    <i class="fas fa-mountain"></i>
                </div>
                <h1>ClimbTrack</h1>
                <p>Track Your Ascent</p>
                <button id="get-started-btn" class="btn btn-primary">Get Started</button>
            </div>
        </div>

        <!-- Main App Container -->
        <div id="main-app" class="hidden">
            <!-- Header -->
            <header class="app-header">
                <div class="header-left">
                    <div class="avatar-small" id="header-avatar"></div>
                    <div class="user-info">
                        <span class="username" id="header-username">Climber</span>
                        <span class="rank-badge" id="header-rank">Beginner</span>
                    </div>
                </div>
                <div class="header-right">
                    <div class="xp-display">
                        <i class="fas fa-bolt"></i>
                        <span id="header-xp">0</span> XP
                    </div>
                </div>
            </header>

            <!-- Weekly Goal Progress -->
            <section class="weekly-goal-banner" id="weekly-goal-banner">
                <div class="goal-info">
                    <span class="goal-label">Weekly Goal</span>
                    <span class="goal-progress"><span id="goal-current">0</span>/<span id="goal-target">3</span> sessions</span>
                </div>
                <div class="goal-bar">
                    <div class="goal-fill" id="goal-fill"></div>
                </div>
            </section>

            <!-- Tab Content -->
            <main class="tab-content">
                <!-- Dashboard Tab -->
                <section id="dashboard-tab" class="tab-panel active">
                    <div class="stats-grid">
                        <div class="stat-card">
                            <i class="fas fa-route"></i>
                            <div class="stat-value" id="total-climbs">0</div>
                            <div class="stat-label">Total Climbs</div>
                        </div>
                        <div class="stat-card">
                            <i class="fas fa-fire"></i>
                            <div class="stat-value" id="current-streak">0</div>
                            <div class="stat-label">Day Streak</div>
                        </div>
                        <div class="stat-card">
                            <i class="fas fa-trophy"></i>
                            <div class="stat-value" id="hardest-grade">-</div>
                            <div class="stat-label">Hardest Send</div>
                        </div>
                        <div class="stat-card">
                            <i class="fas fa-calendar-check"></i>
                            <div class="stat-value" id="sessions-month">0</div>
                            <div class="stat-label">This Month</div>
                        </div>
                    </div>

                    <div class="section-header">
                        <h2>Recent Activity</h2>
                    </div>
                    <div class="activity-feed" id="recent-activity">
                        <div class="empty-state">
                            <i class="fas fa-mountain"></i>
                            <p>No climbs logged yet. Start your journey!</p>
                        </div>
                    </div>

                    <button id="quick-log-btn" class="fab">
                        <i class="fas fa-plus"></i>
                    </button>
                </section>

                <!-- Log Climb Tab -->
                <section id="log-tab" class="tab-panel">
                    <h2>Log a Climb</h2>
                    <form id="log-climb-form">
                        <div class="form-group">
                            <label for="climb-name">Route Name (optional)</label>
                            <input type="text" id="climb-name" placeholder="e.g., The Crimper">
                        </div>

                        <div class="form-group">
                            <label for="climb-type">Climb Type</label>
                            <select id="climb-type">
                                <option value="boulder">Bouldering</option>
                                <option value="sport">Sport Climbing</option>
                                <option value="trad">Trad Climbing</option>
                                <option value="top-rope">Top Rope</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label>Difficulty Grade</label>
                            <div class="grade-selector" id="grade-selector">
                                <!-- Populated by JS based on climb type -->
                            </div>
                        </div>

                        <div class="form-group">
                            <label for="climb-status">Completion Status</label>
                            <div class="status-buttons">
                                <button type="button" class="status-btn active" data-status="send">
                                    <i class="fas fa-check-circle"></i> Send
                                </button>
                                <button type="button" class="status-btn" data-status="flash">
                                    <i class="fas fa-bolt"></i> Flash
                                </button>
                                <button type="button" class="status-btn" data-status="onsight">
                                    <i class="fas fa-eye"></i> Onsight
                                </button>
                                <button type="button" class="status-btn" data-status="project">
                                    <i class="fas fa-clock"></i> Project
                                </button>
                            </div>
                        </div>

                        <div class="form-group">
                            <label for="climb-attempts">Attempts</label>
                            <div class="attempts-counter">
                                <button type="button" class="counter-btn" id="attempts-minus">-</button>
                                <input type="number" id="climb-attempts" value="1" min="1" max="99">
                                <button type="button" class="counter-btn" id="attempts-plus">+</button>
                            </div>
                        </div>

                        <div class="form-group">
                            <label for="climb-notes">Notes</label>
                            <textarea id="climb-notes" placeholder="Beta, conditions, feelings..."></textarea>
                        </div>

                        <div class="form-group">
                            <label for="climb-date">Date</label>
                            <input type="date" id="climb-date">
                        </div>

                        <button type="submit" class="btn btn-primary btn-block">
                            <i class="fas fa-save"></i> Log Climb
                        </button>
                    </form>
                </section>

                <!-- Logbook Tab -->
                <section id="logbook-tab" class="tab-panel">
                    <div class="logbook-header">
                        <h2>Climb Logbook</h2>
                        <div class="filter-controls">
                            <select id="filter-type">
                                <option value="all">All Types</option>
                                <option value="boulder">Bouldering</option>
                                <option value="sport">Sport</option>
                                <option value="trad">Trad</option>
                                <option value="top-rope">Top Rope</option>
                            </select>
                            <select id="filter-status">
                                <option value="all">All Status</option>
                                <option value="send">Sends</option>
                                <option value="flash">Flashes</option>
                                <option value="onsight">Onsights</option>
                                <option value="project">Projects</option>
                            </select>
                        </div>
                    </div>
                    <div class="logbook-list" id="logbook-list">
                        <!-- Populated by JS -->
                    </div>
                </section>

                <!-- Leaderboard Tab -->
                <section id="leaderboard-tab" class="tab-panel">
                    <div class="leaderboard-tabs">
                        <button class="lb-tab active" data-period="weekly">Weekly</button>
                        <button class="lb-tab" data-period="monthly">Monthly</button>
                        <button class="lb-tab" data-period="alltime">All Time</button>
                    </div>

                    <div class="leaderboard-category">
                        <h3><i class="fas fa-bolt"></i> XP Leaders</h3>
                        <div class="leaderboard-list" id="xp-leaderboard">
                            <!-- Populated by JS -->
                        </div>
                    </div>

                    <div class="leaderboard-category">
                        <h3><i class="fas fa-mountain"></i> Most Climbs</h3>
                        <div class="leaderboard-list" id="climbs-leaderboard">
                            <!-- Populated by JS -->
                        </div>
                    </div>

                    <div class="leaderboard-category">
                        <h3><i class="fas fa-fire"></i> Hardest Sends</h3>
                        <div class="leaderboard-list" id="grade-leaderboard">
                            <!-- Populated by JS -->
                        </div>
                    </div>

                    <div class="friends-section">
                        <h3>Friends</h3>
                        <div class="friends-list" id="friends-list">
                            <!-- Populated by JS -->
                        </div>
                        <button class="btn btn-secondary" id="add-friend-btn">
                            <i class="fas fa-user-plus"></i> Add Friend
                        </button>
                    </div>
                </section>

                <!-- Profile Tab -->
                <section id="profile-tab" class="tab-panel">
                    <div class="profile-header">
                        <div class="avatar-large" id="profile-avatar"></div>
                        <button class="btn btn-icon" id="edit-avatar-btn">
                            <i class="fas fa-pencil"></i>
                        </button>
                        <h2 id="profile-username">Climber</h2>
                        <div class="rank-display">
                            <span class="rank-icon" id="profile-rank-icon"></span>
                            <span class="rank-name" id="profile-rank-name">Beginner</span>
                        </div>
                        <div class="xp-bar-container">
                            <div class="xp-bar">
                                <div class="xp-fill" id="profile-xp-fill"></div>
                            </div>
                            <span class="xp-text" id="profile-xp-text">0 / 100 XP</span>
                        </div>
                    </div>

                    <div class="profile-stats">
                        <div class="profile-stat">
                            <div class="stat-value" id="profile-total-climbs">0</div>
                            <div class="stat-label">Climbs</div>
                        </div>
                        <div class="profile-stat">
                            <div class="stat-value" id="profile-total-xp">0</div>
                            <div class="stat-label">Total XP</div>
                        </div>
                        <div class="profile-stat">
                            <div class="stat-value" id="profile-days-active">0</div>
                            <div class="stat-label">Days Active</div>
                        </div>
                    </div>

                    <div class="profile-section">
                        <h3>Weekly Goal Settings</h3>
                        <div class="goal-setting">
                            <label>Sessions per week</label>
                            <div class="goal-selector">
                                <button type="button" class="goal-btn" data-goal="1">1</button>
                                <button type="button" class="goal-btn" data-goal="2">2</button>
                                <button type="button" class="goal-btn active" data-goal="3">3</button>
                                <button type="button" class="goal-btn" data-goal="4">4</button>
                                <button type="button" class="goal-btn" data-goal="5">5</button>
                                <button type="button" class="goal-btn" data-goal="6">6</button>
                                <button type="button" class="goal-btn" data-goal="7">7</button>
                            </div>
                        </div>
                    </div>

                    <div class="profile-section">
                        <h3>Settings</h3>
                        <div class="settings-list">
                            <div class="setting-item">
                                <span>Edit Profile</span>
                                <i class="fas fa-chevron-right"></i>
                            </div>
                            <div class="setting-item">
                                <span>Notifications</span>
                                <i class="fas fa-chevron-right"></i>
                            </div>
                            <div class="setting-item">
                                <span>Privacy</span>
                                <i class="fas fa-chevron-right"></i>
                            </div>
                            <div class="setting-item" id="export-data">
                                <span>Export Data</span>
                                <i class="fas fa-download"></i>
                            </div>
                        </div>
                    </div>
                </section>
            </main>

            <!-- Bottom Navigation -->
            <nav class="bottom-nav">
                <button class="nav-item active" data-tab="dashboard">
                    <i class="fas fa-home"></i>
                    <span>Home</span>
                </button>
                <button class="nav-item" data-tab="log">
                    <i class="fas fa-plus-circle"></i>
                    <span>Log</span>
                </button>
                <button class="nav-item" data-tab="logbook">
                    <i class="fas fa-book"></i>
                    <span>Logbook</span>
                </button>
                <button class="nav-item" data-tab="leaderboard">
                    <i class="fas fa-trophy"></i>
                    <span>Ranks</span>
                </button>
                <button class="nav-item" data-tab="profile">
                    <i class="fas fa-user"></i>
                    <span>Profile</span>
                </button>
            </nav>
        </div>

        <!-- Avatar Customization Modal -->
        <div id="avatar-modal" class="modal hidden">
            <div class="modal-content">
                <div class="modal-header">
                    <h2>Customize Avatar</h2>
                    <button class="modal-close" id="close-avatar-modal">&times;</button>
                </div>
                <div class="avatar-preview" id="avatar-preview"></div>
                <div class="avatar-options">
                    <div class="option-group">
                        <label>Skin Tone</label>
                        <div class="color-options" id="skin-options"></div>
                    </div>
                    <div class="option-group">
                        <label>Hair Style</label>
                        <div class="style-options" id="hair-style-options"></div>
                    </div>
                    <div class="option-group">
                        <label>Hair Color</label>
                        <div class="color-options" id="hair-color-options"></div>
                    </div>
                    <div class="option-group">
                        <label>Eyes</label>
                        <div class="style-options" id="eye-options"></div>
                    </div>
                    <div class="option-group">
                        <label>Outfit</label>
                        <div class="style-options" id="outfit-options"></div>
                    </div>
                    <div class="option-group">
                        <label>Accessories</label>
                        <div class="style-options" id="accessory-options"></div>
                    </div>
                </div>
                <button class="btn btn-primary btn-block" id="save-avatar">Save Avatar</button>
            </div>
        </div>

        <!-- Add Friend Modal -->
        <div id="friend-modal" class="modal hidden">
            <div class="modal-content">
                <div class="modal-header">
                    <h2>Add Friend</h2>
                    <button class="modal-close" id="close-friend-modal">&times;</button>
                </div>
                <div class="form-group">
                    <label for="friend-code">Enter Friend Code</label>
                    <input type="text" id="friend-code" placeholder="ABC123">
                </div>
                <div class="your-code">
                    <span>Your Code:</span>
                    <strong id="your-friend-code">XYZ789</strong>
                    <button class="btn btn-icon" id="copy-code">
                        <i class="fas fa-copy"></i>
                    </button>
                </div>
                <button class="btn btn-primary btn-block" id="send-friend-request">
                    Send Request
                </button>
            </div>
        </div>

        <!-- Achievement Toast -->
        <div id="achievement-toast" class="toast hidden">
            <div class="toast-icon">
                <i class="fas fa-trophy"></i>
            </div>
            <div class="toast-content">
                <span class="toast-title">Achievement Unlocked!</span>
                <span class="toast-message" id="toast-message"></span>
            </div>
        </div>
    </div>

    <script src="js/app.js"></script>
    <script src="js/auth.js"></script>
    <script src="js/climbs.js"></script>
    <script src="js/leaderboard.js"></script>
    <script src="js/avatar.js"></script>
    <script src="js/goals.js"></script>
</body>
</html>
/* ==========================================
   CSS Variables & Reset
   ========================================== */
:root {
    /* Colors */
    --primary: #FF6B35;
    --primary-dark: #E55A2B;
    --primary-light: #FF8F66;
    --secondary: #4ECDC4;
    --secondary-dark: #3DB8B0;
    --accent: #FFE66D;
    --success: #2ECC71;
    --warning: #F39C12;
    --danger: #E74C3C;
    
    /* Neutrals */
    --bg-dark: #1A1A2E;
    --bg-card: #25253D;
    --bg-elevated: #2D2D4A;
    --text-primary: #FFFFFF;
    --text-secondary: #A0A0B8;
    --text-muted: #6B6B80;
    
    /* Rank Colors */
    --rank-beginner: #95A5A6;
    --rank-novice: #3498DB;
    --rank-intermediate: #2ECC71;
    --rank-advanced: #9B59B6;
    --rank-expert: #E74C3C;
    --rank-elite: #F39C12;
    --rank-master: #FF6B35;
    
    /* Spacing */
    --space-xs: 4px;
    --space-sm: 8px;
    --space-md: 16px;
    --space-lg: 24px;
    --space-xl: 32px;
    
    /* Border Radius */
    --radius-sm: 8px;
    --radius-md: 12px;
    --radius-lg: 16px;
    --radius-full: 50%;
    
    /* Transitions */
    --transition-fast: 150ms ease;
    --transition-normal: 250ms ease;
    --transition-slow: 400ms ease;
    
    /* Shadows */
    --shadow-sm: 0 2px 4px rgba(0, 0, 0, 0.2);
    --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.3);
    --shadow-lg: 0 8px 24px rgba(0, 0, 0, 0.4);
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html {
    font-size: 16px;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
    background: var(--bg-dark);
    color: var(--text-primary);
    line-height: 1.5;
    min-height: 100vh;
    overflow-x: hidden;
}

/* ==========================================
   Utility Classes
   ========================================== */
.hidden {
    display: none !important;
}

.active {
    display: block;
}

/* ==========================================
   Splash Screen
   ========================================== */
#splash-screen {
    position: fixed;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, var(--bg-dark) 0%, #2D2D4A 100%);
    z-index: 1000;
}

.splash-content {
    text-align: center;
    animation: fadeInUp 0.8s ease;
}

.splash-content .logo {
    width: 120px;
    height: 120px;
    background: linear-gradient(135deg, var(--primary) 0%, var(--primary-dark) 100%);
    border-radius: var(--radius-lg);
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto var(--space-lg);
    box-shadow: var(--shadow-lg);
}

.splash-content .logo i {
    font-size: 3.5rem;
    color: white;
}

.splash-content h1 {
    font-size: 2.5rem;
    font-weight: 700;
    margin-bottom: var(--space-sm);
    background: linear-gradient(135deg, var(--primary) 0%, var(--accent) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.splash-content p {
    color: var(--text-secondary);
    margin-bottom: var(--space-xl);
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* ==========================================
   Buttons
   ========================================== */
.btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: var(--space-sm);
    padding: var(--space-md) var(--space-lg);
    border: none;
    border-radius: var(--radius-md);
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all var(--transition-fast);
}

.btn-primary {
    background: linear-gradient(135deg, var(--primary) 0%, var(--primary-dark) 100%);
    color: white;
}

.btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow-md);
}

.btn-primary:active {
    transform: translateY(0);
}

.btn-secondary {
    background: var(--bg-elevated);
    color: var(--text-primary);
    border: 1px solid var(--text-muted);
}

.btn-secondary:hover {
    background: var(--bg-card);
    border-color: var(--primary);
}

.btn-block {
    width: 100%;
}

.btn-icon {
    width: 40px;
    height: 40px;
    padding: 0;
    border-radius: var(--radius-full);
    background: var(--bg-elevated);
    color: var(--text-secondary);
}

.btn-icon:hover {
    background: var(--primary);
    color: white;
}

/* ==========================================
   App Header
   ========================================== */
.app-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: var(--space-md);
    background: var(--bg-card);
    border-bottom: 1px solid var(--bg-elevated);
    position: sticky;
    top: 0;
    z-index: 100;
}

.header-left {
    display: flex;
    align-items: center;
    gap: var(--space-sm);
}

.avatar-small {
    width: 40px;
    height: 40px;
    border-radius: var(--radius-full);
    background: var(--bg-elevated);
    overflow: hidden;
}

.user-info {
    display: flex;
    flex-direction: column;
}

.username {
    font-weight: 600;
    font-size: 0.9rem;
}

.rank-badge {
    font-size: 0.75rem;
    color: var(--primary);
    font-weight: 500;
}

.xp-display {
    display: flex;
    align-items: center;
    gap: var(--space-xs);
    background: var(--bg-elevated);
    padding: var(--space-sm) var(--space-md);
    border-radius: var(--radius-md);
    font-weight: 600;
    color: var(--accent);
}

.xp-display i {
    color: var(--accent);
}

/* ==========================================
   Weekly Goal Banner
   ========================================== */
.weekly-goal-banner {
    background: linear-gradient(135deg, var(--bg-card) 0%, var(--bg-elevated) 100%);
    padding: var(--space-md);
    margin: var(--space-md);
    border-radius: var(--radius-md);
    border: 1px solid var(--bg-elevated);
}

.goal-info {
    display: flex;
    justify-content: space-between;
    margin-bottom: var(--space-sm);
}

.goal-label {
    color: var(--text-secondary);
    font-size: 0.85rem;
}

.goal-progress {
    font-weight: 600;
    color: var(--primary);
}

.goal-bar {
    height: 8px;
    background: var(--bg-dark);
    border-radius: var(--radius-full);
    overflow: hidden;
}

.goal-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--primary) 0%, var(--accent) 100%);
    border-radius: var(--radius-full);
    transition: width var(--transition-normal);
    width: 0%;
}

/* ==========================================
   Tab Content & Panels
   ========================================== */
.tab-content {
    padding: var(--space-md);
    padding-bottom: 100px;
    min-height: calc(100vh - 200px);
}

.tab-panel {
    display: none;
    animation: fadeIn 0.3s ease;
}

.tab-panel.active {
    display: block;
}

@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

/* ==========================================
   Dashboard Stats Grid
   ========================================== */
.stats-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: var(--space-md);
    margin-bottom: var(--space-lg);
}

.stat-card {
    background: var(--bg-card);
    padding: var(--space-lg);
    border-radius: var(--radius-md);
    text-align: center;
    transition: transform var(--transition-fast);
}

.stat-card:hover {
    transform: translateY(-2px);
}

.stat-card i {
    font-size: 1.5rem;
    color: var(--primary);
    margin-bottom: var(--space-sm);
}

.stat-value {
    font-size: 1.75rem;
    font-weight: 700;
    color: var(--text-primary);
}

.stat-label {
    font-size: 0.85rem;
    color: var(--text-secondary);
    margin-top: var(--space-xs);
}

/* ==========================================
   Section Headers
   ========================================== */
.section-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--space-md);
}

.section-header h2 {
    font-size: 1.25rem;
    font-weight: 600;
}

/* ==========================================
   Activity Feed
   ========================================== */
.activity-feed {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
}

.activity-item {
    display: flex;
    align-items: center;
    gap: var(--space-md);
    background: var(--bg-card);
    padding: var(--space-md);
    border-radius: var(--radius-md);
    transition: background var(--transition-fast);
}

.activity-item:hover {
    background: var(--bg-elevated);
}

.activity-icon {
    width: 48px;
    height: 48px;
    border-radius: var(--radius-md);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.25rem;
}

.activity-icon.boulder { background: rgba(255, 107, 53, 0.2); color: var(--primary); }
.activity-icon.sport { background: rgba(78, 205, 196, 0.2); color: var(--secondary); }
.activity-icon.trad { background: rgba(155, 89, 182, 0.2); color: #9B59B6; }
.activity-icon.top-rope { background: rgba(46, 204, 113, 0.2); color: var(--success); }

.activity-details {
    flex: 1;
}

.activity-title {
    font-weight: 600;
    margin-bottom: 2px;
}

.activity-meta {
    font-size: 0.85rem;
    color: var(--text-secondary);
}

.activity-xp {
    background: var(--bg-elevated);
    padding: var(--space-xs) var(--space-sm);
    border-radius: var(--radius-sm);
    font-size: 0.85rem;
    font-weight: 600;
    color: var(--accent);
}

.empty-state {
    text-align: center;
    padding: var(--space-xl);
    color: var(--text-muted);
}

.empty-state i {
    font-size: 3rem;
    margin-bottom: var(--space-md);
    opacity: 0.5;
}

/* ==========================================
   Floating Action Button
   ========================================== */
.fab {
    position: fixed;
    bottom: 100px;
    right: var(--space-md);
    width: 56px;
    height: 56px;
    border-radius: var(--radius-full);
    background: linear-gradient(135deg, var(--primary) 0%, var(--primary-dark) 100%);
    color: white;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
    box-shadow: var(--shadow-lg);
    transition: all var(--transition-fast);
    z-index: 90;
}

.fab:hover {
    transform: scale(1.1);
}

.fab:active {
    transform: scale(0.95);
}

/* ==========================================
   Log Climb Form
   ========================================== */
#log-tab h2 {
    margin-bottom: var(--space-lg);
}

.form-group {
    margin-bottom: var(--space-lg);
}

.form-group label {
    display: block;
    margin-bottom: var(--space-sm);
    font-weight: 500;
    color: var(--text-secondary);
}

.form-group input[type="text"],
.form-group input[type="date"],
.form-group input[type="number"],
.form-group select,
.form-group textarea {
    width: 100%;
    padding: var(--space-md);
    background: var(--bg-card);
    border: 1px solid var(--bg-elevated);
    border-radius: var(--radius-md);
    color: var(--text-primary);
    font-size: 1rem;
    transition: border-color var(--transition-fast);
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
    outline: none;
    border-color: var(--primary);
}

.form-group textarea {
    min-height: 100px;
    resize: vertical;
}

/* Grade Selector */
.grade-selector {
    display: flex;
    flex-wrap: wrap;
    gap: var(--space-sm);
}

.grade-btn {
    padding: var(--space-sm) var(--space-md);
    background: var(--bg-card);
    border: 1px solid var(--bg-elevated);
    border-radius: var(--radius-sm);
    color: var(--text-secondary);
    cursor: pointer;
    transition: all var(--transition-fast);
    font-size: 0.9rem;
}

.grade-btn:hover {
    border-color: var(--primary);
    color: var(--primary);
}

.grade-btn.selected {
    background: var(--primary);
    border-color: var(--primary);
    color: white;
}

/* Status Buttons */
.status-buttons {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: var(--space-sm);
}

.status-btn {
    padding: var(--space-md);
    background: var(--bg-card);
    border: 1px solid var(--bg-elevated);
    border-radius: var(--radius-md);
    color: var(--text-secondary);
    cursor: pointer;
    transition: all var(--transition-fast);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--space-xs);
}

.status-btn:hover {
    border-color: var(--primary);
}

.status-btn.active {
    background: rgba(255, 107, 53, 0.15);
    border-color: var(--primary);
    color: var(--primary);
}

.status-btn i {
    font-size: 1.25rem;
}

/* Attempts Counter */
.attempts-counter {
    display: flex;
    align-items: center;
    gap: var(--space-sm);
}

.counter-btn {
    width: 44px;
    height: 44px;
    background: var(--bg-card);
    border: 1px solid var(--bg-elevated);
    border-radius: var(--radius-md);
    color: var(--text-primary);
    font-size: 1.25rem;
    cursor: pointer;
    transition: all var(--transition-fast);
}

.counter-btn:hover {
    background: var(--primary);
    border-color: var(--primary);
}

.attempts-counter input {
    width: 60px;
    text-align: center;
}

/* ==========================================
   Logbook
   ========================================== */
.logbook-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: var(--space-md);
    margin-bottom: var(--space-lg);
}

.filter-controls {
    display: flex;
    gap: var(--space-sm);
}

.filter-controls select {
    padding: var(--space-sm) var(--space-md);
    background: var(--bg-card);
    border: 1px solid var(--bg-elevated);
    border-radius: var(--radius-sm);
    color: var(--text-primary);
    font-size: 0.85rem;
}

.logbook-list {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
}

.logbook-item {
    background: var(--bg-card);
    border-radius: var(--radius-md);
    padding: var(--space-md);
    display: flex;
    align-items: center;
    gap: var(--space-md);
}

.logbook-grade {
    width: 50px;
    height: 50px;
    border-radius: var(--radius-md);
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 1rem;
}

.logbook-grade.boulder { background: var(--primary); }
.logbook-grade.sport { background: var(--secondary); }
.logbook-grade.trad { background: #9B59B6; }
.logbook-grade.top-rope { background: var(--success); }

.logbook-info {
    flex: 1;
}

.logbook-name {
    font-weight: 600;
    margin-bottom: 2px;
}

.logbook-meta {
    font-size: 0.85rem;
    color: var(--text-secondary);
    display: flex;
    gap: var(--space-md);
}

.logbook-status {
    padding: var(--space-xs) var(--space-sm);
    border-radius: var(--radius-sm);
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
}

.logbook-status.send { background: rgba(46, 204, 113, 0.2); color: var(--success); }
.logbook-status.flash { background: rgba(255, 230, 109, 0.2); color: var(--accent); }
.logbook-status.onsight { background: rgba(78, 205, 196, 0.2); color: var(--secondary); }
.logbook-status.project { background: rgba(231, 76, 60, 0.2); color: var(--danger); }

/* ==========================================
   Leaderboard
   ========================================== */
.leaderboard-tabs {
    display: flex;
    gap: var(--space-sm);
    margin-bottom: var(--space-lg);
}

.lb-tab {
    flex: 1;
    padding: var(--space-md);
    background: var(--bg-card);
    border: none;
    border-radius: var(--radius-md);
    color: var(--text-secondary);
    font-weight: 500;
    cursor: pointer;
    transition: all var(--transition-fast);
}

.lb-tab.active {
    background: var(--primary);
    color: white;
}

.leaderboard-category {
    margin-bottom: var(--space-xl);
}

.leaderboard-category h3 {
    display: flex;
    align-items: center;
    gap: var(--space-sm);
    margin-bottom: var(--space-md);
    font-size: 1rem;
    color: var(--text-secondary);
}

.leaderboard-category h3 i {
    color: var(--primary);
}

.leaderboard-list {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
}

.leaderboard-item {
    display: flex;
    align-items: center;
    gap: var(--space-md);
    background: var(--bg-card);
    padding: var(--space-md);
    border-radius: var(--radius-md);
}

.leaderboard-rank {
    width: 32px;
    height: 32px;
    border-radius: var(--radius-full);
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 0.9rem;
}

.leaderboard-rank.gold { background: linear-gradient(135deg, #FFD700 0%, #FFA500 100%); color: #1A1A2E; }
.leaderboard-rank.silver { background: linear-gradient(135deg, #C0C0C0 0%, #A0A0A0 100%); color: #1A1A2E; }
.leaderboard-rank.bronze { background: linear-gradient(135deg, #CD7F32 0%, #A0522D 100%); color: white; }
.leaderboard-rank.other { background: var(--bg-elevated); color: var(--text-secondary); }

.leaderboard-user {
    flex: 1;
    display: flex;
    align-items: center;
    gap: var(--space-sm);
}

.leaderboard-avatar {
    width: 36px;
    height: 36px;
    border-radius: var(--radius-full);
    background: var(--bg-elevated);
}

.leaderboard-name {
    font-weight: 500;
}

.leaderboard-name.you {
    color: var(--primary);
}

.leaderboard-value {
    font-weight: 600;
    color: var(--accent);
}

/* Friends Section */
.friends-section {
    margin-top: var(--space-xl);
    padding-top: var(--space-lg);
    border-top: 1px solid var(--bg-elevated);
}

.friends-section h3 {
    margin-bottom: var(--space-md);
}

.friends-list {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
    margin-bottom: var(--space-md);
}

.friend-item {
    display: flex;
    align-items: center;
    gap: var(--space-md);
    background: var(--bg-card);
    padding: var(--space-md);
    border-radius: var(--radius-md);
}

.friend-avatar {
    width: 44px;
    height: 44px;
    border-radius: var(--radius-full);
    background: var(--bg-elevated);
}

.friend-info {
    flex: 1;
}

.friend-name {
    font-weight: 600;
}

.friend-status {
    font-size: 0.85rem;
    color: var(--text-secondary);
}

/* ==========================================
   Profile Tab
   ========================================== */
.profile-header {
    text-align: center;
    padding: var(--space-lg);
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    margin-bottom: var(--space-lg);
    position: relative;
}

.avatar-large {
    width: 100px;
    height: 100px;
    border-radius: var(--radius-full);
    background: var(--bg-elevated);
    margin: 0 auto var(--space-md);
    border: 3px solid var(--primary);
}

#edit-avatar-btn {
    position: absolute;
    top: var(--space-md);
    right: var(--space-md);
}

#profile-username {
    font-size: 1.5rem;
    margin-bottom: var(--space-sm);
}

.rank-display {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: var(--space-sm);
    margin-bottom: var(--space-md);
}

.rank-icon {
    font-size: 1.5rem;
}

.rank-name {
    font-weight: 600;
    color: var(--primary);
}

.xp-bar-container {
    max-width: 300px;
    margin: 0 auto;
}

.xp-bar {
    height: 12px;
    background: var(--bg-dark);
    border-radius: var(--radius-full);
    overflow: hidden;
    margin-bottom: var(--space-xs);
}

.xp-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--primary) 0%, var(--accent) 100%);
    border-radius: var(--radius-full);
    transition: width var(--transition-slow);
}

.xp-text {
    font-size: 0.85rem;
    color: var(--text-secondary);
}

.profile-stats {
    display: flex;
    justify-content: center;
    gap: var(--space-xl);
    margin-bottom: var(--space-lg);
}

.profile-stat {
    text-align: center;
}

.profile-stat .stat-value {
    font-size: 1.5rem;
    font-weight: 700;
}

.profile-stat .stat-label {
    font-size: 0.85rem;
    color: var(--text-secondary);
}

.profile-section {
    background: var(--bg-card);
    border-radius: var(--radius-md);
    padding: var(--space-lg);
    margin-bottom: var(--space-md);
}

.profile-section h3 {
    margin-bottom: var(--space-md);
    font-size: 1rem;
}

/* Goal Selector */
.goal-selector {
    display: flex;
    flex-wrap: wrap;
    gap: var(--space-sm);
}

.goal-btn {
    width: 44px;
    height: 44px;
    border-radius: var(--radius-md);
    background: var(--bg-elevated);
    border: 1px solid transparent;
    color: var(--text-secondary);
    font-weight: 600;
    cursor: pointer;
    transition: all var(--transition-fast);
}

.goal-btn:hover {
    border-color: var(--primary);
    color: var(--primary);
}

.goal-btn.active {
    background: var(--primary);
    color: white;
}

/* Settings List */
.settings-list {
    display: flex;
    flex-direction: column;
}

.setting-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: var(--space-md) 0;
    border-bottom: 1px solid var(--bg-elevated);
    cursor: pointer;
    color: var(--text-secondary);
    transition: color var(--transition-fast);
}

.setting-item:last-child {
    border-bottom: none;
}

.setting-item:hover {
    color: var(--text-primary);
}

/* ==========================================
   Bottom Navigation
   ========================================== */
.bottom-nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    background: var(--bg-card);
    border-top: 1px solid var(--bg-elevated);
    padding: var(--space-sm) 0;
    padding-bottom: max(var(--space-sm), env(safe-area-inset-bottom));
    z-index: 100;
}

.nav-item {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;
    padding: var(--space-sm);
    background: none;
    border: none;
    color: var(--text-muted);
    font-size: 0.7rem;
    cursor: pointer;
    transition: color var(--transition-fast);
}

.nav-item i {
    font-size: 1.25rem;
}

.nav-item.active {
    color: var(--primary);
}

.nav-item:hover {
    color: var(--text-primary);
}

/* ==========================================
   Modals
   ========================================== */
.modal {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.8);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: var(--space-md);
    z-index: 200;
    animation: fadeIn 0.2s ease;
}

.modal-content {
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    width: 100%;
    max-width: 400px;
    max-height: 90vh;
    overflow-y: auto;
    padding: var(--space-lg);
}

.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--space-lg);
}

.modal-header h2 {
    font-size: 1.25rem;
}

.modal-close {
    width: 32px;
    height: 32px;
    background: var(--bg-elevated);
    border: none;
    border-radius: var(--radius-full);
    color: var(--text-secondary);
    font-size: 1.25rem;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal-close:hover {
    background: var(--danger);
    color: white;
}

/* Avatar Preview */
.avatar-preview {
    width: 120px;
    height: 120px;
    margin: 0 auto var(--space-lg);
    background: var(--bg-elevated);
    border-radius: var(--radius-full);
    border: 3px solid var(--primary);
    overflow: hidden;
}

/* Avatar Options */
.avatar-options {
    max-height: 300px;
    overflow-y: auto;
    margin-bottom: var(--space-lg);
}

.option-group {
    margin-bottom: var(--space-lg);
}

.option-group label {
    display: block;
    margin-bottom: var(--space-sm);
    font-size: 0.85rem;
    color: var(--text-secondary);
}

.color-options {
    display: flex;
    flex-wrap: wrap;
    gap: var(--space-sm);
}

.color-option {
    width: 36px;
    height: 36px;
    border-radius: var(--radius-full);
    border: 2px solid transparent;
    cursor: pointer;
    transition: all var(--transition-fast);
}

.color-option:hover,
.color-option.selected {
    border-color: white;
    transform: scale(1.1);
}

.style-options {
    display: flex;
    flex-wrap: wrap;
    gap: var(--space-sm);
}

.style-option {
    padding: var(--space-sm) var(--space-md);
    background: var(--bg-elevated);
    border: 1px solid transparent;
    border-radius: var(--radius-sm);
    color: var(--text-secondary);
    cursor: pointer;
    font-size: 0.85rem;
    transition: all var(--transition-fast);
}

.style-option:hover {
    border-color: var(--primary);
    color: var(--primary);
}

.style-option.selected {
    background: var(--primary);
    color: white;
}

/* Friend Code */
.your-code {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: var(--space-md);
    background: var(--bg-elevated);
    padding: var(--space-md);
    border-radius: var(--radius-md);
    margin: var(--space-lg) 0;
}

.your-code strong {
    font-size: 1.25rem;
    letter-spacing: 2px;
    color: var(--primary);
}

/* ==========================================
   Achievement Toast
   ========================================== */
.toast {
    position: fixed;
    top: var(--space-lg);
    left: 50%;
    transform: translateX(-50%) translateY(-100px);
    background: linear-gradient(135deg, var(--primary) 0%, var(--primary-dark) 100%);
    padding: var(--space-md) var(--space-lg);
    border-radius: var(--radius-lg);
    display: flex;
    align-items: center;
    gap: var(--space-md);
    box-shadow: var(--shadow-lg);
    z-index: 300;
    transition: transform var(--transition-normal);
}

.toast.show {
    transform: translateX(-50%) translateY(0);
}

.toast-icon {
    width: 48px;
    height: 48px;
    background: rgba(255, 255, 255, 0.2);
    border-radius: var(--radius-full);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.25rem;
}

.toast-content {
    display: flex;
    flex-direction: column;
}

.toast-title {
    font-weight: 600;
    font-size: 0.85rem;
}

.toast-message {
    font-weight: 700;
}

/* ==========================================
   Responsive Adjustments
   ========================================== */
@media (min-width: 768px) {
    .stats-grid {
        grid-template-columns: repeat(4, 1fr);
    }
    
    .tab-content {
        max-width: 800px;
        margin: 0 auto;
    }
    
    .bottom-nav {
        max-width: 500px;
        left: 50%;
        transform: translateX(-50%);
        border-radius: var(--radius-lg) var(--radius-lg) 0 0;
    }
    
    .fab {
        right: calc(50% - 400px + var(--space-md));
    }
}
/**
 * ClimbTrack - Main Application Controller
 * Handles navigation, initialization, and core app state
 */

const App = {
    currentUser: null,
    currentTab: 'dashboard',

    init() {
        this.loadUserData();
        this.bindEvents();
        this.initializeDate();
    },

    loadUserData() {
        const savedUser = localStorage.getItem('climbtrack_user');
        if (savedUser) {
            this.currentUser = JSON.parse(savedUser);
            this.showMainApp();
        }
    },

    saveUserData() {
        localStorage.setItem('climbtrack_user', JSON.stringify(this.currentUser));
    },

    bindEvents() {
        // Get Started button
        document.getElementById('get-started-btn')?.addEventListener('click', () => {
            this.createNewUser();
            this.showMainApp();
        });

        // Navigation
        document.querySelectorAll('.nav-item').forEach(item => {
            item.addEventListener('click', () => {
                const tab = item.dataset.tab;
                this.switchTab(tab);
            });
        });

        // Quick log button
        document.getElementById('quick-log-btn')?.addEventListener('click', () => {
            this.switchTab('log');
        });

        // Export data
        document.getElementById('export-data')?.addEventListener('click', () => {
            this.exportData();
        });
    },

    initializeDate() {
        const dateInput = document.getElementById('climb-date');
        if (dateInput) {
            dateInput.valueAsDate = new Date();
        }
    },

    createNewUser() {
        this.currentUser = {
            id: this.generateId(),
            username: 'Climber',
            friendCode: this.generateFriendCode(),
            xp: 0,
            rank: 'Beginner',
            rankLevel: 1,
            climbs: [],
            friends: [],
            weeklyGoal: 3,
            avatar: {
                skinTone: '#F5D0C5',
                hairStyle: 'short',
                hairColor: '#3D2314',
                eyes: 'normal',
                outfit: 'tank',
                accessory: 'none'
            },
            stats: {
                totalClimbs: 0,
                currentStreak: 0,
                longestStreak: 0,
                sessionsThisMonth: 0,
                daysActive: 0,
                lastClimbDate: null
            },
            createdAt: new Date().toISOString()
        };
        this.saveUserData();
    },

    showMainApp() {
        document.getElementById('splash-screen').classList.add('hidden');
        document.getElementById('main-app').classList.remove('hidden');
        
        this.updateHeader();
        this.updateWeeklyGoal();
        this.updateDashboard();
        
        // Initialize other modules
        Climbs.init();
        Leaderboard.init();
        Avatar.init();
        Goals.init();
    },

    switchTab(tabName) {
        this.currentTab = tabName;

        // Update nav items
        document.querySelectorAll('.nav-item').forEach(item => {
            item.classList.toggle('active', item.dataset.tab === tabName);
        });

        // Update tab panels
        document.querySelectorAll('.tab-panel').forEach(panel => {
            panel.classList.toggle('active', panel.id === `${tabName}-tab`);
        });

        // Tab-specific updates
        if (tabName === 'dashboard') {
            this.updateDashboard();
        } else if (tabName === 'logbook') {
            Climbs.updateLogbook();
        } else if (tabName === 'leaderboard') {
            Leaderboard.update();
        } else if (tabName === 'profile') {
            this.updateProfile();
        }
    },

    updateHeader() {
        const user = this.currentUser;
        document.getElementById('header-username').textContent = user.username;
        document.getElementById('header-rank').textContent = user.rank;
        document.getElementById('header-xp').textContent = this.formatNumber(user.xp);
        Avatar.renderSmall('header-avatar', user.avatar);
    },

    updateWeeklyGoal() {
        const user = this.currentUser;
        const sessions = Goals.getWeeklySessionCount();
        const target = user.weeklyGoal;
        const percentage = Math.min((sessions / target) * 100, 100);

        document.getElementById('goal-current').textContent = sessions;
        document.getElementById('goal-target').textContent = target;
        document.getElementById('goal-fill').style.width = `${percentage}%`;
    },

    updateDashboard() {
        const user = this.currentUser;
        const stats = this.calculateStats();

        document.getElementById('total-climbs').textContent = stats.totalClimbs;
        document.getElementById('current-streak').textContent = stats.currentStreak;
        document.getElementById('hardest-grade').textContent = stats.hardestGrade || '-';
        document.getElementById('sessions-month').textContent = stats.sessionsThisMonth;

        this.renderRecentActivity();
    },

    calculateStats() {
        const user = this.currentUser;
        const climbs = user.climbs || [];
        const now = new Date();
        const startOfMonth = new Date(now.getFullYear(), now.getMonth(), 1);

        // Total climbs
        const totalClimbs = climbs.length;

        // Sessions this month
        const sessionsThisMonth = new Set(
            climbs
                .filter(c => new Date(c.date) >= startOfMonth)
                .map(c => c.date.split('T')[0])
        ).size;

        // Hardest grade (excluding projects)
        const completedClimbs = climbs.filter(c => c.status !== 'project');
        const hardestGrade = this.getHardestGrade(completedClimbs);

        // Current streak
        const currentStreak = this.calculateStreak(climbs);

        return {
            totalClimbs,
            sessionsThisMonth,
            hardestGrade,
            currentStreak
        };
    },

    getHardestGrade(climbs) {
        if (climbs.length === 0) return null;

        const gradeValues = {
            // Bouldering V-scale
            'V0': 0, 'V1': 1, 'V2': 2, 'V3': 3, 'V4': 4, 'V5': 5,
            'V6': 6, 'V7': 7, 'V8': 8, 'V9': 9, 'V10': 10, 'V11': 11,
            'V12': 12, 'V13': 13, 'V14': 14, 'V15': 15, 'V16': 16, 'V17': 17,
            // Sport/Trad YDS
            '5.5': 0, '5.6': 1, '5.7': 2, '5.8': 3, '5.9': 4,
            '5.10a': 5, '5.10b': 6, '5.10c': 7, '5.10d': 8,
            '5.11a': 9, '5.11b': 10, '5.11c': 11, '5.11d': 12,
            '5.12a': 13, '5.12b': 14, '5.12c': 15, '5.12d': 16,
            '5.13a': 17, '5.13b': 18, '5.13c': 19, '5.13d': 20,
            '5.14a': 21, '5.14b': 22, '5.14c': 23, '5.14d': 24,
            '5.15a': 25, '5.15b': 26, '5.15c': 27, '5.15d': 28
        };

        let hardest = null;
        let hardestValue = -1;

        climbs.forEach(climb => {
            const value = gradeValues[climb.grade] ?? -1;
            if (value > hardestValue) {
                hardestValue = value;
                hardest = climb.grade;
            }
        });

        return hardest;
    },

    calculateStreak(climbs) {
        if (climbs.length === 0) return 0;

        const dates = [...new Set(climbs.map(c => c.date.split('T')[0]))]
            .sort((a, b) => new Date(b) - new Date(a));

        let streak = 0;
        const today = new Date().toISOString().split('T')[0];
        const yesterday = new Date(Date.now() - 86400000).toISOString().split('T')[0];

        // Check if climbed today or yesterday
        if (dates[0] !== today && dates[0] !== yesterday) {
            return 0;
        }

        let currentDate = new Date(dates[0]);
        
        for (const dateStr of dates) {
            const date = new Date(dateStr);
            const diff = Math.floor((currentDate - date) / 86400000);
            
            if (diff <= 1) {
                streak++;
                currentDate = date;
            } else {
                break;
            }
        }

        return streak;
    },

    renderRecentActivity() {
        const container = document.getElementById('recent-activity');
        const climbs = (this.currentUser.climbs || [])
            .sort((a, b) => new Date(b.date) - new Date(a.date))
            .slice(0, 5);

        if (climbs.length === 0) {
            container.innerHTML = `
                <div class="empty-state">
                    <i class="fas fa-mountain"></i>
                    <p>No climbs logged yet. Start your journey!</p>
                </div>
            `;
            return;
        }

        container.innerHTML = climbs.map(climb => `
            <div class="activity-item">
                <div class="activity-icon ${climb.type}">
                    <i class="fas fa-${this.getClimbIcon(climb.type)}"></i>
                </div>
                <div class="activity-details">
                    <div class="activity-title">${climb.name || climb.grade} ${this.getStatusIcon(climb.status)}</div>
                    <div class="activity-meta">
                        ${climb.grade} · ${this.formatDate(climb.date)}
                    </div>
                </div>
                <div class="activity-xp">+${climb.xpEarned} XP</div>
            </div>
        `).join('');
    },

    getClimbIcon(type) {
        const icons = {
            'boulder': 'hand-rock',
            'sport': 'bolt',
            'trad': 'mountain',
            'top-rope': 'grip-lines'
        };
        return icons[type] || 'mountain';
    },

    getStatusIcon(status) {
        const icons = {
            'send': '✓',
            'flash': '⚡',
            'onsight': '👁',
            'project': '🔄'
        };
        return icons[status] || '';
    },

    updateProfile() {
        const user = this.currentUser;
        const rankInfo = this.getRankInfo(user.rankLevel);

        document.getElementById('profile-username').textContent = user.username;
        document.getElementById('profile-rank-name').textContent = user.rank;
        document.getElementById('profile-rank-icon').innerHTML = rankInfo.icon;

        // XP bar
        const xpForCurrentRank = rankInfo.xpMin;
        const xpForNextRank = rankInfo.xpMax;
        const xpProgress = user.xp - xpForCurrentRank;
        const xpNeeded = xpForNextRank - xpForCurrentRank;
        const percentage = Math.min((xpProgress / xpNeeded) * 100, 100);

        document.getElementById('profile-xp-fill').style.width = `${percentage}%`;
        document.getElementById('profile-xp-text').textContent = 
            `${this.formatNumber(user.xp)} / ${this.formatNumber(xpForNextRank)} XP`;

        // Stats
        const stats = this.calculateStats();
        document.getElementById('profile-total-climbs').textContent = stats.totalClimbs;
        document.getElementById('profile-total-xp').textContent = this.formatNumber(user.xp);
        document.getElementById('profile-days-active').textContent = 
            new Set(user.climbs.map(c => c.date.split('T')[0])).size;

        // Avatar
        Avatar.renderLarge('profile-avatar', user.avatar);

        // Update friend code
        document.getElementById('your-friend-code').textContent = user.friendCode;
    },

    getRankInfo(level) {
        const ranks = [
            { name: 'Beginner', icon: '🧗', xpMin: 0, xpMax: 100, color: 'var(--rank-beginner)' },
            { name: 'Novice', icon: '🪨', xpMin: 100, xpMax: 300, color: 'var(--rank-novice)' },
            { name: 'Intermediate', icon: '⛰️', xpMin: 300, xpMax: 600, color: 'var(--rank-intermediate)' },
            { name: 'Advanced', icon: '🏔️', xpMin: 600, xpMax: 1000, color: 'var(--rank-advanced)' },
            { name: 'Expert', icon: '🦅', xpMin: 1000, xpMax: 1500, color: 'var(--rank-expert)' },
            { name: 'Elite', icon: '👑', xpMin: 1500, xpMax: 2500, color: 'var(--rank-elite)' },
            { name: 'Master', icon: '🌟', xpMin: 2500, xpMax: 5000, color: 'var(--rank-master)' }
        ];
        return ranks[Math.min(level - 1, ranks.length - 1)];
    },

    checkRankUp() {
        const user = this.currentUser;
        const currentRank = this.getRankInfo(user.rankLevel);
        
        if (user.xp >= currentRank.xpMax && user.rankLevel < 7) {
            user.rankLevel++;
            const newRank = this.getRankInfo(user.rankLevel);
            user.rank = newRank.name;
            this.saveUserData();
            this.showAchievement(`Ranked up to ${newRank.name}! ${newRank.icon}`);
            return true;
        }
        return false;
    },

    showAchievement(message) {
        const toast = document.getElementById('achievement-toast');
        document.getElementById('toast-message').textContent = message;
        toast.classList.remove('hidden');
        toast.classList.add('show');

        setTimeout(() => {
            toast.classList.remove('show');
            setTimeout(() => toast.classList.add('hidden'), 300);
        }, 3000);
    },

    exportData() {
        const data = JSON.stringify(this.currentUser, null, 2);
        const blob = new Blob([data], { type: 'application/json' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = `climbtrack-export-${new Date().toISOString().split('T')[0]}.json`;
        a.click();
        URL.revokeObjectURL(url);
    },

    // Utility methods
    generateId() {
        return Date.now().toString(36) + Math.random().toString(36).substr(2);
    },

    generateFriendCode() {
        const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
        let code = '';
        for (let i = 0; i < 6; i++) {
            code += chars.charAt(Math.floor(Math.random() * chars.length));
        }
        return code;
    },

    formatNumber(num) {
        if (num >= 1000) {
            return (num / 1000).toFixed(1) + 'k';
        }
        return num.toString();
    },

    formatDate(dateStr) {
        const date = new Date(dateStr);
        const now = new Date();
        const diff = Math.floor((now - date) / 86400000);

        if (diff === 0) return 'Today';
        if (diff === 1) return 'Yesterday';
        if (diff < 7) return `${diff} days ago`;

        return date.toLocaleDateString('en-US', { 
            month: 'short', 
            day: 'numeric' 
        });
    }
};

// Initialize app when DOM is ready
document.addEventListener('DOMContentLoaded', () => App.init());
/**
 * ClimbTrack - Climb Logging Module
 * Handles climb logging, XP calculation, and logbook management
 */

const Climbs = {
    selectedGrade: null,
    selectedStatus: 'send',
    selectedType: 'boulder',

    grades: {
        boulder: ['V0', 'V1', 'V2', 'V3', 'V4', 'V5', 'V6', 'V7', 'V8', 'V9', 'V10', 'V11', 'V12', 'V13', 'V14', 'V15', 'V16', 'V17'],
        sport: ['5.5', '5.6', '5.7', '5.8', '5.9', '5.10a', '5.10b', '5.10c', '5.10d', '5.11a', '5.11b', '5.11c', '5.11d', '5.12a', '5.12b', '5.12c', '5.12d', '5.13a', '5.13b', '5.13c', '5.13d', '5.14a', '5.14b', '5.14c', '5.14d'],
        trad: ['5.5', '5.6', '5.7', '5.8', '5.9', '5.10a', '5.10b', '5.10c', '5.10d', '5.11a', '5.11b', '5.11c', '5.11d', '5.12a', '5.12b', '5.12c', '5.12d', '5.13a', '5.13b', '5.13c', '5.13d'],
        'top-rope': ['5.5', '5.6', '5.7', '5.8', '5.9', '5.10a', '5.10b', '5.10c', '5.10d', '5.11a', '5.11b', '5.11c', '5.11d', '5.12a', '5.12b', '5.12c', '5.12d', '5.13a']
    },

    // Base XP values for each grade
    xpValues: {
        // Bouldering
        'V0': 10, 'V1': 15, 'V2': 20, 'V3': 30, 'V4': 45,
        'V5': 60, 'V6': 80, 'V7': 100, 'V8': 130, 'V9': 160,
        'V10': 200, 'V11': 250, 'V12': 300, 'V13': 400, 'V14': 500,
        'V15': 650, 'V16': 800, 'V17': 1000,
        // Sport/Trad
        '5.5': 5, '5.6': 8, '5.7': 12, '5.8': 18, '5.9': 25,
        '5.10a': 35, '5.10b': 40, '5.10c': 50, '5.10d': 60,
        '5.11a': 75, '5.11b': 90, '5.11c': 105, '5.11d': 120,
        '5.12a': 145, '5.12b': 170, '5.12c': 200, '5.12d': 230,
        '5.13a': 275, '5.13b': 320, '5.13c': 375, '5.13d': 430,
        '5.14a': 500, '5.14b': 600, '5.14c': 700, '5.14d': 850
    },

    // Status multipliers
    statusMultipliers: {
        'send': 1.0,
        'flash': 1.5,
        'onsight': 2.0,
        'project': 0.25
    },

    init() {
        this.bindEvents();
        this.renderGradeSelector();
    },

    bindEvents() {
        // Climb type change
        document.getElementById('climb-type')?.addEventListener('change', (e) => {
            this.selectedType = e.target.value;
            this.renderGradeSelector();
        });

        // Status buttons
        document.querySelectorAll('.status-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelectorAll('.status-btn').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                this.selectedStatus = btn.dataset.status;
            });
        });

        // Attempts counter
        document.getElementById('attempts-minus')?.addEventListener('click', () => {
            const input = document.getElementById('climb-attempts');
            if (input.value > 1) input.value = parseInt(input.value) - 1;
        });

        document.getElementById('attempts-plus')?.addEventListener('click', () => {
            const input = document.getElementById('climb-attempts');
            if (input.value < 99) input.value = parseInt(input.value) + 1;
        });

        // Form submission
        document.getElementById('log-climb-form')?.addEventListener('submit', (e) => {
            e.preventDefault();
            this.logClimb();
        });

        // Logbook filters
        document.getElementById('filter-type')?.addEventListener('change', () => this.updateLogbook());
        document.getElementById('filter-status')?.addEventListener('change', () => this.updateLogbook());
    },

    renderGradeSelector() {
        const container = document.getElementById('grade-selector');
        if (!container) return;

        const grades = this.grades[this.selectedType] || this.grades.boulder;
        
        container.innerHTML = grades.map(grade => `
            <button type="button" class="grade-btn ${grade === this.selectedGrade ? 'selected' : ''}" 
                    data-grade="${grade}">${grade}</button>
        `).join('');

        // Bind grade selection
        container.querySelectorAll('.grade-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                container.querySelectorAll('.grade-btn').forEach(b => b.classList.remove('selected'));
                btn.classList.add('selected');
                this.selectedGrade = btn.dataset.grade;
            });
        });

        // Reset selection if grade not available in new type
        if (!grades.includes(this.selectedGrade)) {
            this.selectedGrade = null;
        }
    },

    logClimb() {
        if (!this.selectedGrade) {
            alert('Please select a grade');
            return;
        }

        const user = App.currentUser;
        const name = document.getElementById('climb-name').value.trim();
        const attempts = parseInt(document.getElementById('climb-attempts').value) || 1;
        const notes = document.getElementById('climb-notes').value.trim();
        const date = document.getElementById('climb-date').value || new Date().toISOString();

        // Calculate XP
        const baseXp = this.xpValues[this.selectedGrade] || 10;
        const multiplier = this.statusMultipliers[this.selectedStatus];
        
        // Bonus for fewer attempts (only for sends)
        let attemptBonus = 1.0;
        if (this.selectedStatus === 'send' && attempts === 1) {
            attemptBonus = 1.2;
        }

        const xpEarned = Math.round(baseXp * multiplier * attemptBonus);

        // Create climb record
        const climb = {
            id: App.generateId(),
            name: name || this.selectedGrade,
            type: this.selectedType,
            grade: this.selectedGrade,
            status: this.selectedStatus,
            attempts,
            notes,
            date: new Date(date).toISOString(),
            xpEarned,
            createdAt: new Date().toISOString()
        };

        // Add to user's climbs
        user.climbs.push(climb);
        user.xp += xpEarned;

        // Save and update UI
        App.saveUserData();
        App.updateHeader();
        App.updateWeeklyGoal();
        App.checkRankUp();

        // Show feedback
        App.showAchievement(`+${xpEarned} XP! ${this.getStatusLabel(this.selectedStatus)}`);

        // Reset form
        this.resetForm();

        // Switch to dashboard to show the logged climb
        App.switchTab('dashboard');
    },

    getStatusLabel(status) {
        const labels = {
            'send': 'Nice send!',
            'flash': 'Flashed it! 🔥',
            'onsight': 'Onsight! Amazing! 👁️',
            'project': 'Project logged'
        };
        return labels[status] || 'Logged!';
    },

    resetForm() {
        document.getElementById('climb-name').value = '';
        document.getElementById('climb-attempts').value = '1';
        document.getElementById('climb-notes').value = '';
        document.getElementById('climb-date').valueAsDate = new Date();
        
        // Reset status to send
        document.querySelectorAll('.status-btn').forEach(b => b.classList.remove('active'));
        document.querySelector('.status-btn[data-status="send"]').classList.add('active');
        this.selectedStatus = 'send';
        
        // Reset grade
        document.querySelectorAll('.grade-btn').forEach(b => b.classList.remove('selected'));
        this.selectedGrade = null;
    },

    updateLogbook() {
        const container = document.getElementById('logbook-list');
        if (!container) return;

        const filterType = document.getElementById('filter-type').value;
        const filterStatus = document.getElementById('filter-status').value;

        let climbs = [...(App.currentUser.climbs || [])];

        // Apply filters
        if (filterType !== 'all') {
            climbs = climbs.filter(c => c.type === filterType);
        }
        if (filterStatus !== 'all') {
            climbs = climbs.filter(c => c.status === filterStatus);
        }

        // Sort by date (newest first)
        climbs.sort((a, b) => new Date(b.date) - new Date(a.date));

        if (climbs.length === 0) {
            container.innerHTML = `
                <div class="empty-state">
                    <i class="fas fa-book-open"></i>
                    <p>No climbs match your filters</p>
                </div>
            `;
            return;
        }

        container.innerHTML = climbs.map(climb => `
            <div class="logbook-item" data-id="${climb.id}">
                <div class="logbook-grade ${climb.type}">${climb.grade}</div>
                <div class="logbook-info">
                    <div class="logbook-name">${climb.name || climb.grade}</div>
                    <div class="logbook-meta">
                        <span>${this.capitalize(climb.type)}</span>
                        <span>${App.formatDate(climb.date)}</span>
                        ${climb.attempts > 1 ? `<span>${climb.attempts} attempts</span>` : ''}
                    </div>
                </div>
                <span class="logbook-status ${climb.status}">${this.capitalize(climb.status)}</span>
            </div>
        `).join('');
    },

    capitalize(str) {
        return str.charAt(0).toUpperCase() + str.slice(1).replace('-', ' ');
    }
};
/**
 * ClimbTrack - Leaderboard Module
 * Handles friend leaderboards and rankings
 */

const Leaderboard = {
    currentPeriod: 'weekly',

    // Demo friends data (in real app, this would come from backend)
    demoFriends: [
        {
            id: 'demo1',
            username: 'RockStar_42',
            avatar: { skinTone: '#8D5524', hairStyle: 'curly', hairColor: '#1A1A1A', eyes: 'normal', outfit: 'hoodie', accessory: 'chalk-bag' },
            xp: 1250,
            rank: 'Expert',
            climbs: 87,
            hardestGrade: 'V8',
            weeklyXp: 180,
            monthlyXp: 520
        },
        {
            id: 'demo2',
            username: 'CrimpQueen',
            avatar: { skinTone: '#F5D0C5', hairStyle: 'long', hairColor: '#D4A574', eyes: 'determined', outfit: 'tank', accessory: 'headband' },
            xp: 2100,
            rank: 'Elite',
            climbs: 156,
            hardestGrade: 'V10',
            weeklyXp: 320,
            monthlyXp: 890
        },
        {
            id: 'demo3',
            username: 'BoulderBro',
            avatar: { skinTone: '#C68642', hairStyle: 'buzz', hairColor: '#3D2314', eyes: 'normal', outfit: 'tshirt', accessory: 'none' },
            xp: 680,
            rank: 'Advanced',
            climbs: 45,
            hardestGrade: 'V5',
            weeklyXp: 95,
            monthlyXp: 280
        },
        {
            id: 'demo4',
            username: 'SendIt_Sarah',
            avatar: { skinTone: '#FFDBAC', hairStyle: 'ponytail', hairColor: '#B55239', eyes: 'happy', outfit: 'sports-bra', accessory: 'beanie' },
            xp: 1580,
            rank: 'Elite',
            climbs: 112,
            hardestGrade: 'V9',
            weeklyXp: 245,
            monthlyXp: 680
        }
    ],

    init() {
        this.bindEvents();
    },

    bindEvents() {
        // Period tabs
        document.querySelectorAll('.lb-tab').forEach(tab => {
            tab.addEventListener('click', () => {
                document.querySelectorAll('.lb-tab').forEach(t => t.classList.remove('active'));
                tab.classList.add('active');
                this.currentPeriod = tab.dataset.period;
                this.update();
            });
        });

        // Add friend button
        document.getElementById('add-friend-btn')?.addEventListener('click', () => {
            document.getElementById('friend-modal').classList.remove('hidden');
        });

        // Close friend modal
        document.getElementById('close-friend-modal')?.addEventListener('click', () => {
            document.getElementById('friend-modal').classList.add('hidden');
        });

        // Copy friend code
        document.getElementById('copy-code')?.addEventListener('click', () => {
            const code = App.currentUser.friendCode;
            navigator.clipboard.writeText(code);
            App.showAchievement('Friend code copied!');
        });

        // Send friend request
        document.getElementById('send-friend-request')?.addEventListener('click', () => {
            const code = document.getElementById('friend-code').value.trim().toUpperCase();
            if (code.length === 6) {
                this.sendFriendRequest(code);
            } else {
                alert('Please enter a valid 6-character friend code');
            }
        });
    },

    update() {
        this.updateXPLeaderboard();
        this.updateClimbsLeaderboard();
        this.updateGradeLeaderboard();
        this.updateFriendsList();
    },

    getAllParticipants() {
        const user = App.currentUser;
        const userStats = this.getUserStats(user);
        
        const userEntry = {
            id: user.id,
            username: user.username,
            avatar: user.avatar,
            xp: user.xp,
            rank: user.rank,
            climbs: user.climbs.length,
            hardestGrade: App.getHardestGrade(user.climbs.filter(c => c.status !== 'project')),
            weeklyXp: userStats.weeklyXp,
            monthlyXp: userStats.monthlyXp,
            isCurrentUser: true
        };

        return [userEntry, ...this.demoFriends];
    },

    getUserStats(user) {
        const now = new Date();
        const weekAgo = new Date(now - 7 * 24 * 60 * 60 * 1000);
        const monthAgo = new Date(now - 30 * 24 * 60 * 60 * 1000);

        const weeklyClimbs = user.climbs.filter(c => new Date(c.date) >= weekAgo);
        const monthlyClimbs = user.climbs.filter(c => new Date(c.date) >= monthAgo);

        return {
            weeklyXp: weeklyClimbs.reduce((sum, c) => sum + c.xpEarned, 0),
            monthlyXp: monthlyClimbs.reduce((sum, c) => sum + c.xpEarned, 0)
        };
    },

    updateXPLeaderboard() {
        const container = document.getElementById('xp-leaderboard');
        if (!container) return;

        let participants = this.getAllParticipants();

        // Sort by XP based on period
        if (this.currentPeriod === 'weekly') {
            participants.sort((a, b) => b.weeklyXp - a.weeklyXp);
        } else if (this.currentPeriod === 'monthly') {
            participants.sort((a, b) => b.monthlyXp - a.monthlyXp);
        } else {
            participants.sort((a, b) => b.xp - a.xp);
        }

        container.innerHTML = participants.slice(0, 5).map((p, i) => 
            this.renderLeaderboardItem(p, i + 1, this.getXpValue(p))
        ).join('');
    },

    updateClimbsLeaderboard() {
        const container = document.getElementById('climbs-leaderboard');
        if (!container) return;

        let participants = this.getAllParticipants();
        participants.sort((a, b) => b.climbs - a.climbs);

        container.innerHTML = participants.slice(0, 5).map((p, i) => 
            this.renderLeaderboardItem(p, i + 1, `${p.climbs} climbs`)
        ).join('');
    },

    updateGradeLeaderboard() {
        const container = document.getElementById('grade-leaderboard');
        if (!container) return;

        let participants = this.getAllParticipants()
            .filter(p => p.hardestGrade);

        // Sort by grade difficulty
        participants.sort((a, b) => {
            const gradeOrder = ['V0', 'V1', 'V2', 'V3', 'V4', 'V5', 'V6', 'V7', 'V8', 'V9', 'V10', 'V11', 'V12', 'V13', 'V14', 'V15'];
            return gradeOrder.indexOf(b.hardestGrade) - gradeOrder.indexOf(a.hardestGrade);
        });

        container.innerHTML = participants.slice(0, 5).map((p, i) => 
            this.renderLeaderboardItem(p, i + 1, p.hardestGrade)
        ).join('');
    },

    getXpValue(participant) {
        if (this.currentPeriod === 'weekly') {
            return `${participant.weeklyXp} XP`;
        } else if (this.currentPeriod === 'monthly') {
            return `${participant.monthlyXp} XP`;
        }
        return `${participant.xp} XP`;
    },

    renderLeaderboardItem(participant, rank, value) {
        const rankClass = rank === 1 ? 'gold' : rank === 2 ? 'silver' : rank === 3 ? 'bronze' : 'other';
        
        return `
            <div class="leaderboard-item">
                <div class="leaderboard-rank ${rankClass}">${rank}</div>
                <div class="leaderboard-user">
                    <div class="leaderboard-avatar" id="lb-avatar-${participant.id}"></div>
                    <span class="leaderboard-name ${participant.isCurrentUser ? 'you' : ''}">
                        ${participant.username}${participant.isCurrentUser ? ' (You)' : ''}
                    </span>
                </div>
                <div class="leaderboard-value">${value}</div>
            </div>
        `;
    },

    updateFriendsList() {
        const container = document.getElementById('friends-list');
        if (!container) return;

        if (this.demoFriends.length === 0) {
            container.innerHTML = `
                <div class="empty-state">
                    <p>No friends yet. Add some climbing buddies!</p>
                </div>
            `;
            return;
        }

        container.innerHTML = this.demoFriends.map(friend => `
            <div class="friend-item">
                <div class="friend-avatar" id="friend-avatar-${friend.id}"></div>
                <div class="friend-info">
                    <div class="friend-name">${friend.username}</div>
                    <div class="friend-status">${friend.rank} · ${friend.climbs} climbs</div>
                </div>
            </div>
        `).join('');
    },

    sendFriendRequest(code) {
        // In a real app, this would send to backend
        // For demo, just show success
        App.showAchievement('Friend request sent!');
        document.getElementById('friend-modal').classList.add('hidden');
        document.getElementById('friend-code').value = '';
    }
};
/**
 * ClimbTrack - Avatar Customization Module
 * Handles avatar creation and rendering
 */

const Avatar = {
    options: {
        skinTones: [
            '#FFDBAC', '#F5D0C5', '#E8B89D', '#D4A574', 
            '#C68642', '#8D5524', '#6B4423', '#3D2314'
        ],
        hairStyles: ['none', 'buzz', 'short', 'medium', 'long', 'curly', 'ponytail', 'bun', 'braids'],
        hairColors: [
            '#1A1A1A', '#3D2314', '#6B4423', '#8B4513',
            '#B55239', '#D4A574', '#E8C07D', '#F5DEB3',
            '#DC143C', '#4169E1', '#9B59B6', '#2ECC71'
        ],
        eyes: ['normal', 'determined', 'happy', 'focused', 'sleepy'],
        outfits: ['tank', 'tshirt', 'hoodie', 'sports-bra', 'long-sleeve'],
        accessories: ['none', 'headband', 'beanie', 'chalk-bag', 'glasses', 'bandana']
    },

    currentAvatar: null,

    init() {
        this.bindEvents();
        this.populateOptions();
    },

    bindEvents() {
        // Open avatar modal
        document.getElementById('edit-avatar-btn')?.addEventListener('click', () => {
            this.currentAvatar = { ...App.currentUser.avatar };
            this.updatePreview();
            this.setActiveOptions();
            document.getElementById('avatar-modal').classList.remove('hidden');
        });

        // Close avatar modal
        document.getElementById('close-avatar-modal')?.addEventListener('click', () => {
            document.getElementById('avatar-modal').classList.add('hidden');
        });

        // Save avatar
        document.getElementById('save-avatar')?.addEventListener('click', () => {
            App.currentUser.avatar = { ...this.currentAvatar };
            App.saveUserData();
            App.updateHeader();
            App.updateProfile();
            document.getElementById('avatar-modal').classList.add('hidden');
            App.showAchievement('Avatar updated!');
        });
    },

    populateOptions() {
        // Skin tones
        const skinContainer = document.getElementById('skin-options');
        if (skinContainer) {
            skinContainer.innerHTML = this.options.skinTones.map(color => `
                <div class="color-option" data-type="skinTone" data-value="${color}" 
                     style="background-color: ${color}"></div>
            `).join('');
            this.bindOptionClicks(skinContainer);
        }

        // Hair styles
        const hairStyleContainer = document.getElementById('hair-style-options');
        if (hairStyleContainer) {
            hairStyleContainer.innerHTML = this.options.hairStyles.map(style => `
                <div class="style-option" data-type="hairStyle" data-value="${style}">
                    ${this.capitalize(style)}
                </div>
            `).join('');
            this.bindOptionClicks(hairStyleContainer);
        }

        // Hair colors
        const hairColorContainer = document.getElementById('hair-color-options');
        if (hairColorContainer) {
            hairColorContainer.innerHTML = this.options.hairColors.map(color => `
                <div class="color-option" data-type="hairColor" data-value="${color}" 
                     style="background-color: ${color}"></div>
            `).join('');
            this.bindOptionClicks(hairColorContainer);
        }

        // Eyes
        const eyeContainer = document.getElementById('eye-options');
        if (eyeContainer) {
            eyeContainer.innerHTML = this.options.eyes.map(eye => `
                <div class="style-option" data-type="eyes" data-value="${eye}">
                    ${this.capitalize(eye)}
                </div>
            `).join('');
            this.bindOptionClicks(eyeContainer);
        }

        // Outfits
        const outfitContainer = document.getElementById('outfit-options');
        if (outfitContainer) {
            outfitContainer.innerHTML = this.options.outfits.map(outfit => `
                <div class="style-option" data-type="outfit" data-value="${outfit}">
                    ${this.capitalize(outfit.replace('-', ' '))}
                </div>
            `).join('');
            this.bindOptionClicks(outfitContainer);
        }

        // Accessories
        const accessoryContainer = document.getElementById('accessory-options');
        if (accessoryContainer) {
            accessoryContainer.innerHTML = this.options.accessories.map(acc => `
                <div class="style-option" data-type="accessory" data-value="${acc}">
                    ${this.capitalize(acc.replace('-', ' '))}
                </div>
            `).join('');
            this.bindOptionClicks(accessoryContainer);
        }
    },

    bindOptionClicks(container) {
        container.querySelectorAll('[data-type]').forEach(option => {
            option.addEventListener('click', () => {
                const type = option.dataset.type;
                const value = option.dataset.value;
                
                // Update selection visual
                container.querySelectorAll('[data-type]').forEach(o => o.classList.remove('selected'));
                option.classList.add('selected');
                
                // Update avatar
                this.currentAvatar[type] = value;
                this.updatePreview();
            });
        });
    },

    setActiveOptions() {
        const avatar = this.currentAvatar;
        
        // Set active states based on current avatar
        document.querySelectorAll('[data-type]').forEach(option => {
            const type = option.dataset.type;
            const value = option.dataset.value;
            option.classList.toggle('selected', avatar[type] === value);
        });
    },

    updatePreview() {
        this.renderLarge('avatar-preview', this.currentAvatar);
    },

    renderSmall(containerId, avatarData) {
        const container = document.getElementById(containerId);
        if (!container) return;
        container.innerHTML = this.generateAvatarSVG(avatarData, 40);
    },

    renderLarge(containerId, avatarData) {
        const container = document.getElementById(containerId);
        if (!container) return;
        container.innerHTML = this.generateAvatarSVG(avatarData, 100);
    },

    generateAvatarSVG(avatar, size) {
        const {
            skinTone = '#F5D0C5',
            hairStyle = 'short',
            hairColor = '#3D2314',
            eyes = 'normal',
            outfit = 'tank',
            accessory = 'none'
        } = avatar || {};

        // SVG avatar generation
        return `
            <svg width="${size}" height="${size}" viewBox="0 0 100 100" xmlns="[w3.org](http://www.w3.org/2000/svg)">
                <!-- Background circle -->
                <circle cx="50" cy="50" r="48" fill="${this.darken(skinTone, 20)}"/>
                
                <!-- Neck -->
                <rect x="40" y="65" width="20" height="15" fill="${skinTone}"/>
                
                <!-- Outfit -->
                ${this.renderOutfit(outfit)}
                
                <!-- Face -->
                <ellipse cx="50" cy="45" rx="28" ry="30" fill="${skinTone}"/>
                
                <!-- Hair (back) -->
                ${this.renderHairBack(hairStyle, hairColor)}
                
                <!-- Eyes -->
                ${this.renderEyes(eyes)}
                
                <!-- Nose -->
                <ellipse cx="50" cy="50" rx="3" ry="4" fill="${this.darken(skinTone, 10)}" opacity="0.5"/>
                
                <!-- Mouth -->
                <path d="M 43 58 Q 50 63 57 58" stroke="${this.darken(skinTone, 30)}" stroke-width="2" fill="none"/>
                
                <!-- Hair (front) -->
                ${this.renderHairFront(hairStyle, hairColor)}
                
                <!-- Accessory -->
                ${this.renderAccessory(accessory)}
            </svg>
        `;
    },

    renderOutfit(outfit) {
        const outfitColors = {
            'tank': '#FF6B35',
            'tshirt': '#4ECDC4',
            'hoodie': '#6B6B80',
            'sports-bra': '#9B59B6',
            'long-sleeve': '#2ECC71'
        };
        const color = outfitColors[outfit] || '#FF6B35';

        switch(outfit) {
            case 'tank':
                return `<path d="M 30 80 L 35 65 L 45 70 L 50 68 L 55 70 L 65 65 L 70 80 Z" fill="${color}"/>`;
            case 'hoodie':
                return `<path d="M 25 80 L 30 60 L 40 65 L 50 62 L 60 65 L 70 60 L 75 80 Z" fill="${color}"/>
                        <path d="M 40 65 Q 50 55 60 65" stroke="${this.darken(color, 20)}" stroke-width="3" fill="none"/>`;
            default:
                return `<path d="M 28 80 L 33 63 L 45 68 L 50 66 L 55 68 L 67 63 L 72 80 Z" fill="${color}"/>`;
        }
    },

    renderEyes(eyeType) {
        const baseEyes = `
            <ellipse cx="40" cy="42" rx="5" ry="4" fill="white"/>
            <ellipse cx="60" cy="42" rx="5" ry="4" fill="white"/>
        `;

        switch(eyeType) {
            case 'determined':
                return baseEyes + `
                    <circle cx="40" cy="42" r="2.5" fill="#3D2314"/>
                    <circle cx="60" cy="42" r="2.5" fill="#3D2314"/>
                    <line x1="35" y1="38" x2="45" y2="40" stroke="#3D2314" stroke-width="2"/>
                    <line x1="55" y1="40" x2="65" y2="38" stroke="#3D2314" stroke-width="2"/>
                `;
            case 'happy':
                return `
                    <path d="M 35 42 Q 40 46 45 42" stroke="#3D2314" stroke-width="2.5" fill="none"/>
                    <path d="M 55 42 Q 60 46 65 42" stroke="#3D2314" stroke-width="2.5" fill="none"/>
                `;
            case 'focused':
                return baseEyes + `
                    <circle cx="40" cy="43" r="2" fill="#3D2314"/>
                    <circle cx="60" cy="43" r="2" fill="#3D2314"/>
                `;
            case 'sleepy':
                return `
                    <line x1="35" y1="42" x2="45" y2="42" stroke="#3D2314" stroke-width="2.5"/>
                    <line x1="55" y1="42" x2="65" y2="42" stroke="#3D2314" stroke-width="2.5"/>
                `;
            default:
                return baseEyes + `
                    <circle cx="40" cy="42" r="2.5" fill="#3D2314"/>
                    <circle cx="60" cy="42" r="2.5" fill="#3D2314"/>
                `;
        }
    },

    renderHairBack(style, color) {
        switch(style) {
            case 'long':
                return `<ellipse cx="50" cy="40" rx="32" ry="35" fill="${color}"/>
                        <rect x="20" y="40" width="15" height="40" rx="5" fill="${color}"/>
                        <rect x="65" y="40" width="15" height="40" rx="5" fill="${color}"/>`;
            case 'ponytail':
                return `<ellipse cx="50" cy="35" rx="30" ry="28" fill="${color}"/>
                        <ellipse cx="70" cy="25" rx="10" ry="15" fill="${color}"/>`;
            case 'bun':
                return `<ellipse cx="50" cy="35" rx="30" ry="28" fill="${color}"/>
                        <circle cx="50" cy="12" r="12" fill="${color}"/>`;
            default:
                return '';
        }
    },

    renderHairFront(style, color) {
        switch(style) {
            case 'none':
                return '';
            case 'buzz':
                return `<path d="M 25 35 Q 50 10 75 35 Q 75 20 50 15 Q 25 20 25 35" fill="${color}"/>`;
            case 'short':
                return `<path d="M 22 40 Q 50 5 78 40 Q 78 25 50 15 Q 22 25 22 40" fill="${color}"/>`;
            case 'medium':
                return `<path d="M 20 45 Q 50 0 80 45 Q 80 25 50 12 Q 20 25 20 45" fill="${color}"/>
                        <path d="M 25 40 Q 35 35 30 50" fill="${color}"/>
                        <path d="M 75 40 Q 65 35 70 50" fill="${color}"/>`;
            case 'curly':
                return `<circle cx="30" cy="30" r="10" fill="${color}"/>
                        <circle cx="45" cy="20" r="10" fill="${color}"/>
                        <circle cx="55" cy="20" r="10" fill="${color}"/>
                        <circle cx="70" cy="30" r="10" fill="${color}"/>
                        <circle cx="25" cy="40" r="8" fill="${color}"/>
                        <circle cx="75" cy="40" r="8" fill="${color}"/>`;
            case 'braids':
                return `<path d="M 22 40 Q 50 5 78 40 Q 78 25 50 15 Q 22 25 22 40" fill="${color}"/>
                        <rect x="20" y="35" width="8" height="45" rx="4" fill="${color}"/>
                        <rect x="72" y="35" width="8" height="45" rx="4" fill="${color}"/>`;
            default:
                return `<path d="M 22 40 Q 50 5 78 40 Q 78 25 50 15 Q 22 25 22 40" fill="${color}"/>`;
        }
    },

    renderAccessory(accessory) {
        switch(accessory) {
            case 'headband':
                return `<rect x="22" y="28" width="56" height="6" rx="3" fill="#FF6B35"/>`;
            case 'beanie':
                return `<path d="M 20 35 Q 50 0 80 35 L 80 40 Q 50 20 20 40 Z" fill="#E74C3C"/>
                        <circle cx="50" cy="5" r="5" fill="#E74C3C"/>`;
            case 'glasses':
                return `<circle cx="38" cy="42" r="10" stroke="#1A1A1A" stroke-width="2" fill="none"/>
                        <circle cx="62" cy="42" r="10" stroke="#1A1A1A" stroke-width="2" fill="none"/>
                        <line x1="48" y1="42" x2="52" y2="42" stroke="#1A1A1A" stroke-width="2"/>
                        <line x1="28" y1="42" x2="22" y2="40" stroke="#1A1A1A" stroke-width="2"/>
                        <line x1="72" y1="42" x2="78" y2="40" stroke="#1A1A1A" stroke-width="2"/>`;
            case 'chalk-bag':
                return `<rect x="70" y="75" width="12" height="10" rx="2" fill="#4ECDC4"/>
                        <rect x="70" y="73" width="12" height="4" fill="#3DB8B0"/>`;
            case 'bandana':
                return `<path d="M 20 32 Q 50 22 80 32 L 78 38 Q 50 30 22 38 Z" fill="#9B59B6"/>`;
            default:
                return '';
        }
    },

    darken(hex, percent) {
        const num = parseInt(hex.replace('#', ''), 16);
        const amt = Math.round(2.55 * percent);
        const R = Math.max((num >> 16) - amt, 0);
        const G = Math.max((num >> 8 & 0x00FF) - amt, 0);
        const B = Math.max((num & 0x0000FF) - amt, 0);
        return `#${(1 << 24 | R << 16 | G << 8 | B).toString(16).slice(1)}`;
    },

    capitalize(str) {
        return str.charAt(0).toUpperCase() + str.slice(1);
    }
};
/**
 * ClimbTrack - Goals Module
 * Handles weekly goals and progress tracking
 */

const Goals = {
    init() {
        this.bindEvents();
    },

    bindEvents() {
        // Goal selector buttons
        document.querySelectorAll('.goal-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                const goal = parseInt(btn.dataset.goal);
                this.setWeeklyGoal(goal);
                
                // Update UI
                document.querySelectorAll('.goal-btn').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
            });
        });
    },

    setWeeklyGoal(sessions) {
        App.currentUser.weeklyGoal = sessions;
        App.saveUserData();
        App.updateWeeklyGoal();
        App.showAchievement(`Weekly goal set to ${sessions} sessions`);
    },

    getWeeklySessionCount() {
        const user = App.currentUser;
        if (!user || !user.climbs) return 0;

        const now = new Date();
        const startOfWeek = new Date(now);
        startOfWeek.setDate(now.getDate() - now.getDay()); // Start from Sunday
        startOfWeek.setHours(0, 0, 0, 0);

        // Get unique dates this week where user climbed
        const sessionsThisWeek = new Set(
            user.climbs
                .filter(c => new Date(c.date) >= startOfWeek)
                .map(c => c.date.split('T')[0])
        );

        return sessionsThisWeek.size;
    },

    checkGoalCompletion() {
        const sessions = this.getWeeklySessionCount();
        const goal = App.currentUser.weeklyGoal;

        if (sessions >= goal) {
            // Check if we already celebrated this week
            const lastCelebration = localStorage.getItem('lastGoalCelebration');
            const thisWeek = this.getWeekNumber();

            if (lastCelebration !== thisWeek) {
                localStorage.setItem('lastGoalCelebration', thisWeek);
                App.showAchievement('🎉 Weekly goal achieved!');
                
                // Bonus XP for completing goal
                App.currentUser.xp += 50;
                App.saveUserData();
                App.updateHeader();
            }
        }
    },

    getWeekNumber() {
        const now = new Date();
        const start = new Date(now.getFullYear(), 0, 1);
        const diff = now - start;
        const oneWeek = 604800000;
        return `${now.getFullYear()}-W${Math.ceil(diff / oneWeek)}`;
    }
};
# ClimbTrack 🧗

A mobile-first web application for tracking rock climbing progress, inspired by fitness tracking apps. Built with vanilla HTML, CSS, and JavaScript.

## Features

### 📊 Dashboard
- View total climbs, current streak, hardest grade, and monthly sessions
- Recent activity feed showing your latest sends
- Weekly goal progress bar

### 📝 Climb Logging
- Support for bouldering, sport, trad, and top rope climbing
- Grade selection (V-scale for bouldering, YDS for roped climbing)
- Completion status: Send, Flash, Onsight, or Project
- Attempt tracking and notes

### 📖 Logbook
- Complete history of all logged climbs
- Filter by climb type and completion status
- Chronological view with grade and status badges

### 🏆 Leaderboards & Rankings
- XP-based ranking system with 7 ranks:
  - Beginner → Novice → Intermediate → Advanced → Expert → Elite → Master
- Weekly, monthly, and all-time leaderboards
- Compare with friends on multiple metrics:
  - Total XP
  - Number of climbs
  - Hardest grades

### 👤 Avatar Customization
- Customizable SVG avatars with:
  - 8 skin tones
  - 9 hair styles
  - 12 hair colors
  - 5 eye styles
  - 5 outfit options
  - 6 accessories

### 🎯 Weekly Goals
- Set personalized weekly climbing session goals (1-7 sessions)
- Progress tracking with visual progress bar
- Bonus XP for completing weekly goals

## XP System

### Base XP by Grade

**Bouldering:**
| Grade | XP |
|-------|-----|
| V0-V2 | 10-20 |
| V3-V5 | 30-60 |
| V6-V8 | 80-130 |
| V9-V12 | 160-300 |
| V13+ | 400+ |

**Sport/Trad:**
| Grade | XP |
|-------|-----|
| 5.5-5.9 | 5-25 |
| 5.10a-d | 35-60 |
| 5.11a-d | 75-120 |
| 5.12a-d | 145-230 |
| 5.13+ | 275+ |

### Status Multipliers
- **Send**: 1.0x
- **Flash**: 1.5x
- **Onsight**: 2.0x
- **Project**: 0.25x

### Bonus XP
- First-try send: +20% bonus
- Weekly goal completion: +50 XP

## Rank Progression

| Rank | XP Required |
|------|-------------|
| Beginner | 0 |
| Novice | 100 |
| Intermediate | 300 |
| Advanced | 600 |
| Expert | 1,000 |
| Elite | 1,500 |
| Master | 2,500 |

## Setup

1. Clone or download the repository
2. Open `index.html` in a modern web browser
3. No build process or dependencies required!

## Browser Support

- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+

## Data Storage

All data is stored locally in the browser using `localStorage`. To export your data:
1. Go to Profile tab
2. Click "Export Data"
3. Save the JSON file

## Future Enhancements

- [ ] Backend integration for cloud sync
- [ ] Real friend system with invites
- [ ] Climbing gym integration
- [ ] Route photos
- [ ] Training plans
- [ ] Achievement badges
- [ ] Statistics and charts

## License

MIT License - Feel free to use and modify!
