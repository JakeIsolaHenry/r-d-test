!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>System1 - Monetizing Content for Creators</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            background-attachment: fixed;
            overflow-x: hidden;
            min-height: 100vh;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .solar-flow-section .container {
            background: transparent;
        }

        .header {
            text-align: center;
            padding: 60px 20px 40px;
            color: white;
        }

        .header h1 {
            font-size: 48px;
            font-weight: 700;
            margin-bottom: 20px;
            letter-spacing: -1px;
        }

        .system1-logo {
            font-size: 24px;
            margin-bottom: 10px;
            font-weight: 600;
        }

        .tab-container {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            flex-wrap: wrap;
        }

        .tab-button {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            border: 2px solid rgba(255, 255, 255, 0.3);
            padding: 12px 32px;
            border-radius: 25px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            backdrop-filter: blur(10px);
        }

        .tab-button:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: translateY(-2px);
        }

        .tab-button.active {
            background: white;
            color: #667eea;
            border-color: white;
        }

        .flow-section {
            min-height: 400vh;
            position: relative;
            display: none;
        }

        .flow-section.active {
            display: block;
        }

        .solar-flow-section .flow-section {
            background: transparent;
        }

        .sticky-container {
            position: sticky;
            top: 0;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .solar-flow-section .sticky-container {
            background: transparent;
        }

        .phone-container-wrapper {
            display: flex;
            align-items: center;
            gap: 80px;
            justify-content: center;
        }

        .phone-with-controls {
            display: flex;
            align-items: center;
            gap: 40px;
        }

        .phone-container {
            display: flex;
            gap: 80px;
            align-items: center;
            justify-content: center;
        }

        .phone {
            width: 320px;
            height: 650px;
            background: #1a1a1a;
            border-radius: 40px;
            padding: 12px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.4);
            position: relative;
            opacity: 0;
            transform: translateY(100px);
            transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .phone.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .phone-screen {
            width: 100%;
            height: 100%;
            background: white;
            border-radius: 32px;
            overflow: hidden;
            position: relative;
        }

        .phone-notch {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 150px;
            height: 28px;
            background: #1a1a1a;
            border-radius: 0 0 20px 20px;
            z-index: 10;
        }

        .arrow {
            font-size: 60px;
            color: white;
            opacity: 0;
            transform: scale(0);
            transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        .arrow.visible {
            opacity: 1;
            transform: scale(1);
        }

        .phone-content {
            padding: 40px 20px 20px;
            height: 100%;
            overflow-y: auto;
        }

        .phone-content::-webkit-scrollbar {
            width: 4px;
        }

        .phone-content::-webkit-scrollbar-thumb {
            background: #ccc;
            border-radius: 2px;
        }

        .linktree {
            background: linear-gradient(180deg, #FFB6D9 0%, #FFC9E3 100%);
            height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .linktree.blue {
            background: linear-gradient(180deg, #a8edea 0%, #fed6e3 100%);
        }

        .linktree.purple {
            background: linear-gradient(180deg, #d4a5ff 0%, #e8c4ff 100%);
        }

        .linktree.green {
            background: linear-gradient(180deg, #a8e6cf 0%, #dcedc1 100%);
        }

        .profile-pic {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background: #FFD93D;
            margin: 20px 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
            font-weight: 700;
            color: #333;
        }

        .username {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 10px;
        }

        .bio {
            font-size: 12px;
            text-align: center;
            margin-bottom: 20px;
            padding: 0 20px;
            color: #333;
        }

        .social-icons {
            display: flex;
            gap: 15px;
            margin-bottom: 30px;
        }

        .social-icon {
            width: 30px;
            height: 30px;
            background: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
        }

        .link-button {
            width: 260px;
            padding: 15px;
            background: white;
            border-radius: 25px;
            margin: 8px 0;
            text-align: center;
            font-size: 13px;
            font-weight: 500;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .link-button:hover {
            transform: scale(1.05);
        }

        .link-button.highlight {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            font-weight: 600;
        }

        .link-button.highlight-alt1 {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            font-weight: 600;
        }

        .link-button.highlight-alt2 {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            font-weight: 600;
        }

        .link-button.highlight-alt3 {
            background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
            color: white;
            font-weight: 600;
        }

        .article {
            padding: 40px 20px 20px;
            background: linear-gradient(180deg, #FFB6D9 0%, #FFC9E3 100%);
            height: 100%;
        }

        .article.blue {
            background: linear-gradient(180deg, #a8edea 0%, #fed6e3 100%);
        }

        .article.purple {
            background: linear-gradient(180deg, #d4a5ff 0%, #e8c4ff 100%);
        }

        .article.green {
            background: linear-gradient(180deg, #a8e6cf 0%, #dcedc1 100%);
        }

        .article.solar {
            background: linear-gradient(180deg, #ffeaa7 0%, #fdcb6e 100%);
        }

        .article-header {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 20px;
            background: white;
            padding: 15px;
            border-radius: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .article-avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: #FFD93D;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 16px;
            font-weight: 700;
            color: #333;
        }

        .author-info h3 {
            font-size: 16px;
            margin-bottom: 3px;
        }

        .author-link {
            font-size: 12px;
            color: #667eea;
        }

        .article-title {
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 15px;
            line-height: 1.3;
        }

        .article-content-block .article-title {
            margin-top: 0;
        }

        .article-text {
            font-size: 13px;
            line-height: 1.6;
            color: #444;
            margin-bottom: 15px;
        }

        .article-content-block {
            background: white;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }

        .article-content-block .article-text:last-child {
            margin-bottom: 0;
        }

        .related-searches {
            background: white;
            border-radius: 20px;
            padding: 15px;
            margin-bottom: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .search-title {
            font-size: 12px;
            color: #666;
            margin-bottom: 12px;
            font-weight: 600;
        }

        .search-chip {
            display: inline-block;
            background: #f8f9fa;
            padding: 8px 16px;
            border-radius: 20px;
            margin: 4px;
            font-size: 13px;
            cursor: pointer;
            border: 1px solid #e0e0e0;
            transition: all 0.2s;
        }

        .search-chip:hover {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-color: transparent;
            transform: scale(1.05);
        }

        .search-chip.alt1:hover {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
        }

        .search-chip.alt2:hover {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        }

        .search-chip.alt3:hover {
            background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
        }

        .serp {
            padding: 40px 20px 20px;
            background: linear-gradient(180deg, #FFB6D9 0%, #FFC9E3 100%);
            height: 100%;
        }

        .serp.blue {
            background: linear-gradient(180deg, #a8edea 0%, #fed6e3 100%);
        }

        .serp.purple {
            background: linear-gradient(180deg, #d4a5ff 0%, #e8c4ff 100%);
        }

        .serp.green {
            background: linear-gradient(180deg, #a8e6cf 0%, #dcedc1 100%);
        }

        .serp.solar {
            background: linear-gradient(180deg, #ffeaa7 0%, #fdcb6e 100%);
        }

        .search-bar {
            background: white;
            padding: 12px 16px;
            border-radius: 24px;
            font-size: 14px;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .sponsored-badge {
            display: inline-block;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 10px;
            font-weight: 600;
            margin-bottom: 10px;
        }

        .sponsored-badge.alt1 {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
        }

        .sponsored-badge.alt2 {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        }

        .sponsored-badge.alt3 {
            background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
        }

        .serp-result {
            padding: 20px;
            border-radius: 25px;
            margin-bottom: 16px;
            background: white;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .result-url {
            font-size: 11px;
            color: #5f6368;
            margin-bottom: 4px;
        }

        .result-link {
            color: #1a73e8;
            font-size: 13px;
            text-decoration: none;
            display: block;
            margin-bottom: 6px;
        }

        .result-title {
            font-size: 16px;
            font-weight: 600;
            color: #1a0dab;
            margin-bottom: 6px;
        }

        .result-description {
            font-size: 12px;
            color: #4d5156;
            line-height: 1.5;
        }

        .visit-button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 12px 24px;
            border-radius: 25px;
            border: none;
            font-size: 14px;
            font-weight: 600;
            margin-top: 12px;
            cursor: pointer;
            transition: all 0.2s;
            width: 100%;
        }

        .visit-button:hover {
            transform: scale(1.02);
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
        }

        .visit-button.alt1 {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
        }

        .visit-button.alt1:hover {
            box-shadow: 0 4px 12px rgba(240, 147, 251, 0.4);
        }

        .visit-button.alt2 {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        }

        .visit-button.alt2:hover {
            box-shadow: 0 4px 12px rgba(79, 172, 254, 0.4);
        }

        .visit-button.alt3 {
            background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
        }

        .visit-button.alt3:hover {
            box-shadow: 0 4px 12px rgba(67, 233, 123, 0.4);
        }

        .stage-label {
            position: absolute;
            top: -60px;
            left: 50%;
            transform: translateX(-50%);
            background: white;
            padding: 12px 24px;
            border-radius: 25px;
            font-size: 14px;
            font-weight: 600;
            color: #667eea;
            white-space: nowrap;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            opacity: 0;
            transition: opacity 0.6s;
        }

        .phone.visible .stage-label {
            opacity: 1;
        }

        .solar-flow-section {
            background: transparent;
            padding: 80px 20px;
            border-top: 3px solid rgba(255, 255, 255, 0.2);
        }

        .solar-flow-header {
            text-align: center;
            color: white;
            margin-bottom: 60px;
        }

        .solar-flow-header h2 {
            font-size: 42px;
            margin-bottom: 15px;
        }

        .solar-flow-header p {
            font-size: 18px;
            opacity: 0.9;
        }

        .solar-entry-controls {
            text-align: center;
            margin-bottom: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .solar-entry-label {
            background: white;
            padding: 10px 20px;
            border-radius: 20px;
            font-size: 13px;
            font-weight: 600;
            color: #667eea;
            display: inline-block;
            margin-bottom: 15px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            white-space: nowrap;
        }

        .solar-toggle-container {
            display: flex;
            justify-content: center;
            gap: 8px;
            flex-wrap: wrap;
        }

        .toggle-btn {
            background: rgba(255, 255, 255, 0.2);
            border: 2px solid rgba(255, 255, 255, 0.5);
            padding: 10px 16px;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 12px;
            font-weight: 600;
            color: white;
            backdrop-filter: blur(10px);
            text-align: center;
        }

        .toggle-btn.active {
            background: white;
            color: #667eea;
            border-color: white;
        }

        .toggle-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: translateY(-2px);
        }

        .footer {
            text-align: center;
            padding: 80px 20px;
            color: white;
        }

        .footer h2 {
            font-size: 32px;
            margin-bottom: 20px;
        }

        .footer p {
            font-size: 18px;
            opacity: 0.9;
        }

        @media (max-width: 1200px) {
            .phone-container {
                gap: 40px;
            }
            .phone-container-wrapper {
                gap: 40px;
            }
            .phone-with-controls {
                gap: 20px;
            }
            .phone {
                width: 280px;
                height: 570px;
            }
        }

        @media (max-width: 900px) {
            .phone-container {
                flex-direction: column;
                gap: 60px;
            }
            .phone-container-wrapper {
                flex-direction: column;
                gap: 60px;
                align-items: center;
            }
            .phone-with-controls {
                flex-direction: column;
                gap: 30px;
            }
            .solar-toggle-container {
                flex-direction: row !important;
            }
            .toggle-btn {
                width: auto !important;
            }
            .arrow {
                transform: rotate(90deg);
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <div class="system1-logo">SYSTEM1</div>
        <h1>MONETIZING CONTENT FOR CREATORS</h1>
    </div>

    <div class="tab-container">
        <button class="tab-button active" onclick="switchTab('linktree1')">Linktree 1</button>
        <button class="tab-button" onclick="switchTab('linktree2')">Linktree 2</button>
        <button class="tab-button" onclick="switchTab('linktree3')">Linktree 3</button>
        <button class="tab-button" onclick="switchTab('linktree4')">Linktree 4</button>
    </div>

    <div class="container">
        <!-- Linktree 1 - Position 4 -->
        <div class="flow-section active" id="linktree1">
            <div class="sticky-container">
                <div class="phone-container">
                    <div class="phone phone1">
                        <div class="stage-label">CREATOR'S LINKTREE</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="linktree">
                                <div class="profile-pic">KD</div>
                                <div class="username">Katy_Delma</div>
                                <div class="bio">💼💰 | Exploring the intersection of tech and finance | Sharing insights, guides, and tools ✨</div>
                                <div class="social-icons">
                                    <div class="social-icon">🎵</div>
                                    <div class="social-icon">▶️</div>
                                    <div class="social-icon">💻</div>
                                    <div class="social-icon">📷</div>
                                </div>
                                <div class="link-button">Instagram</div>
                                <div class="link-button">TikTok</div>
                                <div class="link-button">YouTube</div>
                                <div class="link-button highlight">How Google Pixel 10 Transforms Smartphone Tech</div>
                            </div>
                        </div>
                    </div>

                    <div class="arrow arrow1">→</div>

                    <div class="phone phone2">
                        <div class="stage-label">ARTICLE WITH RELATED SEARCHES</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="article phone-content">
                                <div class="article-header">
                                    <div class="article-avatar">KD</div>
                                    <div class="author-info">
                                        <h3>Katy Delma</h3>
                                        <div class="author-link">Linktree ✨</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h1 class="article-title">How Google Pixel 10 Transforms Smartphone Tech</h1>
                                    <div class="article-text">
                                        The Google Pixel 10 smartphone represents a leap forward in technology with its advanced AI capabilities and innovative features. Powered by the Google Tensor G5 chip, it enhances on-device AI tasks, revolutionizes photography, and provides seamless language translation.
                                    </div>
                                    <div class="article-text">
                                        This chip doesn't just enhance performance; it opens up new possibilities for on-device AI applications by providing power for features like the Gemini Nano model, enabling complex and generative AI tasks.
                                    </div>
                                </div>

                                <div class="related-searches">
                                    <div class="search-title">Related Searches</div>
                                    <div class="search-chip">Google Pixel Pro</div>
                                    <div class="search-chip">Google Tensor G5</div>
                                    <div class="search-chip">Gemini Nano AI</div>
                                </div>

                                <div class="article-content-block">
                                    <div class="article-text">
                                        One of the standout features is the Magic Cue, which seamlessly integrates with popular apps such as Gmail and Calendar to offer proactive suggestions and display relevant information at a glance. This feature not only enhances user convenience and efficiency but also upholds privacy.
                                    </div>
                                    <div class="article-text">
                                        Photography has been taken up a notch with a 5x telephoto lens and Super Res Zoom, boasting up to 20x zoom for capturing distant details. The Google Pixel 10 does not disappoint in the camera department, improving on past success with higher-quality photos achievable with faster autofocusing and advanced AI features.
                                    </div>
                                </div>

                                <div class="related-searches">
                                    <div class="search-title">More Related Searches</div>
                                    <div class="search-chip">Pixel 10 Camera</div>
                                    <div class="search-chip">5x Telephoto Lens</div>
                                    <div class="search-chip">Magic Cue Features</div>
                                </div>

                                <div class="article-content-block">
                                    <div class="article-text">
                                        The Pixel 10's unique AI-driven experiences do not stop at picture-taking. With the Pixel 10, AI takes on an even more comprehensive role, supporting real-time call translations through Voice Translate which allows conversations to flow naturally across different languages.
                                    </div>
                                    <div class="article-text">
                                        The visual and tactile appeal of the Pixel 10 cannot be understated. The series comes with a modern design incorporating a satin-finish metal frame and polished glass back, available in four distinct color options: Obsidian, Frost, Indigo, and Lemongrass.
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="arrow arrow2">→</div>

                    <div class="phone phone3">
                        <div class="stage-label">BRANDED SEARCH RESULTS PAGE</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="serp phone-content">
                                <div class="search-bar">🔍 Google Pixel Pro</div>
                                
                                <div class="serp-result">
                                    <div class="sponsored-badge">Sponsored</div>
                                    <div class="result-url">google.com</div>
                                    <div class="result-title">Get Google One Premium Storage</div>
                                    <div class="result-description">Shop Online - 2 TB of storage w/ VPN & Premium features on $9.99/mo plan w/AutoPay.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="sponsored-badge">Sponsored</div>
                                    <div class="result-url">t-mobile.com</div>
                                    <div class="result-title">Get Google Pixel 10 Pro On Us</div>
                                    <div class="result-description">Shop Online or In-Store - On us via 24 mo crdt w/ new line on $100+/mo plan w/AutoPay.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Linktree 2 - Position 1 -->
        <div class="flow-section" id="linktree2">
            <div class="sticky-container">
                <div class="phone-container">
                    <div class="phone phone1">
                        <div class="stage-label">CREATOR'S LINKTREE</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="linktree blue">
                                <div class="profile-pic">KD</div>
                                <div class="username">Katy_Delma</div>
                                <div class="bio">💼💰 | Exploring the intersection of tech and finance | Sharing insights, guides, and tools ✨</div>
                                <div class="social-icons">
                                    <div class="social-icon">🎵</div>
                                    <div class="social-icon">▶️</div>
                                    <div class="social-icon">💻</div>
                                    <div class="social-icon">📷</div>
                                </div>
                                <div class="link-button highlight-alt1">How Google Pixel 10 Transforms Smartphone Tech</div>
                                <div class="link-button">YouTube</div>
                                <div class="link-button">Instagram</div>
                                <div class="link-button">TikTok</div>
                            </div>
                        </div>
                    </div>

                    <div class="arrow arrow1">→</div>

                    <div class="phone phone2">
                        <div class="stage-label">ARTICLE WITH RELATED SEARCHES</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="article blue phone-content">
                                <div class="article-header">
                                    <div class="article-avatar">KD</div>
                                    <div class="author-info">
                                        <h3>Katy Delma</h3>
                                        <div class="author-link">Linktree ✨</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h1 class="article-title">How Google Pixel 10 Transforms Smartphone Tech</h1>
                                    <div class="article-text">Revolutionary AI-powered photography meets stunning design. The Pixel 10 introduces breakthrough features that redefine mobile computing for 2025 with the powerful Tensor G5 chip.</div>
                                    <div class="article-text">This chip doesn't just enhance performance; it opens up new possibilities for on-device AI applications by providing power for features like the Gemini Nano model, enabling complex and generative AI tasks without cloud dependency.</div>
                                </div>

                                <div class="related-searches">
                                    <div class="search-title">Related Searches</div>
                                    <div class="search-chip alt1">Best Smartphone 2025</div>
                                    <div class="search-chip alt1">Pixel 10 Camera</div>
                                    <div class="search-chip alt1">On-Device AI</div>
                                </div>

                                <div class="article-content-block">
                                    <div class="article-text">Adding to these innovative features is Pixel Journal, providing a private space for user reflection and well-being with personalized writing prompts and pattern insights, enhanced with AI.</div>
                                    <div class="article-text">The AI enhancements also extend to the sound experience. The Pixel 10 Recorder can now transform vocal recordings into music tracks, allowing for a thriving environment for creative expression.</div>
                                </div>

                                <div class="related-searches">
                                    <div class="search-title">More Related Searches</div>
                                    <div class="search-chip alt1">Pixel Journal App</div>
                                    <div class="search-chip alt1">AI Music Creation</div>
                                    <div class="search-chip alt1">Gboard AI Tools</div>
                                </div>

                                <div class="article-content-block">
                                    <div class="article-text">Writing Tools in Gboard have been improved with style-specific rewrites and suggestions boosted by voice commands.</div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="arrow arrow2">→</div>

                    <div class="phone phone3">
                        <div class="stage-label">BRANDED SEARCH RESULTS PAGE</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="serp blue phone-content">
                                <div class="search-bar">🔍 Best Smartphone 2025</div>
                                
                                <div class="serp-result">
                                    <div class="sponsored-badge alt1">Sponsored</div>
                                    <div class="result-url">bestbuy.com</div>
                                    <div class="result-title">Google Pixel 10 - Save $200</div>
                                    <div class="result-description">Limited time offer on the latest Pixel with AI features. Free shipping + trade-in credit.</div>
                                    <button class="visit-button alt1">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="sponsored-badge alt1">Sponsored</div>
                                    <div class="result-url">verizon.com</div>
                                    <div class="result-title">Switch to Verizon - Get Pixel 10 Free</div>
                                    <div class="result-description">When you switch and trade in. Plus unlimited data for your whole family.</div>
                                    <button class="visit-button alt1">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Linktree 3 - Position 2 -->
        <div class="flow-section" id="linktree3">
            <div class="sticky-container">
                <div class="phone-container">
                    <div class="phone phone1">
                        <div class="stage-label">CREATOR'S LINKTREE</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="linktree purple">
                                <div class="profile-pic">KD</div>
                                <div class="username">Katy_Delma</div>
                                <div class="bio">💼💰 | Exploring the intersection of tech and finance | Sharing insights, guides, and tools ✨</div>
                                <div class="social-icons">
                                    <div class="social-icon">🎵</div>
                                    <div class="social-icon">▶️</div>
                                    <div class="social-icon">💻</div>
                                    <div class="social-icon">📷</div>
                                </div>
                                <div class="link-button">TikTok</div>
                                <div class="link-button highlight-alt2">How Google Pixel 10 Transforms Smartphone Tech</div>
                                <div class="link-button">Instagram</div>
                                <div class="link-button">YouTube</div>
                            </div>
                        </div>
                    </div>

                    <div class="arrow arrow1">→</div>

                    <div class="phone phone2">
                        <div class="stage-label">ARTICLE WITH RELATED SEARCHES</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="article purple phone-content">
                                <div class="article-header">
                                    <div class="article-avatar">KD</div>
                                    <div class="author-info">
                                        <h3>Katy Delma</h3>
                                        <div class="author-link">Linktree ✨</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h1 class="article-title">How Google Pixel 10 Transforms Smartphone Tech</h1>
                                    <div class="article-text">Experience the future with Tensor G5 chip. Advanced machine learning brings unprecedented speed and intelligence to every interaction, from photography to real-time translation.</div>
                                    <div class="article-text">This chip doesn't just enhance performance; it opens up new possibilities for on-device AI applications by providing power for features like the Gemini Nano model.</div>
                                </div>

                                <div class="related-searches">
                                    <div class="search-title">Related Searches</div>
                                    <div class="search-chip alt2">Pixel 10 vs iPhone</div>
                                    <div class="search-chip alt2">Tensor G5 Chip</div>
                                    <div class="search-chip alt2">Real-Time Translation</div>
                                </div>

                                <div class="article-content-block">
                                    <div class="article-text">The Pixel 10's unique AI-driven experiences support real-time call translations through Voice Translate which allows conversations to flow naturally across different languages, including English, Spanish, and French.</div>
                                    <div class="article-text">In a move supporting long-term value, Google ensures that every Pixel 10 smartphone experience will be continually enhanced through software updates for seven years delivering sustained performance.</div>
                                </div>

                                <div class="related-searches">
                                    <div class="search-title">More Related Searches</div>
                                    <div class="search-chip alt2">Voice Translate</div>
                                    <div class="search-chip alt2">7 Years Updates</div>
                                    <div class="search-chip alt2">Android 15 Features</div>
                                </div>

                                <div class="article-content-block">
                                    <div class="article-text">This 'never-aging' promise is a significant leap toward longevity and sustainability in smartphone usage.</div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="arrow arrow2">→</div>

                    <div class="phone phone3">
                        <div class="stage-label">BRANDED SEARCH RESULTS PAGE</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="serp purple phone-content">
                                <div class="search-bar">🔍 Tensor G5 Chip</div>
                                
                                <div class="serp-result">
                                    <div class="sponsored-badge alt2">Sponsored</div>
                                    <div class="result-url">google.com</div>
                                    <div class="result-title">Tensor G5 - The Brain Behind Pixel 10</div>
                                    <div class="result-description">Discover how Google's custom chip revolutionizes mobile AI. Learn more about Pixel 10.</div>
                                    <button class="visit-button alt2">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="sponsored-badge alt2">Sponsored</div>
                                    <div class="result-url">amazon.com</div>
                                    <div class="result-title">Google Pixel 10 Unlocked</div>
                                    <div class="result-description">Prime members get exclusive pricing. Free returns and fast shipping available.</div>
                                    <button class="visit-button alt2">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Linktree 4 - Position 3 -->
        <div class="flow-section" id="linktree4">
            <div class="sticky-container">
                <div class="phone-container">
                    <div class="phone phone1">
                        <div class="stage-label">CREATOR'S LINKTREE</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="linktree green">
                                <div class="profile-pic">KD</div>
                                <div class="username">Katy_Delma</div>
                                <div class="bio">💼💰 | Exploring the intersection of tech and finance | Sharing insights, guides, and tools ✨</div>
                                <div class="social-icons">
                                    <div class="social-icon">🎵</div>
                                    <div class="social-icon">▶️</div>
                                    <div class="social-icon">💻</div>
                                    <div class="social-icon">📷</div>
                                </div>
                                <div class="link-button">YouTube</div>
                                <div class="link-button">TikTok</div>
                                <div class="link-button highlight-alt3">How Google Pixel 10 Transforms Smartphone Tech</div>
                                <div class="link-button">Instagram</div>
                            </div>
                        </div>
                    </div>

                    <div class="arrow arrow1">→</div>

                    <div class="phone phone2">
                        <div class="stage-label">ARTICLE WITH RELATED SEARCHES</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="article green phone-content">
                                <div class="article-header">
                                    <div class="article-avatar">KD</div>
                                    <div class="author-info">
                                        <h3>Katy Delma</h3>
                                        <div class="author-link">Linktree ✨</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h1 class="article-title">How Google Pixel 10 Transforms Smartphone Tech</h1>
                                    <div class="article-text">Sustainability meets innovation. The Pixel 10 features recycled materials and energy-efficient design while delivering flagship performance powered by the revolutionary Tensor G5 chip.</div>
                                    <div class="article-text">This chip doesn't just enhance performance; it opens up new possibilities for on-device AI applications while maintaining exceptional battery efficiency.</div>
                                </div>

                                <div class="related-searches">
                                    <div class="search-title">Related Searches</div>
                                    <div class="search-chip alt3">Eco-Friendly Phone</div>
                                    <div class="search-chip alt3">Pixel 10 Battery Life</div>
                                    <div class="search-chip alt3">Sustainable Tech</div>
                                </div>

                                <div class="article-content-block">
                                    <div class="article-text">The visual and tactile appeal of the Pixel 10 cannot be understated. The series comes with a modern design incorporating a satin-finish metal frame and polished glass back, available in four distinct color options.</div>
                                    <div class="article-text">Furthermore, switching to Google Pixel has been streamlined, as it offers compatible experiences with popular devices, ensuring that users do not feel isolated from other ecosystems.</div>
                                </div>

                                <div class="related-searches">
                                    <div class="search-title">More Related Searches</div>
                                    <div class="search-chip alt3">Pixel Watch 3</div>
                                    <div class="search-chip alt3">Pixel Buds Pro 2</div>
                                    <div class="search-chip alt3">3000 Nits Display</div>
                                </div>

                                <div class="article-content-block">
                                    <div class="article-text">Additional seamless integrations are evident with accessories like the Pixel Watch and Pixel Buds with dynamic spatial audio.</div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="arrow arrow2">→</div>

                    <div class="phone phone3">
                        <div class="stage-label">BRANDED SEARCH RESULTS PAGE</div>
                        <div class="phone-screen">
                            <div class="phone-notch"></div>
                            <div class="serp green phone-content">
                                <div class="search-bar">🔍 Eco-Friendly Phone</div>
                                
                                <div class="serp-result">
                                    <div class="sponsored-badge alt3">Sponsored</div>
                                    <div class="result-url">google.com</div>
                                    <div class="result-title">Pixel 10 - Built with 70% Recycled Materials</div>
                                    <div class="result-description">Our most sustainable phone yet. Carbon neutral shipping and energy efficient design.</div>
                                    <button class="visit-button alt3">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="sponsored-badge alt3">Sponsored</div>
                                    <div class="result-url">att.com</div>
                                    <div class="result-title">AT&T - Trade In & Go Green</div>
                                    <div class="result-description">Recycle your old device and get the new Pixel 10. We'll plant a tree with every purchase.</div>
                                    <button class="visit-button alt3">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SolarFlow - User Journey Overview</title>
    
    <!-- SEO Meta Tags -->
    <meta name="description" content="Interactive solar panel marketing flow demonstration showing user journey from social media to content engagement.">
    <meta name="keywords" content="solar panels, solar energy, user journey, marketing flow, lead generation">
    
    <!-- Open Graph Meta Tags -->
    <meta property="og:title" content="SolarFlow - User Journey Overview">
    <meta property="og:description" content="Interactive demonstration of solar panel marketing user journey">
    <meta property="og:type" content="website">
    
    <!-- Favicon -->
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='0.9em' font-size='90'>☀️</text></svg>" type="image/svg+xml">
    
    <script>
        // GLOBAL FUNCTIONS - LOADED FIRST
        let autoRotateInterval;
        let currentView = 0; // 0 = social, 1 = thank you, 2 = disqualify, 3 = linktree
        const views = ['social', 'thankyou', 'disqualify', 'linktree'];
        const ROTATION_INTERVAL = 5000; // 5 seconds between rotations
        
        // Handle Linktree click to navigate to external URL
        function handleLinktreeClick() {
            // Stop auto-rotation on user interaction
            stopAutoRotation();
            
            // Open the Nation.com article in a new tab
            window.open('https://www.nation.com/how-solar-energy-reduces-costs-and-boosts-home-value-en-us/', '_blank');
        }
        
        // Main view functions
        function showSocial() {
            // Stop auto-rotation on user interaction
            stopAutoRotation();
            
            document.getElementById('stage1-iframe').style.display = 'none';
            document.getElementById('stage1-social-div').style.display = 'block';
            document.getElementById('stage1-linktree-div').style.display = 'none';
            document.getElementById('stage1-linktree-div').style.visibility = 'hidden';
            
            // Update button highlighting
            document.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelector('[onclick="showSocial()"]').classList.add('active');
            
            // Update bottom section
            document.getElementById('stage1-title').textContent = 'Ad on Socials';
            document.getElementById('stage1-description').innerHTML = '<p style="margin: 0; color: #555; line-height: 1.6;">Learn More button links out to content page.</p>';
            
            currentView = 0;
        }
        
        function showThankYou() {
            // Stop auto-rotation on user interaction
            stopAutoRotation();
            
            document.getElementById('stage1-social-div').style.display = 'none';
            document.getElementById('stage1-linktree-div').style.display = 'none';
            document.getElementById('stage1-linktree-div').style.visibility = 'hidden';
            document.getElementById('stage1-iframe').style.display = 'block';
            document.getElementById('stage1-iframe').src = 'flow.html?step=6&hideDevNav=true';
            
            // Update button highlighting
            document.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelector('[onclick="showThankYou()"]').classList.add('active');
            
            // Update bottom section
            document.getElementById('stage1-title').textContent = 'Thank You Page';
            document.getElementById('stage1-description').innerHTML = '<p style="margin: 0 0 15px 0; color: #555; line-height: 1.6;">One option to place content articles within the flow. Can be slotted in to any part of the flow on any vertical.</p><div style="text-align: right;"><a href="index.html" class="path-button">Path</a></div>';
            
            currentView = 1;
        }
        
        function showDisqualify() {
            // Stop auto-rotation on user interaction
            stopAutoRotation();
            
            document.getElementById('stage1-social-div').style.display = 'none';
            document.getElementById('stage1-linktree-div').style.display = 'none';
            document.getElementById('stage1-linktree-div').style.visibility = 'hidden';
            document.getElementById('stage1-iframe').style.display = 'block';
            document.getElementById('stage1-iframe').src = 'flow.html?step=4&autoSelect=mostly-shade&showPopup=true&hideDevNav=true';
            
            // Update button highlighting
            document.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelector('[onclick="showDisqualify()"]').classList.add('active');
            
            // Update bottom section
            document.getElementById('stage1-title').textContent = 'Disqualifying Offer';
            document.getElementById('stage1-description').innerHTML = '<p style="margin: 0 0 15px 0; color: #555; line-height: 1.6;">User can be shown a link to a content article on any vertical if they do not qualify for an offer.</p><div style="text-align: right;"><a href="index.html" class="path-button">Path</a></div>';
            
            currentView = 2;
        }
        
        function showLinktree() {
            // Stop auto-rotation on user interaction
            stopAutoRotation();
            
            document.getElementById('stage1-iframe').style.display = 'none';
            document.getElementById('stage1-social-div').style.display = 'none';
            
            const linktreeDiv = document.getElementById('stage1-linktree-div');
            linktreeDiv.style.display = 'block';
            linktreeDiv.style.visibility = 'visible';
            
            // Update button highlighting
            document.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelector('[onclick="showLinktree()"]').classList.add('active');
            
            // Update bottom section
            document.getElementById('stage1-title').textContent = 'Linktree';
            document.getElementById('stage1-description').innerHTML = '<p style="margin: 0; color: #555; line-height: 1.6;">User clicks on Linktree button linking out to article.</p>';
            
            currentView = 3;
        }
        
        // Auto-rotation function
        function rotateView() {
            // Move to next view
            currentView = (currentView + 1) % 4;
            
            // Show appropriate view
            if (currentView === 0) {
                showSocial();
            } else if (currentView === 1) {
                showThankYou();
            } else if (currentView === 2) {
                showDisqualify();
            } else {
                showLinktree();
            }
        }
        
        // Start auto-rotation
        function startAutoRotation() {
            // Clear any existing interval
            if (autoRotateInterval) {
                clearInterval(autoRotateInterval);
            }
            
            // Set up new rotation interval
            autoRotateInterval = setInterval(rotateView, ROTATION_INTERVAL);
        }
        
        // Stop auto-rotation
        function stopAutoRotation() {
            if (autoRotateInterval) {
                clearInterval(autoRotateInterval);
                autoRotateInterval = null;
            }
        }
        
        // Restart auto-rotation
        function restartAutoRotation() {
            stopAutoRotation();
            startAutoRotation();
        }
        
        // Manually switch to a specific view
        function switchToView(viewName) {
            if (viewName === 'social') {
                showSocial();
            } else if (viewName === 'thankyou') {
                showThankYou();
            } else if (viewName === 'disqualify') {
                showDisqualify();
            }
            
            // Restart the rotation timer
            restartAutoRotation();
        }
    </script>
    
    <style>
        /* ============================================
           MAIN NAVIGATION
           ============================================ */
        .main-nav {
            display: none;
        }

        .nav-close {
            display: none;
        }

        .nav-restore {
            display: none;
        }

        .main-nav a {
            color: #4CAF50;
            text-decoration: none;
            margin: 0 20px;
            padding: 8px 16px;
            border-radius: 25px;
            background: rgba(76, 175, 80, 0.1);
            transition: all 0.3s ease;
            font-weight: 500;
            border: 1px solid rgba(76, 175, 80, 0.3);
        }

        .main-nav a:hover {
            background: rgba(76, 175, 80, 0.2);
            transform: translateY(-1px);
            box-shadow: 0 4px 8px rgba(76, 175, 80, 0.2);
        }

        .main-nav a.current {
            background: #4CAF50;
            color: white;
            font-weight: 600;
            border-color: #4CAF50;
        }

        .nav-toggle {
            background: rgba(76, 175, 80, 0.2);
            color: #4CAF50;
            border: 1px solid rgba(76, 175, 80, 0.3);
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            cursor: pointer;
            margin-left: 20px;
            transition: all 0.3s ease;
        }

        .nav-toggle:hover {
            background: rgba(76, 175, 80, 0.3);
            transform: translateY(-1px);
        }

        .nav-close {
            position: fixed;
            top: 15px;
            right: 15px;
            background: rgba(255, 0, 0, 0.8);
            color: white;
            border: none;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            font-size: 16px;
            cursor: pointer;
            z-index: 10002;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
            font-weight: bold;
        }

        .nav-close:hover {
            background: rgba(255, 0, 0, 1);
            transform: scale(1.1);
        }

        .nav-restore {
            position: fixed;
            top: 10px;
            right: 10px;
            background: #4CAF50;
            color: white;
            border: none;
            padding: 8px 12px;
            border-radius: 20px;
            font-size: 12px;
            cursor: pointer;
            z-index: 10001;
            display: none;
            box-shadow: 0 2px 10px rgba(76, 175, 80, 0.3);
            transition: all 0.3s ease;
        }

        .nav-restore:hover {
            background: #45a049;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(76, 175, 80, 0.4);
        }

        /* SERP iframe specific styling */
        .serp-iframe {
            transform: scale(0.45) !important;
            margin-top: -650px !important;
            height: 1200px !important;
        }
        
        /* Mobile Navigation */
        @media (max-width: 768px) {
            .main-nav {
                padding: 10px 5px;
                font-size: 12px;
            }
            
            .main-nav a {
                margin: 0 8px;
                padding: 6px 12px;
                font-size: 12px;
            }
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Helvetica Neue', Arial, sans-serif;
            padding-top: 0;
            background: #f8f9fa;
            margin: 0;
            min-height: 100vh;
            -webkit-text-size-adjust: 100%;
            -webkit-tap-highlight-color: transparent;
            touch-action: manipulation;
            transition: padding-top 0.3s ease;
            /* Improve iOS scrolling performance */
            -webkit-overflow-scrolling: touch;
            overflow-x: hidden; /* Prevent horizontal body scroll */
        }
        
        body.dev-nav-hidden {
            padding-top: 0;
        }

        .page-title {
            text-align: center;
            margin-bottom: 30px;
            margin-top: 40px;
            padding: 0 20px;
            display: flex;
            align-items: flex-end;
            justify-content: center;
            gap: 20px;
        }

        .page-title h1 {
            font-size: 2.5rem;
            font-weight: 700;
            color: #333;
            margin: 0;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Helvetica Neue', Arial, sans-serif;
        }

        .path-button {
            background: linear-gradient(135deg, #4CAF50 0%, #45a049 100%);
            color: white;
            text-decoration: none;
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 0.8rem;
            font-weight: 500;
            transition: all 0.3s ease;
            box-shadow: 0 2px 8px rgba(76, 175, 80, 0.3);
            border: 1px solid rgba(255,255,255,0.2);
            align-self: center;
            transform: translateY(4px);
        }

        .path-button:hover {
            transform: translateY(-1px);
            box-shadow: 0 3px 10px rgba(76, 175, 80, 0.35);
            background: linear-gradient(135deg, #45a049 0%, #4CAF50 100%);
        }

        /* Hide title on mobile */
        @media (max-width: 768px) {
            .page-title {
                display: none;
            }
        }
        /* Conference presentation mode */
        .conference-mode {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: #000;
            color: white;
            z-index: 20000;
            display: none;
            padding: 20px;
            overflow-y: auto;
        }
        
        .conference-mode.active {
            display: block;
        }
        
        .conference-toggle {
            position: fixed;
            top: 50px;
            right: 20px;
            background: #333;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 20px;
            font-size: 0.8rem;
            cursor: pointer;
            z-index: 15000;
            display: none; /* Hidden for now */
        }
        
        .conference-toggle:hover {
            background: #555;
        }
        
        @media (max-width: 768px) {
            .conference-toggle {
                top: 45px;
                right: 10px;
                padding: 8px 12px;
                font-size: 0.75rem;
            }
        }

        .flow-container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0px 20px 20px 20px; /* Removed top padding completely */
        }

        .flow-header {
            text-align: center;
            margin-bottom: 0px; /* Removed margin completely */
            display: none; /* Hide the header completely */
        }

        .flow-title {
            font-size: 2.5rem;
            font-weight: 700;
            color: #333;
            margin-bottom: 10px;
        }

        .flow-subtitle {
            font-size: 1.2rem;
            color: #666;
            max-width: 600px;
            margin: 0 auto;
        }

        .flow-stages {
            display: flex;
            gap: 40px;
            justify-content: center;
            align-items: flex-start; /* Changed from stretch to flex-start */
            flex-wrap: wrap;
        }

        .flow-stage {
            flex: 1;
            min-width: 350px;
            max-width: 400px;
            background: white;
            border-radius: 20px;
            padding: 5px 20px 5px 20px; /* Further reduced bottom padding to 5px */
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            position: relative;
            display: flex;
            flex-direction: column;
        }

        .stage-header {
            text-align: center;
            margin-bottom: 15px; /* Keep same margin below */
            min-height: 50px; /* Slightly reduced */
            display: flex;
            flex-direction: column;
            justify-content: center; /* Center vertically */
            align-items: center;
            padding: 10px 0 20px 0; /* Less space above, more below */
        }

        .stage-title {
            font-size: 1.4rem;
            font-weight: 600;
            color: #333;
            margin-bottom: 0px;
            min-height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            line-height: 1.2;
        }

        /* Larger titles for stages 2 and 3 */
        .flow-stage:nth-child(2) .stage-title,
        .flow-stage:nth-child(3) .stage-title {
            font-size: 1.5rem;
            font-weight: 700;
        }

        .stage-description {
            display: none; /* Hide all descriptions */
        }

        /* Stage 1 Toggle Buttons */
        .stage-toggle-buttons {
            display: flex;
            gap: 3px; /* Reduced from 5px */
            margin-top: 10px;
            margin-bottom: 0px;
            flex-wrap: nowrap; /* Changed from wrap to nowrap */
            justify-content: center;
            width: 100%;
        }

        .toggle-btn {
            padding: 4px 8px; /* Reduced padding */
            border: 2px solid #e9ecef;
            border-radius: 12px; /* Smaller radius */
            background: #f8f9fa;
            color: #495057;
            font-size: 0.65rem; /* Smaller font */
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s;
            min-height: 28px; /* Smaller height */
            flex: 1; /* Make buttons flex to fit */
            text-align: center;
            white-space: nowrap; /* Prevent text wrapping */
        }

        /* iPhone 12 specific optimizations */
        @media (max-width: 390px) and (min-width: 375px) {
            .toggle-btn {
                padding: 3px 6px; /* Even smaller padding for iPhone 12 */
                font-size: 0.6rem; /* Smaller font for iPhone 12 */
                min-height: 26px;
            }
            
            .stage-toggle-buttons {
                gap: 2px; /* Tighter gap for iPhone 12 */
            }
        }

        .toggle-btn:hover {
            border-color: #f5a623;
            background: #fff3cd;
            color: #856404;
        }

        .toggle-btn.active {
            border-color: #f5a623;
            background: #f5a623;
            color: white;
        }

        /* Stage 1 Version Management */
        .stage1-version {
            position: static;
        }

        .stage1-version.active {
            display: block;
        }

        /* Facebook Ad Mockup Styles */
        .social-ad-mockup {
            background: #f0f2f5;
            padding: 0;
            overflow-y: auto;
            height: 100%;
            display: flex;
            flex-direction: column;
        }

        .facebook-ad {
            background: white;
            margin: 8px;
            border-radius: 8px;
            overflow: hidden;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            flex: 1;
            display: flex;
            flex-direction: column;
            min-height: 700px; /* Even taller for much longer video */
        }

        .fb-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 14px 16px; /* Smaller padding to maximize video space */
            flex-shrink: 0;
        }

        .fb-profile {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .fb-avatar img {
            width: 50px; /* Larger avatar */
            height: 50px;
            border-radius: 50%;
        }

        .fb-info {
            display: flex;
            flex-direction: column;
        }

        .fb-name {
            font-weight: 600;
            font-size: 18px; /* Larger text */
            color: #1c1e21;
            line-height: 1.2;
        }

        .fb-sponsored {
            font-size: 15px; /* Larger text */
            color: #65676b;
            line-height: 1.2;
        }

        .fb-library-id {
            font-size: 13px;
            color: #65676b;
            line-height: 1.2;
            margin-top: 2px;
        }

        .fb-menu {
            color: #65676b;
            font-size: 24px; /* Larger menu */
            cursor: pointer;
            padding: 12px;
            border-radius: 50%;
        }

        .fb-menu:hover {
            background: #f2f3f4;
        }

        .fb-content {
            padding: 0 16px 12px; /* Minimal padding */
            flex-shrink: 0;
        }

        .fb-text {
            font-size: 15px; /* Smaller to save space */
            line-height: 1.3;
            color: #1c1e21;
            margin: 0;
        }

        .fb-media {
            position: relative;
            flex: 1; /* Take all remaining space */
            margin-bottom: 12px; /* Minimal margin */
            min-height: 520px; /* Much taller video area */
        }

        .fb-video-container {
            position: relative;
            background: transparent !important;
            height: 100% !important;
            width: 100% !important;
            min-height: 520px !important;
        }

        .fb-video-placeholder {
            width: 100% !important;
            height: 100% !important;
            background: url('https://images.unsplash.com/photo-1497440001374-f26997328c1b?w=600&h=800&fit=crop&crop=entropy') center/cover !important;
            position: relative !important;
            display: flex !important;
            align-items: center !important;
            justify-content: center !important;
            min-height: 520px !important;
        }

        .fb-video-overlay {
            position: absolute !important;
            top: 0 !important;
            left: 0 !important;
            right: 0 !important;
            bottom: 0 !important;
            width: 100% !important;
            height: 100% !important;
            display: flex !important;
            align-items: center !important;
            justify-content: center !important;
            background: rgba(0,0,0,0.2) !important;
        }

        .fb-play-button {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background: rgba(255,255,255,0.9);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px;
            color: #333;
            cursor: pointer;
            transition: all 0.2s;
            padding-left: 4px; /* Offset triangle to appear more centered */
        }

        .fb-play-button:hover {
            background: white;
            transform: scale(1.05);
        }

        .solarflow-logo-overlay {
            display: none;
        }

        .fb-video-overlay {
            position: absolute;
            inset: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(0,0,0,0.3);
        }

        .fb-play-button {
            width: 80px; /* Much larger play button */
            height: 80px;
            border-radius: 50%;
            background: rgba(255,255,255,0.9);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px; /* Larger play icon */
            color: #333;
            cursor: pointer;
            transition: all 0.2s;
        }

        .fb-play-button:hover {
            background: white;
            transform: scale(1.05);
        }

        .solarflow-logo-overlay {
            position: absolute;
            top: 25px; /* More space from top */
            left: 50%;
            transform: translateX(-50%);
        }

        .solarflow-logo-bg {
            background: #f5a623;
            color: white;
            padding: 12px 20px; /* Larger logo */
            border-radius: 6px;
            font-weight: bold;
            font-size: 16px; /* Larger text */
            text-align: center;
            line-height: 1.2;
        }

        .fb-cta {
            padding: 20px 16px; /* More padding */
            border-top: 1px solid #e4e6ea;
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-top: auto; /* Push to bottom */
        }

        .fb-cta-text {
            flex: 1;
        }

        .fb-url {
            font-size: 13px; /* Slightly larger */
            color: #65676b;
            text-transform: uppercase;
            margin-bottom: 4px; /* More space */
        }

        .fb-headline {
            font-size: 18px; /* Larger headline */
            font-weight: 600;
            color: #1c1e21;
            margin-bottom: 4px; /* More space */
            line-height: 1.2;
        }

        .fb-description {
            font-size: 15px; /* Larger description */
            color: #65676b;
            line-height: 1.2;
        }

        .fb-learn-more {
            background: #e4e6ea;
            color: #65676b;
            border: 1px solid #dadde1;
            padding: 12px 20px; /* Larger button */
            border-radius: 6px;
            font-weight: 600;
            font-size: 15px; /* Larger text */
            cursor: pointer;
            transition: background 0.2s;
        }

        .fb-learn-more:hover {
            background: #d8dadf;
        }

        .live-link {
            display: inline-flex;
            align-items: center;
            gap: 5px;
            padding: 12px 20px;
            background: #f5a623;
            color: white;
            text-decoration: none;
            border-radius: 25px;
            font-size: 0.85rem;
            font-weight: 500;
            transition: background 0.2s;
            min-height: 44px;
            justify-content: center;
        }

        .live-link:hover {
            background: #e0941f;
        }

        /* iPhone Frame - iPhone 14 Pro Max exact dimensions */
        .phone-frame {
            background: #1f1f1f;
            border-radius: 35px;
            padding: 8px;
            margin: 5px auto; /* Minimal margin */
            width: 300px;
            height: 650px;
            position: relative;
            box-shadow: 0 15px 40px rgba(0,0,0,0.3);
        }

        .phone-screen {
            width: 100%;
            height: 100%;
            border-radius: 27px;
            overflow: hidden;
            position: relative;
            background: white;
        }

        .page-iframe {
            width: 430px;
            height: 932px;
            border: none;
            border-radius: 27px;
            transform: scale(0.675);;
            transform-origin: center center;
            position: absolute;
            top: 50%;
            left: 50%;
            margin-left: -215px;
            margin-top: -466px;
        }

        /* Key Terms Section */
        .key-terms {
            margin-top: 10px; /* Further reduced from 15px to 10px */
            margin-bottom: 5px; /* Added small bottom margin to end container shortly after content */
        }

        .section-title {
            font-size: 1.1rem;
            font-weight: 600;
            color: #333;
            margin-bottom: 15px;
        }

        .terms-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 10px; /* Reduced from 20px to 10px */
        }

        .term-button {
            padding: 8px 14px;
            border: 2px solid #e9ecef;
            border-radius: 20px;
            background: #f8f9fa;
            color: #495057;
            font-size: 0.8rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s;
            text-decoration: none;
            display: inline-block;
            min-height: 44px;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
        }

        .term-button:hover {
            border-color: #f5a623;
            background: #fff3cd;
            color: #856404;
        }

        .term-button.thank-you { border-color: #28a745; color: #155724; }
        .term-button.thank-you:hover { background: #d4edda; }

        .term-button.content { border-color: #007bff; color: #004085; }
        .term-button.content:hover { background: #cce7ff; }

        .term-button.serp { border-color: #dc3545; color: #721c24; }
        .term-button.serp:hover { background: #f8d7da; }

        /* Flow Arrows - Redesigned */
        .flow-arrow {
            display: none; /* Hide arrows on desktop */
            position: absolute;
            top: 370px;
            right: -35px;
            width: 70px;
            height: 40px;
            background: linear-gradient(135deg, #f5a623, #e0941f);
            border-radius: 25px;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.4rem;
            font-weight: 600;
            z-index: 10;
            box-shadow: 0 4px 15px rgba(245, 166, 35, 0.3);
            transition: all 0.3s ease;
        }

        .flow-arrow:before {
            content: "→";
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 300;
            font-size: 1.6rem;
        }

        .flow-arrow:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 20px rgba(245, 166, 35, 0.4);
        }

        .flow-stage:last-child .flow-arrow {
            display: none;
        }

        /* Desktop: Hide scroll hints */
        @media (min-width: 769px) {
            .scroll-hint {
                display: none !important;
            }
        }

        /* Mobile Responsive - Horizontal Swipe Experience */
        @media (max-width: 768px) {
            /* Mobile-specific adjustment for SERP iframe */
            .serp-iframe {
                transform: scale(0.43) !important;
                margin-top: -670px !important;
                height: 1300px !important;
            }
            
            // Force stage 1 to be visible first using order
            .flow-stage:nth-child(1) {
                order: 1;
                display: block !important;
                visibility: visible !important;
                opacity: 1 !important;
                min-width: 100vw !important;
                width: 100vw !important;
                left: 0 !important;
                position: relative !important;
                transform: translateX(0px) !important;
            }
            .flow-stage:nth-child(2) {
                order: 2;
            }
            .flow-stage:nth-child(3) {
                order: 3;
            }
            
            .flow-container {
                padding: 0;
                height: 100vh;
                display: flex;
                flex-direction: column;
                overflow: hidden;
            }
            
            .flow-stages {
                display: flex;
                flex-direction: row;
                flex-wrap: nowrap;
                overflow-x: auto;
                overflow-y: hidden;
                scroll-snap-type: x mandatory;
                -webkit-overflow-scrolling: touch;
                width: 100vw;
                height: calc(100vh - 120px);
                scroll-behavior: smooth;
            }
            
            .flow-stage {
                min-width: 100vw;
                width: 100vw;
                flex: 0 0 100vw;
                flex-shrink: 0;
                scroll-snap-align: start;
                height: 100%;
                overflow-y: auto;
            }
        }
        @media (max-width: 768px) {
            .flow-container {
                padding: 0px 0 0 0; /* Removed 20px top padding */
                height: 100vh;
                display: flex;
                flex-direction: column;
                overflow: hidden;
            }
            
            .flow-header {
                margin-bottom: 20px;
                padding: 0 20px;
                flex-shrink: 0;
            }
            
            .flow-title {
                font-size: 1.8rem;
            }
            
            .flow-subtitle {
                font-size: 1rem;
                padding: 0;
            }
            
            /* Show scroll hints on mobile for stages 1 and 2 */
            .flow-stage:nth-child(1) .scroll-hint,
            .flow-stage:nth-child(2) .scroll-hint {
                display: none; /* Hide the old arrow hints */
            }
            
            .flow-stage:nth-child(3) .scroll-hint {
                display: none !important;
            }
            
            /* Horizontal scroll container - FIXED */
            .flow-stages {
                display: flex !important;
                flex-direction: row !important;
                flex-wrap: nowrap !important;
                overflow-x: scroll !important;
                overflow-y: hidden !important;
                scroll-snap-type: x mandatory !important;
                -webkit-overflow-scrolling: touch !important;
                width: 100vw !important;
                height: calc(100vh - 80px) !important; /* Reduced from 120px to give more space */
                scroll-behavior: smooth !important;
                /* Hardware acceleration for smoother scrolling */
                transform: translateZ(0) !important;
                will-change: scroll-position !important;
                /* Highlight scroll container */
                border-top: 3px solid #f5a623 !important;
                border-bottom: 3px solid #f5a623 !important;
                touch-action: pan-x pan-y !important; /* Allow both horizontal and vertical panning */
            }
            
            .flow-stage {
                min-width: 100vw !important;
                width: 100vw !important;
                max-width: 100vw !important;
                padding: 10px 20px 20px 20px !important; /* Reduced top padding */
                margin: 0 !important;
                flex-shrink: 0 !important;
                flex-grow: 0 !important;
                scroll-snap-align: start !important;
                display: flex !important;
                flex-direction: column !important;
                height: 100%;
                box-sizing: border-box;
                background: white;
                border-radius: 0;
                box-shadow: none;
                border-right: 3px solid #f5a623;
                overflow-y: auto !important; /* Ensure vertical scrolling within each stage */
                -webkit-overflow-scrolling: touch !important; /* Smooth scrolling on iOS */
                scroll-behavior: smooth !important; /* Smooth scrolling behavior */
                position: relative;
            }
            
            .stage-header {
                margin-bottom: 10px; /* Keep same margin below */
                flex-shrink: 0;
                min-height: 40px; /* Slightly reduced */
                display: flex;
                flex-direction: column;
                justify-content: center; /* Center vertically */
                align-items: center;
                padding: 8px 0 15px 0; /* Less space above, more below */
            }
            
            .stage-title {
                font-size: 1.2rem;
                margin-bottom: 0px;
                min-height: 25px;
                display: flex;
                align-items: center;
                justify-content: center;
                text-align: center;
                line-height: 1.2;
            }

            /* Larger titles for stages 2 and 3 on mobile */
            .flow-stage:nth-child(2) .stage-title,
            .flow-stage:nth-child(3) .stage-title {
                font-size: 1.4rem; /* Increased from 1.2rem for better readability */
                font-weight: 700;
                white-space: nowrap; /* Prevent line breaks */
                overflow: hidden;
                text-overflow: ellipsis; /* Add ... if text still too long */
                max-width: 100%; /* Ensure it doesn't exceed container */
                letter-spacing: -0.4px; /* Slightly tighter spacing to help fit */
            }
            
            .stage-description {
                display: none; /* Hide all descriptions on mobile too */
            }
            
            .phone-frame {
                width: 300px;
                height: 650px;
                padding: 8px;
                margin: 5px auto 15px auto; /* Added bottom margin */
                flex-shrink: 0;
                position: relative;
                top: 0;
            }
            
            .page-iframe {
                width: 430px;
                height: 932px;
                transform: scale(0.69);;
                transform-origin: center center;
                position: absolute;
                top: 50%;
                left: 50%;
                margin-left: -215px;
                margin-top: -466px;
            }
            
            /* Remove vertical flow arrows, add horizontal indicators */
            .flow-arrow {
                display: none;
            }
            
            .key-terms {
                margin-top: 10px; /* Reduced */
                flex: 0 0 auto; /* Don't stretch, size to content */
                overflow-y: visible; /* Remove scroll constraint */
                min-height: auto; /* Remove min-height constraint */
                padding-bottom: 60px; /* Add padding to account for scroll indicators */
                -webkit-overflow-scrolling: touch; /* Smooth scrolling on iOS */
            }
            
            .section-title {
                font-size: 1.5rem;
                margin-bottom: 8px;
            }
            
            .terms-grid {
                gap: 4px;
                margin-bottom: 10px;
            }
            
            .term-button {
                padding: 4px 8px;
                font-size: 0.7rem;
            }
            
            /* Mobile Scrolling Hints - Stage-specific */
            .scroll-hint {
                position: absolute;
                top: 45%; /* Moved up to middle of phone frame */
                right: 20px;
                transform: translateY(-50%);
                background: rgba(245, 166, 35, 0.9);
                color: white;
                padding: 8px 12px;
                border-radius: 25px;
                font-size: 1.2rem;
                font-weight: 300;
                z-index: 1000;
                animation: slideHint 3s ease-in-out infinite;
                box-shadow: 0 4px 12px rgba(0,0,0,0.3);
                cursor: pointer;
                user-select: none;
                -webkit-user-select: none;
                -webkit-tap-highlight-color: transparent;
                transition: all 0.3s ease;
                display: none; /* Hide on desktop */
            }
            
            .scroll-hint:hover {
                background: rgba(245, 166, 35, 1);
                transform: translateY(-50%) scale(1.1);
            }
            
            .scroll-hint:active {
                transform: translateY(-50%) scale(0.95);
                background: rgba(224, 148, 31, 1);
            }
            
            .scroll-hint.left {
                left: 20px;
                right: auto;
            }
            
            .scroll-hint.right {
                right: 20px;
                left: auto;
            }
            
            @keyframes slideHint {
                0%, 100% { opacity: 0.7; transform: translateY(-50%) translateX(0); }
                50% { opacity: 1; transform: translateY(-50%) translateX(10px); }
            }
            
            /* Hide hints after user starts scrolling */
            .scroll-hint.hidden {
                display: none;
            }
            
            /* Hide scroll hints on all stages for desktop */
            .flow-stage .scroll-hint {
                display: none !important;
            }
            
            .live-link {
                padding: 6px 12px;
                font-size: 0.75rem;
            }
            
            /* Scroll indicators */
            .scroll-indicators {
                display: flex;
                justify-content: center;
                gap: 8px;
                position: fixed;
                bottom: 10px; /* Reduced from 20px */
                left: 50%;
                transform: translateX(-50%);
                background: rgba(255,255,255,0.95);
                border-radius: 20px;
                padding: 8px 16px; /* Reduced padding */
                backdrop-filter: blur(10px);
                box-shadow: 0 4px 20px rgba(0,0,0,0.1);
                z-index: 1000;
            }
            
            .scroll-dot {
                width: 10px;
                height: 10px;
                border-radius: 50%;
                background: #ccc;
                transition: all 0.3s ease;
                cursor: pointer;
                position: relative;
                z-index: 1001;
            }
            
            .scroll-dot.active {
                background: #f5a623;
                transform: scale(1.2);
            }
            
            .scroll-dot:hover {
                background: #f5a623;
                opacity: 0.7;
            }
        }

        /* Extra small phones */
        @media (max-width: 480px) {
            .serp-iframe {
                transform: scale(0.41) !important;
                margin-top: -690px !important;
                height: 1400px !important;
            }
            
            .flow-title {
                font-size: 1.6rem;
            }
            
            .flow-subtitle {
                font-size: 0.9rem;
            }
            
            .phone-frame {
                width: 280px;
                height: 600px;
            }
            
            .page-iframe {
                transform: scale(0.62);;
            }
            
            .flow-stage {
                padding: 5px 10px 80px 10px; /* Increased bottom padding from 15px to 80px for scroll indicators */
            }
            
            .term-button {
                padding: 4px 6px;
                font-size: 0.65rem;
            }
            
            /* Further reduce title size for very small phones */
            .flow-stage:nth-child(2) .stage-title,
            .flow-stage:nth-child(3) .stage-title {
                font-size: 1.15rem; /* Increased from 1.0rem, still fits on small phones */
                letter-spacing: -0.4px;
            }
        }

        /* Specific optimizations for iPhone 12 Pro and similar sizes (390px width) */
        @media (max-width: 390px) and (min-width: 375px) {
            .flow-stage:nth-child(2) .stage-title,
            .flow-stage:nth-child(3) .stage-title {
                font-size: 1.3rem; /* Increased from 1.1rem for iPhone 12 Pro */
                letter-spacing: -0.6px; /* Tighter letter spacing to help fit */
            }
        }

        /* Linktree Mockup Styles - Exact match to screenshot */
        .linktree-mockup {
            background: linear-gradient(180deg, #7dd3fc 0%, #06b6d4 100%) !important;
            padding: 0 !important;
            overflow-y: auto !important;
            height: 100% !important;
            display: flex !important;
            flex-direction: column !important;
            width: 100% !important;
            position: relative !important;
        }

        .linktree-container {
            padding: 40px 30px 60px;
            display: flex;
            flex-direction: column;
            align-items: center;
            height: 100%;
            max-width: 300px;
            margin: 0 auto;
        }

        .linktree-header {
            text-align: center;
            margin-bottom: 32px;
            width: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .linktree-avatar {
            width: 80px;
            height: 80px;
            margin: 0 auto 20px auto;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .linktree-name {
            color: #1a1a1a !important;
            font-size: 22px !important;
            font-weight: bold !important;
            margin: 0 0 12px 0 !important;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif !important;
            text-align: center !important;
            line-height: 1.2 !important;
        }

        .linktree-bio {
            color: #4a5568 !important;
            font-size: 15px !important;
            margin: 0 !important;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif !important;
            font-weight: 400 !important;
            line-height: 1.4 !important;
            text-align: center !important;
            max-width: 250px !important;
        }

        .linktree-links {
            width: 100%;
            display: flex;
            flex-direction: column;
            gap: 16px;
            margin-bottom: 24px;
            max-width: 280px;
        }

        .linktree-link {
            background: #f7fafc !important;
            color: #2d3748 !important;
            text-decoration: none !important;
            padding: 14px 18px !important;
            border-radius: 25px !important;
            text-align: left !important;
            font-weight: 600 !important;
            font-size: 14px !important;
            transition: all 0.2s ease !important;
            border: 1px solid #e2e8f0 !important;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif !important;
            display: flex !important;
            align-items: center !important;
            justify-content: space-between !important;
            min-height: 48px !important;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1) !important;
        }

        .linktree-link:hover {
            transform: translateY(-1px) !important;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15) !important;
            background: #ffffff !important;
        }

        .content-page-link:hover {
            transform: translateY(-2px) !important;
            box-shadow: 0 6px 20px rgba(245, 166, 35, 0.4) !important;
        }

        /* Section headers styling */
        .section-header {
            background: #4a90e2 !important;
            color: white !important;
            padding: 10px 20px !important;
            border-radius: 25px !important;
            text-align: center !important;
            font-weight: bold !important;
            font-size: 13px !important;
            margin: 8px 0 !important;
            width: 100% !important;
            box-sizing: border-box !important;
        }

        .social-icon svg {
            width: 20px;
            height: 20px;
        }

        /* Pulse animation for click indicator */
        @keyframes pulse {
            0%, 100% { opacity: 0.8; transform: scale(1); }
            50% { opacity: 1; transform: scale(1.05); }
        }
    </style>
</head>
<body>
    <div class="flow-container">

        <!-- Page Title (Desktop Only) -->
        <div class="page-title">
            <h1>Flow Overview</h1>
            <a href="index.html" class="path-button">Path</a>
        </div>

        <div class="flow-stages">
            <!-- Stage 1: Thank You Page -->
            <div class="flow-stage">
                <!-- Mobile Scrolling Hint -->
                <div class="scroll-hint right">→</div>
                
                <div class="stage-header">
                    <h2 class="stage-title" style="display: none;">Stage 1 Options</h2> <!-- Hidden title -->
                    
                    <!-- Stage 1 Toggle Buttons -->
                    <div class="stage-toggle-buttons">
                        <button class="toggle-btn active" onclick="showSocial()">Socials</button>
                        <button class="toggle-btn" onclick="showThankYou()">Thank You Page</button>
                        <button class="toggle-btn" onclick="showDisqualify()">Disqualifying Offer</button>
                        <button class="toggle-btn" onclick="showLinktree()">Linktree</button>
                    </div>
                </div>

                <div class="phone-frame">
                    <div class="phone-screen">
                        <!-- Main iframe for Thank You and Disqualify pages -->
                        <iframe 
                            id="stage1-iframe"
                            src="about:blank" 
                            class="page-iframe"
                            title="Stage 1 Content"
                            style="display: none;">
                        </iframe>
                        
                        <!-- Social mockup div (shows by default) -->
                        <div id="stage1-social-div" class="page-iframe social-ad-mockup" style="display: block;">
                            <!-- Facebook Ad Mockup -->
                            <div class="facebook-ad">
                                <div class="fb-header">
                                    <div class="fb-profile">
                                        <div class="fb-avatar">
                                            <img src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNTAiIGhlaWdodD0iNTAiIHZpZXdCb3g9IjAgMCA1MCA1MCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGRlZnM+CjxsaW5lYXJHcmFkaWVudCBpZD0iYmciIHgxPSIwJSIgeTE9IjAlIiB4Mj0iMTAwJSIgeTI9IjEwMCUiPgo8c3RvcCBvZmZzZXQ9IjAlIiBzdHlsZT0ic3RvcC1jb2xvcjojNENBRjUwIi8+CjxzdG9wIG9mZnNldD0iNTAlIiBzdHlsZT0ic3RvcC1jb2xvcjojZjVhNjIzIi8+CjxzdG9wIG9mZnNldD0iMTAwJSIgc3R5bGU9InN0b3AtY29sb3I6IzRhOTBlMiIvPgo8L2xpbmVhckdyYWRpZW50Pgo8L2RlZnM+CjxjaXJjbGUgY3g9IjI1IiBjeT0iMjUiIHI9IjI1IiBmaWxsPSJ1cmwoI2JnKSIvPgo8Y2lyY2xlIGN4PSIzOCIgY3k9IjEyIiByPSI0IiBmaWxsPSIjRkZENzAwIi8+Cjx0ZXh0IHg9IjI1IiB5PSIzMiIgZm9udC1mYW1pbHk9IkFyaWFsIiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZmlsbD0id2hpdGUiIHRleHQtYW5jaG9yPSJtaWRkbGUiPlNGPC90ZXh0Pgo8L3N2Zz4=" alt="SolarFlow" />
                                        </div>
                                        <div class="fb-info">
                                            <div class="fb-name">SolarFlow</div>
                                            <div class="fb-sponsored">Sponsored</div>
                                            <div class="fb-library-id">Library ID: 418984130123537</div>
                                        </div>
                                    </div>
                                    <div class="fb-menu">⋯</div>
                                </div>
                                
                                <div class="fb-content">
                                    <p class="fb-text">Thinking about solar for your home? Learn about the potential benefits and see if solar might be a good fit for your situation. Every home is different - find out what options could work for you.</p>
                                </div>
                                
                                <div class="fb-media">
                                    <div class="fb-video-container">
                                        <div class="fb-video-placeholder">
                                            <div class="fb-video-overlay">
                                                <div class="fb-play-button">▶</div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="fb-cta">
                                    <div class="fb-cta-text">
                                        <div class="fb-url">HTTPS://WWW.SOLARFLOW.XYZ/</div>
                                        <div class="fb-headline">Learn How Solar Energy Reduces Costs and Boosts Home Value</div>
                                        <div class="fb-description">Get information and see what might work</div>
                                    </div>
                                    <button class="fb-learn-more">Learn More</button>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Linktree mockup div (hidden by default) -->
<div id="stage1-linktree-div" class="page-iframe" style="display: none !important; visibility: hidden !important; width: 430px; height: 932px; border: none; border-radius: 27px; transform: scale(0.725); transform-origin: center center; position: absolute; top: 50%; left: 50%; margin-left: -215px; margin-top: -466px;" 
                             onclick="handleLinktreeClick()" 
                             title="Click to open Nation.com solar article">
                            <img src="Linktree-pic.png" 
                                 alt="Solar Linktree Screenshot" 
                                 style="width: 100%; height: 100%; object-fit: cover; object-position: center center; pointer-events: none;"
                                 onerror="this.style.display='none'; this.parentElement.innerHTML='<div style=\'padding: 20px; text-align: center; color: #666;\'>Image not found: Linktree-pic.png</div>'" />
                        </div>
                    </div>
                </div>

                <div class="key-terms">
                    <h3 class="section-title" id="stage1-title" style="margin-bottom: 15px;">Social Advertisement</h3>
                    
                    <div class="option-description" id="stage1-description" style="background: #f8f9fa; padding: 15px; border-radius: 8px; border-left: 4px solid #f5a623; margin-bottom: 15px;">
                        <p style="margin: 0; color: #555; line-height: 1.6;">Learn More button links out to content page.</p>
                    </div>
                </div>
            </div>

            <!-- Stage 2: Content Page -->
            <div class="flow-stage">
                <!-- Mobile Scrolling Hint -->
                <div class="scroll-hint right">→</div>
                
                <div class="stage-header">
                    <h2 class="stage-title">Content Page with Keyword Block</h2>
                    <p class="stage-description">
                        User is shown the Keyword Block that contains search terms on a content page.
                    </p>
                </div>

                <div class="phone-frame">
                    <div class="phone-screen">
                        <iframe 
                            src="rsoc-page.html?hideGlossary=true&hideDevNav=true" 
                            class="page-iframe"
                            title="RSOC Content Page">
                        </iframe>
                    </div>
                </div>

                <div class="key-terms">
                    <h3 class="section-title">Keyword Block</h3>
                    
                    <!-- Description above the block -->
                    <div class="option-description" style="background: #f8f9fa; padding: 15px; border-radius: 8px; border-left: 4px solid #5865f2; margin-bottom: 15px;">
                        <p style="margin: 0; color: #555; line-height: 1.6;">An iframe containing search terms (ForceKeys). Clicks on one of these search terms is shown on the next page, the SERP. These are the related searches on content: RSOC.</p>
                    </div>
                    
                    <!-- Keyword blocks without container - CENTERED -->
                    <div style="display: flex; flex-direction: column; align-items: center;">
                        <div class="keyword-block-header" style="font-size: 0.7rem; color: #666; font-weight: normal; margin-bottom: 8px; width: 280px; text-align: left;">Related searches</div>
                        <div class="keyword-search-terms" style="display: flex; flex-direction: column; gap: 6px; width: 280px;">
                            <div class="keyword-search-term" style="height: 40px; width: 100%; display: flex; background: #5865f2; border-radius: 4px; padding: 8px 12px; cursor: pointer; transition: all 0.3s ease; align-items: center; justify-content: flex-start; font-size: 0.8rem; font-weight: 600; color: white; border: none; font-family: 'Source Serif Pro', Book Antiqua, Palatino, serif;" 
                                 onmouseover="this.style.background='#f5a623'; this.style.transform='translateY(-1px)'" 
                                 onmouseout="this.style.background='#5865f2'; this.style.transform='translateY(0)'">
                                <span style="margin-right: 8px; font-size: 1.1rem;">›</span>
                                <span style="flex: 1; text-align: left;">Solar Panel Installation</span>
                                <span style="margin-left: auto; font-size: 1.1rem;">›</span>
                            </div>
                            <div class="keyword-search-term" style="height: 40px; width: 100%; display: flex; background: #5865f2; border-radius: 4px; padding: 8px 12px; cursor: pointer; transition: all 0.3s ease; align-items: center; justify-content: flex-start; font-size: 0.8rem; font-weight: 600; color: white; border: none; font-family: 'Source Serif Pro', Book Antiqua, Palatino, serif;" 
                                 onmouseover="this.style.background='#f5a623'; this.style.transform='translateY(-1px)'" 
                                 onmouseout="this.style.background='#5865f2'; this.style.transform='translateY(0)'">
                                <span style="margin-right: 8px; font-size: 1.1rem;">›</span>
                                <span style="flex: 1; text-align: left;">Residential Solar Panels Near Me</span>
                                <span style="margin-left: auto; font-size: 1.1rem;">›</span>
                            </div>
                            <div class="keyword-search-term" style="height: 40px; width: 100%; display: flex; background: #5865f2; border-radius: 4px; padding: 8px 12px; cursor: pointer; transition: all 0.3s ease; align-items: center; justify-content: flex-start; font-size: 0.8rem; font-weight: 600; color: white; border: none; font-family: 'Source Serif Pro', Book Antiqua, Palatino, serif;" 
                                 onmouseover="this.style.background='#f5a623'; this.style.transform='translateY(-1px)'" 
                                 onmouseout="this.style.background='#5865f2'; this.style.transform='translateY(0)'">
                                <span style="margin-right: 8px; font-size: 1.1rem;">›</span>
                                <span style="flex: 1; text-align: left;">Solar Panel Energy Savings</span>
                                <span style="margin-left: auto; font-size: 1.1rem;">›</span>
                            </div>
                        </div>
                    </div>

                    <!-- ForceKeys Section -->
                    <div style="margin-top: 25px;">
                        <h3 class="section-title">ForceKeys</h3>
                        <div class="option-description" style="background: #f8f9fa; padding: 15px; border-radius: 8px; border-left: 4px solid #0693e3; margin-bottom: 15px;">
                            <p style="margin: 0; color: #555; line-height: 1.6;">Optimized search terms / keywords. These are passed in the URL and are requested to be shown by Google.</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Stage 3: SERP Page -->
            <div class="flow-stage">
                <div class="stage-header">
                    <h2 class="stage-title">SERP (Search Engine Results Page)</h2>
                    <p class="stage-description">
                        Search Engine Results Page with monetized clicks to advertiser with "Visit Website" button
                    </p>
                </div>

                <div class="phone-frame">
                    <div class="phone-screen">
                        <iframe 
                            src="serp.html?hideDevNav=true" 
                            class="page-iframe"
                            title="Nation.com SERP">
                        </iframe>
                    </div>
                </div>

                <div class="key-terms">
                    <h3 class="section-title">Monetization Event</h3>
                    
                    <!-- Description below the button -->
                    <div class="option-description" style="background: #f8f9fa; padding: 15px; border-radius: 8px; border-left: 4px solid #0e50c4; margin-bottom: 15px;">
                        <p style="margin: 0; color: #555; line-height: 1.6;">A user clicks on the <button class="serp-visit-btn" style="-webkit-text-size-adjust: 100%; font-family: arial, sans-serif; text-decoration: none; text-transform: none; display: inline-flex; box-sizing: border-box; overflow: hidden; font-weight: 700; background-color: #0e50c4; border-radius: 20px; border: 2px solid #dadce0; font-size: 14px; line-height: 20px; max-height: 32px; margin: 0 4px; padding: 6px 12px; color: #ffffff; flex-direction: row; justify-content: center; align-items: center; cursor: pointer; transition: all 0.1s ease; vertical-align: middle;" onmouseover="this.style.backgroundColor='#1a5bcd'" onmouseout="this.style.backgroundColor='#0e50c4'">Visit Website</button> button. This is the monetization event where we calculate RPC. User is taken to the advertiser's page.</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Mobile Scroll Indicators -->
    <div class="scroll-indicators" id="scrollIndicators">
        <div class="scroll-dot active" data-stage="0" onclick="scrollToStage(0)"></div>
        <div class="scroll-dot" data-stage="1" onclick="scrollToStage(1)"></div>
        <div class="scroll-dot" data-stage="2" onclick="scrollToStage(2)"></div>
    </div>

    <script>
        // Helper function to scroll to a specific stage
        function scrollToStage(stageIndex) {
            const flowStages = document.querySelector('.flow-stages');
            const scrollDots = document.querySelectorAll('.scroll-dot');
            
            if (flowStages) {
                // Calculate position
                const targetScroll = window.innerWidth * stageIndex;
                
                // Scroll to target stage
                flowStages.scrollTo({
                    left: targetScroll,
                    behavior: 'smooth'
                });
                
                // Force scroll position after animation
                setTimeout(() => {
                    flowStages.scrollLeft = targetScroll;
                    
                    // Update active state on dots
                    scrollDots.forEach((dot, i) => {
                        dot.classList.toggle('active', i === stageIndex);
                    });
                    
                    console.log(`Scrolled to stage ${stageIndex + 1}`);
                }, 300);
            }
        }
        // Make sure stages are scrollable on mobile
        window.addEventListener('load', function() {
            // Force scrollable container on mobile
            if (window.innerWidth <= 768) {
                const flowStages = document.querySelector('.flow-stages');
                
                if (flowStages) {
                    // Force scrollability with inline styles
                    flowStages.style.display = 'flex';
                    flowStages.style.flexDirection = 'row';
                    flowStages.style.flexWrap = 'nowrap';
                    flowStages.style.overflowX = 'scroll';
                    flowStages.style.overflowY = 'hidden';
                    flowStages.style.scrollSnapType = 'x mandatory';
                    flowStages.style.WebkitOverflowScrolling = 'touch';
                    flowStages.style.width = '100vw';
                    
                    // Set each stage to be full width
                    const stages = flowStages.querySelectorAll('.flow-stage');
                    stages.forEach(stage => {
                        stage.style.minWidth = '100vw';
                        stage.style.width = '100vw';
                        stage.style.flex = '0 0 100vw';
                        stage.style.flexShrink = '0';
                    });
                    
                    // CRITICAL: Force reset to stage 1
                    setTimeout(() => {
                        console.log("Forcing scroll to stage 1");
                        flowStages.scrollLeft = 0;
                        
                        // HOTFIX: Force scroll to negative position to compensate
                        setTimeout(() => {
                            if (flowStages.scrollLeft !== 0) {
                                flowStages.scrollLeft = -window.innerWidth;
                                setTimeout(() => flowStages.scrollLeft = 0, 50);
                            }
                        }, 100);
                        
                        // Update scroll dot indicators
                        const scrollDots = document.querySelectorAll('.scroll-dot');
                        scrollDots.forEach((dot, index) => {
                            dot.classList.toggle('active', index === 0);
                        });
                        
                        // Set up scroll listener
                        flowStages.addEventListener('scroll', function() {
                            const scrollLeft = flowStages.scrollLeft;
                            const stageWidth = flowStages.clientWidth;
                            const currentStage = Math.round(scrollLeft / stageWidth);
                            
                            console.log(`Scrolled to position ${scrollLeft}, stage ${currentStage}`);
                            
                            scrollDots.forEach((dot, index) => {
                                dot.classList.toggle('active', index === currentStage);
                            });
                        });
                    }, 200);
                    
                    // Add stronger scroll reset on dots
                    const scrollDots = document.querySelectorAll('.scroll-dot');
                    scrollDots.forEach((dot, index) => {
                        dot.addEventListener('click', function() {
                            const targetScroll = index * window.innerWidth;
                            console.log(`Dot clicked: ${index}, scrolling to ${targetScroll}`);
                            flowStages.scrollTo({
                                left: targetScroll,
                                behavior: 'smooth'
                            });
                            
                            // Update active state
                            scrollDots.forEach((d, i) => {
                                d.classList.toggle('active', i === index);
                            });
                        });
                    });
                    
                    console.log("Mobile scrolling enabled - refresh to see changes");
                }
            }
        });
        
        // THREE SIMPLE FUNCTIONS - GLOBAL SCOPE
        function showSocial() {
            document.getElementById('stage1-iframe').style.display = 'none';
            document.getElementById('stage1-social-div').style.display = 'block';
            
            // Update buttons
            document.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelector('[onclick="showSocial()"]').classList.add('active');
        }
        
        function showThankYou() {
            console.log('Showing thank you page');
            document.getElementById('stage1-social-div').style.display = 'none';
            document.getElementById('stage1-iframe').style.display = 'block';
            document.getElementById('stage1-iframe').src = 'flow.html?step=6&hideDevNav=true';
            
            // Update buttons
            document.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelector('[onclick="showThankYou()"]').classList.add('active');
        }
        
        function showDisqualify() {
            console.log('Showing disqualify page');
            document.getElementById('stage1-social-div').style.display = 'none';
            document.getElementById('stage1-iframe').style.display = 'block';
            document.getElementById('stage1-iframe').src = 'flow.html?step=4&autoSelect=mostly-shade&showPopup=true&hideDevNav=true';
            
            // Update buttons
            document.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelector('[onclick="showDisqualify()"]').classList.add('active');
        }

        // SUPER SIMPLE - Just switch what's in the iPhone frame - GLOBAL FUNCTION
        function loadStage1(version) {
            console.log(`🔴 BUTTON CLICKED! Switching to: ${version}`);
            alert(`Button clicked: ${version}`); // Visual confirmation
            
            const iframe = document.getElementById('stage1-iframe');
            const socialDiv = document.getElementById('stage1-social-div');
            
            console.log('iframe:', iframe);
            console.log('socialDiv:', socialDiv);
            
            // Update button colors
            document.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            
            if (version === 'social') {
                // Show social ad
                iframe.style.display = 'none';
                socialDiv.style.display = 'block';
                document.querySelector('[onclick="loadStage1(\'social\')"]').classList.add('active');
                console.log('✅ Showing social');
                
            } else if (version === 'thankyou') {
                // Show thank you page
                socialDiv.style.display = 'none';
                iframe.style.display = 'block';
                iframe.src = 'flow.html?step=6&hideDevNav=true';
                document.querySelector('[onclick="loadStage1(\'thankyou\')"]').classList.add('active');
                console.log('✅ Loading thank you page...');
                
            } else if (version === 'disqualify') {
                // Show disqualifying offer
                socialDiv.style.display = 'none';
                iframe.style.display = 'block';
                iframe.src = 'flow.html?step=4&autoSelect=mostly-shade&showPopup=true&hideDevNav=true';
                document.querySelector('[onclick="loadStage1(\'disqualify\')"]').classList.add('active');
                console.log('✅ Loading disqualify page...');
            }
        }

        // Log page load
        console.log('SolarFlow User Journey Overview loaded');
        console.log('All 3 stages embedded with live iframes in iPhone 14 Pro Max view');

        // Force mobile viewport and layout for iframes
        document.addEventListener('DOMContentLoaded', function() {
            console.log('🚀 Page loaded - Setting up Stage 1 functionality');
            
            // Debug: List all stage1 versions
            const allStage1Versions = document.querySelectorAll('.stage1-version');
            console.log(`Found ${allStage1Versions.length} stage1 versions:`);
            allStage1Versions.forEach((version, index) => {
                console.log(`- ${version.id} (${version.tagName}) - src: ${version.src || 'N/A'}`);
            });
            
            // Set up button event listeners immediately
            console.log('🔘 Setting up toggle button event listeners...');
            const toggleButtons = document.querySelectorAll('.toggle-btn');
            console.log(`Found ${toggleButtons.length} toggle buttons`);
            
            toggleButtons.forEach((button, index) => {
                const version = button.getAttribute('data-version');
                console.log(`Button ${index + 1}: "${button.textContent}" -> version: ${version}`);
                
                // Add click handler
                button.addEventListener('click', function(e) {
                    e.preventDefault();
                    e.stopPropagation();
                    
                    console.log(`🔘 BUTTON CLICKED: "${this.textContent}" -> ${version}`);
                    
                    if (version) {
                        switchStage1Version(version);
                    } else {
                        console.error(`No version found for button: ${this.textContent}`);
                    }
                });
                
                console.log(`✅ Event listener added to button ${index + 1}`);
            });
            
            // Ensure proper initial state
            setTimeout(() => {
                console.log('🔧 Setting initial state to social version');
                // Call showSocial directly
                showSocial();
            }, 100);
            
            const iframes = document.querySelectorAll('.page-iframe');
            
            iframes.forEach((iframe, index) => {
                // Set iframe to exact iPhone 14 Pro Max dimensions
                iframe.style.width = '430px';
                iframe.style.height = '932px';
                
                iframe.onload = function() {
                    console.log(`📱 Iframe ${index + 1} loaded: ${iframe.src}`);
                    try {
                        const iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
                        
                        // Set viewport to iPhone 14 Pro Max
                        let viewportMeta = iframeDoc.querySelector('meta[name="viewport"]');
                        if (!viewportMeta) {
                            viewportMeta = iframeDoc.createElement('meta');
                            viewportMeta.name = 'viewport';
                            iframeDoc.head.appendChild(viewportMeta);
                        }
                        viewportMeta.content = 'width=430, initial-scale=1.0, user-scalable=no';
                        
                        // Force mobile layout by setting window properties
                        if (iframe.contentWindow) {
                            // Override screen dimensions to trigger mobile CSS
                            Object.defineProperty(iframe.contentWindow.screen, 'width', { value: 430 });
                            Object.defineProperty(iframe.contentWindow.screen, 'height', { value: 932 });
                            
                            // Set window inner dimensions
                            Object.defineProperty(iframe.contentWindow, 'innerWidth', { value: 430 });
                            Object.defineProperty(iframe.contentWindow, 'innerHeight', { value: 932 });
                        }
                        
                        // Force body width to trigger mobile breakpoints
                        const html = iframeDoc.documentElement;
                        const body = iframeDoc.body;
                        
                        if (html) {
                            html.style.width = '430px';
                            html.style.maxWidth = '430px';
                        }
                        
                        if (body) {
                            body.style.width = '430px';
                            body.style.maxWidth = '430px';
                            body.style.overflow = 'auto';
                        }
                        
                        // Trigger resize event to activate mobile CSS
                        if (iframe.contentWindow) {
                            const resizeEvent = new iframe.contentWindow.Event('resize');
                            iframe.contentWindow.dispatchEvent(resizeEvent);
                        }
                        
                        console.log(`Mobile layout forced for iframe ${index + 1} (430x932)`);
                    } catch (e) {
                        console.log(`Cross-origin restriction for iframe ${index + 1}, using CSS scaling fallback`);
                    }
                };
                
                iframe.onerror = function() {
                    console.log(`Iframe ${index + 1} failed to load`);
                };
            });
        });

        // Add click tracking for toggle buttons - ENHANCED
        document.querySelectorAll('.toggle-btn').forEach(button => {
            button.addEventListener('click', function(e) {
                e.preventDefault();
                e.stopPropagation();
                
                const buttonText = this.textContent.trim();
                const version = this.getAttribute('data-version');
                
                console.log(`🔘 Toggle button clicked: "${buttonText}"`);
                console.log(`🎯 Data version: ${version}`);
                
                if (version) {
                    console.log(`🎯 Switching to version: ${version}`);
                    switchStage1Version(version);
                    
                    // Reset user interaction for auto-rotation
                    if (typeof resetStage1UserInteraction === 'function') {
                        resetStage1UserInteraction();
                    }
                } else {
                    console.error(`❌ No data-version found on button: ${buttonText}`);
                }
            });
        });

        // Mobile stage advancement function
        function advanceToStage(targetStage) {
            if (window.innerWidth > 768) return; // Only work on mobile
            
            const flowStages = document.querySelector('.flow-stages');
            const scrollDots = document.querySelectorAll('.scroll-dot');
            
            console.log(`📱 Mobile navigation: advancing to stage ${targetStage + 1}`);
            
            // Calculate scroll position for target stage
            const targetScroll = window.innerWidth * targetStage;
            
            // Smooth scroll to target stage
            flowStages.scrollTo({
                left: targetScroll,
                behavior: 'smooth'
            });
            
            // Update active dot
            scrollDots.forEach((dot, index) => {
                dot.classList.toggle('active', index === targetStage);
            });
            
            // Visual feedback
            const clickedOverlay = event.target;
            clickedOverlay.style.background = 'rgba(245, 166, 35, 0.6)';
            clickedOverlay.textContent = '✓';
            
            setTimeout(() => {
                clickedOverlay.style.background = '';
                clickedOverlay.textContent = 'Next →';
            }, 1000);
        }

        // Mobile scrolling hints
        function initScrollHints() {
            if (window.innerWidth > 768) return;
            
            console.log('🎯 Initializing mobile scroll hints');
            
            const flowStages = document.querySelector('.flow-stages');
            const scrollHints = document.querySelectorAll('.scroll-hint');
            let hasScrolled = false;
            
            console.log(`Found ${scrollHints.length} scroll hints`);
            
            // Make scroll hints clickable to advance stages
            scrollHints.forEach((hint, index) => {
                console.log(`Setting up click handler for hint ${index + 1}`);
                
                const clickHandler = function(e) {
                    e.preventDefault();
                    e.stopPropagation();
                    
                    console.log(`📱 Scroll hint clicked on stage ${index + 1}`);
                    
                    // Calculate next stage (current index + 1, max 2 for 3 stages total)
                    const nextStage = Math.min(index + 1, 2);
                    const targetScroll = window.innerWidth * nextStage;
                    
                    console.log(`Moving from stage ${index + 1} to stage ${nextStage + 1}`);
                    console.log(`Target scroll position: ${targetScroll}px`);
                    console.log(`Window width: ${window.innerWidth}px`);
                    
                    // Smooth scroll to next stage
                    flowStages.scrollTo({
                        left: targetScroll,
                        behavior: 'smooth'
                    });
                    
                    // Also set directly as backup
                    setTimeout(() => {
                        flowStages.scrollLeft = targetScroll;
                        console.log(`Backup scroll set to: ${targetScroll}px`);
                    }, 100);
                    
                    // Update scroll dots
                    const scrollDots = document.querySelectorAll('.scroll-dot');
                    scrollDots.forEach((dot, dotIndex) => {
                        dot.classList.toggle('active', dotIndex === nextStage);
                    });
                    
                    // Visual feedback
                    hint.style.background = 'rgba(76, 175, 80, 0.9)';
                    hint.textContent = '✓';
                    
                    setTimeout(() => {
                        hint.style.background = 'rgba(245, 166, 35, 0.9)';
                        hint.textContent = '→';
                    }, 1000);
                    
                    // Hide all hints after first click
                    hasScrolled = true;
                    setTimeout(() => {
                        scrollHints.forEach(h => h.classList.add('hidden'));
                    }, 1500);
                };
                
                // Add multiple event listeners for better compatibility
                hint.addEventListener('click', clickHandler);
                hint.addEventListener('touchend', clickHandler);
                
                // Add touch feedback
                hint.addEventListener('touchstart', function(e) {
                    e.preventDefault();
                    console.log(`Touch start on hint ${index + 1}`);
                    hint.style.background = 'rgba(224, 148, 31, 1)';
                    hint.style.transform = 'translateY(-50%) scale(0.95)';
                });
                
                // Reset touch feedback
                hint.addEventListener('touchcancel', function() {
                    hint.style.background = 'rgba(245, 166, 35, 0.9)';
                    hint.style.transform = 'translateY(-50%) scale(1)';
                });
                
                console.log(`✅ Event listeners attached to hint ${index + 1}`);
            });
            
            // Hide hints after user scrolls manually
            flowStages.addEventListener('scroll', function() {
                if (!hasScrolled) {
                    hasScrolled = true;
                    console.log('Manual scroll detected, hiding hints');
                    scrollHints.forEach(hint => hint.classList.add('hidden'));
                }
            });
            
            // Auto-hide hints after 8 seconds
            setTimeout(() => {
                if (!hasScrolled) {
                    console.log('Auto-hiding hints after 8 seconds');
                    scrollHints.forEach(hint => hint.classList.add('hidden'));
                }
            }, 8000);
            
            console.log('✅ Mobile scroll hints initialized');
        }

        // Conference mode toggle
        function toggleConferenceMode() {
            const mainNav = document.querySelector('.main-nav');
            const conferenceToggle = document.querySelector('.conference-toggle');
            
            if (mainNav.style.display === 'none') {
                // Exit conference mode
                mainNav.style.display = 'block';
                conferenceToggle.textContent = '📱 Conference Mode';
                console.log('Conference mode OFF');
            } else {
                // Enter conference mode
                mainNav.style.display = 'none';
                conferenceToggle.textContent = '🔙 Exit Conference';  
                console.log('Conference mode ON - Main nav hidden for clean presentation');
            }
        }

        function toggleNavigation() {
            const mainNav = document.querySelector('.main-nav');
            const navToggle = document.querySelector('.nav-toggle');
            const navRestore = document.querySelector('.nav-restore');
            
            if (mainNav.style.display === 'none') {
                // Show navigation
                mainNav.style.display = 'block';
                navRestore.style.display = 'none';
                console.log('Navigation shown');
            } else {
                // Hide navigation
                mainNav.style.display = 'none';
                navRestore.style.display = 'block';
                console.log('Navigation hidden');
            }
        }

        function hideNavigation() {
            const mainNav = document.querySelector('.main-nav');
            const navClose = document.querySelector('.nav-close');
            const navRestore = document.querySelector('.nav-restore');
            
            mainNav.style.display = 'none';
            navClose.style.display = 'none';
            navRestore.style.display = 'block';
            console.log('Navigation hidden via X button');
        }

        function showNavigation() {
            const mainNav = document.querySelector('.main-nav');
            const navClose = document.querySelector('.nav-close');
            const navRestore = document.querySelector('.nav-restore');
            
            mainNav.style.display = 'block';
            navClose.style.display = 'flex';
            navRestore.style.display = 'none';
            console.log('Navigation shown via restore button');
        }

        // Removed old dev nav toggle function - no longer needed

        // Function to update Stage 1 dynamic section based on version
        function updateStage1SectionFromVersion(version) {
            let title = '';
            let description = '';
            
            switch(version) {
                case 'thankyou':
                    title = 'Thank You Page';
                    description = 'One option to place content articles within the flow. Can be slotted in to any part of the flow on any vertical.';
                    break;
                case 'disqualify':
                    title = 'Disqualifying Offer';
                    description = 'User can be shown a link to a content article on any vertical if they do not qualify for an offer.';
                    break;
                case 'social':
                    title = 'Socials';
                    description = 'Learn More button links out to content page.';
                    break;
                default:
                    return; // Don\'t show section if unknown version
            }
            
            updateStage1Section(title, description);
        }

        // Mobile horizontal scroll management - FIXED VERSION
        function initMobileScroll() {
            console.log('=== INIT MOBILE SCROLL ===');
            console.log(`Window width: ${window.innerWidth}px`);
            console.log(`Should be mobile: ${window.innerWidth <= 768}`);
            
            const flowStages = document.querySelector('.flow-stages');
            const scrollDots = document.querySelectorAll('.scroll-dot');
            const scrollIndicators = document.getElementById('scrollIndicators');
            
            if (!flowStages) {
                console.error('Flow stages container not found!');
                return;
            }
            
            // ALWAYS show debug button on mobile (even if width check fails)
            const isMobile = window.innerWidth <= 768;
            console.log(`Is mobile: ${isMobile}`);
            
            if (isMobile) {
                // Show scroll indicators
                if (scrollIndicators) {
                    scrollIndicators.style.display = 'flex';
                    console.log('Scroll indicators shown');
                }
                
                // Force mobile layout with JavaScript - FIXED CONTAINER WIDTH
                const viewportWidth = window.innerWidth;
                const totalContentWidth = viewportWidth * 3; // 3 stages
                
                flowStages.style.cssText = `
                    display: flex !important;
                    flex-direction: row !important;
                    flex-wrap: nowrap !important;
                    overflow-x: scroll !important;
                    overflow-y: hidden !important;
                    scroll-snap-type: x mandatory !important;
                    -webkit-overflow-scrolling: touch !important;
                    width: ${viewportWidth}px !important;
                    max-width: ${viewportWidth}px !important;
                    height: calc(100vh - 120px) !important;
                    cursor: grab !important;
                    position: relative !important;
                    box-sizing: border-box !important;
                `;
                
                console.log(`🔧 FIXED: Container constrained to ${viewportWidth}px, content is ${totalContentWidth}px`);
                
                // Force reflow
                flowStages.offsetWidth;
                
                // Add drag scrolling for desktop testing
                let isScrolling = false;
                let startX = 0;
                let scrollLeft = 0;
                
                flowStages.addEventListener('mousedown', (e) => {
                    isScrolling = true;
                    flowStages.style.cursor = 'grabbing';
                    startX = e.pageX - flowStages.offsetLeft;
                    scrollLeft = flowStages.scrollLeft;
                    console.log('🖱️ Mouse drag started');
                });
                
                flowStages.addEventListener('mouseleave', () => {
                    isScrolling = false;
                    flowStages.style.cursor = 'grab';
                });
                
                flowStages.addEventListener('mouseup', () => {
                    isScrolling = false;
                    flowStages.style.cursor = 'grab';
                    console.log('🖱️ Mouse drag ended');
                });
                
                flowStages.addEventListener('mousemove', (e) => {
                    if (!isScrolling) return;
                    e.preventDefault();
                    const x = e.pageX - flowStages.offsetLeft;
                    const walk = (x - startX) * 2; // Scroll speed
                    flowStages.scrollLeft = scrollLeft - walk;
                    console.log(`🖱️ Dragging: scrollLeft = ${flowStages.scrollLeft}`);
                });
                
                // Force stage widths and ENSURE PROPER ORDERING - FIXED
                const stages = document.querySelectorAll('.flow-stage');
                let totalWidth = 0;
                
                // REORDER: Make sure Thank You page is truly first
                console.log('🔄 CHECKING STAGE ORDER:');
                stages.forEach((stage, index) => {
                    const title = stage.querySelector('.stage-title').textContent;
                    console.log(`Stage ${index}: ${title}`);
                });
                
                // Force positioning - REMOVE LEFT POSITIONING
                stages.forEach((stage, index) => {
                    const stageWidth = window.innerWidth;
                    totalWidth += stageWidth;
                    
                    stage.style.cssText = `
                        min-width: ${stageWidth}px !important;
                        width: ${stageWidth}px !important;
                        max-width: ${stageWidth}px !important;
                        flex: 0 0 ${stageWidth}px !important;
                        flex-shrink: 0 !important;
                        flex-grow: 0 !important;
                        scroll-snap-align: start !important;
                        border-right: 1px solid #eee !important;
                        background: ${index % 2 === 0 ? '#fff' : '#f9f9f9'} !important;
                        display: block !important;
                        box-sizing: border-box !important;
                        overflow-y: auto !important;
                        padding: 20px !important;
                        height: 100% !important;
                        position: relative !important;
                        order: ${index} !important;
                    `;
                    
                    console.log(`Stage ${index + 1} (${stage.querySelector('.stage-title').textContent}): Natural flex position, width ${stageWidth}px`);
                });
                
                console.log(`Total content width: ${totalWidth}px (${stages.length} stages × ${window.innerWidth}px)`);
                // DON'T set container width to total - that was the bug!
                // Final verification and INITIAL POSITIONING
                setTimeout(() => {
                    console.log('=== FINAL VERIFICATION ===');
                    console.log(`Container scroll width: ${flowStages.scrollWidth}px`);
                    console.log(`Container client width: ${flowStages.clientWidth}px`);
                    console.log(`Container offset width: ${flowStages.offsetWidth}px`);
                    console.log(`Is definitely scrollable: ${flowStages.scrollWidth > flowStages.clientWidth}`);
                    console.log(`Max scroll position: ${flowStages.scrollWidth - flowStages.clientWidth}px`);
                    
                    // Check each stage position
                    const stages = document.querySelectorAll('.flow-stage');
                    stages.forEach((stage, index) => {
                        const rect = stage.getBoundingClientRect();
                        const containerRect = flowStages.getBoundingClientRect();
                        const relativeLeft = rect.left - containerRect.left + flowStages.scrollLeft;
                        console.log(`📍 Stage ${index + 1} (${stage.querySelector('.stage-title').textContent}): Position ${relativeLeft}px, Width ${rect.width}px`);
                    });
                    
                    // FORCE START AT STAGE 1 (Thank You page) - FIXED APPROACH
                    console.log('🎯 FORCING START POSITION TO STAGE 1 - FIXED');
                    const firstStage = stages[0];
                    
                    // Simple approach: just ensure we start at 0
                    flowStages.scrollLeft = 0;
                    currentStage = 0;
                    
                    // Update the first dot to be active
                    const firstDot = document.querySelector('.scroll-dot[data-stage="0"]');
                    if (firstDot) {
                        document.querySelectorAll('.scroll-dot').forEach(dot => dot.classList.remove('active'));
                        firstDot.classList.add('active');
                    }
                    
                    if (flowStages.scrollWidth <= flowStages.clientWidth) {
                        console.error('❌ CONTAINER IS NOT SCROLLABLE - This is the problem!');
                    } else {
                        console.log('✅ Container is properly scrollable!');
                    }
                }, 500);
                
                // Clean mobile scroll - Mobile scrolling setup complete
                // Add scroll event listener
                flowStages.addEventListener('scroll', function() {
                    const scrollLeft = flowStages.scrollLeft;
                    const containerWidth = window.innerWidth;
                    const currentStage = Math.round(scrollLeft / containerWidth);
                    
                    scrollDots.forEach((dot, index) => {
                        dot.classList.toggle('active', index === currentStage);
                    });
                });
                
                // Add dot click handlers
                scrollDots.forEach((dot, index) => {
                    dot.addEventListener('click', function() {
                        const targetScroll = window.innerWidth * index;
                        
                        flowStages.scrollTo({
                            left: targetScroll,
                            behavior: 'smooth'
                        });
                        
                        // Update active dot
                        scrollDots.forEach((d, i) => {
                            d.classList.toggle('active', i === index);
                        });
                    });
                });
                
                console.log('Mobile scroll setup complete!');
                
            } else {
                // Desktop mode
                if (scrollIndicators) {
                    scrollIndicators.style.display = 'none';
                }
                
                console.log('Desktop mode - mobile features disabled');
            }
        }
        
        // Handle window resize
        window.addEventListener('resize', function() {
            initMobileScroll();
        });
        
        // Initialize on load
        // BROKEN MOBILE INIT - COMMENTED OUT
        /*
        document.addEventListener('DOMContentLoaded', function() {
            console.log('🚀 DOM LOADED - Initializing mobile scroll');
            
            if (window.innerWidth <= 768) {
                const flowStages = document.querySelector('.flow-stages');
                const scrollDots = document.querySelectorAll('.scroll-dot');
                const scrollIndicators = document.getElementById('scrollIndicators');
                
                console.log('Flow stages found:', !!flowStages);
                    z-index: 999999 !important;
                    background: #ff4444 !important;
                    color: white !important;
                    padding: 15px 20px !important;
                    border: 3px solid white !important;
                    border-radius: 25px !important;
                    font-size: 16px !important;
                    font-weight: bold !important;
                    cursor: pointer !important;
                    box-shadow: 0 4px 12px rgba(0,0,0,0.5) !important;
                    pointer-events: auto !important;
                    user-select: none !important;
                    -webkit-user-select: none !important;
                    -webkit-tap-highlight-color: transparent !important;
                `;
                
                let currentStage = 0;
                
                // Multiple event listeners for better compatibility - FIXED POSITIONING
                const clickHandler = function(e) {
                    e.preventDefault();
                    e.stopPropagation();
                    
                    console.log(`🔥 BUTTON CLICKED!`);
                    console.log(`Current scroll position: ${flowStages.scrollLeft}px`);
                    console.log(`Current stage before: ${currentStage}`);
                    
                    // Cycle through stages: 0, 1, 2, then back to 0
                    currentStage = (currentStage + 1) % 3;
                    
                    // Calculate actual position of target stage
                    const stages = document.querySelectorAll('.flow-stage');
                    const targetStage = stages[currentStage];
                    const containerRect = flowStages.getBoundingClientRect();
                    const stageRect = targetStage.getBoundingClientRect();
                    
                    // Calculate the scroll position needed to show this stage
                    const targetScroll = stageRect.left - containerRect.left + flowStages.scrollLeft;
                    
                    const stageNames = ['Thank You', 'Content', 'SERP'];
                    console.log(`🎯 Going to stage ${currentStage} (${stageNames[currentStage]})`);
                    console.log(`Target scroll position: ${targetScroll}px (calculated from actual stage position)`);
                    
                    // Smooth scroll to target
                    flowStages.scrollTo({
                        left: targetScroll,
                        behavior: 'smooth'
                    });
                    
                    // Also set directly as backup
                    setTimeout(() => {
                        flowStages.scrollLeft = targetScroll;
                    }, 100);
                    
                    // Update button text to show current stage
                    debugBtn.style.background = '#00ff00';
                    debugBtn.textContent = `→ ${stageNames[currentStage]}`;
                    
                    setTimeout(() => {
                        debugBtn.style.background = '#ff4444';
                        debugBtn.textContent = 'Next Stage →';
                    }, 1000);
                    
                    // Verify result
                    setTimeout(() => {
                        console.log(`✅ Final position: ${flowStages.scrollLeft}px (expected: ${targetScroll}px)`);
                        const actualStageIndex = Math.round(flowStages.scrollLeft / window.innerWidth);
                        console.log(`Now showing: Stage ${actualStageIndex} (${stageNames[actualStageIndex] || 'Unknown'})`);
                    }, 600);
                };
                
                debugBtn.addEventListener('click', clickHandler);
                debugBtn.addEventListener('touchstart', clickHandler);
                debugBtn.addEventListener('mousedown', clickHandler);
                
                document.body.appendChild(debugBtn);
                console.log('🔥 DEBUG BUTTON CREATED WITH MULTIPLE EVENT LISTENERS');
                
                // Add a second button for direct scroll testing
                const testBtn = document.createElement('button');
                testBtn.id = 'testDirectScroll';
                testBtn.textContent = 'Scroll 500px →';
                testBtn.style.cssText = `
                    position: fixed !important;
                    top: 130px !important;
                    right: 10px !important;
                    z-index: 999999 !important;
                    background: #0066ff !important;
                    color: white !important;
                    padding: 10px 15px !important;
                    border: 2px solid white !important;
                    border-radius: 20px !important;
                    font-size: 14px !important;
                    font-weight: bold !important;
                    cursor: pointer !important;
                    pointer-events: auto !important;
                `;
                
                testBtn.addEventListener('click', function(e) {
                    e.preventDefault();
                    console.log('🔵 DIRECT SCROLL TEST - Scrolling 500px');
                    console.log(`Before: ${flowStages.scrollLeft}px`);
                    
                    flowStages.scrollLeft += 500;
                    
                    setTimeout(() => {
                        console.log(`After: ${flowStages.scrollLeft}px`);
                    }, 100);
                });
                
                document.body.appendChild(testBtn);
                console.log('🔵 DIRECT SCROLL TEST BUTTON ADDED');
                
                // Add "Go to Stage 1" button
                const stage1Btn = document.createElement('button');
                stage1Btn.id = 'goToStage1';
                stage1Btn.textContent = 'Go to Stage 1';
                stage1Btn.style.cssText = `
                    position: fixed !important;
                    top: 180px !important;
                    right: 10px !important;
                    z-index: 999999 !important;
                    background: #28a745 !important;
                    color: white !important;
                    padding: 10px 15px !important;
                    border: 2px solid white !important;
                    border-radius: 20px !important;
                    font-size: 14px !important;
                    font-weight: bold !important;
                    cursor: pointer !important;
                    pointer-events: auto !important;
                `;
                
                stage1Btn.addEventListener('click', function(e) {
                    e.preventDefault();
                    console.log('🟢 GO TO STAGE 1 (Thank You) - Calculating actual position');
                    console.log(`Before: ${flowStages.scrollLeft}px`);
                    
                    // Find the actual position of the first stage
                    const stages = document.querySelectorAll('.flow-stage');
                    const firstStage = stages[0];
                    const containerRect = flowStages.getBoundingClientRect();
                    const stageRect = firstStage.getBoundingClientRect();
                    
                    const targetScroll = stageRect.left - containerRect.left + flowStages.scrollLeft;
                    console.log(`Calculated position for Stage 1: ${targetScroll}px`);
                    
                    currentStage = 0;
                    flowStages.scrollTo({
                        left: targetScroll,
                        behavior: 'smooth'
                    });
                    
                    setTimeout(() => {
                        flowStages.scrollLeft = targetScroll;
                    }, 100);
                    
                    stage1Btn.style.background = '#00ff00';
                    stage1Btn.textContent = 'Going to Stage 1...';
                    setTimeout(() => {
                        stage1Btn.style.background = '#28a745';
                        stage1Btn.textContent = 'Go to Stage 1';
                        console.log(`After: ${flowStages.scrollLeft}px`);
                    }, 600);
                });
                
                document.body.appendChild(stage1Btn);
                console.log('🟢 GO TO STAGE 1 BUTTON ADDED');
                
                // Add "Reset to Start" button
                const resetBtn = document.createElement('button');
                resetBtn.id = 'resetToStart';
                resetBtn.textContent = 'Reset to Start';
                resetBtn.style.cssText = `
                    position: fixed !important;
                    top: 230px !important;
                    right: 10px !important;
                    z-index: 999999 !important;
                    background: #dc3545 !important;
                    color: white !important;
                    padding: 10px 15px !important;
                    border: 2px solid white !important;
                    border-radius: 20px !important;
                    font-size: 14px !important;
                    font-weight: bold !important;
                    cursor: pointer !important;
                    pointer-events: auto !important;
                `;
                
                resetBtn.addEventListener('click', function(e) {
                    e.preventDefault();
                    console.log('🔴 RESET TO START - Forcing scroll to 0px');
                    console.log(`Before: ${flowStages.scrollLeft}px`);
                    
                    // Force to absolute beginning
                    currentStage = 0;
                    flowStages.scrollLeft = 0;
                    flowStages.scrollTo({ left: 0, behavior: 'smooth' });
                    
                    // Update dots
                    const dots = document.querySelectorAll('.scroll-dot');
                    dots.forEach((dot, index) => {
                        dot.classList.toggle('active', index === 0);
                    });
                    
                    resetBtn.style.background = '#00ff00';
                    resetBtn.textContent = 'Reset!';
                    setTimeout(() => {
                        resetBtn.style.background = '#dc3545';
                        resetBtn.textContent = 'Reset to Start';
                        console.log(`After reset: ${flowStages.scrollLeft}px`);
                    }, 600);
                });
                
                document.body.appendChild(resetBtn);
                console.log('🔴 RESET TO START BUTTON ADDED');
                
                // Add debug info button
                const debugInfoBtn = document.createElement('button');
                debugInfoBtn.id = 'debugInfo';
                debugInfoBtn.textContent = 'Debug Info';
                debugInfoBtn.style.cssText = `
                    position: fixed !important;
                    top: 280px !important;
                    right: 10px !important;
                    z-index: 999999 !important;
                    background: #6f42c1 !important;
                    color: white !important;
                    padding: 8px 12px !important;
                    border: 2px solid white !important;
                    border-radius: 15px !important;
                    font-size: 12px !important;
                    font-weight: bold !important;
                    cursor: pointer !important;
                    pointer-events: auto !important;
                `;
                
                debugInfoBtn.addEventListener('click', function(e) {
                    e.preventDefault();
                    console.log('🔍 === DEBUG INFO ===');
                    console.log(`Current scroll: ${flowStages.scrollLeft}px`);
                    console.log(`Container width: ${flowStages.clientWidth}px`);
                    console.log(`Total scroll width: ${flowStages.scrollWidth}px`);
                    
                    const stages = document.querySelectorAll('.flow-stage');
                    stages.forEach((stage, index) => {
                        const rect = stage.getBoundingClientRect();
                        const containerRect = flowStages.getBoundingClientRect();
                        const relativeLeft = rect.left - containerRect.left;
                        const isVisible = relativeLeft >= 0 && relativeLeft < containerRect.width;
                        const title = stage.querySelector('.stage-title').textContent;
                        console.log(`Stage ${index}: "${title}" - Position: ${relativeLeft}px, Visible: ${isVisible}`);
                    });
                    
                    // Test specific scroll positions
                    console.log('🧪 Testing scroll positions:');
                    for (let i = 0; i < 3; i++) {
                        const testPos = window.innerWidth * i;
                        console.log(`Position ${testPos}px should show stage ${i + 1}`);
                    }
                });
                
                document.body.appendChild(debugInfoBtn);
                console.log('🔍 DEBUG INFO BUTTON ADDED');
                
                // Add scroll event listener
                flowStages.addEventListener('scroll', function() {
                    const scrollLeft = flowStages.scrollLeft;
                    const containerWidth = window.innerWidth;
                    const currentStage = Math.round(scrollLeft / containerWidth);
                    
                    console.log(`SCROLL EVENT: left=${scrollLeft}, width=${containerWidth}, stage=${currentStage}`);
                    
                    scrollDots.forEach((dot, index) => {
                        dot.classList.toggle('active', index === currentStage);
                    });
                });
                
                // Click dots to navigate
                scrollDots.forEach((dot, index) => {
                    dot.addEventListener('click', function() {
                        const targetScroll = window.innerWidth * index;
                        console.log(`DOT CLICKED: stage=${index}, scrollTo=${targetScroll}px`);
                        
                        flowStages.scrollTo({
                            left: targetScroll,
                            behavior: 'smooth'
                        });
                    });
                });
                
                console.log('Mobile scroll setup complete!');
                
            } else {
                // Desktop mode
                if (scrollIndicators) {
                    scrollIndicators.style.display = 'none';
                }
                
                console.log('Desktop mode - mobile features disabled');
            }
        }
        */
        // END BROKEN MOBILE INIT

        // Handle window resize
        window.addEventListener('resize', function() {
            initMobileScroll();
        });

        // Initialize on load
        document.addEventListener('DOMContentLoaded', function() {
            console.log('🚀 DOM LOADED - Initializing mobile scroll');
            
            if (window.innerWidth <= 768) {
                const flowStages = document.querySelector('.flow-stages');
                const scrollDots = document.querySelectorAll('.scroll-dot');
                const scrollIndicators = document.getElementById('scrollIndicators');
                
                console.log('Flow stages found:', !!flowStages);
                
                if (flowStages) {
                    // Apply mobile scrolling CSS
                    console.log('Applying CSS to flowStages');
                    
                    flowStages.style.cssText = `
                        display: flex !important;
                        flex-direction: row !important;
                        overflow-x: scroll !important;
                        overflow-y: hidden !important;
                        scroll-snap-type: x mandatory !important;
                        -webkit-overflow-scrolling: touch !important;
                        width: 100vw !important;
                        height: calc(100vh - 80px) !important;
                        position: relative !important;
                        margin: 0 !important;
                        padding: 0 !important;
                        border: none !important;
                        scroll-behavior: smooth !important;
                        scrollbar-width: none !important;
                        -ms-overflow-style: none !important;
                    `;
                    
                    // Hide scrollbar for WebKit browsers
                    flowStages.style.setProperty('-webkit-scrollbar', 'none', 'important');
                    
                    // Ensure each stage is properly sized
                    const stages = flowStages.querySelectorAll('.flow-stage');
                    console.log('Stages found:', stages.length);
                    
                    stages.forEach((stage, index) => {
                        stage.style.minWidth = '100vw';
                        stage.style.width = '100vw';
                        stage.style.flexShrink = '0';
                        stage.style.scrollSnapAlign = 'start';
                        // Add smooth vertical scrolling within each stage
                        stage.style.overflowY = 'auto';
                        stage.style.webkitOverflowScrolling = 'touch';
                        stage.style.scrollBehavior = 'smooth';
                    });
                    
                    console.log('Mobile scrolling CSS applied');
                    
                    setTimeout(() => {
                        // CRITICAL: Force start at Stage 1 (index 0) - ALWAYS first
                        flowStages.scrollLeft = 0;
                        
                        // Double-check and force again if needed
                        setTimeout(() => {
                            if (flowStages.scrollLeft !== 0) {
                                console.log('🔧 Secondary reset needed');
                                flowStages.scrollLeft = 0;
                            }
                        }, 100);
                        
                        console.log('✅ FORCED START: Stage 1 at position 0px');
                        console.log('ScrollWidth:', flowStages.scrollWidth, 'ClientWidth:', flowStages.clientWidth);
                        console.log('Can scroll:', flowStages.scrollWidth > flowStages.clientWidth);
                        
                        // Ensure first dot is active
                        if (scrollDots.length > 0) {
                            scrollDots.forEach((dot, index) => {
                                dot.classList.toggle('active', index === 0);
                            });
                            console.log('✅ First scroll indicator activated');
                        }
                    }, 200);
                    
                    console.log('✅ Mobile scroll enabled');
                    
                    // Show scroll indicators
                    if (scrollIndicators) {
                        scrollIndicators.style.display = 'flex';
                    }
                    
                    // Add scroll event listener for dot indicators - IMPROVED
                    flowStages.addEventListener('scroll', function() {
                        const scrollLeft = flowStages.scrollLeft;
                        const stageWidth = flowStages.clientWidth;
                        const currentStage = Math.round(scrollLeft / stageWidth);
                        
                        console.log(`📱 Scroll Event: position=${scrollLeft}px, stage=${currentStage}`);
                        
                        // Update active dot with bounds checking
                        scrollDots.forEach((dot, index) => {
                            const isActive = index === Math.max(0, Math.min(currentStage, scrollDots.length - 1));
                            dot.classList.toggle('active', isActive);
                        });
                    }, { passive: true });
                    
                    // Add click handlers for dots
                    scrollDots.forEach((dot, index) => {
                        dot.addEventListener('click', function() {
                            const targetPosition = index * flowStages.clientWidth;
                            flowStages.scrollTo({
                                left: targetPosition,
                                behavior: 'smooth'
                            });
                        });
                        dot.setAttribute('data-stage', index);
                    });
                    
                    // Debug: Test scroll after 3 seconds
                    setTimeout(() => {
                        console.log('Testing scroll to stage 2...');
                        flowStages.scrollTo({ left: flowStages.clientWidth, behavior: 'smooth' });
                    }, 3000);
                }
            }
        });

        // Handle refresh case - apply mobile styles on window load
        window.addEventListener('load', function() {
            console.log('🔄 Window loaded - checking for mobile refresh');
            
            if (window.innerWidth <= 768) {
                const flowStages = document.querySelector('.flow-stages');
                if (flowStages) {
                    console.log('Applying mobile CSS on refresh');
                    
                    // Re-apply mobile scrolling CSS for refresh case
                    flowStages.style.cssText = `
                        display: flex !important;
                        flex-direction: row !important;
                        overflow-x: scroll !important;
                        overflow-y: hidden !important;
                        scroll-snap-type: x mandatory !important;
                        -webkit-overflow-scrolling: touch !important;
                        width: 100vw !important;
                        height: calc(100vh - 120px) !important;
                        position: relative !important;
                        margin: 0 !important;
                        padding: 0 !important;
                        border: none !important;
                    `;
                    
                    // Ensure each stage is properly sized
                    const stages = flowStages.querySelectorAll('.flow-stage');
                    stages.forEach(stage => {
                        stage.style.minWidth = '100vw';
                        stage.style.width = '100vw';
                        stage.style.flexShrink = '0';
                        stage.style.scrollSnapAlign = 'start';
                    });
                    
                    // Reset to stage 1 after applying CSS
                    setTimeout(() => {
                        flowStages.scrollLeft = 0;
                        console.log('Refresh: Reset to Stage 1');
                        console.log('Refresh ScrollWidth:', flowStages.scrollWidth, 'ClientWidth:', flowStages.clientWidth);
                    }, 200);
                }
            }
        });

        // Handle iframe communication if needed
        window.addEventListener('message', function(event) {
            // Accept messages from any origin for production
            //if (event.origin === 'http://localhost:8084') {
                console.log('Message from iframe:', event.data);
            //}
        });

        // Center iframe content horizontally when loaded
        document.addEventListener('DOMContentLoaded', function() {
            console.log('DOM loaded - starting auto-rotation');
            
            // Start with the social view
            showSocial();
            
            // Start auto-rotation immediately
            startAutoRotation();
            
            // Add click handlers for the toggle buttons
            document.querySelectorAll('.toggle-btn').forEach(button => {
                button.addEventListener('click', function() {
                    // Get the view name from the function
                    const onclickAttr = this.getAttribute('onclick');
                    if (onclickAttr && onclickAttr.includes('show')) {
                        const viewName = onclickAttr.replace('show', '').replace('()', '').toLowerCase();
                        console.log('Button clicked for view: ' + viewName);
                        
                        // Restart auto-rotation when a button is clicked
                        restartAutoRotation();
                    }
                });
            });
            
            const iframes = document.querySelectorAll('.page-iframe');
            
            iframes.forEach(function(iframe) {
                iframe.addEventListener('load', function() {
                    try {
                        // Calculate center position for horizontal scroll
                        const iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
                        const scrollWidth = iframeDoc.documentElement.scrollWidth;
                        const clientWidth = iframeDoc.documentElement.clientWidth;
                        const centerPosition = (scrollWidth - clientWidth) / 2;
                        
                        // Set horizontal scroll to center
                        iframeDoc.documentElement.scrollLeft = centerPosition;
                        iframeDoc.body.scrollLeft = centerPosition;
                        
                        console.log('Centered iframe content:', iframe.title);
                    } catch (e) {
                        // Handle cross-origin issues silently
                        console.log('Could not center iframe due to cross-origin restrictions:', iframe.title);
                    }
                });
            });
        });

        // Stage 1 Dynamic Section Handler
        // Listen for messages from Stage 1 iframe to detect clicked options
        window.addEventListener('message', function(event) {
            // Accept messages from any origin for production
            //if (event.origin === 'http://localhost:8084') {
                // Check if message is from Stage 1 and contains option data
                if (event.data && event.data.type === 'option-clicked' && event.data.stage === 1) {
                    updateStage1Section(event.data.option, event.data.description);
                }
            }
        });
                height: calc(100vh - 120px) !important;
                position: relative !important;
                margin: 0 !important;
                padding: 0 !important;
                border: none !important;
                background: transparent !important;
                box-sizing: border-box !important;
            `;
            
            // Clean up stage styling
            const stages = flowStages.querySelectorAll('.flow-stage');
            console.log(`Found ${stages.length} stages`);
            
            stages.forEach((stage, index) => {
                stage.removeAttribute('style');
                stage.style.cssText = `
                    min-width: 100vw !important;
                    width: 100vw !important;
                    max-width: 100vw !important;
                    flex: 0 0 100vw !important;
                    flex-shrink: 0 !important;
                    scroll-snap-align: start !important;
                    padding: 20px !important;
                    margin: 0 !important;
                    box-sizing: border-box !important;
                    overflow-y: auto !important;
                    position: relative !important;
                    background: white !important;
                    border: none !important;
                    border-radius: 0 !important;
                    box-shadow: none !important;
                `;
            });
            
            // Show scroll indicators
            if (scrollIndicators) {
                scrollIndicators.style.display = 'flex';
            }
            
            // Reset to first stage
            setTimeout(() => {
                flowStages.scrollLeft = 0;
                
                // Activate first dot
                scrollDots.forEach((dot, index) => {
                    dot.classList.toggle('active', index === 0);
                });
                
                console.log('✅ Mobile scrolling initialized successfully');
                console.log(`ScrollWidth: ${flowStages.scrollWidth}, ClientWidth: ${flowStages.clientWidth}`);
                console.log(`Can scroll: ${flowStages.scrollWidth > flowStages.clientWidth}`);
            }, 100);
            
            // Add scroll event listener (only once)
            flowStages.removeEventListener('scroll', handleMobileScroll);
            flowStages.addEventListener('scroll', handleMobileScroll);
            
            // Add dot click handlers (only once)
            scrollDots.forEach((dot, index) => {
                dot.removeEventListener('click', handleDotClick);
                dot.addEventListener('click', handleDotClick);
                dot.setAttribute('data-stage', index);
            });
        }

        // Separate scroll handler to avoid duplicate listeners
        function handleMobileScroll() {
            const flowStages = document.querySelector('.flow-stages');
            const scrollDots = document.querySelectorAll('.scroll-dot');
            
            if (!flowStages) return;
            
            const scrollLeft = flowStages.scrollLeft;
            const stageWidth = flowStages.clientWidth;
            const currentStage = Math.round(scrollLeft / stageWidth);
            
            scrollDots.forEach((dot, index) => {
                dot.classList.toggle('active', index === currentStage);
            });
        }

        // Separate dot click handler to avoid duplicate listeners
        function handleDotClick(event) {
            const flowStages = document.querySelector('.flow-stages');
            const index = parseInt(event.target.getAttribute('data-stage'));
            
            if (!flowStages || isNaN(index)) return;
            
            const targetPosition = index * flowStages.clientWidth;
            flowStages.scrollTo({
                left: targetPosition,
                behavior: 'smooth'
            });
        }

        // Handle refresh case - apply mobile styles on window load
        window.addEventListener('load', function() {
            console.log('🔄 Window loaded - checking for mobile refresh');
            
            if (window.innerWidth <= 768) {
                const flowStages = document.querySelector('.flow-stages');
                if (flowStages) {
                    console.log('Applying mobile CSS on refresh');
                    
                    // Re-apply mobile scrolling CSS for refresh case
                    flowStages.style.cssText = `
                        display: flex !important;
                        flex-direction: row !important;
                        overflow-x: scroll !important;
                        overflow-y: hidden !important;
                        scroll-snap-type: x mandatory !important;
                        -webkit-overflow-scrolling: touch !important;
                        width: 100vw !important;
                        height: calc(100vh - 120px) !important;
                        position: relative !important;
                        margin: 0 !important;
                        padding: 0 !important;
                        border: none !important;
                    `;
                    
                    // Ensure each stage is properly sized
                    const stages = flowStages.querySelectorAll('.flow-stage');
                    stages.forEach(stage => {
                        stage.style.minWidth = '100vw';
                        stage.style.width = '100vw';
                        stage.style.flexShrink = '0';
                        stage.style.scrollSnapAlign = 'start';
                    });
                    
                    // Reset to stage 1 after applying CSS
                    setTimeout(() => {
                        flowStages.scrollLeft = 0;
                        console.log('Refresh: Reset to Stage 1');
                        console.log('Refresh ScrollWidth:', flowStages.scrollWidth, 'ClientWidth:', flowStages.clientWidth);
                    }, 200);
                }
            }
        });

        // Handle iframe communication if needed
        window.addEventListener('message', function(event) {
            // Accept messages from any origin for production
            //if (event.origin === 'http://localhost:8084') {
                console.log('Message from iframe:', event.data);
            //}
        });

        // Handle iframe communication and message events
        window.addEventListener('message', function(event) {
            // Accept messages from any origin for production
            //if (event.origin === 'http://localhost:8084') {
                // Check if message is from Stage 1 and contains option data
                if (event.data && event.data.type === 'option-clicked' && event.data.stage === 1) {
                    updateStage1Section(event.data.option, event.data.description);
                } else {
                    console.log('Message from iframe:', event.data);
                }
            //}
        });

        // Function to update Stage 1 dynamic section
        function updateStage1Section(optionTitle, description) {
            const dynamicSection = document.getElementById('stage1-dynamic-section');
            const titleElement = document.getElementById('stage1-option-title');
            const descriptionElement = document.getElementById('stage1-option-description');
            
            // Update content
            titleElement.textContent = optionTitle;
            
            // Handle empty description
            if (description && description.trim() !== '') {
                descriptionElement.querySelector('p').textContent = description;
                descriptionElement.style.display = 'block';
            } else {
                descriptionElement.style.display = 'none'; // Hide description area if empty
            }
            
            // Show the section
            dynamicSection.style.display = 'block';
            
            console.log('Stage 1 section updated:', optionTitle);
        }

        // Test function for console debugging - SIMPLIFIED
        window.testStage1Switch = function(version) {
            console.log(`🧪 Manual test: Switching to ${version}`);
            switchStage1Version(version);
        };
        
        // Simple direct test functions
        window.showThankYou = function() {
            console.log('🎯 DIRECT: Showing Thank You page');
            document.getElementById('stage1-social').style.display = 'none';
            document.getElementById('stage1-disqualify').style.display = 'none';
            document.getElementById('stage1-thankyou').style.display = 'block';
            console.log('✅ Thank you iframe should now be visible');
        };
        
        window.showDisqualify = function() {
            console.log('🎯 DIRECT: Showing Disqualify page');
            document.getElementById('stage1-social').style.display = 'none';
            document.getElementById('stage1-thankyou').style.display = 'none';
            document.getElementById('stage1-disqualify').style.display = 'block';
            console.log('✅ Disqualify iframe should now be visible');
        };
        
        window.showSocial = function() {
            console.log('🎯 DIRECT: Showing Social page');
            document.getElementById('stage1-thankyou').style.display = 'none';
            document.getElementById('stage1-disqualify').style.display = 'none';
            document.getElementById('stage1-social').style.display = 'block';
            console.log('✅ Social div should now be visible');
        };
        
        // Test function to show all elements
        window.debugStage1Elements = function() {
            console.log('🔍 DEBUGGING STAGE 1 ELEMENTS:');
            console.log('=================================');
            
            const buttons = document.querySelectorAll('.toggle-btn');
            console.log(`Found ${buttons.length} toggle buttons:`);
            buttons.forEach((btn, i) => {
                console.log(`  ${i+1}. "${btn.textContent}" - data-version: ${btn.getAttribute('data-version')}`);
            });
            
            const versions = document.querySelectorAll('.stage1-version');
            console.log(`\nFound ${versions.length} stage1 versions:`);
            versions.forEach((version, i) => {
                const rect = version.getBoundingClientRect();
                const isVisible = rect.width > 0 && rect.height > 0;
                console.log(`  ${i+1}. ${version.id} (${version.tagName}) - display: ${getComputedStyle(version).display} - visible: ${isVisible}`);
                if (version.src) console.log(`      src: ${version.src}`);
            });
        };
        
        // Make functions available globally for console testing
        function switchStage1Version(version) {
            console.log(`Switching Stage 1 to: ${version}`);
            switchToView(version);
        }
        
        window.switchStage1Version = switchStage1Version;

        // SIMPLIFIED AUTO-ROTATION: USING NEW SYSTEM
        console.log('Using new auto-rotation system');
    </script>
    
    <!-- Auto-rotation script -->
    <script src="auto-rotate.js">// Just run at the end of all scripts
console.log('SolarFlow page loaded!');

// EMERGENCY MOBILE STAGE 1 FIX
if (window.innerWidth <= 768) {
    console.log('🚨 EMERGENCY MOBILE FIX: Enabling Stage 1 access');
    
    // Find all stages
    const stages = document.querySelectorAll('.flow-stage');
    const flowStages = document.querySelector('.flow-stages');
    
    // Completely different approach: Reorder the DOM elements
    if (stages.length >= 3 && flowStages) {
        console.log('Restructuring stages to ensure Stage 1 is accessible');
        
        // Clone the stages
        const stage1 = stages[0].cloneNode(true);
        const stage2 = stages[1].cloneNode(true);
        const stage3 = stages[2].cloneNode(true);
        
        // Remove existing stages
        flowStages.innerHTML = '';
        
        // Add them back in the correct order
        flowStages.appendChild(stage1);
        flowStages.appendChild(stage2);
        flowStages.appendChild(stage3);
        
        // Apply fixed styling
        flowStages.style.cssText = `
            display: flex !important;
            flex-direction: row !important;
            flex-wrap: nowrap !important;
            overflow-x: scroll !important;
            overflow-y: hidden !important;
            scroll-snap-type: x mandatory !important;
            -webkit-overflow-scrolling: touch !important;
            width: 100vw !important;
            height: calc(100vh - 120px) !important;
            position: relative !important;
            margin: 0 !important;
            padding: 0 !important;
            border: none !important;
        `;
        
        // Style each stage properly
        document.querySelectorAll('.flow-stage').forEach((stage, index) => {
            stage.style.cssText = `
                min-width: 100vw !important;
                width: 100vw !important;
                flex: 0 0 100vw !important;
                flex-shrink: 0 !important;
                scroll-snap-align: start !important;
                height: 100% !important;
                overflow-y: auto !important;
                position: relative !important;
                display: block !important;
                visibility: visible !important;
                opacity: 1 !important;
                order: ${index + 1} !important;
            `;
        });
        
        // Forcefully scroll to stage 1
        flowStages.scrollLeft = 0;
        
        // Set up button functionality in Stage 1
        const toggleBtns = document.querySelectorAll('.toggle-btn');
        if (toggleBtns.length > 0) {
            // Social button
            toggleBtns[0].addEventListener('click', function() {
                const socialDiv = document.getElementById('stage1-social-div');
                const iframe = document.getElementById('stage1-iframe');
                if (socialDiv && iframe) {
                    iframe.style.display = 'none';
                    socialDiv.style.display = 'block';
                    toggleBtns.forEach(btn => btn.classList.remove('active'));
                    this.classList.add('active');
                }
            });
            
            // Thank You button
            if (toggleBtns[1]) {
                toggleBtns[1].addEventListener('click', function() {
                    const socialDiv = document.getElementById('stage1-social-div');
                    const iframe = document.getElementById('stage1-iframe');
                    if (socialDiv && iframe) {
                        socialDiv.style.display = 'none';
                        iframe.style.display = 'block';
                        iframe.src = 'flow.html?step=6&hideDevNav=true';
                        toggleBtns.forEach(btn => btn.classList.remove('active'));
                        this.classList.add('active');
                    }
                });
            }
            
            // Disqualify button
            if (toggleBtns[2]) {
                toggleBtns[2].addEventListener('click', function() {
                    const socialDiv = document.getElementById('stage1-social-div');
                    const iframe = document.getElementById('stage1-iframe');
                    if (socialDiv && iframe) {
                        socialDiv.style.display = 'none';
                        iframe.style.display = 'block';
                        iframe.src = 'flow.html?step=4&autoSelect=mostly-shade&showPopup=true&hideDevNav=true';
                        toggleBtns.forEach(btn => btn.classList.remove('active'));
                        this.classList.add('active');
                    }
                });
            }
            
            // Default to showing social
            toggleBtns[0].click();
        }
    }
    
    // Fix scroll dots
    const scrollDots = document.querySelectorAll('.scroll-dot');
    scrollDots.forEach((dot, index) => {
        dot.addEventListener('click', function() {
            const flowStages = document.querySelector('.flow-stages');
            if (flowStages) {
                const targetScroll = window.innerWidth * index;
                flowStages.scrollTo({left: targetScroll, behavior: 'smooth'});
                
                // Update active state
                scrollDots.forEach((d, i) => {
                    d.classList.toggle('active', i === index);
                });
            }
        });
    });
    
    // Activate first dot
    if (scrollDots.length > 0) {
        scrollDots.forEach(dot => dot.classList.remove('active'));
        scrollDots[0].classList.add('active');
    }
    
    // Fix scroll position - try multiple times
    const forceScroll = function() {
        if (flowStages) {
            flowStages.scrollLeft = 0;
            console.log('Forced scroll to Stage 1');
        }
    };
    
    forceScroll();
    setTimeout(forceScroll, 100);
    setTimeout(forceScroll, 500);
    setTimeout(forceScroll, 1000);
}
</script>
</body>
</html>
