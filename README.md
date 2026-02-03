movie-streaming-ott/
├── client/                          # React.js Frontend
│   ├── public/
│   │   ├── index.html
│   │   ├── favicon.ico
│   │   └── assets/                  # Static assets (logos, icons)
│   ├── src/
│   │   ├── components/              # Reusable UI components
│   │   │   ├── Header.js            # Navigation bar
│   │   │   ├── Footer.js            # Footer
│   │   │   ├── MovieCard.js         # Card for movie thumbnails
│   │   │   ├── VideoPlayer.js       # Custom video player (supports multiple servers)
│   │   │   ├── DownloadModal.js     # Modal for download links
│   │   │   ├── ChatWidget.js        # Live chat component
│   │   │   ├── AIBot.js             # AI Bot for queries
│   │   │   └── CategorySection.js   # Section for categories (Movies, 18+, etc.)
│   │   ├── pages/                   # Page components
│   │   │   ├── HomePage.js          # Main homepage (code provided below)
│   │   │   ├── MovieDetails.js      # Individual movie page
│   │   │   ├── CategoryPage.js      # Page for specific categories
│   │   │   ├── AdminDashboard.js    # Admin panel (code provided below)
│   │   │   ├── Login.js             # User/Admin login
│   │   │   ├── Signup.js            # User signup
│   │   │   └── Profile.js           # User profile
│   │   ├── hooks/                   # Custom React hooks
│   │   │   ├── useAuth.js           # Authentication hook
│   │   │   └── useMovies.js         # Hook for fetching movies
│   │   ├── utils/                   # Utility functions
│   │   │   ├── api.js               # Axios instance for API calls
│   │   │   └── constants.js         # App constants (e.g., categories)
│   │   ├── context/                 # React Context for global state
│   │   │   ├── AuthContext.js       # User authentication state
│   │   │   └── MovieContext.js      # Movie data state
│   │   ├── App.js                   # Main app component with routing
│   │   ├── index.js                 # Entry point
│   │   └── styles/                  # Tailwind CSS custom styles
│   │       └── tailwind.config.js   # Tailwind config for dark theme
│   ├── package.json                 # Frontend dependencies (e.g., react, tailwindcss, axios)
│   └── .env                         # Environment variables (e.g., API_BASE_URL)
├── server/                          # Node.js/Express Backend
│   ├── controllers/                 # Route handlers
│   │   ├── authController.js        # Login/signup logic
│   │   ├── movieController.js       # Movie CRUD operations
│   │   ├── categoryController.js    # Category management
│   │   ├── adminController.js       # Admin-specific actions (upload, edit)
│   │   └── chatController.js        # Live chat and AI bot logic
│   ├── models/                      # MongoDB schemas
│   │   ├── User.js                  # User schema (with roles: user/admin)
│   │   ├── Movie.js                 # Movie schema (title, servers, downloads, category)
│   │   ├── Category.js              # Category schema
│   │   └── Chat.js                  # Chat message schema
│   ├── routes/                      # API routes
│   │   ├── auth.js                  # /api/auth
│   │   ├── movies.js                # /api/movies
│   │   ├── categories.js            # /api/categories
│   │   ├── admin.js                 # /api/admin (protected)
│   │   └── chat.js                  # /api/chat
│   ├── middleware/                  # Custom middleware
│   │   ├── authMiddleware.js        # JWT verification and role checks
│   │   ├── uploadMiddleware.js      # File upload (e.g., for movie posters)
│   │   └── securityMiddleware.js    # CORS, rate limiting, helmet for security
│   ├── config/                      # Configuration files
│   │   ├── database.js              # MongoDB connection
│   │   └── jwt.js                   # JWT secret setup
│   ├── utils/                       # Utilities
│   │   ├── aiBot.js                 # AI bot logic (integrate with Dialogflow/Rasa)
│   │   └── linkShortener.js         # Link shortener/ads integration
│   ├── app.js                       # Express app setup
│   ├── server.js                    # Server entry point
│   ├── package.json                 # Backend dependencies (e.g., express, mongoose, bcrypt, jsonwebtoken, socket.io)
│   └── .env                         # Environment variables (e.g., MONGO_URI, JWT_SECRET)
├── database/                        # MongoDB setup (optional, for local dev)
│   └── seed.js                      # Script to seed initial data
├── docs/                            # Documentation
│   ├── API.md                       # API endpoints
│   └── README.md                    # Project overview
├── .gitignore                       # Ignore node_modules, .env, etc.
├── package.json                     # Root package.json for scripts
└── README.md                        # Project README
