<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ISKCON Daily Puja</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #FF8C00;
            --secondary-color: #FFA500;
            --text-color: #fff;
            --dark-color: #222;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }

        body {
            color: var(--text-color);
            line-height: 1.6;
            overflow-x: hidden;
            background-image: url('https://i.imgur.com/JrQ8yHd.jpg');
            background-size: cover;
            background-attachment: fixed;
            background-position: center;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: -1;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            margin-bottom: 30px;
            border-bottom: 2px solid var(--primary-color);
        }

        .logo {
            display: flex;
            align-items: center;
        }

        .logo img {
            height: 50px;
            margin-right: 15px;
            border-radius: 50%;
            border: 2px solid var(--primary-color);
        }

        .logo h1 {
            color: var(--primary-color);
            font-size: 24px;
            text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5);
        }

        .admin-login {
            font-size: 24px;
            color: var(--primary-color);
            cursor: pointer;
            transition: transform 0.3s;
            background: rgba(255, 255, 255, 0.2);
            padding: 8px;
            border-radius: 50%;
        }

        .admin-login:hover {
            transform: scale(1.1);
        }

        main {
            flex: 1;
        }

        .video-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .video-card {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            transition: all 0.3s;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            position: relative;
        }

        .video-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.4);
            border: 1px solid var(--primary-color);
        }

        .video-player {
            width: 100%;
            height: 180px;
            background-color: var(--dark-color);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .video-player video {
            max-width: 100%;
            max-height: 100%;
        }

        .video-info {
            padding: 15px;
        }

        .video-info h3 {
            margin-bottom: 10px;
            color: var(--primary-color);
        }

        .video-date {
            font-size: 14px;
            color: #ccc;
        }

        .delete-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: rgba(255, 0, 0, 0.7);
            color: white;
            border: none;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .video-card:hover .delete-btn {
            opacity: 1;
        }

        .delete-btn:hover {
            background: rgba(255, 0, 0, 0.9);
        }

        .no-videos {
            text-align: center;
            grid-column: 1 / -1;
            padding: 50px;
            color: #ccc;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
        }

        .no-videos i {
            font-size: 50px;
            margin-bottom: 20px;
            color: var(--primary-color);
        }

        footer {
            text-align: center;
            padding: 20px;
            margin-top: 30px;
            border-top: 1px solid rgba(255, 140, 0, 0.3);
            color: var(--primary-color);
            font-weight: bold;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 5px;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .mantra {
            font-size: 16px;
            margin: 10px 0;
            line-height: 1.8;
        }

        .developer-credit {
            font-size: 14px;
            color: #aaa;
            margin-top: 10px;
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            overflow: auto;
        }

        .modal-content {
            background: rgba(40, 40, 40, 0.95);
            margin: 5% auto;
            padding: 30px;
            border-radius: 8px;
            width: 90%;
            max-width: 500px;
            position: relative;
            border: 1px solid var(--primary-color);
            box-shadow: 0 0 20px rgba(255, 140, 0, 0.3);
        }

        .close-btn {
            position: absolute;
            top: 15px;
            right: 20px;
            font-size: 24px;
            cursor: pointer;
            color: #ccc;
        }

        .close-btn:hover {
            color: var(--primary-color);
        }

        .modal-content h2 {
            color: var(--primary-color);
            margin-bottom: 20px;
            text-align: center;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #ddd;
        }

        .form-group input {
            width: 100%;
            padding: 12px;
            border: 1px solid #444;
            border-radius: 4px;
            font-size: 16px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
        }

        .form-group input:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 5px rgba(255, 140, 0, 0.5);
        }

        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s;
            width: 100%;
            margin-top: 10px;
        }

        button:hover {
            background-color: var(--secondary-color);
            transform: translateY(-2px);
        }

        button i {
            margin-right: 8px;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .logo h1 {
                font-size: 20px;
            }
            
            .video-container {
                grid-template-columns: 1fr;
            }
            
            .modal-content {
                padding: 20px;
            }
            
            .mantra {
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header with ISKCON Logo -->
        <header>
            <div class="logo">
                <img src="https://i.imgur.com/3JQZQ9u.png" alt="ISKCON Logo">
                <h1>ISKCON Daily Puja</h1>
            </div>
            <div class="admin-login" id="adminLoginBtn">
                <i class="fas fa-user-shield"></i>
            </div>
        </header>

        <!-- Main Content Area -->
        <main>
            <div class="video-container" id="videoContainer">
                <!-- Videos will be loaded here dynamically -->
                <div class="no-videos">
                    <i class="fas fa-video-slash"></i>
                    <p>No puja videos available yet</p>
                </div>
            </div>
        </main>

        <!-- Footer -->
        <footer>
            <p>Hare Krishna Hare Krishna<br>Krishna Krishna Hare Hare<br>Hare Rama Hare Rama<br>Rama Rama Hare Hare</p>
            
            <div class="mantra">
                श्रीकृष्णचैतन्य प्रभु नित्यानंद ।<br>
                श्री अद्वैत गदाधर श्रीवासादि गौर भक्तवृंद ॥
            </div>
            
            <div class="developer-credit">
                App Developed By Dev Makwana<br>EbixServer Pvt Ltd © 2025
            </div>
        </footer>
    </div>

    <!-- Admin Login Modal -->
    <div class="modal" id="loginModal">
        <div class="modal-content">
            <span class="close-btn">&times;</span>
            <h2><i class="fas fa-user-shield"></i> Admin Login</h2>
            <form id="loginForm">
                <div class="form-group">
                    <label for="username"><i class="fas fa-user"></i> Username:</label>
                    <input type="text" id="username" required>
                </div>
                <div class="form-group">
                    <label for="password"><i class="fas fa-lock"></i> Password:</label>
                    <input type="password" id="password" required>
                </div>
                <button type="submit"><i class="fas fa-sign-in-alt"></i> Login</button>
            </form>
        </div>
    </div>

    <!-- Upload Modal -->
    <div class="modal" id="uploadModal">
        <div class="modal-content">
            <span class="close-btn">&times;</span>
            <h2><i class="fas fa-cloud-upload-alt"></i> Upload New Puja Video</h2>
            <form id="uploadForm">
                <div class="form-group">
                    <label for="videoTitle"><i class="fas fa-heading"></i> Title:</label>
                    <input type="text" id="videoTitle" required placeholder="e.g., Morning Aarti - Janmashtami Special">
                </div>
                <div class="form-group">
                    <label for="videoDate"><i class="fas fa-calendar-alt"></i> Date:</label>
                    <input type="date" id="videoDate" required>
                </div>
                <div class="form-group">
                    <label for="videoFile"><i class="fas fa-video"></i> Video File:</label>
                    <input type="file" id="videoFile" accept="video/*" required>
                </div>
                <button type="submit"><i class="fas fa-upload"></i> Upload</button>
            </form>
        </div>
    </div>

    <script>
        // Sample video data (in a real app, this would come from a database)
        let videos = [
            {
                id: 1,
                title: "Morning Aarti - Janmashtami Special",
                date: "2023-08-30",
                url: "https://example.com/video1.mp4"
            },
            {
                id: 2,
                title: "Evening Puja - Radha Krishna",
                date: "2023-08-29",
                url: "https://example.com/video2.mp4"
            }
        ];

        let isAdminLoggedIn = false;

        // DOM Elements
        const adminLoginBtn = document.getElementById('adminLoginBtn');
        const loginModal = document.getElementById('loginModal');
        const uploadModal = document.getElementById('uploadModal');
        const loginForm = document.getElementById('loginForm');
        const uploadForm = document.getElementById('uploadForm');
        const videoContainer = document.getElementById('videoContainer');
        const closeButtons = document.querySelectorAll('.close-btn');

        // Event Listeners
        document.addEventListener('DOMContentLoaded', renderVideos);

        adminLoginBtn.addEventListener('click', () => {
            if (isAdminLoggedIn) {
                if (confirm('Do you want to logout?')) {
                    logoutAdmin();
                }
            } else {
                loginModal.style.display = 'block';
            }
        });

        closeButtons.forEach(btn => {
            btn.addEventListener('click', () => {
                loginModal.style.display = 'none';
                uploadModal.style.display = 'none';
            });
        });

        window.addEventListener('click', (e) => {
            if (e.target === loginModal) {
                loginModal.style.display = 'none';
            }
            if (e.target === uploadModal) {
                uploadModal.style.display = 'none';
            }
        });

        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            // Credentials as per your request
            if (username === 'iskconpali' && password === 'haribol') {
                loginAdmin();
            } else {
                alert('Invalid credentials. Please try again.');
            }
        });

        uploadForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const title = document.getElementById('videoTitle').value;
            const date = document.getElementById('videoDate').value;
            const fileInput = document.getElementById('videoFile');
            
            if (fileInput.files.length > 0) {
                const file = fileInput.files[0];
                const videoUrl = URL.createObjectURL(file);
                
                // Add new video to the array
                const newVideo = {
                    id: Date.now(), // Unique ID
                    title: title,
                    date: date,
                    url: videoUrl
                };
                
                videos.unshift(newVideo); // Add to beginning of array
                renderVideos();
                uploadModal.style.display = 'none';
                uploadForm.reset();
                
                alert('Hare Krishna! Video uploaded successfully!');
            }
        });

        // Functions
        function renderVideos() {
            if (videos.length === 0) {
                videoContainer.innerHTML = `
                    <div class="no-videos">
                        <i class="fas fa-video-slash"></i>
                        <p>No puja videos available yet</p>
                    </div>
                `;
                return;
            }
            
            videoContainer.innerHTML = videos.map(video => `
                <div class="video-card">
                    ${isAdminLoggedIn ? 
                        `<button class="delete-btn" onclick="deleteVideo(${video.id})">
                            <i class="fas fa-trash"></i>
                        </button>` : ''
                    }
                    <div class="video-player">
                        <video controls>
                            <source src="${video.url}" type="video/mp4">
                            Your browser does not support the video tag.
                        </video>
                    </div>
                    <div class="video-info">
                        <h3>${video.title}</h3>
                        <p class="video-date">${formatDate(video.date)}</p>
                    </div>
                </div>
            `).join('');
        }

        function formatDate(dateString) {
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            return new Date(dateString).toLocaleDateString('en-IN', options);
        }

        function loginAdmin() {
            isAdminLoggedIn = true;
            adminLoginBtn.innerHTML = '<i class="fas fa-sign-out-alt"></i>';
            loginModal.style.display = 'none';
            loginForm.reset();
            alert('Hare Krishna! Admin login successful!');
            renderVideos(); // Re-render to show delete buttons
            uploadModal.style.display = 'block'; // Show upload modal immediately after login
        }

        function logoutAdmin() {
            isAdminLoggedIn = false;
            adminLoginBtn.innerHTML = '<i class="fas fa-user-shield"></i>';
            alert('Logged out successfully. Hare Krishna!');
            renderVideos(); // Re-render to hide delete buttons
        }

        function deleteVideo(id) {
            if (confirm('Are you sure you want to delete this puja video?')) {
                videos = videos.filter(video => video.id !== id);
                renderVideos();
                alert('Video deleted successfully!');
            }
        }

        // Set today's date as default in upload form
        document.getElementById('videoDate').valueAsDate = new Date();
    </script>
</body>
</html>
