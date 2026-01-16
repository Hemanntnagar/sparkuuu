SparkUU - Attendance & Timetable Management Platform
A comprehensive platform for managing student attendance, timetables, and batch management with face recognition and real-time updates.

Features
Student Features
Email/OTP login
Face recognition registration and attendance marking
Real-time timetable view with system date/time
Batch-based timetable access
Liveness detection for attendance (prevents photo/video spoofing)
Admin Features
User management (Students, Teachers, Admins)
Batch creation and management
Weekly timetable management (grid view)
Student approval system
Attendance reports with percentages
Export attendance reports to CSV
Search and alphabetical sorting
Teacher Features
Class management
Schedule viewing
Tech Stack
Backend
Node.js
Express.js
MongoDB with Mongoose
JWT authentication
Frontend
React 18
React Router
Face-api.js
Tailwind CSS
Vite
Project Structure
sparkuu/
├── backend/              # Node.js/Express backend
│   ├── models/          # MongoDB models
│   ├── routes/          # API routes
│   ├── server.js        # Main server file
│   └── package.json
├── frontend/            # React frontend
│   ├── src/
│   │   ├── components/  # React components
│   │   ├── pages/       # Page components
│   │   ├── services/    # API services
│   │   └── context/     # React context
│   └── package.json
└── index.html           # Original single-page application
Setup Instructions
Backend Setup
Navigate to backend directory:

cd backend
Install dependencies:

npm install
Set up environment variables:

cp .env.example .env
Edit .env and configure:

MongoDB connection string
JWT secret
Port (default: 5000)
Start MongoDB (if running locally):

mongod
Or use MongoDB Atlas cloud database.

Run the server:

npm start
For development with auto-reload:

npm run dev
Frontend Setup
Navigate to frontend directory:

cd frontend
Install dependencies:

npm install
Set up environment variables: Create .env file:

VITE_API_URL=http://localhost:5000/api
Download face-api.js models:

Download from: https://github.com/justadudewhohacks/face-api.js/tree/master/weights
Place in public/models/ directory
Run the development server:

npm run dev
Build for production:

npm run build
API Endpoints
See backend/README.md for complete API documentation.

Key Features Implementation
Liveness Detection
Face movement tasks (Look Left, Look Right, Move Closer, Move Away)
Movement distance tracking
Face size variation detection
Prevents photo/video spoofing
Attendance System
Face recognition matching
Location verification
Daily attendance tracking
Percentage calculation
Batch-wise reports
Timetable Management
Weekly grid view for admins
Real-time date calculation
Batch-based access
Auto-refresh on updates
Development Notes
Face recognition models need to be downloaded separately
OTP system is simplified (for production, integrate SMS/Email service)
JWT authentication middleware should be added for protected routes
Face matching algorithm is simplified (enhance for production)
License
ISC
