<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Combined Project: Monetizing Content & SolarFlow</title>

    <meta name="description" content="Interactive demonstration of user journeys for both content monetization and solar panel marketing flows.">
    <meta name="keywords" content="content monetization, creators, solar panels, solar energy, user journey, marketing flow, lead generation">

    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='0.9em' font-size='90'>💡</text></svg>" type="image/svg+xml">

    <style>
        /* ============================================
           MERGED CSS STYLES
           ============================================ */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            /* Project 1 Gradient Background */
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            background-attachment: fixed;
            overflow-x: hidden;
            min-height: 100vh;
        }

        /* Project 1 Styles */
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
            /* Added padding-top to separate from main header on large screens */
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
        
        /* NOTE: .phone-screen selector exists in BOTH CSS blocks, Project 1's is more specific here */

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

        /* Merged Toggle Button Style Conflict - Project 1 version kept due to usage */
        /* .toggle-btn style from Project 1 is kept for main tabs */
        /* .toggle-btn style from Project 2 is more specific and only appears in the appended content */
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
        
        /* Using the Project 1 active style for the SolarFlow section as well */
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
        
        /* Merged Media Queries (Project 1) */
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

        /* Project 2 Overriding/Additional Styles (only a few kept for a non-iframe, simple display) */
        /* NOTE: The elaborate mobile scrolling logic from Project 2 CSS is intentionally omitted
           as it relies on a multi-stage layout and external files that can't be merged easily. 
           We're keeping only the essential styles for the SolarFlow content itself. */
        
        .flow-container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            background: white; /* Added white background for the SolarFlow content block */
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            margin-top: 40px;
            padding-bottom: 40px;
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

        .phone-frame {
            background: #1f1f1f;
            border-radius: 35px;
            padding: 8px;
            margin: 5px auto; 
            width: 300px;
            height: 650px;
            position: relative;
            box-shadow: 0 15px 40px rgba(0,0,0,0.3);
        }
        
        .phone-frame .phone-screen {
             border-radius: 27px; /* Override Project 1 inner border-radius */
        }
        
        .page-iframe {
            /* This is the critical scaling to make a larger page fit inside a small phone frame */
            width: 430px;
            height: 932px;
            border: none;
            border-radius: 27px;
            transform: scale(0.675);
            transform-origin: center center;
            position: absolute;
            top: 50%;
            left: 50%;
            margin-left: -215px;
            margin-top: -466px;
        }

        /* SolarFlow Mobile Mockup Styles */
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
        
        /* The rest of the Project 2 mock-up styles are included in the HTML inline or below the main media query block in Project 1's code. */
        
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
        <button class="tab-button" onclick="switchTab('solarflow')">SolarFlow Demo</button>
    </div>

    <div class="container">
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
    
    <div class="container solar-flow-section" id="solarflow">
        <div class="flow-section active" style="min-height: 100vh;"> 
            <div class="flow-container" style="background: white;">
                <div class="page-title">
                    <h1>SolarFlow Demo</h1>
                    <a href="#" class="path-button">Flow Demo</a>
                </div>
                
                <div class="flow-stages" style="display: flex; gap: 40px; justify-content: center; flex-wrap: wrap;">
                    
                    <div class="flow-stage" style="min-width: 350px; max-width: 400px; padding: 20px; box-shadow: 0 5px 15px rgba(0,0,0,0.1);">
                        <div class="stage-header">
                            <h2 class="stage-title" id="stage1-title">Ad on Socials</h2>
                            <div class="stage-toggle-buttons">
                                <button class="toggle-btn active" onclick="showSolarView('social', this)">Socials</button>
                                <button class="toggle-btn" onclick="showSolarView('thankyou', this)">Thank You Page</button>
                                <button class="toggle-btn" onclick="showSolarView('disqualify', this)">Disqualifying Offer</button>
                                <button class="toggle-btn" onclick="showSolarView('linktree', this)">Linktree</button>
                            </div>
                        </div>
    
                        <div class="phone-frame">
                            <div class="phone-screen">
                                <div id="solarflow-content-area" class="page-iframe" style="position: static; width: 100%; height: 100%; transform: scale(1); margin: 0; background: #f0f2f5; display: block; overflow: hidden;">
                                    <div id="social-mockup" class="social-ad-mockup" style="display: block; width: 100%; height: 100%;">
                                        <div class="facebook-ad">
                                             <div class="fb-header">
                                                <div class="fb-profile">
                                                    <div class="fb-avatar">
                                                        
                                                    </div>
                                                    <div class="fb-info">
                                                        <div class="fb-name">SolarFlow</div>
                                                        <div class="fb-sponsored">Sponsored</div>
                                                    </div>
                                                </div>
                                                <div class="fb-menu">⋯</div>
                                            </div>
                                            <div class="fb-content"><p class="fb-text">Thinking about solar for your home? Learn about the potential benefits...</p></div>
                                            <div class="fb-media" style="background: #ccc; min-height: 400px; display: flex; align-items: center; justify-content: center;">
                                                
                                            </div>
                                            <div class="fb-cta">
                                                <div class="fb-cta-text">
                                                    <div class="fb-headline">Learn How Solar Energy Reduces Costs and Boosts Home Value</div>
                                                </div>
                                                <button class="fb-learn-more">Learn More</button>
                                            </div>
                                        </div>
                                    </div>
                                    <div id="thankyou-mockup" style="display: none; padding: 50px; text-align: center; background: linear-gradient(180deg, #d4edda 0%, #c3e6cb 100%); height: 100%;">
                                        <h2 style="color: #155724;">Thank You!</h2><p style="color: #155724; margin-top: 20px;">Your solar eligibility is confirmed. Now read our educational article.</p>
                                        <button style="background: #28a745; color: white; padding: 10px 20px; border: none; border-radius: 20px; margin-top: 30px;">Read Article</button>
                                    </div>
                                    <div id="disqualify-mockup" style="display: none; padding: 50px; text-align: center; background: linear-gradient(180deg, #f8d7da 0%, #f5c6cb 100%); height: 100%;">
                                        <h2 style="color: #721c24;">Sorry!</h2><p style="color: #721c24; margin-top: 20px;">You did not qualify for a quote. Read this content instead to learn more.</p>
                                        <button style="background: #dc3545; color: white; padding: 10px 20px; border: none; border-radius: 20px; margin-top: 30px;">Educational Content</button>
                                    </div>
                                    <div id="linktree-mockup" class="linktree-mockup" style="display: none; width: 100%; height: 100%;">
                                        <div class="linktree-container">
                                            <div class="linktree-header">
                                                
                                                <div class="linktree-name">Solar Guru</div>
                                                <div class="linktree-bio">Eco-enthusiast showing you how to save with clean energy!</div>
                                            </div>
                                            <div class="linktree-links">
                                                <div class="linktree-link content-page-link" style="background: #f5a623 !important; color: white !important;">How Solar Energy Reduces Costs (Content Link)</div>
                                                <div class="linktree-link">Get a Free Solar Quote</div>
                                                <div class="linktree-link">Watch our latest video</div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
    
                        <div class="key-terms">
                            <h3 class="section-title" id="stage1-description-title" style="margin-bottom: 15px;">Option Description</h3>
                            <div class="option-description" id="stage1-description-text" style="background: #f8f9fa; padding: 15px; border-radius: 8px; border-left: 4px solid #f5a623; margin-bottom: 15px;">
                                <p style="margin: 0; color: #555; line-height: 1.6;">Learn More button links out to content page.</p>
                            </div>
                        </div>
                    </div>
    
                    <div class="flow-stage" style="min-width: 350px; max-width: 400px; padding: 20px; box-shadow: 0 5px 15px rgba(0,0,0,0.1);">
                        <div class="stage-header">
                            <h2 class="stage-title">Content Page with Keyword Block</h2>
                        </div>
                        
                        <div class="phone-frame">
                            <div class="phone-screen">
                                <div id="content-page-mockup" style="width: 100%; height: 100%; padding: 20px; overflow-y: auto;">
                                    <h1 style="font-size: 20px; margin-bottom: 15px;">How Solar Energy Reduces Costs and Boosts Home Value</h1>
                                    <p style="font-size: 14px; margin-bottom: 15px;">Installing solar panels drastically cuts down on monthly electricity bills, providing significant long-term savings. The initial investment often pays for itself within a few years through reduced utility costs.</p>
                                    <div class="related-searches" style="margin-top: 20px; border: none; box-shadow: none; padding: 0;">
                                        <div class="search-title">Related Searches</div>
                                        <div class="search-chip" style="color: white; background: #5865f2;">Solar Panel Installation</div>
                                        <div class="search-chip" style="color: white; background: #5865f2;">Residential Solar Panels Near Me</div>
                                        <div class="search-chip" style="color: white; background: #5865f2;">Solar Panel Energy Savings</div>
                                    </div>
                                    <p style="font-size: 14px; margin-top: 15px;">Beyond savings, solar installations are shown to increase a home's market value, often attracting buyers interested in sustainable living and lower operating costs.</p>
                                </div>
                            </div>
                        </div>
    
                        <div class="key-terms">
                            <h3 class="section-title">Keyword Block (RSOC)</h3>
                            <div class="option-description" style="background: #f8f9fa; padding: 15px; border-radius: 8px; border-left: 4px solid #5865f2; margin-bottom: 15px;">
                                <p style="margin: 0; color: #555; line-height: 1.6;">User clicks a keyword (e.g., "Residential Solar Panels Near Me") to navigate to the search results page (SERP).</p>
                            </div>
                        </div>
                    </div>
    
                    <div class="flow-stage" style="min-width: 350px; max-width: 400px; padding: 20px; box-shadow: 0 5px 15px rgba(0,0,0,0.1);">
                        <div class="stage-header">
                            <h2 class="stage-title">SERP (Search Engine Results Page)</h2>
                        </div>
    
                        <div class="phone-frame">
                            <div class="phone-screen">
                                <div id="serp-mockup" class="serp solar phone-content" style="background: linear-gradient(180deg, #ffeaa7 0%, #fdcb6e 100%); height: 100%;">
                                    <div class="search-bar">🔍 Residential Solar Panels Near Me</div>
                                    
                                    <div class="serp-result">
                                        <div class="sponsored-badge">Sponsored</div>
                                        <div class="result-url">nation.com</div>
                                        <div class="result-title">Get a Free Solar Quote for Your Home</div>
                                        <div class="result-description">See how much you can save with a top-rated solar installer near you. Quick & free online check.</div>
                                        <button class="visit-button">Visit Website</button>
                                    </div>
    
                                    <div class="serp-result">
                                        <div class="result-url">solarenergycorp.com</div>
                                        <div class="result-title">Top Solar Panel Installers 2024</div>
                                        <div class="result-description">Compare local companies and find the best fit. Read customer reviews.</div>
                                    </div>
                                </div>
                            </div>
                        </div>
    
                        <div class="key-terms">
                            <h3 class="section-title">Monetization Event</h3>
                            <div class="option-description" style="background: #f8f9fa; padding: 15px; border-radius: 8px; border-left: 4px solid #0e50c4; margin-bottom: 15px;">
                                <p style="margin: 0; color: #555; line-height: 1.6;">A user clicks on the <strong>Visit Website</strong> button. This is the monetization event (RPC).</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <div class="footer">
        <h2>Ready to Combine & Publish?</h2>
        <p>Follow the steps below to make this a live page on GitHub!</p>
    </div>

    <script>
        // Project 1 Tab Switching Logic
        function switchTab(tabId) {
            // Hide all flow sections
            document.querySelectorAll('.flow-section').forEach(section => {
                section.classList.remove('active');
                section.style.display = 'none';
            });

            // Show the selected flow section
            const activeSection = document.getElementById(tabId);
            if (activeSection) {
                activeSection.classList.add('active');
                activeSection.style.display = 'block';
                
                // Special handling for the SolarFlow section to reduce its height on screen if needed
                if (tabId === 'solarflow') {
                    // This section has its own layout, ensure it's positioned correctly
                    activeSection.style.minHeight = '100vh';
                } else {
                    // Restore original height for scrolling sections
                    activeSection.style.minHeight = '400vh'; 
                }
            }

            // Update tab button active state
            document.querySelectorAll('.tab-button').forEach(button => {
                button.classList.remove('active');
                if (button.getAttribute('onclick').includes(`'${tabId}'`)) {
                    button.classList.add('active');
                }
            });

            // Make the first phone in the new tab visible right away
            const firstPhone = activeSection.querySelector('.phone1');
            if (firstPhone) {
                firstPhone.classList.add('visible');
            }
            // And remove the visibility class from all phones that are not the first
            document.querySelectorAll('.flow-section:not(#' + tabId + ') .phone').forEach(phone => {
                phone.classList.remove('visible');
            });
        }

        // Project 1 Scroll Visibility Logic (slightly modified to use display: block/none for phones)
        function checkScrollVisibility() {
            const sections = document.querySelectorAll('.flow-section.active');
            sections.forEach(section => {
                const phoneElements = section.querySelectorAll('.phone');
                const arrowElements = section.querySelectorAll('.arrow');

                if (phoneElements.length === 0) return;

                const phone1 = phoneElements[0];
                const phone2 = phoneElements[1];
                const phone3 = phoneElements[2];

                const arrow1 = arrowElements[0];
                const arrow2 = arrowElements[1];

                const scrollPos = window.scrollY;
                const offset = section.offsetTop;
                const windowHeight = window.innerHeight;

                // Position calculation is complex and depends on min-height: 400vh on most sections.
                const oneQuarter = offset + (section.offsetHeight * 0.25);
                const oneHalf = offset + (section.offsetHeight * 0.5);
                const threeQuarters = offset + (section.offsetHeight * 0.75);

                // Phone 1 visibility (start to 3/4 way down)
                if (scrollPos + windowHeight > offset + 100) {
                    phone1.classList.add('visible');
                } else {
                    phone1.classList.remove('visible');
                }
                
                // Phone 2 visibility (1/4 way down)
                if (scrollPos + windowHeight > oneQuarter) {
                    phone2.classList.add('visible');
                    arrow1.classList.add('visible');
                } else {
                    phone2.classList.remove('visible');
                    arrow1.classList.remove('visible');
                }

                // Phone 3 visibility (1/2 way down)
                if (scrollPos + windowHeight > oneHalf) {
                    phone3.classList.add('visible');
                    arrow2.classList.add('visible');
                } else {
                    phone3.classList.remove('visible');
                    arrow2.classList.remove('visible');
                }
                
                // For the SolarFlow tab, we disable the visibility logic since it's an inline 100vh page
                if (section.id === 'solarflow') {
                    phone1.classList.add('visible');
                    if (phone2) phone2.classList.add('visible');
                    if (phone3) phone3.classList.add('visible');
                    if (arrow1) arrow1.classList.add('visible');
                    if (arrow2) arrow2.classList.add('visible');
                }
            });
        }

        // Initialize visibility and set scroll listener
        window.onload = function() {
            // Set initial active tab
            switchTab('linktree1');
            
            // Set scroll listener only for Project 1 sections
            document.addEventListener('scroll', checkScrollVisibility);
            checkScrollVisibility();
        };
        
        // --- Project 2 Simplified Mockup Switching Logic ---
        function showSolarView(viewName, buttonElement) {
            // Hide all mockups in the content area
            document.getElementById('social-mockup').style.display = 'none';
            document.getElementById('thankyou-mockup').style.display = 'none';
            document.getElementById('disqualify-mockup').style.display = 'none';
            document.getElementById('linktree-mockup').style.display = 'none';

            // Show the selected mockup
            if (viewName === 'social') {
                document.getElementById('social-mockup').style.display = 'block';
                document.getElementById('stage1-title').textContent = 'Ad on Socials';
                document.getElementById('stage1-description-text').innerHTML = '<p style="margin: 0; color: #555; line-height: 1.6;">Learn More button links out to content page.</p>';
            } else if (viewName === 'thankyou') {
                document.getElementById('thankyou-mockup').style.display = 'block';
                document.getElementById('stage1-title').textContent = 'Thank You Page';
                document.getElementById('stage1-description-text').innerHTML = '<p style="margin: 0; color: #555; line-height: 1.6;">Content embedded on a Thank You page as a follow-up action.</p>';
            } else if (viewName === 'disqualify') {
                document.getElementById('disqualify-mockup').style.display = 'block';
                document.getElementById('stage1-title').textContent = 'Disqualifying Offer';
                document.getElementById('stage1-description-text').innerHTML = '<p style="margin: 0; color: #555; line-height: 1.6;">User shown educational content after failing qualification check.</p>';
            } else if (viewName === 'linktree') {
                document.getElementById('linktree-mockup').style.display = 'flex'; // Use flex to center the content
                document.getElementById('stage1-title').textContent = 'Linktree';
                document.getElementById('stage1-description-text').innerHTML = '<p style="margin: 0; color: #555; line-height: 1.6;">User clicks on a Linktree button leading to the article/content.</p>';
            }

            // Update button highlighting
            buttonElement.parentElement.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            buttonElement.classList.add('active');
        }

    </script>
</body>
</html>
