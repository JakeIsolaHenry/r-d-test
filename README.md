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
           PROJECT 1 & 2 - MERGED & CLEANED CSS
           ============================================ */
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
        
        /* Containers */
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
        
        /* Tabs and Buttons (Project 1) */
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
        
        /* Flow Sections */
        .flow-section {
            position: relative;
            display: none;
            min-height: 400vh; /* Default for the Project 1 scrolling demos */
        }
        
        .flow-section#solarflow {
             min-height: 100vh; /* Reduced height for the self-contained solar demo */
             background: transparent;
        }

        .flow-section.active {
            display: block;
        }
        
        /* Sticky Wrapper & Phone Container (Project 1) */
        .sticky-container {
            position: sticky;
            top: 0;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
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
        
        /* Arrows & Labels */
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
        
        /* Phone Content Styles (Project 1) */
        .phone-content {
            padding: 40px 20px 20px;
            height: 100%;
            overflow-y: auto;
        }
        
        /* --- Linktree & Article Styles --- */
        .linktree { /* Pink default */
            background: linear-gradient(180deg, #FFB6D9 0%, #FFC9E3 100%);
            height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        /* [Additional Linktree/Article color classes (.blue, .purple, .green, .solar) kept] */
        .linktree.blue { background: linear-gradient(180deg, #a8edea 0%, #fed6e3 100%); }
        .linktree.purple { background: linear-gradient(180deg, #d4a5ff 0%, #e8c4ff 100%); }
        .linktree.green { background: linear-gradient(180deg, #a8e6cf 0%, #dcedc1 100%); }
        
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
        
        /* [All other Project 1 inner styles kept for consistency] */
        .article { /* Pink default */
            padding: 40px 20px 20px;
            background: linear-gradient(180deg, #FFB6D9 0%, #FFC9E3 100%);
            height: 100%;
        }
        
        /* --- SolarFlow Specific Styles (Project 2 Integration) --- */
        .solar-container {
            max-width: 1200px;
            margin: 40px auto;
            padding: 40px 20px;
            background: #ffffff;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .solar-header {
            text-align: center;
            color: #333;
            margin-bottom: 40px;
        }

        .solar-header h2 {
            font-size: 36px;
            margin-bottom: 10px;
        }
        
        .flow-stages-wrapper {
            display: flex;
            gap: 40px;
            justify-content: center;
            align-items: flex-start;
            flex-wrap: wrap;
        }
        
        .flow-stage-solar {
            min-width: 300px;
            max-width: 350px;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            background: #f8f9fa;
        }
        
        .stage-toggle-buttons {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 5px;
            margin-bottom: 15px;
        }

        /* Override Project 1 .toggle-btn for SolarFlow inner nav */
        .flow-stage-solar .toggle-btn {
            background: #e9ecef;
            border: 1px solid #ced4da;
            color: #495057;
            padding: 8px 12px;
            font-size: 11px;
            font-weight: 500;
            border-radius: 15px;
            flex-grow: 1;
            backdrop-filter: none;
        }
        
        .flow-stage-solar .toggle-btn.active {
            background: #f5a623;
            color: white;
            border-color: #f5a623;
        }
        
        /* Phone Frame for SolarFlow */
        .phone-frame-solar {
            width: 300px;
            height: 600px;
            background: #1f1f1f;
            border-radius: 35px;
            padding: 8px;
            margin: 10px auto 20px auto;
            position: relative;
            box-shadow: 0 15px 40px rgba(0,0,0,0.3);
        }
        
        /* Solar Flow Mockup Content Styles */
        .mockup-content {
            width: 100%; 
            height: 100%; 
            overflow-y: auto; 
            background: #f0f2f5;
            padding: 15px;
        }
        
        /* Social Ad Mockup */
        .facebook-ad-mockup {
            background: white;
            border-radius: 8px;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            min-height: 580px;
        }
        .fb-header, .fb-content, .fb-cta { padding: 8px 12px; }
        .fb-media-placeholder { 
            background: url('https://images.unsplash.com/photo-1509376662483-36657c7d42a4?w=400&auto=format&fit=crop') center/cover;
            height: 350px; 
            display: flex; align-items: center; justify-content: center;
        }
        
        /* Thank You/Disqualify Mockup */
        .message-mockup {
            padding: 40px 20px;
            text-align: center;
            height: 100%;
        }
        .thankyou-bg { background: linear-gradient(180deg, #d4edda 0%, #c3e6cb 100%); }
        .disqualify-bg { background: linear-gradient(180deg, #f8d7da 0%, #f5c6cb 100%); }
        .linktree-bg { background: linear-gradient(180deg, #7dd3fc 0%, #06b6d4 100%); display: flex; flex-direction: column; align-items: center; }
        
        .mockup-button {
            background: #4CAF50; 
            color: white; 
            padding: 10px 20px; 
            border: none; 
            border-radius: 20px; 
            margin-top: 20px;
            font-weight: 600;
        }
        
        /* Content Page Mockup */
        .content-mockup { padding: 20px; overflow-y: auto; height: 100%; }
        .content-mockup .search-chip { background: #5865f2; color: white; margin: 4px; }
        .content-mockup .search-chip:hover { background: #f5a623; }
        
        /* SERP Mockup */
        .serp-mockup { 
            background: linear-gradient(180deg, #ffeaa7 0%, #fdcb6e 100%); 
            padding: 20px 15px;
            height: 100%;
        }
        
        /* Mobile Responsiveness (Project 1's media query is broader, using that) */
        @media (max-width: 900px) {
            .phone-container {
                flex-direction: column;
                gap: 60px;
            }
            .arrow {
                transform: rotate(90deg);
            }
            .flow-stages-wrapper {
                flex-direction: column;
                align-items: center;
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
                                    <div class="article-text">The Google Pixel 10 smartphone represents a leap forward in technology with its advanced AI capabilities and innovative features. Powered by the Google Tensor G5 chip...</div>
                                    <div class="article-text">This chip doesn't just enhance performance; it opens up new possibilities for on-device AI applications...</div>
                                </div>

                                <div class="related-searches">
                                    <div class="search-title">Related Searches</div>
                                    <div class="search-chip">Google Pixel Pro</div>
                                    <div class="search-chip">Google Tensor G5</div>
                                    <div class="search-chip">Gemini Nano AI</div>
                                </div>
                                <div class="article-content-block">...</div>
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
                                </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="flow-section" id="linktree2">
            </div>

        <div class="flow-section" id="linktree3">
            </div>

        <div class="flow-section" id="linktree4">
            </div>


        <div class="flow-section" id="solarflow">
            <div class="sticky-container">
                <div class="solar-container">
                    <div class="solar-header">
                        <h2>SolarFlow User Journey Demo</h2>
                        <p>Visualizing the user journey for lead generation.</p>
                    </div>
                    
                    <div class="flow-stages-wrapper">
                        
                        <div class="flow-stage-solar">
                            <h3 class="stage-title">Ad Click Source</h3>
                            
                            <div class="stage-toggle-buttons">
                                <button class="toggle-btn active" onclick="showSolarView('social', this)">Socials</button>
                                <button class="toggle-btn" onclick="showSolarView('thankyou', this)">Thank You Page</button>
                                <button class="toggle-btn" onclick="showSolarView('disqualify', this)">Disqualify</button>
                                <button class="toggle-btn" onclick="showSolarView('linktree', this)">Linktree</button>
                            </div>
                            
                            <div class="phone-frame-solar">
                                <div class="phone-screen">
                                    <div id="solarflow-content-area" class="mockup-content">
                                        <div id="social-mockup" class="facebook-ad-mockup">
                                            <div class="fb-header">**SolarFlow** <span style="font-size: 10px;">Sponsored</span></div>
                                            <div class="fb-media-placeholder">▶️ Video Placeholder</div>
                                            <div class="fb-content">Thinking about solar? Learn more.</div>
                                            <div class="fb-cta"><button class="mockup-button" style="background: #e4e6ea; color: #65676b; border: 1px solid #dadde1;">Learn More</button></div>
                                        </div>
                                        
                                        <div id="thankyou-mockup" class="message-mockup thankyou-bg" style="display: none;">
                                            <h2 style="color: #155724;">Thank You!</h2>
                                            <p style="color: #155724; margin-top: 20px;">Your solar eligibility is confirmed. Now read our educational article.</p>
                                            <button class="mockup-button" style="background: #28a745;">Read Article</button>
                                        </div>
                                        
                                        <div id="disqualify-mockup" class="message-mockup disqualify-bg" style="display: none;">
                                            <h2 style="color: #721c24;">Sorry!</h2>
                                            <p style="color: #721c24; margin-top: 20px;">You did not qualify for a quote. Read this content instead to learn more.</p>
                                            <button class="mockup-button" style="background: #dc3545;">Educational Content</button>
                                        </div>

                                        <div id="linktree-mockup" class="message-mockup linktree-bg" style="display: none;">
                                            <h2 style="color: white; margin-bottom: 20px;">Solar Guru Linktree</h2>
                                            <button class="mockup-button" style="background: #f5a623; margin: 5px 0;">How Solar Energy Reduces Costs (Content Link)</button>
                                            <button class="mockup-button" style="background: white; color: #2d3748; margin: 5px 0; border: 1px solid #e2e8f0;">Get a Free Solar Quote</button>
                                            <button class="mockup-button" style="background: white; color: #2d3748; margin: 5px 0; border: 1px solid #e2e8f0;">Watch our latest video</button>
                                        </div>

                                    </div>
                                </div>
                            </div>
                        </div>
        
                        <div class="flow-stage-solar">
                            <h3 class="stage-title">Content Page with Keyword Block (RSOC)</h3>
                            
                            <div class="phone-frame-solar">
                                <div class="phone-screen">
                                    <div id="content-page-mockup" class="content-mockup">
                                        <h1 style="font-size: 20px; margin-bottom: 15px;">How Solar Energy Reduces Costs and Boosts Home Value</h1>
                                        <p style="font-size: 14px; margin-bottom: 20px;">Installing solar panels drastically cuts down on monthly electricity bills, providing significant long-term savings...</p>
                                        
                                        <div class="related-searches" style="margin-top: 20px; border: none; box-shadow: none; padding: 0;">
                                            <div class="search-title" style="color: #666;">Related Searches (Click to Monetize)</div>
                                            <div class="search-chip">Solar Panel Installation</div>
                                            <div class="search-chip">Residential Solar Panels Near Me</div>
                                            <div class="search-chip">Solar Panel Energy Savings</div>
                                        </div>
                                        <p style="font-size: 14px; margin-top: 20px;">Beyond savings, solar installations are shown to increase a home's market value...</p>
                                    </div>
                                </div>
                            </div>
                        </div>
        
                        <div class="flow-stage-solar">
                            <h3 class="stage-title">SERP & Monetization Event</h3>
                            
                            <div class="phone-frame-solar">
                                <div class="phone-screen">
                                    <div id="serp-mockup-content" class="serp-mockup">
                                        <div class="search-bar">🔍 Residential Solar Panels Near Me</div>
                                        
                                        <div class="serp-result">
                                            <div class="sponsored-badge">Sponsored</div>
                                            <div class="result-url">nation.com</div>
                                            <div class="result-title">Get a Free Solar Quote for Your Home</div>
                                            <div class="result-description">See how much you can save with a top-rated solar installer near you. Quick & free online check.</div>
                                            <button class="visit-button" style="background: #4CAF50;">Visit Website</button>
                                        </div>
        
                                        <div class="serp-result">
                                            <div class="result-url">solarenergycorp.com</div>
                                            <div class="result-title">Top Solar Panel Installers 2024</div>
                                            <div class="result-description">Compare local companies and find the best fit. Read customer reviews.</div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
    
    <div class="footer">
        <h2>Ready to Publish?</h2>
        <p>This is the final combined and corrected HTML. You can now use it to publish on GitHub Pages.</p>
    </div>

    <script>
        // Project 1 Tab Switching Logic
        function switchTab(tabId) {
            // Hide all flow sections
            document.querySelectorAll('.flow-section').forEach(section => {
                section.classList.remove('active');
                section.style.display = 'none';
                // Stop scroll visibility logic on all sections
                section.querySelectorAll('.phone').forEach(p => p.classList.remove('visible'));
                section.querySelectorAll('.arrow').forEach(a => a.classList.remove('visible'));
            });

            // Show the selected flow section
            const activeSection = document.getElementById(tabId);
            if (activeSection) {
                activeSection.classList.add('active');
                activeSection.style.display = 'block';
            }

            // Update tab button active state
            document.querySelectorAll('.tab-button').forEach(button => {
                button.classList.remove('active');
                if (button.getAttribute('onclick').includes(`'${tabId}'`)) {
                    button.classList.add('active');
                }
            });

            // If it's the solarflow section, ensure initial visibility is set manually (no scrolling needed)
            if (tabId === 'solarflow') {
                document.querySelectorAll('#solarflow .phone-frame-solar').forEach(p => {
                    const phone = p.parentElement;
                    phone.classList.add('visible'); // Added a 'visible' style to the parent container for mobile visual effects
                    phone.style.opacity = '1';
                    phone.style.transform = 'translateY(0)';
                });
            } else {
                // For Project 1 sections, restart the scrolling logic
                checkScrollVisibility();
            }
        }

        // Project 1 Scroll Visibility Logic (for Linktree sections only)
        function checkScrollVisibility() {
            const activeSection = document.querySelector('.flow-section.active');
            
            if (!activeSection || activeSection.id === 'solarflow') return;

            const phoneElements = activeSection.querySelectorAll('.phone');
            const arrowElements = activeSection.querySelectorAll('.arrow');

            if (phoneElements.length === 0) return;

            const phone1 = phoneElements[0];
            const phone2 = phoneElements[1];
            const phone3 = phoneElements[2];

            const arrow1 = arrowElements[0];
            const arrow2 = arrowElements[1];

            const scrollPos = window.scrollY;
            const offset = activeSection.offsetTop;
            const sectionHeight = activeSection.offsetHeight;

            // Define trigger points relative to the section start
            const oneQuarter = offset + (sectionHeight * 0.25);
            const oneHalf = offset + (sectionHeight * 0.5);
            const threeQuarters = offset + (sectionHeight * 0.75);

            // Phone 1 visibility (start to 3/4 way down)
            phone1.classList.toggle('visible', scrollPos + window.innerHeight > offset + 100);
            
            // Phone 2 visibility (triggered at ~25% down the section)
            if (phone2) {
                const isVisible = scrollPos + (window.innerHeight * 0.8) > oneQuarter;
                phone2.classList.toggle('visible', isVisible);
                if (arrow1) arrow1.classList.toggle('visible', isVisible);
            }

            // Phone 3 visibility (triggered at ~50% down the section)
            if (phone3) {
                const isVisible = scrollPos + (window.innerHeight * 0.8) > oneHalf;
                phone3.classList.toggle('visible', isVisible);
                if (arrow2) arrow2.classList.toggle('visible', isVisible);
            }
        }

        // Project 2 Simplified Mockup Switching Logic (Internal to SolarFlow)
        function showSolarView(viewName, buttonElement) {
            // Hide all mockups in the content area
            document.getElementById('social-mockup').style.display = 'none';
            document.getElementById('thankyou-mockup').style.display = 'none';
            document.getElementById('disqualify-mockup').style.display = 'none';
            document.getElementById('linktree-mockup').style.display = 'none';
            
            // Show the selected mockup
            document.getElementById(`${viewName}-mockup`).style.display = (viewName === 'linktree' ? 'flex' : 'block');

            // Update the Stage 1 main title/description (these elements are outside the mockup in this section)
            let newTitle = '';
            let newDescription = '';

            if (viewName === 'social') {
                newTitle = 'Ad on Socials';
                newDescription = '<p style="margin: 0; color: #555; line-height: 1.6;">"Learn More" button links out to content page.</p>';
            } else if (viewName === 'thankyou') {
                newTitle = 'Thank You Page';
                newDescription = '<p style="margin: 0; color: #555; line-height: 1.6;">Content embedded on a Thank You page as a follow-up action.</p>';
            } else if (viewName === 'disqualify') {
                newTitle = 'Disqualifying Offer';
                newDescription = '<p style="margin: 0; color: #555; line-height: 1.6;">User shown educational content after failing qualification check.</p>';
            } else if (viewName === 'linktree') {
                newTitle = 'Linktree';
                newDescription = '<p style="margin: 0; color: #555; line-height: 1.6;">User clicks on a Linktree button leading to the article/content.</p>';
            }

            document.getElementById('stage1-title').textContent = newTitle;
            document.getElementById('stage1-description-text').innerHTML = newDescription;

            // Update button highlighting
            buttonElement.parentElement.querySelectorAll('.toggle-btn').forEach(btn => btn.classList.remove('active'));
            buttonElement.classList.add('active');
        }

        // Initialize visibility and set scroll listener
        window.onload = function() {
            // Set initial active tab (Linktree 1)
            switchTab('linktree1');
            
            // Set scroll listener for Project 1 sections
            document.addEventListener('scroll', checkScrollVisibility);
        };
    </script>
</body>
</html>
