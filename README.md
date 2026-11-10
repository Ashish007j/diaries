<div align="center">

# The Diaries

### A modern blogging platform with an AI-powered admin workspace.

Discover articles, explore categories, join conversations, and manage content from one place.

[![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-7-646CFF?logo=vite&logoColor=white)](https://vite.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-Backend-339933?logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-5-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Database-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)

</div>

---

## Overview

**The Diaries** is a full-stack blogging platform that combines a reader-friendly publishing experience with a dedicated administrator workspace.

Readers can discover published articles, browse content by category, and submit comments. Administrators can create and manage posts, moderate comments, upload cover images, and generate article drafts with Google Gemini.

## Features

### For readers

- Browse published articles and open individual posts.
- Explore articles by category.
- Submit comments for administrator review.
- Use the responsive interface on desktop and mobile devices.

### For administrators

- Secure administrator sign-in using JWT-based authentication.
- View dashboard statistics and recent posts.
- Create, publish, unpublish, and delete blog posts.
- Write and format articles using a rich-text editor.
- Generate article drafts with Google Gemini.
- Upload and optimize cover images using ImageKit.
- Review, approve, and delete comments.

## Technology Stack

| Area | Technologies |
| --- | --- |
| Frontend | React 19, Vite 7, React Router 7, Tailwind CSS 4 |
| UI and content | Quill, Motion, Marked, React Hot Toast |
| Backend | Node.js, Express 5 |
| Database | MongoDB, Mongoose |
| Authentication | JSON Web Token (JWT) |
| AI content generation | Google Gemini, Google GenAI SDK |
| Image uploads | ImageKit, Multer |
| HTTP requests | Axios |

## Project Structure

```text
diaries/
└── DevTales-main/
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
```

## Getting Started

Follow the steps below to run the project locally.

### Prerequisites

Make sure the following are installed or available:

- [Node.js](https://nodejs.org/) and npm
- A MongoDB database (local installation or [MongoDB Atlas](https://www.mongodb.com/atlas))
- An [ImageKit](https://imagekit.io/) account for image uploads
- A [Google AI Studio](https://aistudio.google.com/) API key for Gemini-powered content generation

### 1. Clone the repository

```bash
git clone https://github.com/Ashish007j/diaries.git
cd diaries
```

The application source is inside `DevTales-main`. Move into that directory:

```bash
cd DevTales-main
```

> If you have placed the contents of `DevTales-main` directly in the repository root, you can skip this directory change.

### 2. Configure and run the backend

Open a terminal in the project directory:

```bash
cd server
npm install
```

Create a `.env` file inside the `server` directory:

```env
PORT=3000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_long_random_secret

ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=your_strong_admin_password

IMAGEKIT_PUBLIC_KEY=your_imagekit_public_key
IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key
IMAGEKIT_URL_ENDPOINT=https://ik.imagekit.io/your_imagekit_id

GEMINI_API_KEY=your_gemini_api_key
```

Start the backend development server:

```bash
npm run server
```

The API will be available at:

```text
http://localhost:3000
```

When the server is running and the database connection is successful, the root endpoint should return:

```text
API is working
```

### 3. Configure and run the frontend

Open a **second terminal** in the `DevTales-main` project directory:

```bash
cd client
npm install
```

Create a `.env` file inside the `client` directory:

```env
VITE_BASE_URL=http://localhost:3000
```

Start the frontend:

```bash
npm run dev
```

Open the local URL printed by Vite. The default is usually:

```text
http://localhost:5173
```

### 4. Open the admin panel

Visit:

```text
http://localhost:5173/admin
```

Sign in using the `ADMIN_EMAIL` and `ADMIN_PASSWORD` values configured in `server/.env`.

## API Reference

**Base URL:** `http://localhost:3000`

### Blog routes

| Method | Endpoint | Description | Access |
| --- | --- | --- | --- |
| GET | `/api/blog/all` | Get published blog posts | Public |
| GET | `/api/blog/:blogId` | Get a blog post by ID | Public |
| POST | `/api/blog/add` | Create a blog post with an image | Admin JWT |
| POST | `/api/blog/delete` | Delete a blog post | Admin JWT |
| POST | `/api/blog/toggle-publish` | Toggle publication status | Admin JWT |
| POST | `/api/blog/add-comment` | Submit a comment | Public |
| POST | `/api/blog/comments` | Get comments for a blog post | Public |
| POST | `/api/blog/generate` | Generate draft content with Gemini | Admin JWT |

### Admin routes

| Method | Endpoint | Description | Access |
| --- | --- | --- | --- |
| POST | `/api/admin/login` | Sign in as administrator | Public |
| GET | `/api/admin/dashboard` | Get dashboard data | Admin JWT |
| GET | `/api/admin/blogs` | Get all posts for management | Admin JWT |
| GET | `/api/admin/comments` | Get comments for moderation | Admin JWT |
| POST | `/api/admin/approve-comment` | Approve a comment | Admin JWT |
| POST | `/api/admin/delete-comment` | Delete a comment | Admin JWT |

### Authentication

Protected API requests use a JWT in the `Authorization` header.

Blog creation uses `multipart/form-data` with an image file and a JSON-encoded `blog` field.

## Available Scripts

| Directory | Command | Description |
| --- | --- | --- |
| `client` | `npm run dev` | Start the Vite development server |
| `client` | `npm run build` | Create a production build |
| `client` | `npm run preview` | Preview the production build |
| `client` | `npm run lint` | Run ESLint |
| `server` | `npm run server` | Start the backend with Nodemon |
| `server` | `npm start` | Start the backend with Node.js |

## Environment Variables

Keep credentials in local environment files and configure the corresponding values in your deployment environment.

| File | Purpose |
| --- | --- |
| `server/.env` | Backend, database, authentication, ImageKit, and Gemini configuration |
| `client/.env` | Frontend API base URL |

Never commit real API keys, database credentials, JWT secrets, or administrator passwords.

## Deployment

The project includes Vercel configuration files for the frontend and backend. A typical deployment workflow is:

1. Deploy the backend and configure its environment variables.
2. Confirm that the backend can connect to MongoDB and the ImageKit and Gemini services.
3. Set `VITE_BASE_URL` in the frontend deployment environment to the public backend URL.
4. Deploy the frontend.
5. Verify administrator authentication, article publishing, image uploads, and comment moderation in the deployed environment.

> Deployment should be tested in your own hosting environment before the application is considered production-ready.

## Security Notes

- Do not commit `.env` files or expose API keys and passwords.
- Add environment files to `.gitignore`.
- Provide sanitized `.env.example` files so other developers know which variables are required.
- If credentials have already been pushed to a remote repository, rotate them with the relevant providers. Deleting a file from the latest commit does not remove it from Git history.
- Use a strong, unique `JWT_SECRET` and a strong administrator password.

Recommended `.gitignore` entries:

```gitignore
node_modules/
.env
.env.*
!.env.example
dist/
```

## Project Notes

- The admin area uses configured administrator credentials; the current codebase does not implement a public user-registration flow.
- The newsletter section is currently a frontend interface. A working newsletter subscription backend is not included in the supplied source.

## Author

**Ashish Kumar Jha**

- GitHub: [@Ashish007j](https://github.com/Ashish007j)
- Project Repository: [diaries](https://github.com/Ashish007j/diaries)

---

<div align="center">

If you find this project useful, consider giving the repository a ⭐.

</div>
