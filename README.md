<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stephen Mburu - Senior UI/UX Frontend Architect</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #333;
            line-height: 1.6;
            overflow-x: hidden;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header Section */
        .header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 40px 0;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(45deg, rgba(102, 126, 234, 0.1), rgba(118, 75, 162, 0.1));
            z-index: -1;
        }

        .hero {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 40px;
            align-items: center;
        }

        .avatar {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            background: linear-gradient(135deg, #667eea, #764ba2);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 72px;
            font-weight: bold;
            color: white;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
        }

        .avatar:hover {
            transform: scale(1.05);
        }

        .hero-content h1 {
            font-size: 3rem;
            font-weight: 700;
            margin-bottom: 10px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .hero-content .subtitle {
            font-size: 1.5rem;
            color: #666;
            margin-bottom: 20px;
        }

        .hero-content .location {
            font-size: 1.1rem;
            color: #888;
            margin-bottom: 30px;
        }

        .social-links {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .social-btn {
            display: inline-flex;
            align-items: center;
            padding: 12px 24px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            text-decoration: none;
            border-radius: 25px;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        .social-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
        }

        /* Main Content */
        .main-content {
            background: white;
            margin-top: -20px;
            border-radius: 20px 20px 0 0;
            position: relative;
            z-index: 1;
        }

        .section {
            padding: 60px 0;
            border-bottom: 1px solid #eee;
        }

        .section:last-child {
            border-bottom: none;
        }

        .section-title {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 40px;
            text-align: center;
            position: relative;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            border-radius: 2px;
        }

        /* About Section */
        .about-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
            margin-top: 40px;
        }

        .about-text {
            font-size: 1.1rem;
            line-height: 1.8;
            color: #555;
        }

        .current-project {
            background: linear-gradient(135deg, #f8f9ff, #e8f2ff);
            padding: 30px;
            border-radius: 15px;
            border-left: 4px solid #667eea;
        }

        .current-project h3 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.3rem;
        }

        /* Tech Stack */
        .tech-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            margin-top: 40px;
        }

        .tech-category {
            background: #f8f9fa;
            padding: 30px;
            border-radius: 15px;
            transition: transform 0.3s ease;
        }

        .tech-category:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }

        .tech-category h3 {
            color: #667eea;
            margin-bottom: 20px;
            font-size: 1.2rem;
        }

        .tech-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .tech-tag {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 500;
        }

        /* Projects Section */
        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin-top: 40px;
        }

        .project-card {
            background: white;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .project-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
        }

        .project-header {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 25px;
        }

        .project-header h3 {
            font-size: 1.5rem;
            margin-bottom: 10px;
        }

        .project-content {
            padding: 25px;
        }

        .project-features {
            margin: 20px 0;
        }

        .project-features ul {
            list-style: none;
            padding: 0;
        }

        .project-features li {
            padding: 8px 0;
            color: #666;
            position: relative;
            padding-left: 20px;
        }

        .project-features li::before {
            content: '▸';
            position: absolute;
            left: 0;
            color: #667eea;
            font-weight: bold;
        }

        .project-tech {
            margin-top: 20px;
        }

        .project-tech-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 10px;
        }

        .project-tech-tag {
            background: #f0f4ff;
            color: #667eea;
            padding: 6px 12px;
            border-radius: 15px;
            font-size: 0.8rem;
            font-weight: 500;
        }

        /* Skills Icons */
        .skills-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
            gap: 20px;
            margin-top: 40px;
        }

        .skill-icon {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            border-radius: 15px;
            background: #f8f9fa;
            transition: all 0.3s ease;
        }

        .skill-icon:hover {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            transform: translateY(-5px);
        }

        .skill-icon-img {
            width: 40px;
            height: 40px;
            background: #667eea;
            border-radius: 8px;
            margin-bottom: 10px;
        }

        /* Achievements */
        .achievements-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 40px;
        }

        .achievement {
            background: linear-gradient(135deg, #f8f9ff, #e8f2ff);
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            border: 1px solid #e0e8ff;
        }

        .achievement-icon {
            font-size: 2rem;
            margin-bottom: 15px;
            color: #667eea;
        }

        .achievement h3 {
            color: #333;
            margin-bottom: 10px;
        }

        .achievement p {
            color: #666;
            font-size: 0.9rem;
        }

        /* Services Table */
        .services-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 40px;
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }

        .services-table th,
        .services-table td {
            padding: 20px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }

        .services-table th {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            font-weight: 600;
        }

        .services-table tbody tr:hover {
            background: #f8f9ff;
        }

        /* Goals */
        .goals-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 40px;
        }

        .goal {
            background: white;
            padding: 25px;
            border-radius: 15px;
            border-left: 4px solid #667eea;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .goal-checkbox {
            width: 20px;
            height: 20px;
            border: 2px solid #667eea;
            border-radius: 3px;
            display: inline-block;
            margin-right: 15px;
            vertical-align: middle;
        }

        /* Progress Bar */
        .progress-section {
            margin-top: 40px;
        }

        .progress-item {
            margin-bottom: 25px;
        }

        .progress-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }

        .progress-bar {
            width: 100%;
            height: 20px;
            background: #f0f0f0;
            border-radius: 10px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(135deg, #667eea, #764ba2);
            transition: width 0.3s ease;
        }

        /* Fun Facts */
        .fun-facts {
            background: linear-gradient(135deg, #f8f9ff, #e8f2ff);
            padding: 40px;
            border-radius: 20px;
            margin-top: 40px;
        }

        .fun-facts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
        }

        .fun-fact {
            text-align: center;
            padding: 20px;
        }

        .fun-fact-icon {
            font-size: 2rem;
            margin-bottom: 10px;
        }

        /* Footer */
        .footer {
            background: #333;
            color: white;
            padding: 40px 0;
            text-align: center;
        }

        .footer-quote {
            font-size: 1.2rem;
            font-style: italic;
            margin-bottom: 20px;
            color: #ccc;
        }

        .footer-tagline {
            color: #667eea;
            font-weight: 600;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .hero {
                grid-template-columns: 1fr;
                text-align: center;
            }

            .hero-content h1 {
                font-size: 2rem;
            }

            .about-grid {
                grid-template-columns: 1fr;
            }

            .tech-grid {
                grid-template-columns: 1fr;
            }

            .projects-grid {
                grid-template-columns: 1fr;
            }

            .skills-grid {
                grid-template-columns: repeat(4, 1fr);
            }
        }

        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .section {
            animation: fadeInUp 0.6s ease;
        }

        /* Smooth scrolling */
        html {
            scroll-behavior: smooth;
        }
    </style>
</head>
<body>
    <!-- Header Section -->
    <header class="header">
        <div class="container">
            <div class="hero">
                <div class="avatar">SM</div>
                <div class="hero-content">
                    <h1>Stephen Mburu</h1>
                    <p class="subtitle">Senior UI/UX Frontend Architect</p>
                    <p class="location">📍 Nairobi, Kenya 🇰🇪</p>
                    <div class="social-links">
                        <a href="https://linkedin.com/in/stephen-mburu" class="social-btn">LinkedIn</a>
                        <a href="https://mac254.dev" class="social-btn">Portfolio</a>
                        <a href="mailto:mburustephen167@gmail.com" class="social-btn">Email</a>
                        <a href="https://twitter.com/stephen_mburu" class="social-btn">Twitter</a>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="main-content">
        <div class="container">
            <!-- About Section -->
            <section class="section">
                <h2 class="section-title">About Me</h2>
                <div class="about-grid">
                    <div class="about-text">
                        <p>I'm a passionate frontend architect with 5+ years of experience crafting user-centered digital experiences. I specialize in building scalable React applications, design systems, and leading cross-functional teams to deliver exceptional products.</p>
                        <p>My expertise spans modern web technologies, user experience design, and technical leadership. I'm committed to creating accessible, performant, and beautiful digital experiences that solve real-world problems.</p>
                    </div>
                    <div class="current-project">
                        <h3>🚀 Currently Building</h3>
                        <p><strong>KenyaTech</strong> - A platform connecting Kenyan developers with global opportunities, fostering local tech talent and bridging the gap between African developers and international markets.</p>
                    </div>
                </div>
            </section>

            <!-- Tech Stack Section -->
            <section class="section">
                <h2 class="section-title">Technology Stack</h2>
                <div class="tech-grid">
                    <div class="tech-category">
                        <h3>Languages</h3>
                        <div class="tech-tags">
                            <span class="tech-tag">JavaScript</span>
                            <span class="tech-tag">TypeScript</span>
                            <span class="tech-tag">HTML</span>
                            <span class="tech-tag">CSS</span>
                            <span class="tech-tag">Python</span>
                        </div>
                    </div>
                    <div class="tech-category">
                        <h3>Frameworks</h3>
                        <div class="tech-tags">
                            <span class="tech-tag">React</span>
                            <span class="tech-tag">Next.js</span>
                            <span class="tech-tag">Angular</span>
                            <span class="tech-tag">Vue.js</span>
                        </div>
                    </div>
                    <div class="tech-category">
                        <h3>Styling</h3>
                        <div class="tech-tags">
                            <span class="tech-tag">Tailwind CSS</span>
                            <span class="tech-tag">SCSS</span>
                            <span class="tech-tag">Styled Components</span>
                            <span class="tech-tag">Material-UI</span>
                        </div>
                    </div>
                    <div class="tech-category">
                        <h3>Tools & Databases</h3>
                        <div class="tech-tags">
                            <span class="tech-tag">Figma</span>
                            <span class="tech-tag">Storybook</span>
                            <span class="tech-tag">Jest</span>
                            <span class="tech-tag">MongoDB</span>
                            <span class="tech-tag">PostgreSQL</span>
                        </div>
                    </div>
                </div>
            </section>

            <!-- What I Do Section -->
            <section class="section">
                <h2 class="section-title">What I Do</h2>
                <div class="tech-grid">
                    <div class="tech-category">
                        <h3>Frontend Development</h3>
                        <p>Building responsive, performant web applications with modern frameworks and tools. Creating reusable component libraries and implementing efficient development workflows.</p>
                    </div>
                    <div class="tech-category">
                        <h3>UI/UX Design</h3>
                        <p>Conducting user research and usability testing. Creating wireframes and prototypes in Figma with accessibility-first design principles.</p>
                    </div>
                    <div class="tech-category">
                        <h3>Technical Leadership</h3>
                        <p>Mentoring junior developers, conducting code reviews, and establishing best practices. Making architecture decisions and defining technical strategy.</p>
                    </div>
                </div>
            </section>

            <!-- Featured Projects Section -->
            <section class="section">
                <h2 class="section-title">Featured Projects</h2>
                <div class="projects-grid">
                    <div class="project-card">
                        <div class="project-header">
                            <h3>🌐 KenyaTech Platform</h3>
                            <p>Comprehensive developer platform</p>
                        </div>
                        <div class="project-content">
                            <div class="project-features">
                                <strong>Key Features:</strong>
                                <ul>
                                    <li>Developer profiles and portfolios</li>
                                    <li>Job matching algorithm</li>
                                    <li>Community forums and events</li>
                                    <li>Skills assessment tools</li>
                                </ul>
                            </div>
                            <div class="project-tech">
                                <strong>Technologies:</strong>
                                <div class="project-tech-tags">
                                    <span class="project-tech-tag">React</span>
                                    <span class="project-tech-tag">TypeScript</span>
                                    <span class="project-tech-tag">Next.js</span>
                                    <span class="project-tech-tag">Tailwind CSS</span>
                                    <span class="project-tech-tag">PostgreSQL</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="project-card">
                        <div class="project-header">
                            <h3>🎨 Design System Library</h3>
                            <p>Enterprise-grade component library</p>
                        </div>
                        <div class="project-content">
                            <div class="project-features">
                                <strong>Key Features:</strong>
                                <ul>
                                    <li>50+ accessible components</li>
                                    <li>Dark/light theme support</li>
                                    <li>Comprehensive documentation</li>
                                    <li>95% test coverage</li>
                                </ul>
                            </div>
                            <div class="project-tech">
                                <strong>Technologies:</strong>
                                <div class="project-tech-tags">
                                    <span class="project-tech-tag">React</span>
                                    <span class="project-tech-tag">Storybook</span>
                                    <span class="project-tech-tag">SCSS</span>
                                    <span class="project-tech-tag">Jest</span>
                                    <span class="project-tech-tag">Chromatic</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="project-card">
                        <div class="project-header">
                            <h3>📊 Analytics Dashboard</h3>
                            <p>Real-time business intelligence</p>
                        </div>
                        <div class="project-content">
                            <div class="project-features">
                                <strong>Key Features:</strong>
                                <ul>
                                    <li>Real-time data streaming</li>
                                    <li>Interactive charts and graphs</li>
                                    <li>Customizable widgets</li>
                                    <li>Export functionality</li>
                                </ul>
                            </div>
                            <div class="project-tech">
                                <strong>Technologies:</strong>
                                <div class="project-tech-tags">
                                    <span class="project-tech-tag">React</span>
                                    <span class="project-tech-tag">Redux</span>
                                    <span class="project-tech-tag">Chart.js</span>
                                    <span class="project-tech-tag">Material-UI</span>
                                    <span class="project-tech-tag">WebSocket</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Achievements Section -->
            <section class="section">
                <h2 class="section-title">Achievements</h2>
                <div class="achievements-grid">
                    <div class="achievement">
                        <div class="achievement-icon">🏆</div>
                        <h3>Top 1% GitHub Contributor</h3>
                        <p>Recognized among top contributors in Kenya</p>
                    </div>
                    <div class="achievement">
                        <div class="achievement-icon">🎨</div>
                        <h3>UI/UX Certified</h3>
                        <p>Google Design certification</p>
                    </div>
                    <div class="achievement">
                        <div class="achievement-icon">📱</div>
                        <h3>React Native Expert</h3>
                        <p>Built 50+ mobile applications</p>
                    </div>
                    <div class="achievement">
                        <div class="achievement-icon">🚀</div>
                        <h3>Open Source Contributor</h3>
                        <p>1000+ commits to various projects</p>
                    </div>
                    <div class="achievement">
                        <div class="achievement-icon">👥</div>
                        <h3>Community Leader</h3>
                        <p>Organized 10+ tech meetups</p>
                    </div>
                </div>
            </section>

            <!-- Professional Services Section -->
            <section class="section">
                <h2 class="section-title">Professional Services</h2>
                <table class="services-table">
                    <thead>
                        <tr>
                            <th>Service</th>
                            <th>Description</th>
                            <th>Technologies</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>Frontend Development</strong></td>
                            <td>Custom web applications and SPAs</td>
                            <td>React, Next.js, TypeScript</td>
                        </tr>
                        <tr>
                            <td><strong>UI/UX Design</strong></td>
                            <td>User research, wireframing, prototyping</td>
                            <td>Figma, Adobe XD, Sketch</td>
                        </tr>
                        <tr>
                            <td><strong>Design Systems</strong></td>
                            <td>Component libraries and style guides</td>
                            <td>Storybook, Tailwind, SCSS</td>
                        </tr>
                        <tr>
                            <td><strong>Mobile Development</strong></td>
                            <td>Cross-platform mobile applications</td>
                            <td>React Native, Flutter</td>
                        </tr>
                        <tr>
                            <td><strong>Technical Consulting</strong></td>
                            <td>Code reviews, architecture planning</td>
                            <td>Various technologies</td>
                        </tr>
                    </tbody>
                </table>
            </section>

            <!-- Goals Section -->
            <section class="section">
                <h2 class="section-title">Goals for 2025</h2>
                <div class="goals-grid">
                    <div class="goal">
                        <span class="goal-checkbox"></span>
                        Launch KenyaTech platform with 1000+ developers
                    </div>
                    <div class="goal">
                        <span class="goal-checkbox"></span>
                        Contribute to 5 major open source projects
                    </div>
                    <div class="goal">
                        <span class="goal-checkbox"></span>
                        Speak at 3 international tech conferences
                    </div>
                    <div class="goal">
                        <span class="goal-checkbox"></span>
                        Mentor 20+ junior developers
                    </div>
                    <div class="goal">
                        <span class="goal-checkbox"></span>
                        Complete AWS Solutions Architect certification
                    </div>
                </div>
            </section>

            <!-- Weekly Development Breakdown -->
            <section class="section">
                <h2 class="section-title">Weekly Development Breakdown</h2>
                <div class="progress-section">
                    <div class="progress-item">
                        <div class="progress-header">
                            <span>TypeScript</span>
                            <span>45.2%</span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 45.2%"></div>
                        </div>
                    </div>
                    <div class="progress-item">
                        <div class="progress-header">
                            <span>React</span>
                            <span>29.8%</span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 29.8%"></div>
                        </div>
                    </div>
                    <div class="progress-item">
                        <div class="progress-header">
                            <span>SCSS</span>
                            <span>13.5%</span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 13.5%"></div>
                        </div>
                    </div>
                    <div class="progress-item">
                        <div class="progress-header">
                            <span>Figma</span>
                            <span>9.0%</span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 9.0%"></div>
                        </div>
                    </div>
                    <div class="progress-item">
                        <div class="progress-header">
                            <span>Other</span>
                            <span>2.5%</span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 2.5%"></div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Fun Facts Section -->
            <section class="section">
                <h2 class="section-title">Fun Facts</h2>
                <div class="fun-facts">
                    <div class="fun-facts-grid">
                        <div class="fun-fact">
                            <div class="fun-fact-icon">
