Overview
The Diaries is a full-stack blogging platform that brings together a reader-friendly publishing experience and a dedicated admin workspace. Readers can discover articles, explore categories, and leave comments. Administrators can manage posts and comments, upload cover images, and use Google Gemini to generate article drafts.
Features
For readers
- Browse published articles and view individual posts.
- Explore posts by category.
- Submit comments for administrator review.
- Use a responsive interface across desktop and mobile screens.
For administrators
- Secure admin sign-in with JWT-based authentication.
- View dashboard statistics and recent posts.
- Create, publish, unpublish, and delete blog posts.
- Write and format articles with the rich-text editor.
- Generate article drafts with Google Gemini.
- Upload and optimize cover images using ImageKit.
- Review, approve, and delete comments.
Tech stack
Area	Technologies
Frontend	React 19, Vite 7, React Router 7, Tailwind CSS 4
UI and content	Quill, Motion, Marked, React Hot Toast
Backend	Node.js, Express 5
Database	MongoDB, Mongoose
Authentication	JSON Web Token (JWT)
AI content generation	Google Gemini (Google GenAI SDK)
Image uploads	ImageKit, Multer
HTTP requests	Axios


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
│   ├── configs/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── server.js
│   ├── package.json
│   └── vercel.json
└── .gitignore
Getting started
Follow these steps to run DevTales locally.
Prerequisites
Make sure you have the following:
- Node.js and npm installed.
- A MongoDB database (local or Atlas).
- An ImageKit account for image uploads.
- A Google AI Studio API key for Gemini-powered content generation.
1. Clone the repository
git clone https://github.com/Ashish007j/diaries.git
cd diaries
The source code is inside DevTales-main. Move into that directory before continuing:
cd DevTales-main
If you have placed the contents of DevTales-main directly in the repository root, skip that command.
2. Set up the backend
cd server
npm install
Create a .env file inside the server directory:
PORT=3000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_long_random_secret
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=your_strong_admin_password
IMAGEKIT_PUBLIC_KEY=your_imagekit_public_key
IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key
IMAGEKIT_URL_ENDPOINT=https://ik.imagekit.io/your_imagekit_id
GEMINI_API_KEY=your_gemini_api_key
Start the backend development server:
npm run server
The API runs at http://localhost:3000. When the server and database are connected, the root endpoint should return API is working.
3. Set up the frontend
Open a second terminal and navigate to the client directory from the project root:
cd DevTales-main/client
npm install
Create a .env file inside client:
VITE_BASE_URL=http://localhost:3000
Start the frontend:
npm run dev
Open the local URL printed by Vite (usually http://localhost:5173).
4. Open the admin panel
Visit http://localhost:5173/admin and sign in with the ADMIN_EMAIL and ADMIN_PASSWORD configured in server/.env.
API reference
Base URL: http://localhost:3000
Blog routes
Method	Endpoint	Description	Authentication
GET	/api/blog/all	Get published blog posts	Public
GET	/api/blog/:blogId	Get a blog post by ID	Public
POST	/api/blog/add	Create a blog post with an image	Admin JWT
POST	/api/blog/delete	Delete a blog post	Admin JWT
POST	/api/blog/toggle-publish	Toggle publication status	Admin JWT
POST	/api/blog/add-comment	Submit a comment	Public
POST	/api/blog/comments	Get comments for a blog post	Public
POST	/api/blog/generate	Generate draft content with Gemini	Admin JWT


Admin routes
Method	Endpoint	Description	Authentication
POST	/api/admin/login	Sign in as administrator	Public
GET	/api/admin/dashboard	Get dashboard data	Admin JWT
GET	/api/admin/blogs	Get all posts for management	Admin JWT
GET	/api/admin/comments	Get comments for moderation	Admin JWT
POST	/api/admin/approve-comment	Approve a comment	Admin JWT
POST	/api/admin/delete-comment	Delete a comment	Admin JWT


Authentication note: Protected API requests use a JWT in the Authorization header. Blog creation uses multipart/form-data with an image file and a JSON-encoded blog field.
Available scripts
Directory	Command	Purpose
client	npm run dev	Start the Vite development server
client	npm run build	Create a production build
client	npm run preview	Preview the production build
client	npm run lint	Run ESLint
server	npm run server	Start the backend with Nodemon
server	npm start	Start the backend with Node.js


Environment variables
Keep all credentials in local environment files and configure the same variables in your deployment environment. Never place real API keys, database credentials, JWT secrets, or admin passwords in source code.

For local development, the project uses:
- server/.env for backend and third-party service configuration.
- client/.env for the frontend API base URL.
Deployment
The project includes Vercel configuration files for the frontend and backend. To deploy it:
1. Deploy the backend and configure its environment variables.
2. Ensure the deployed backend can connect to MongoDB and the ImageKit and Gemini services.
3. Set VITE_BASE_URL in the frontend deployment to the public backend URL.
4. Deploy the frontend.
5. Test admin authentication, article publishing, image uploads, and comment moderation in the deployed environment.
Deployment should be verified in your own hosting environment before treating the application as production-ready.
Security
- Do not commit .env files or expose API keys and passwords.
- Add environment files to .gitignore and provide sanitized .env.example files for other developers.
- If credentials have already been pushed to a remote repository, rotate them with the relevant providers. Removing a file from the latest commit does not remove it from Git history.
- Use a strong, unique JWT_SECRET and a strong administrator password.
Recommended .gitignore entries:
node_modules/
.env
.env.*
!.env.example
dist/
Project notes
- The admin area uses configured administrator credentials; the current codebase does not implement a public user-registration flow.
- The newsletter section is currently a frontend interface; a working subscription backend is not included in the supplied source.
Author
Ashish Kumar Jha
GitHub
