The Diaries — AI-Powered Blogging Platform
A full-stack blogging application built with the MERN stack (MongoDB, Express.js, React, and Node.js). DevTales combines a responsive public blog with an administrator workspace for publishing articles, managing comments, and generating article drafts with Google Gemini.
Repository: Ashish007j/diaries

Features
Reader experience
- Browse published blog posts and open individual articles.
- Explore articles by category and use the blog search interface.
- Submit comments on blog posts, subject to administrator approval.
- Responsive interface with loading indicators and toast notifications.
Administrator workspace
- Sign in using configured administrator credentials; protected routes use JWT authentication.
- View dashboard statistics and recent posts.
- Create posts with titles, subtitles, categories, rich-text content, and cover images.
- Generate draft content from a title using the Google Gemini API.
- Upload and optimize blog cover images with ImageKit.
- List, publish/unpublish, and delete blog posts.
- Review, approve, and delete reader comments.
Current scope: The newsletter subscription section is a UI form; the provided code does not establish a working subscription backend. This project uses a configured single-admin login rather than a general user registration system.

Tech stack
Layer	Technologies
Frontend	React 19, Vite 7, React Router 7, Tailwind CSS 4
UI and editing	Quill, Motion, React Hot Toast, Marked
Backend	Node.js, Express 5
Database	MongoDB, Mongoose
Authentication	JSON Web Tokens (JWT)
AI integration	Google GenAI SDK (Gemini)
Image management	ImageKit, Multer
HTTP client	Axios
Deployment configuration	Vercel configuration files in both client and server


Project structure
DevTales-main/
├── client/
│   ├── public/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   │   └── admin/
│   │   ├── context/
│   │   ├── pages/
│   │   │   └── admin/
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   └── vercel.json
├── server/
│   ├── configs/          # MongoDB, Gemini, ImageKit
│   ├── controllers/      # Blog and admin handlers
│   ├── middleware/       # JWT verification and file uploads
│   ├── models/           # Blog and Comment schemas
│   ├── routes/           # Blog and admin endpoints
│   ├── server.js
│   ├── package.json
│   └── vercel.json
└── .gitignore
Getting started
Prerequisites
- Node.js and npm (use a recent Node.js LTS version compatible with Vite 7)
- MongoDB instance (local or MongoDB Atlas)
- ImageKit account and API credentials
- Google Gemini API key for AI-assisted writing
1. Clone the repository
git clone https://github.com/Ashish007j/diaries.git
cd diaries
The uploaded archive contains a DevTales-main/ directory. If that directory is retained in your GitHub repository, enter it with cd DevTales-main before running the commands below. Otherwise, run them from the directory containing client/ and server/.

2. Configure and start the backend
cd server
npm install
Create server/.env:
PORT=3000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=replace_with_a_long_random_secret
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=replace_with_a_strong_password
IMAGEKIT_PUBLIC_KEY=your_imagekit_public_key
IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key
IMAGEKIT_URL_ENDPOINT=https://ik.imagekit.io/your_id
GEMINI_API_KEY=your_gemini_api_key
Run the development server:
npm run server
The API should respond at http://localhost:3000/ with API is working after MongoDB connects successfully.
3. Configure and start the frontend
Open a second terminal from the project root:
cd client
npm install
Create client/.env:
VITE_BASE_URL=http://localhost:3000
Start the frontend:
npm run dev
Open the URL displayed by Vite (typically http://localhost:5173).
4. Open the admin dashboard
Navigate to http://localhost:5173/admin and sign in using the ADMIN_EMAIL and ADMIN_PASSWORD values configured in server/.env.
API reference
Base URL for local development: http://localhost:3000
Blog endpoints
Method	Endpoint	Purpose	JWT required
GET	/api/blog/all	Get published blogs	No
GET	/api/blog/:blogId	Get a blog by ID	No
POST	/api/blog/add	Create a blog with an image	Yes
POST	/api/blog/delete	Delete a blog	Yes
POST	/api/blog/toggle-publish	Change publication status	Yes
POST	/api/blog/add-comment	Submit a comment	No
POST	/api/blog/comments	Get comments for a blog	No
POST	/api/blog/generate	Generate article content with Gemini	Yes


Admin endpoints
Method	Endpoint	Purpose	JWT required
POST	/api/admin/login	Authenticate administrator	No
GET	/api/admin/dashboard	Retrieve dashboard data	Yes
GET	/api/admin/blogs	Retrieve all blogs for administration	Yes
GET	/api/admin/comments	Retrieve comments for moderation	Yes
POST	/api/admin/approve-comment	Approve a comment	Yes
POST	/api/admin/delete-comment	Delete a comment	Yes


Authentication: The current middleware reads the JWT directly from the Authorization header. The frontend sends the token in that header after login. Blog creation uses multipart/form-data with an image file and a JSON-encoded blog field.
Available scripts
Directory	Command	Description
client	npm run dev	Start Vite development server
client	npm run build	Build the frontend for production
client	npm run preview	Preview the production build
client	npm run lint	Run ESLint
server	npm run server	Start the API with Nodemon
server	npm start	Start the API with Node.js


Data models
Blog: title, subtitle, description, category, image URL, publication status, and timestamps.

Comment: related blog, commenter name, content, approval status, and timestamps.

MongoDB is configured with the database name quickblog in server/configs/db.js.
Deployment notes
The project includes vercel.json files for the client and server. Before deploying:
1. Configure the frontend and backend build/runtime settings for your hosting platform.
2. Set backend secrets as environment variables on the server deployment.
3. Set VITE_BASE_URL to the publicly accessible backend URL in the frontend build environment.
4. Allow your deployed backend to access MongoDB and confirm ImageKit/Gemini credentials.
5. Test authentication, publishing, image uploads, and comment moderation after deployment.
Deployment has not been verified as part of this README preparation.
Security notes
- Do not commit .env files, API keys, JWT secrets, or administrator credentials. The supplied archive contains both client/.env and server/.env; remove them from Git tracking before publishing.
- The supplied root .gitignore only ignores node_modules. Add .env patterns to .gitignore and keep sanitized .env.example files for onboarding.
- If real credentials have already been committed or exposed, rotate them with their providers. Adding .gitignore does not remove secrets from existing Git history.
- For production use, consider stronger admin authentication, login rate limiting, stricter CORS rules, request validation, and appropriate token expiry/handling.
Recommended .gitignore additions:
node_modules/
.env
.env.*
!.env.example
dist/
Author
Ashish Kumar Jha
GitHub: @Ashish007j
