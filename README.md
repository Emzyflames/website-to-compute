<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TradeMonitor Academy</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            color: #f0f8ff;
            min-height: 100vh;
            padding: 10px;
        }
        
        header {
            background: rgba(10, 25, 47, 0.9);
            padding: 1rem;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            margin-bottom: 15px;
        }
        
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.2rem;
            font-weight: 700;
            color: #64ffda;
        }
        
        .nav-links {
            display: none;
            gap: 1rem;
            flex-direction: column;
            position: absolute;
            top: 70px;
            right: 10px;
            background: rgba(10, 25, 47, 0.95);
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .nav-links.active {
            display: flex;
        }
        
        .nav-links a {
            color: #ccd6f6;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
            padding: 8px 0;
        }
        
        .nav-links a:hover, .nav-links a.active {
            color: #64ffda;
        }
        
        .menu-btn {
            background: none;
            border: none;
            color: #64ffda;
            font-size: 1.5rem;
            cursor: pointer;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 0.5rem;
        }
        
        .hero {
            text-align: center;
            padding: 2rem 1rem;
            background: rgba(17, 34, 64, 0.5);
            border-radius: 15px;
            margin-bottom: 2rem;
        }
        
        .hero h1 {
            font-size: 2rem;
            margin-bottom: 1rem;
            background: linear-gradient(90deg, #64ffda, #00aaff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .hero p {
            font-size: 1rem;
            margin: 0 auto 1.5rem;
            color: #a8b2d1;
        }
        
        .btn {
            background: linear-gradient(90deg, #64ffda, #00aaff);
            color: #0a192f;
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 50px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            display: inline-block;
            margin: 5px;
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        .section-title {
            text-align: center;
            margin: 2rem 0 1.5rem;
            font-size: 1.5rem;
            color: #64ffda;
        }
        
        .features {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1.5rem;
            margin-bottom: 3rem;
        }
        
        .feature-card {
            background: rgba(17, 34, 64, 0.7);
            padding: 1.5rem;
            border-radius: 15px;
            text-align: center;
            transition: transform 0.3s;
        }
        
        .feature-card:hover {
            transform: translateY(-5px);
        }
        
        .feature-icon {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            color: #64ffda;
        }
        
        .testimonials {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1.5rem;
            margin-bottom: 3rem;
        }
        
        .testimonial-card {
            background: rgba(17, 34, 64, 0.7);
            padding: 1.5rem;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        
        .testimonial-header {
            display: flex;
            align-items: center;
            margin-bottom: 1rem;
        }
        
        .testimonial-avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: #64ffda;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            font-weight: bold;
            margin-right: 1rem;
            color: #0a192f;
        }
        
        .profit-badge {
            background: rgba(100, 255, 218, 0.2);
            color: #64ffda;
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
        }
        
        .dashboard {
            background: rgba(17, 34, 64, 0.7);
            padding: 1.5rem;
            border-radius: 15px;
            margin-bottom: 3rem;
        }
        
        .chart-container {
            position: relative;
            height: 300px;
            margin-bottom: 1.5rem;
        }
        
        .notification-container {
            position: fixed;
            top: 10px;
            right: 10px;
            z-index: 1000;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        
        .notification {
            background: rgba(17, 34, 64, 0.95);
            color: #64ffda;
            padding: 0.8rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            display: flex;
            align-items: center;
            gap: 10px;
            animation: slideIn 0.5s ease;
            max-width: 300px;
            font-size: 0.9rem;
        }
        
        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
        
        footer {
            background: rgba(10, 25, 47, 0.9);
            padding: 1.5rem;
            text-align: center;
            margin-top: 3rem;
            border-radius: 10px;
        }
        
        .footer-content {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        
        .social-links {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-top: 1rem;
        }
        
        .social-links a {
            color: #ccd6f6;
            font-size: 1.2rem;
            transition: color 0.3s;
        }
        
        .social-links a:hover {
            color: #64ffda;
        }
        
        @media (min-width: 768px) {
            .features, .testimonials {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .hero h1 {
                font-size: 2.5rem;
            }
            
            .nav-links {
                position: static;
                flex-direction: row;
                display: flex;
                background: none;
                padding: 0;
                box-shadow: none;
            }
            
            .menu-btn {
                display: none;
            }
        }
        
        @media (min-width: 1024px) {
            .features, .testimonials {
                grid-template-columns: repeat(3, 1fr);
            }
            
            .hero h1 {
                font-size: 3rem;
            }
        }
    </style>
</head>
<body>
    <header>
        <nav>
            <div class="logo">
                <i class="fas fa-chart-line"></i>
                <span>TradeMonitor Academy</span>
            </div>
            <button class="menu-btn" id="menuBtn">
                <i class="fas fa-bars"></i>
            </button>
            <div class="nav-links" id="navLinks">
                <a href="#" class="active">Home</a>
                <a href="#">Dashboard</a>
                <a href="#">Learn</a>
                <a href="#">Testimonials</a>
                <a href="#">About</a>
            </div>
        </nav>
    </header>
    
    <div class="container">
        <section class="hero">
            <h1>Master The Art of Trade Monitoring</h1>
            <p>Learn how to effectively monitor trades, analyze market trends, and maximize your profits with our comprehensive educational platform.</p>
            <button class="btn">Start Learning Now</button>
        </section>
        
        <h2 class="section-title">Key Features</h2>
        <section class="features">
            <div class="feature-card">
                <div class="feature-icon">
                    <i class="fas fa-chart-bar"></i>
                </div>
                <h3>Real-time Analytics</h3>
                <p>Access live market data and advanced charting tools to make informed trading decisions.</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">
                    <i class="fas fa-graduation-cap"></i>
                </div>
                <h3>Expert Lessons</h3>
                <p>Learn from industry experts with years of experience in trading and market analysis.</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">
                    <i class="fas fa-bell"></i>
                </div>
                <h3>Smart Alerts</h3>
                <p>Get notified about market movements and potential trading opportunities instantly.</p>
            </div>
        </section>
        
        <h2 class="section-title">Crypto AI Dashboard</h2>
        <section class="dashboard">
            <div class="chart-container">
                <canvas id="cryptoChart"></canvas>
            </div>
            <div style="text-align: center;">
                <button class="btn" id="toggleChart">Switch Chart Type</button>
            </div>
        </section>
        
        <h2 class="section-title">Success Stories</h2>
        <section class="testimonials">
            <div class="testimonial-card">
                <div class="testimonial-header">
                    <div class="testimonial-avatar">JD</div>
                    <div>
                        <h3>John Doe</h3>
                        <div class="profit-badge">+290% profit</div>
                    </div>
                </div>
                <p>"I made a 290% profit in just 14 hours after applying the techniques I learned here. The chart analysis lessons were incredibly helpful!"</p>
            </div>
            <div class="testimonial-card">
                <div class="testimonial-header">
                    <div class="testimonial-avatar">SM</div>
                    <div>
                        <h3>Sarah Miller</h3>
                        <div class="profit-badge">+200% profit</div>
                    </div>
                </div>
                <p>"The real-time notifications helped me catch a market trend early. I made a 200% return on my investment in just 10 hours. Amazing platform!"</p>
            </div>
            <div class="testimonial-card">
                <div class="testimonial-header">
                    <div class="testimonial-avatar">RJ</div>
                    <div>
                        <h3>Robert Johnson</h3>
                        <div class="profit-badge">+350% profit</div>
                    </div>
                </div>
                <p>"I've tried many trading courses, but this one stands out. The AI chart predictions are incredibly accurate. I made 350% profit in 29 hours!"</p>
            </div>
        </section>
    </div>
    
    <div class="notification-container" id="notificationContainer">
        <!-- Notifications will appear here -->
    </div>
    
    <footer>
        <div class="footer-content">
            <p>© 2023 TradeMonitor Academy. All rights reserved.</p>
            <p>Learn how to monitor trades like a professional</p>
            <div class="social-links">
                <a href="#"><i class="fab fa-twitter"></i></a>
                <a href="#"><i class="fab fa-facebook-f"></i></a>
                <a href="#"><i class="fab fa-instagram"></i></a>
                <a href="#"><i class="fab fa-linkedin-in"></i></a>
                <a href="#"><i class="fab fa-youtube"></i></a>
            </div>
        </div>
    </footer>

    <script>
        // Mobile menu toggle
        const menuBtn = document.getElementById('menuBtn');
        const navLinks = document.getElementById('navLinks');
        
        menuBtn.addEventListener('click', () => {
            navLinks.classList.toggle('active');
        });
        
        // Crypto Chart
        const ctx = document.getElementById('cryptoChart').getContext('2d');
        let chartType = 'line';
        
        // Generate random chart data
        function generateChartData() {
            let data = [];
            let value = 300;
            for (let i = 0; i < 100; i++) {
                value += Math.random() * 10 - 5;
                data.push(value);
            }
            return data;
        }
        
        const chartData = generateChartData();
        
        let cryptoChart = new Chart(ctx, {
            type: chartType,
            data: {
                labels: Array.from({length: 100}, (_, i) => i + 1),
                datasets: [{
                    label: 'BTC/USD',
                    data: chartData,
                    borderColor: '#64ffda',
                    backgroundColor: 'rgba(100, 255, 218, 0.1)',
                    borderWidth: 2,
                    pointRadius: 0,
                    fill: true,
                    tension: 0.4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        display: false
                    },
                    tooltip: {
                        mode: 'index',
                        intersect: false
                    }
                },
                scales: {
                    x: {
                        grid: {
                            display: false,
                            drawBorder: false
                        },
                        ticks: {
                            display: false
                        }
                    },
                    y: {
                        grid: {
                            color: 'rgba(255, 255, 255, 0.05)'
                        },
                        ticks: {
                            color: '#a8b2d1'
                        }
                    }
                }
            }
        });
        
        // Toggle chart type
        document.getElementById('toggleChart').addEventListener('click', function() {
            chartType = chartType === 'line' ? 'bar' : 'line';
            cryptoChart.destroy();
            
            cryptoChart = new Chart(ctx, {
                type: chartType,
                data: {
                    labels: Array.from({length: 100}, (_, i) => i + 1),
                    datasets: [{
                        label: 'BTC/USD',
                        data: chartData,
                        borderColor: '#64ffda',
                        backgroundColor: 'rgba(100, 255, 218, 0.1)',
                        borderWidth: 2,
                        pointRadius: 0,
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            mode: 'index',
                            intersect: false
                        }
                    },
                    scales: {
                        x: {
                            grid: {
                                display: false,
                                drawBorder: false
                            },
                            ticks: {
                                display: false
                            }
                        },
                        y: {
                            grid: {
                                color: 'rgba(255, 255, 255, 0.05)'
                            },
                            ticks: {
                                color: '#a8b2d1'
                            }
                        }
                    }
                }
            });
        });
        
        // Notifications
        const notifications = [
            { name: 'Michael C.', time: '10', gain: '100%' },
            { name: 'Jessica T.', time: '20', gain: '200%' },
            { name: 'David L.', time: '14', gain: '290%' },
            { name: 'Amanda R.', time: '29', gain: '350%' },
            { name: 'Kevin M.', time: '17', gain: '180%' },
            { name: 'Sophia P.', time: '22', gain: '240%' }
        ];
        
        function showRandomNotification() {
            const notification = notifications[Math.floor(Math.random() * notifications.length)];
            const notificationElement = document.createElement('div');
            notificationElement.className = 'notification';
            notificationElement.innerHTML = `
                <i class="fas fa-money-bill-wave"></i>
                <div>
                    <strong>${notification.name}</strong> made ${notification.gain} profit in ${notification.time} minutes!
                </div>
            `;
            
            document.getElementById('notificationContainer').appendChild(notificationElement);
            
            // Remove notification after 5 seconds
            setTimeout(() => {
                notificationElement.remove();
            }, 5000);
        }
        
        // Show initial notification
        showRandomNotification();
        
        // Show notification every 10 seconds
        setInterval(showRandomNotification, 10000);
        
        // Simulate chart updates
        setInterval(() => {
            cryptoChart.data.datasets[0].data.push(cryptoChart.data.datasets[0].data[cryptoChart.data.datasets[0].data.length - 1] + Math.random() * 10 - 5);
            cryptoChart.data.datasets[0].data.shift();
            cryptoChart.update('none');
        }, 2000);
    </script>
</body>
</html>
