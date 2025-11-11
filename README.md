<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Content Monetization & Solar Flow Demo | System1</title>
    <meta name="description" content="Interactive demonstration of user journeys for both content monetization and solar panel marketing flows.">
    <meta name="keywords" content="content monetization, creators, solar panels, solar energy, user journey, marketing flow, lead generation">
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='0.9em' font-size='90'>💡</text></svg>" type="image/svg+xml">

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
            padding-top: 0;
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

        .sticky-container {
            position: sticky;
            top: 0;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
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

        .solar-entry-flow {
            display: none;
        }

        .solar-entry-flow.active {
            display: flex;
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

        .social-ad-mockup {
            background: #f0f2f5;
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
            min-height: 700px;
            flex: 1;
            display: flex;
            flex-direction: column;
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
        <div class="system1-logo">⚡ System1</div>
        <h1>Content Monetization Flow Demo</h1>
    </div>

    <div class="tab-container">
        <button class="tab-button active" data-flow="creator1">Creator Journey: Beauty Tips</button>
        <button class="tab-button" data-flow="creator2">Creator Journey: Tech Reviews</button>
        <button class="tab-button" data-flow="creator3">Creator Journey: Fitness</button>
        <button class="tab-button" data-flow="creator4">Creator Journey: Finance</button>
        <button class="tab-button" data-flow="solar">Solar Flow Journeys</button>
    </div>

    <!-- CREATOR 1 FLOW -->
    <div class="flow-section active" id="creator1-flow">
        <div class="sticky-container">
            <div class="phone-container">
                <div class="phone phone1">
                    <div class="stage-label">Stage 1: Linktree</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="linktree">
                                <div class="profile-pic">BT</div>
                                <div class="username">@beautytips_daily</div>
                                <div class="bio">Your daily source for beauty tips, skincare routines, and makeup tutorials ✨</div>
                                <div class="social-icons">
                                    <div class="social-icon">📷</div>
                                    <div class="social-icon">🎵</div>
                                    <div class="social-icon">▶️</div>
                                </div>
                                <div class="link-button">Shop My Favorites</div>
                                <div class="link-button">YouTube Channel</div>
                                <div class="link-button highlight">Best Anti-Aging Skincare Products 2024</div>
                                <div class="link-button">TikTok</div>
                                <div class="link-button">Instagram</div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone2">
                    <div class="stage-label">Stage 2: Article</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="article">
                                <div class="article-header">
                                    <div class="article-avatar">BT</div>
                                    <div class="author-info">
                                        <h3>Beauty Tips Daily</h3>
                                        <div class="author-link">beautytips.com</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h2 class="article-title">The Ultimate Guide to Anti-Aging Skincare in 2024</h2>
                                    <p class="article-text">Discover the most effective anti-aging ingredients and routines that actually work. From retinol to vitamin C, we break down everything you need to know...</p>
                                    <p class="article-text">The key to youthful skin isn't just about expensive products - it's about consistency and using the right ingredients for your skin type.</p>
                                </div>
                                <div class="related-searches">
                                    <div class="search-title">Related searches</div>
                                    <div>
                                        <span class="search-chip">💆 Best Anti-Aging Creams</span>
                                        <span class="search-chip">✨ Retinol Products</span>
                                        <span class="search-chip">🧴 Skincare Routine 40+</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone3">
                    <div class="stage-label">Stage 3: SERP</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="serp">
                                <div class="search-bar">
                                    <span>🔍</span>
                                    <span style="flex: 1; color: #666;">Best Anti-Aging Creams</span>
                                    <span style="color: #667eea; cursor: pointer;">✕</span>
                                </div>
                                
                                <div class="serp-result">
                                    <span class="sponsored-badge">Sponsored</span>
                                    <div class="result-title">Top Dermatologist-Recommended Anti-Aging Creams</div>
                                    <div class="result-description">Compare prices and find the best anti-aging skincare products. Expert reviews, clinical results, and exclusive discounts available.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Professional Anti-Aging Solutions - Free Consultation</div>
                                    <div class="result-description">Get personalized skincare recommendations from certified dermatologists. Free skin analysis included.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Best Anti-Aging Creams 2024 - Reviews & Ratings</div>
                                    <div class="result-description">Comprehensive reviews of top-rated anti-aging creams. See real results and before/after photos.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- CREATOR 2 FLOW -->
    <div class="flow-section" id="creator2-flow">
        <div class="sticky-container">
            <div class="phone-container">
                <div class="phone phone1">
                    <div class="stage-label">Stage 1: Linktree</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="linktree blue">
                                <div class="profile-pic" style="background: #4facfe;">TR</div>
                                <div class="username">@tech_reviewer</div>
                                <div class="bio">Honest tech reviews & gadget comparisons 🔌 Helping you make smart buying decisions</div>
                                <div class="social-icons">
                                    <div class="social-icon">📱</div>
                                    <div class="social-icon">▶️</div>
                                    <div class="social-icon">🐦</div>
                                </div>
                                <div class="link-button">Latest Reviews</div>
                                <div class="link-button">Amazon Storefront</div>
                                <div class="link-button highlight-alt2">Best Budget Smartphones 2024</div>
                                <div class="link-button">Newsletter</div>
                                <div class="link-button">Support My Work</div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone2">
                    <div class="stage-label">Stage 2: Article</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="article blue">
                                <div class="article-header">
                                    <div class="article-avatar" style="background: #4facfe;">TR</div>
                                    <div class="author-info">
                                        <h3>Tech Reviewer</h3>
                                        <div class="author-link">techreviewer.com</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h2 class="article-title">Top 5 Budget Smartphones Under $500 in 2024</h2>
                                    <p class="article-text">You don't need to spend a fortune to get a great smartphone. These budget-friendly options offer flagship features at half the price...</p>
                                    <p class="article-text">From camera quality to battery life, we've tested dozens of phones to find the best value options for every budget.</p>
                                </div>
                                <div class="related-searches">
                                    <div class="search-title">Related searches</div>
                                    <div>
                                        <span class="search-chip alt2">📱 Budget Smartphones</span>
                                        <span class="search-chip alt2">💰 Best Phone Deals</span>
                                        <span class="search-chip alt2">🔋 Long Battery Phones</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone3">
                    <div class="stage-label">Stage 3: SERP</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="serp blue">
                                <div class="search-bar">
                                    <span>🔍</span>
                                    <span style="flex: 1; color: #666;">Budget Smartphones</span>
                                    <span style="color: #667eea; cursor: pointer;">✕</span>
                                </div>
                                
                                <div class="serp-result">
                                    <span class="sponsored-badge alt2">Sponsored</span>
                                    <div class="result-title">Best Smartphone Deals - Save Up to 50%</div>
                                    <div class="result-description">Compare prices from top retailers. Find the perfect budget smartphone with our price comparison tool.</div>
                                    <button class="visit-button alt2">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Budget Phones with Premium Features - Shop Now</div>
                                    <div class="result-description">Discover affordable smartphones that don't compromise on quality. Free shipping on all orders.</div>
                                    <button class="visit-button alt2">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">2024's Best Budget Smartphones - Expert Reviews</div>
                                    <div class="result-description">Detailed comparisons and honest reviews of the top budget-friendly phones available today.</div>
                                    <button class="visit-button alt2">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- CREATOR 3 FLOW -->
    <div class="flow-section" id="creator3-flow">
        <div class="sticky-container">
            <div class="phone-container">
                <div class="phone phone1">
                    <div class="stage-label">Stage 1: Linktree</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="linktree purple">
                                <div class="profile-pic" style="background: #d4a5ff;">FJ</div>
                                <div class="username">@fitness_journey</div>
                                <div class="bio">Certified trainer | Nutrition tips | Home workout routines 💪 Your fitness transformation starts here</div>
                                <div class="social-icons">
                                    <div class="social-icon">💪</div>
                                    <div class="social-icon">📷</div>
                                    <div class="social-icon">▶️</div>
                                </div>
                                <div class="link-button">Free Workout Plans</div>
                                <div class="link-button">Meal Prep Guide</div>
                                <div class="link-button highlight-alt1">Best Home Gym Equipment 2024</div>
                                <div class="link-button">1-on-1 Coaching</div>
                                <div class="link-button">Instagram</div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone2">
                    <div class="stage-label">Stage 2: Article</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="article purple">
                                <div class="article-header">
                                    <div class="article-avatar" style="background: #d4a5ff;">FJ</div>
                                    <div class="author-info">
                                        <h3>Fitness Journey</h3>
                                        <div class="author-link">fitnessjourney.com</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h2 class="article-title">Essential Home Gym Equipment for Beginners</h2>
                                    <p class="article-text">Building a home gym doesn't have to break the bank. Here are the must-have pieces of equipment to start your fitness journey...</p>
                                    <p class="article-text">From adjustable dumbbells to resistance bands, these versatile tools will help you achieve your fitness goals from the comfort of home.</p>
                                </div>
                                <div class="related-searches">
                                    <div class="search-title">Related searches</div>
                                    <div>
                                        <span class="search-chip alt1">🏋️ Home Gym Equipment</span>
                                        <span class="search-chip alt1">💪 Adjustable Dumbbells</span>
                                        <span class="search-chip alt1">🤸 Resistance Bands</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone3">
                    <div class="stage-label">Stage 3: SERP</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="serp purple">
                                <div class="search-bar">
                                    <span>🔍</span>
                                    <span style="flex: 1; color: #666;">Home Gym Equipment</span>
                                    <span style="color: #667eea; cursor: pointer;">✕</span>
                                </div>
                                
                                <div class="serp-result">
                                    <span class="sponsored-badge alt1">Sponsored</span>
                                    <div class="result-title">Complete Home Gym Sets - Free Shipping</div>
                                    <div class="result-description">Save big on premium home gym equipment. Shop adjustable dumbbells, benches, and more. Limited time offer!</div>
                                    <button class="visit-button alt1">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Best Home Gym Equipment 2024 - Expert Reviews</div>
                                    <div class="result-description">Compare top-rated home gym equipment. Read reviews from fitness professionals and verified buyers.</div>
                                    <button class="visit-button alt1">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Affordable Home Gym Setup - Budget Options</div>
                                    <div class="result-description">Build your dream home gym without breaking the bank. Curated selection of quality equipment at great prices.</div>
                                    <button class="visit-button alt1">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- CREATOR 4 FLOW -->
    <div class="flow-section" id="creator4-flow">
        <div class="sticky-container">
            <div class="phone-container">
                <div class="phone phone1">
                    <div class="stage-label">Stage 1: Linktree</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="linktree green">
                                <div class="profile-pic" style="background: #43e97b;">FA</div>
                                <div class="username">@finance_advisor</div>
                                <div class="bio">Personal finance tips | Investment strategies | Debt-free living 💰 Building wealth one step at a time</div>
                                <div class="social-icons">
                                    <div class="social-icon">💵</div>
                                    <div class="social-icon">📊</div>
                                    <div class="social-icon">▶️</div>
                                </div>
                                <div class="link-button">Free Budget Template</div>
                                <div class="link-button">Investing for Beginners</div>
                                <div class="link-button highlight-alt3">Best Credit Cards for Cashback 2024</div>
                                <div class="link-button">Debt Payoff Calculator</div>
                                <div class="link-button">YouTube</div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone2">
                    <div class="stage-label">Stage 2: Article</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="article green">
                                <div class="article-header">
                                    <div class="article-avatar" style="background: #43e97b;">FA</div>
                                    <div class="author-info">
                                        <h3>Finance Advisor</h3>
                                        <div class="author-link">financeadvisor.com</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h2 class="article-title">Maximize Your Rewards: Top Cashback Credit Cards of 2024</h2>
                                    <p class="article-text">Want to earn while you spend? These cashback credit cards offer the best rewards programs, with rates up to 5% on everyday purchases...</p>
                                    <p class="article-text">Learn how to strategically use credit cards to maximize rewards while maintaining excellent credit health and avoiding interest charges.</p>
                                </div>
                                <div class="related-searches">
                                    <div class="search-title">Related searches</div>
                                    <div>
                                        <span class="search-chip alt3">💳 Best Cashback Cards</span>
                                        <span class="search-chip alt3">🎁 Credit Card Rewards</span>
                                        <span class="search-chip alt3">✈️ Travel Rewards Cards</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone3">
                    <div class="stage-label">Stage 3: SERP</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="serp green">
                                <div class="search-bar">
                                    <span>🔍</span>
                                    <span style="flex: 1; color: #666;">Best Cashback Cards</span>
                                    <span style="color: #667eea; cursor: pointer;">✕</span>
                                </div>
                                
                                <div class="serp-result">
                                    <span class="sponsored-badge alt3">Sponsored</span>
                                    <div class="result-title">Top Cashback Credit Cards - Compare & Apply</div>
                                    <div class="result-description">Find the perfect cashback card for your spending habits. Get approved in minutes with our easy comparison tool.</div>
                                    <button class="visit-button alt3">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Best Credit Card Offers - Up to $200 Bonus</div>
                                    <div class="result-description">Exclusive sign-up bonuses on top-rated cashback cards. Start earning rewards on every purchase today.</div>
                                    <button class="visit-button alt3">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">2024 Credit Card Reviews - Expert Recommendations</div>
                                    <div class="result-description">Detailed reviews of the best cashback and rewards cards. Find the right card for your financial goals.</div>
                                    <button class="visit-button alt3">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- SOLAR FLOW SECTION -->
    <div class="flow-section" id="solar-flow">
        <div class="solar-flow-section">
            <div class="solar-flow-header">
                <h2>Solar Flow User Journeys</h2>
                <p>Multiple entry points leading to high-intent search results</p>
            </div>

            <div class="solar-entry-controls">
                <div class="solar-entry-label">Choose Entry Point:</div>
                <div class="solar-toggle-container">
                    <button class="toggle-btn active" data-solar="socials">Socials</button>
                    <button class="toggle-btn" data-solar="thankyou">Thank You Page</button>
                    <button class="toggle-btn" data-solar="disqualify">Disqualifying Offer</button>
                    <button class="toggle-btn" data-solar="linktree">Linktree</button>
                </div>
            </div>
        </div>

        <!-- SOCIALS ENTRY FLOW -->
        <div class="sticky-container solar-entry-flow active" id="solar-socials">
            <div class="phone-container-wrapper">
                <div class="phone phone1">
                    <div class="stage-label">Ad on Socials</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="social-ad-mockup">
                                <div class="facebook-ad">
                                    <div style="padding: 12px; border-bottom: 1px solid #e4e6eb;">
                                        <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 12px;">
                                            <div style="width: 40px; height: 40px; background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 18px; font-weight: 700;">S</div>
                                            <div style="flex: 1;">
                                                <div style="font-weight: 600; font-size: 15px; color: #050505;">SolarFlow</div>
                                                <div style="font-size: 13px; color: #65676b;">Sponsored · Utility ID: 4398841102783837</div>
                                            </div>
                                        </div>
                                        <div style="font-size: 15px; color: #050505; line-height: 1.3; margin-bottom: 12px;">
                                            Thinking about solar for your home? Learn about the potential benefits and see if solar might be a good fit for your situation. Every home is different - find out what's right for you.
                                        </div>
                                    </div>
                                    <div style="position: relative; background: #000; padding-top: 75%; overflow: hidden;">
                                        <img src="https://images.unsplash.com/photo-1509391366360-2e959784a276?w=600&h=450&fit=crop" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover;">
                                        <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); width: 60px; height: 60px; background: rgba(255,255,255,0.95); border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer; box-shadow: 0 2px 12px rgba(0,0,0,0.3);">
                                            <div style="width: 0; height: 0; border-left: 18px solid #333; border-top: 12px solid transparent; border-bottom: 12px solid transparent; margin-left: 4px;"></div>
                                        </div>
                                    </div>
                                    <div style="padding: 12px; background: #f0f2f5;">
                                        <div style="font-weight: 600; font-size: 14px; color: #050505; margin-bottom: 4px;">Learn How Solar Energy Reduces Costs and Boosts Home Value</div>
                                        <div style="font-size: 12px; color: #65676b; margin-bottom: 12px;">Get information and see what might work for your situation.</div>
                                        <button style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border: none; padding: 10px 20px; border-radius: 6px; font-weight: 600; font-size: 15px; width: 100%; cursor: pointer;">Learn More</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone2">
                    <div class="stage-label">Content Page with Keyword Block</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="article solar">
                                <div class="article-header">
                                    <div class="article-avatar" style="background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%);">🌟</div>
                                    <div class="author-info">
                                        <h3>Nation</h3>
                                        <div class="author-link">@nationnews</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h2 class="article-title">How Solar Energy Reduces Costs and Boosts Home Value</h2>
                                    <div style="font-size: 11px; color: #666; margin-bottom: 15px;">By Nikki Cross · Jan 8, 2025</div>
                                    <p class="article-text">Solar energy presents an exceptional opportunity for American homeowners to realize significant financial savings alongside environmental benefits. By reducing electricity bills and potentially increasing property values, solar panels offer a versatile solution to lower energy consumption.</p>
                                    <p class="article-text">With incentives available to mitigate initial costs and community solar projects providing accessible alternatives, solar power serves as an efficient and sustainable choice for diverse households. Examine the factors shaping solar's appeal and discover its transformative impact on energy use and household economics.</p>
                                </div>
                                <div class="related-searches">
                                    <div class="search-title">Related searches</div>
                                    <div>
                                        <span class="search-chip">☀️ Solar Panel Installation</span>
                                        <span class="search-chip">🏘️ Residential Solar Panels Near Me</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone3">
                    <div class="stage-label">SERP (Monetization Event)</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="serp solar">
                                <div class="search-bar">
                                    <span>🔍</span>
                                    <span style="flex: 1; color: #666;">Solar Panel Installation</span>
                                    <span style="color: #667eea; cursor: pointer;">✕</span>
                                </div>
                                
                                <div class="serp-result">
                                    <span class="sponsored-badge">Ad</span>
                                    <div class="result-title">Miracula: 90,000 more jobs - Austen boosts careers - Commitment to the future</div>
                                    <div class="result-description">Sponsored · https://www.austenrenewables.com.br Austen Renewables will create opportunities for the local economy through Suncable. Advancing local development with renewable energy innovation and sustainability, Aus Austen Renewables</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Just Enter Your Zip Code - Lighting Experts</div>
                                    <div class="result-description">Sponsored · https://www.homesadviser.com/electrical Real reviews, view cost estimates, and get matched with electricians near you.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Why Homes Need Energy Audits - Boost Home Energy Savings Tips</div>
                                    <div class="result-description">Sponsored · https://www.arenepedia.com/energy_audit/upgrades Maximize Energy Efficiency In Your Home With A Professional Audit That Finds Hidden Waste.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- THANK YOU PAGE ENTRY FLOW -->
        <div class="sticky-container solar-entry-flow" id="solar-thankyou">
            <div class="phone-container-wrapper">
                <div class="phone phone1">
                    <div class="stage-label">Thank You Page</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content" style="background: linear-gradient(180deg, #e8f5e9 0%, #c8e6c9 100%); padding: 20px;">
                            <div style="text-align: center; padding-top: 40px;">
                                <div style="width: 80px; height: 80px; background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%); border-radius: 50%; margin: 0 auto 20px; display: flex; align-items: center; justify-content: center; font-size: 40px;">✅</div>
                                <h2 style="font-size: 28px; font-weight: 700; margin-bottom: 20px; color: #1b5e20;">Thank You!</h2>
                                <p style="font-size: 16px; color: #2e7d32; margin-bottom: 30px; line-height: 1.5;">Your solar inquiry will call Soon, Alex!</p>
                                
                                <div style="background: white; padding: 16px; border-radius: 16px; margin-bottom: 20px; text-align: left; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
                                    <div style="display: flex; align-items: center; gap: 8px; color: #1565c0; margin-bottom: 8px;">
                                        <span>📞</span>
                                        <span style="font-size: 14px; font-weight: 600;">Please don't miss the call!</span>
                                    </div>
                                    <p style="font-size: 13px; color: #666; margin: 0;">The expert won't be able to provide you the estimate if you miss it.</p>
                                </div>

                                <div style="background: white; padding: 20px; border-radius: 16px; margin-bottom: 20px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
                                    <h3 style="font-size: 16px; font-weight: 600; margin-bottom: 16px; color: #333;">What's next?</h3>
                                    <div style="text-align: left; font-size: 13px; color: #666; line-height: 1.6;">
                                        <p style="margin-bottom: 8px;">Your solar panel expert will reach you for reach info by phone, if no answer from you — you'll receive a text with link to schedule your solar installation call.</p>
                                        <p style="margin: 0;">No obligation - you're not tied to anything.</p>
                                    </div>
                                </div>

                                <div style="background: white; padding: 16px; border-radius: 16px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
                                    <h3 style="font-size: 14px; font-weight: 600; margin-bottom: 12px; color: #333;">You may also like:</h3>
                                    <div style="display: flex; gap: 12px; margin-bottom: 16px;">
                                        <div style="flex: 1; text-align: center;">
                                            <div style="width: 60px; height: 60px; background: #e3f2fd; border-radius: 50%; margin: 0 auto 8px; display: flex; align-items: center; justify-content: center; font-size: 24px;">💧</div>
                                            <div style="font-size: 11px; font-weight: 600; margin-bottom: 6px; color: #333;">Save your roof from repairs?</div>
                                            <button style="background: #4caf50; color: white; border: none; padding: 6px 12px; border-radius: 12px; font-size: 11px; font-weight: 600;">Learn More</button>
                                        </div>
                                        <div style="flex: 1; text-align: center;">
                                            <div style="width: 60px; height: 60px; background: #fff3e0; border-radius: 50%; margin: 0 auto 8px; display: flex; align-items: center; justify-content: center; font-size: 24px;">💰</div>
                                            <div style="font-size: 11px; font-weight: 600; margin-bottom: 6px; color: #333;">Need cash fast? Same-day?</div>
                                            <button style="background: #4caf50; color: white; border: none; padding: 6px 12px; border-radius: 12px; font-size: 11px; font-weight: 600;">Learn More</button>
                                        </div>
                                        <div style="flex: 1; text-align: center;">
                                            <div style="width: 60px; height: 60px; background: #fce4ec; border-radius: 50%; margin: 0 auto 8px; display: flex; align-items: center; justify-content: center; font-size: 24px;">🏆</div>
                                            <div style="font-size: 11px; font-weight: 600; margin-bottom: 6px; color: #333;">Interested in your credit score?</div>
                                            <button style="background: #4caf50; color: white; border: none; padding: 6px 12px; border-radius: 12px; font-size: 11px; font-weight: 600;">Learn More</button>
                                        </div>
                                    </div>
                                    <button style="background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%); color: white; border: none; padding: 12px; border-radius: 12px; font-size: 14px; font-weight: 600; width: 100%; cursor: pointer;">Learn More About Solar Benefits</button>
                                </div>

                                <div style="margin-top: 24px; display: flex; align-items: center; justify-content: center; gap: 8px;">
                                    <span style="color: #ffa000;">⭐⭐⭐⭐⭐</span>
                                    <span style="font-size: 12px; color: #666;">4.8/5 (2536 reviews)</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone2">
                    <div class="stage-label">Content Page with Keyword Block</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="article solar">
                                <div class="article-header">
                                    <div class="article-avatar" style="background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%);">🌟</div>
                                    <div class="author-info">
                                        <h3>Nation</h3>
                                        <div class="author-link">@nationnews</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h2 class="article-title">How Solar Energy Reduces Costs and Boosts Home Value</h2>
                                    <div style="font-size: 11px; color: #666; margin-bottom: 15px;">By Nikki Cross · Jan 8, 2025</div>
                                    <p class="article-text">Solar energy presents an exceptional opportunity for American homeowners to realize significant financial savings alongside environmental benefits. By reducing electricity bills and potentially increasing property values, solar panels offer a versatile solution to lower energy consumption.</p>
                                    <p class="article-text">With incentives available to mitigate initial costs and community solar projects providing accessible alternatives, solar power serves as an efficient and sustainable choice for diverse households. Examine the factors shaping solar's appeal and discover its transformative impact on energy use and household economics.</p>
                                </div>
                                <div class="related-searches">
                                    <div class="search-title">Related searches</div>
                                    <div>
                                        <span class="search-chip">☀️ Solar Panel Installation</span>
                                        <span class="search-chip">🏘️ Residential Solar Panels Near Me</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone3">
                    <div class="stage-label">SERP (Monetization Event)</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="serp solar">
                                <div class="search-bar">
                                    <span>🔍</span>
                                    <span style="flex: 1; color: #666;">Solar Panel Installation</span>
                                    <span style="color: #667eea; cursor: pointer;">✕</span>
                                </div>
                                
                                <div class="serp-result">
                                    <span class="sponsored-badge">Ad</span>
                                    <div class="result-title">Miracula: 90,000 more jobs - Austen boosts careers - Commitment to the future</div>
                                    <div class="result-description">Sponsored · https://www.austenrenewables.com.br Austen Renewables will create opportunities for the local economy through Suncable. Advancing local development with renewable energy innovation and sustainability, Aus Austen Renewables</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Just Enter Your Zip Code - Lighting Experts</div>
                                    <div class="result-description">Sponsored · https://www.homesadviser.com/electrical Real reviews, view cost estimates, and get matched with electricians near you.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Why Homes Need Energy Audits - Boost Home Energy Savings Tips</div>
                                    <div class="result-description">Sponsored · https://www.arenepedia.com/energy_audit/upgrades Maximize Energy Efficiency In Your Home With A Professional Audit That Finds Hidden Waste.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- DISQUALIFYING OFFER ENTRY FLOW -->
        <div class="sticky-container solar-entry-flow" id="solar-disqualify">
            <div class="phone-container-wrapper">
                <div class="phone phone1">
                    <div class="stage-label">Disqualifying Offer</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content" style="background: linear-gradient(180deg, #f3e5f5 0%, #e1bee7 100%); padding: 20px;">
                            <div style="background: white; border-radius: 20px; padding: 24px; margin-top: 40px; box-shadow: 0 4px 12px rgba(0,0,0,0.1);">
                                <div style="text-align: center; margin-bottom: 24px;">
                                    <div style="width: 60px; height: 60px; background: linear-gradient(135deg, #d4a5ff 0%, #e8c4ff 100%); border-radius: 50%; margin: 0 auto 16px; display: flex; align-items: center; justify-content: center; font-size: 28px;">❌</div>
                                    <h2 style="font-size: 22px; font-weight: 700; margin-bottom: 12px; color: #333;">We Found Great Alternatives!</h2>
                                    <p style="font-size: 14px; color: #666; line-height: 1.5;">While solar panels might not be the perfect fit, we have other excellent energy solutions for you.</p>
                                </div>

                                <div style="margin-bottom: 20px;">
                                    <div style="background: #f5f5f5; padding: 16px; border-radius: 12px; margin-bottom: 16px;">
                                        <div style="display: flex; align-items: center; gap: 12px; margin-bottom: 12px;">
                                            <div style="width: 50px; height: 50px; background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); border-radius: 12px; display: flex; align-items: center; justify-content: center; font-size: 24px;">🌳</div>
                                            <div style="flex: 1;">
                                                <h3 style="font-size: 16px; font-weight: 600; margin-bottom: 4px; color: #333;">Tree Trimming Service</h3>
                                                <p style="font-size: 12px; color: #666; margin: 0;">Interested in getting a quote for tree trimming? Discover various available.</p>
                                            </div>
                                        </div>
                                        <div style="padding-left: 8px; font-size: 12px; color: #666; line-height: 1.5;">
                                            <div style="margin-bottom: 4px;">✅ Improve home aesthetics</div>
                                            <div style="margin-bottom: 4px;">✅ Property maintenance tips</div>
                                            <div style="margin-bottom: 4px;">✅ Connect with local arborists</div>
                                        </div>
                                        <button style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border: none; padding: 12px; border-radius: 12px; font-size: 14px; font-weight: 600; width: 100%; margin-top: 12px; cursor: pointer;">Learn More</button>
                                    </div>

                                    <div style="background: #f5f5f5; padding: 16px; border-radius: 12px;">
                                        <div style="display: flex; align-items: center; gap: 12px; margin-bottom: 12px;">
                                            <div style="width: 50px; height: 50px; background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%); border-radius: 12px; display: flex; align-items: center; justify-content: center; font-size: 24px;">🏠</div>
                                            <div style="flex: 1;">
                                                <h3 style="font-size: 16px; font-weight: 600; margin-bottom: 4px; color: #333;">Home Financing</h3>
                                                <p style="font-size: 12px; color: #666; margin: 0;">You could explore Home Equity Line of Credit options to finance property improvements.</p>
                                            </div>
                                        </div>
                                        <div style="padding-left: 8px; font-size: 12px; color: #666; line-height: 1.5;">
                                            <div style="margin-bottom: 4px;">✅ Learn about interest rates</div>
                                            <div style="margin-bottom: 4px;">✅ Explore access to funds</div>
                                            <div style="margin-bottom: 4px;">✅ Understand tax advantages</div>
                                        </div>
                                        <button style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border: none; padding: 12px; border-radius: 12px; font-size: 14px; font-weight: 600; width: 100%; margin-top: 12px; cursor: pointer;">Learn More</button>
                                    </div>
                                </div>

                                <p style="font-size: 11px; color: #999; text-align: center; margin-top: 20px;">You could still save money and improve your home!</p>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone2">
                    <div class="stage-label">Content Page with Keyword Block</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="article solar">
                                <div class="article-header">
                                    <div class="article-avatar" style="background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%);">🌟</div>
                                    <div class="author-info">
                                        <h3>Nation</h3>
                                        <div class="author-link">@nationnews</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h2 class="article-title">How Solar Energy Reduces Costs and Boosts Home Value</h2>
                                    <div style="font-size: 11px; color: #666; margin-bottom: 15px;">By Nikki Cross · Jan 8, 2025</div>
                                    <p class="article-text">Solar energy presents an exceptional opportunity for American homeowners to realize significant financial savings alongside environmental benefits. By reducing electricity bills and potentially increasing property values, solar panels offer a versatile solution to lower energy consumption.</p>
                                    <p class="article-text">With incentives available to mitigate initial costs and community solar projects providing accessible alternatives, solar power serves as an efficient and sustainable choice for diverse households. Examine the factors shaping solar's appeal and discover its transformative impact on energy use and household economics.</p>
                                </div>
                                <div class="related-searches">
                                    <div class="search-title">Related searches</div>
                                    <div>
                                        <span class="search-chip">☀️ Solar Panel Installation</span>
                                        <span class="search-chip">🏘️ Residential Solar Panels Near Me</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone3">
                    <div class="stage-label">SERP (Monetization Event)</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="serp solar">
                                <div class="search-bar">
                                    <span>🔍</span>
                                    <span style="flex: 1; color: #666;">Solar Panel Installation</span>
                                    <span style="color: #667eea; cursor: pointer;">✕</span>
                                </div>
                                
                                <div class="serp-result">
                                    <span class="sponsored-badge">Ad</span>
                                    <div class="result-title">Miracula: 90,000 more jobs - Austen boosts careers - Commitment to the future</div>
                                    <div class="result-description">Sponsored · https://www.austenrenewables.com.br Austen Renewables will create opportunities for the local economy through Suncable. Advancing local development with renewable energy innovation and sustainability, Aus Austen Renewables</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Just Enter Your Zip Code - Lighting Experts</div>
                                    <div class="result-description">Sponsored · https://www.homesadviser.com/electrical Real reviews, view cost estimates, and get matched with electricians near you.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Why Homes Need Energy Audits - Boost Home Energy Savings Tips</div>
                                    <div class="result-description">Sponsored · https://www.arenepedia.com/energy_audit/upgrades Maximize Energy Efficiency In Your Home With A Professional Audit That Finds Hidden Waste.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- LINKTREE ENTRY FLOW -->
        <div class="sticky-container solar-entry-flow" id="solar-linktree">
            <div class="phone-container-wrapper">
                <div class="phone phone1">
                    <div class="stage-label">Linktree</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="linktree" style="background: linear-gradient(180deg, #ffeaa7 0%, #fdcb6e 100%);">
                                <div class="profile-pic" style="background: white; width: 100px; height: 100px; margin-top: 30px;">
                                    <span style="font-size: 40px; font-weight: 700; color: #f39c12;">S</span>
                                </div>
                                <div class="username" style="font-size: 24px; font-weight: 700; color: #333;">SolarSavr</div>
                                <div style="display: flex; gap: 15px; margin-bottom: 20px; justify-content: center;">
                                    <div class="social-icon" style="background: white; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">📷</div>
                                    <div class="social-icon" style="background: white; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">🎵</div>
                                    <div class="social-icon" style="background: white; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">👍</div>
                                    <div class="social-icon" style="background: white; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">☁️</div>
                                </div>

                                <div style="width: 100%; max-width: 300px; padding: 0 20px;">
                                    <div style="position: relative; width: 100%; padding-top: 56.25%; background: white; border-radius: 12px; overflow: hidden; margin-bottom: 20px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);">
                                        <img src="https://images.unsplash.com/photo-1509391366360-2e959784a276?w=600&h=338&fit=crop" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover;">
                                        <div style="position: absolute; bottom: 12px; left: 12px; right: 12px; color: white; text-shadow: 0 2px 4px rgba(0,0,0,0.5);">
                                            <div style="font-size: 13px; font-weight: 600; line-height: 1.3;">How Solar Energy Reduces Costs and Boosts Home Value</div>
                                        </div>
                                    </div>

                                    <button class="link-button" style="background: white; color: #333; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">Instagram</button>
                                    <button class="link-button" style="background: white; color: #333; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">TikTok</button>
                                    <button class="link-button" style="background: white; color: #333; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">Facebook</button>
                                    <button class="link-button highlight-alt3" style="margin-top: 16px;">Linktree🔗</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone2">
                    <div class="stage-label">Content Page with Keyword Block</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="article solar">
                                <div class="article-header">
                                    <div class="article-avatar" style="background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%);">🌟</div>
                                    <div class="author-info">
                                        <h3>Nation</h3>
                                        <div class="author-link">@nationnews</div>
                                    </div>
                                </div>
                                <div class="article-content-block">
                                    <h2 class="article-title">How Solar Energy Reduces Costs and Boosts Home Value</h2>
                                    <div style="font-size: 11px; color: #666; margin-bottom: 15px;">By Nikki Cross · Jan 8, 2025</div>
                                    <p class="article-text">Solar energy presents an exceptional opportunity for American homeowners to realize significant financial savings alongside environmental benefits. By reducing electricity bills and potentially increasing property values, solar panels offer a versatile solution to lower energy consumption.</p>
                                    <p class="article-text">With incentives available to mitigate initial costs and community solar projects providing accessible alternatives, solar power serves as an efficient and sustainable choice for diverse households. Examine the factors shaping solar's appeal and discover its transformative impact on energy use and household economics.</p>
                                </div>
                                <div class="related-searches">
                                    <div class="search-title">Related searches</div>
                                    <div>
                                        <span class="search-chip">☀️ Solar Panel Installation</span>
                                        <span class="search-chip">🏘️ Residential Solar Panels Near Me</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="arrow">→</div>

                <div class="phone phone3">
                    <div class="stage-label">SERP (Monetization Event)</div>
                    <div class="phone-screen">
                        <div class="phone-notch"></div>
                        <div class="phone-content">
                            <div class="serp solar">
                                <div class="search-bar">
                                    <span>🔍</span>
                                    <span style="flex: 1; color: #666;">Solar Panel Installation</span>
                                    <span style="color: #667eea; cursor: pointer;">✕</span>
                                </div>
                                
                                <div class="serp-result">
                                    <span class="sponsored-badge">Ad</span>
                                    <div class="result-title">Miracula: 90,000 more jobs - Austen boosts careers - Commitment to the future</div>
                                    <div class="result-description">Sponsored · https://www.austenrenewables.com.br Austen Renewables will create opportunities for the local economy through Suncable. Advancing local development with renewable energy innovation and sustainability, Aus Austen Renewables</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Just Enter Your Zip Code - Lighting Experts</div>
                                    <div class="result-description">Sponsored · https://www.homesadviser.com/electrical Real reviews, view cost estimates, and get matched with electricians near you.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>

                                <div class="serp-result">
                                    <div class="result-title">Why Homes Need Energy Audits - Boost Home Energy Savings Tips</div>
                                    <div class="result-description">Sponsored · https://www.arenepedia.com/energy_audit/upgrades Maximize Energy Efficiency In Your Home With A Professional Audit That Finds Hidden Waste.</div>
                                    <button class="visit-button">Visit Website</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="footer">
        <h2>Ready to Explore More?</h2>
        <p>Discover how System1 can help monetize your content</p>
    </div>

    <script>
        // Tab switching for main sections
        document.querySelectorAll('.tab-button').forEach(button => {
            button.addEventListener('click', () => {
                // Update active button
                document.querySelectorAll('.tab-button').forEach(b => b.classList.remove('active'));
                button.classList.add('active');
                
                // Update active flow section
                document.querySelectorAll('.flow-section').forEach(s => s.classList.remove('active'));
                const flowId = button.getAttribute('data-flow');
                document.getElementById(`${flowId}-flow`).classList.add('active');
                
                // Reset scroll position
                window.scrollTo(0, 0);
            });
        });

        // Solar entry point switching
        document.querySelectorAll('.toggle-btn').forEach(button => {
            button.addEventListener('click', () => {
                const solarType = button.getAttribute('data-solar');
                
                // Update active button
                document.querySelectorAll('.toggle-btn').forEach(b => b.classList.remove('active'));
                button.classList.add('active');
                
                // Update active solar flow
                document.querySelectorAll('.solar-entry-flow').forEach(f => f.classList.remove('active'));
                document.getElementById(`solar-${solarType}`).classList.add('active');
                
                // Trigger animation
                setTimeout(() => {
                    document.querySelectorAll(`#solar-${solarType} .phone`).forEach((phone, index) => {
                        setTimeout(() => {
                            phone.classList.add('visible');
                        }, index * 200);
                    });
                    document.querySelectorAll(`#solar-${solarType} .arrow`).forEach((arrow, index) => {
                        setTimeout(() => {
                            arrow.classList.add('visible');
                        }, (index * 200) + 400);
                    });
                }, 100);
            });
        });

        // Scroll-based animations for all flows
        const observerOptions = {
            threshold: 0.3,
            rootMargin: '0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.querySelectorAll('.phone').forEach((phone, index) => {
                        setTimeout(() => {
                            phone.classList.add('visible');
                        }, index * 200);
                    });
                    entry.target.querySelectorAll('.arrow').forEach((arrow, index) => {
                        setTimeout(() => {
                            arrow.classList.add('visible');
                        }, (index * 200) + 400);
                    });
                }
            });
        }, observerOptions);

        // Observe all sticky containers
        document.querySelectorAll('.sticky-container').forEach(container => {
            observer.observe(container);
        });

        // Initialize first flow
        document.querySelector('#creator1-flow .sticky-container').querySelectorAll('.phone').forEach((phone, index) => {
            setTimeout(() => {
                phone.classList.add('visible');
            }, index * 200 + 500);
        });
        document.querySelector('#creator1-flow .sticky-container').querySelectorAll('.arrow').forEach((arrow, index) => {
            setTimeout(() => {
                arrow.classList.add('visible');
            }, (index * 200) + 900);
        });

        // Initialize first solar flow entry (socials)
        setTimeout(() => {
            const firstSolarFlow = document.querySelector('#solar-socials');
            if (firstSolarFlow) {
                firstSolarFlow.querySelectorAll('.phone').forEach((phone, index) => {
                    setTimeout(() => {
                        phone.classList.add('visible');
                    }, index * 200);
                });
                firstSolarFlow.querySelectorAll('.arrow').forEach((arrow, index) => {
                    setTimeout(() => {
                        arrow.classList.add('visible');
                    }, (index * 200) + 400);
                });
            }
        }, 500);
    </script>
</body>
</html>
