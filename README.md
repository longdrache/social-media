# VN-Social Network (social-media)

A full-featured social media platform built as a graduation thesis project at Ho Chi Minh City University of Technology and Education (HCMUTE). The app includes posts, comments, likes, real-time chat, video calling, notifications, and an admin panel.

---

## Features

### User Features
- **Authentication** — Register, login, email verification, password reset, JWT-based sessions
- **Posts** — Create text posts or posts with image, audio, video, and file attachments
- **Comments & Likes** — Comment on posts, like/unlike posts and comments
- **Real-time Chat** — Private and group conversations with text, media, reactions, and message recall
- **Video/Audio Calling** — WebRTC-based calls with signaling through Socket.IO
- **Follow System** — Follow/unfollow other users
- **Notifications** — Real-time notifications for interactions
- **User Profiles** — Change avatar, update profile info, change password
- **File Sharing** — Upload and share files up to 500 MB
- **NSFW Filtering** — Client-side NSFW detection (nsfwjs + TensorFlow.js) and server-side profanity filter

### Admin Features
- **Admin Panel** — Separate admin login and dashboard
- **User Management** — Block/unblock users, delete posts
- **Admin Creation** — Create new admin accounts
- **Role-Based Access** — Three roles: user, admin, superadmin

---

## Tech Stack

### Backend — Main API Server (`source_Back-end/source_BE`)
| Technology | Purpose |
|------------|---------|
| Node.js 12+ | Runtime |
| Express 4.17 | REST API framework |
| MongoDB 4.1 + Mongoose 5.13 | Database & ODM |
| Passport + JWT | Authentication |
| Multer + GridFS | File upload & storage |
| Sharp | Image processing |
| Socket.IO 4.3 | Real-time communication |
| Swagger | API documentation |
| Joi | Request validation |
| Winston + Morgan | Logging |
| PM2 | Process manager |
| Helmet | Security headers |
| express-rate-limit | Rate limiting |
| bad-words | Content filtering |

### Backend — Socket Server (`source_Back-end/source_BE_socket`)
| Technology | Purpose |
|------------|---------|
| Node.js 12+ | Runtime |
| Express 4.17 | HTTP server |
| Socket.IO 4.3 | Real-time events |
| MongoDB + Mongoose | Database |
| Passport + JWT | Socket authentication |
| PM2 | Process manager |

### Frontend (`source_Front-end`)
| Technology | Purpose |
|------------|---------|
| React 17 | UI framework |
| Redux + redux-thunk + redux-persist | State management |
| React Router 5 | Routing |
| Axios | HTTP client |
| MUI (Material UI) 5 | UI components |
| Tailwind CSS | Styling |
| Socket.IO Client | Real-time client |
| nsfwjs + TensorFlow.js | NSFW detection |
| Formik + Yup | Form handling |
| Emoji Picker | Emoji support |
| CRACO | Build configuration |

---

## Prerequisites

- Node.js 12+
- MongoDB 4.1+ (multiple databases for different file types)
- SMTP server (for email verification and password reset)

---

## Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/longdrache/social-media.git
cd social-media
```

### 2. Configure Environment Variables

```bash
cp source_Back-end/source_BE/.env.example source_Back-end/source_BE/.env
cp source_Back-end/source_BE_SOCKET/.env.example source_Back-end/source_BE_SOCKET/.env
```

Edit the `.env` files with your configuration. See the [Environment Variables](#environment-variables) section below.

### 3. Install Dependencies

```bash
cd source_Back-end/source_BE
npm install

cd ../source_BE_socket
npm install

cd ../../source_Front-end
npm install
```

### 4. Start the Applications

**Backend (Main API):**
```bash
cd source_Back-end/source_BE
npm run dev
```

**Backend (Socket Server):**
```bash
cd source_Back-end/source_BE_socket
npm run dev
```

**Frontend:**
```bash
cd source_Front-end
npm start
```

The apps will be available at:
- **Frontend:** http://localhost:3000
- **Backend API:** http://localhost:3000 (configured via `PORT`)
- **Socket Server:** http://localhost:3001 (configured via `PORT`)

---

## Environment Variables

### Main API Server (`source_Back-end/source_BE/.env`)

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | API server port | 3000 |
| `MONGODB_URL` | Main MongoDB URL | `mongodb://127.0.0.1:27017/node-boilerplate` |
| `MONGODB_URL_TEST` | Test database URL | (required) |
| `MONGODB_URL_IMAGE` | Image GridFS database URL | (required) |
| `MONGODB_URL_AUDIO` | Audio GridFS database URL | (required) |
| `MONGODB_URL_VIDEO` | Video GridFS database URL | (required) |
| `MONGODB_URL_FILE` | File GridFS database URL | (required) |
| `JWT_SECRET` | JWT signing secret | `thisisasamplesecret` |
| `JWT_ACCESS_EXPIRATION_MINUTES` | Access token TTL | 30 |
| `JWT_REFRESH_EXPIRATION_DAYS` | Refresh token TTL | 30 |
| `JWT_RESET_PASSWORD_EXPIRATION_MINUTES` | Reset password token TTL | 10 |
| `JWT_VERIFY_EMAIL_EXPIRATION_MINUTES` | Verify email token TTL | 10 |
| `SMTP_HOST` | Email server host | `email-server` |
| `SMTP_PORT` | Email server port | 587 |
| `SMTP_USERNAME` | Email username | — |
| `SMTP_PASSWORD` | Email password | — |
| `EMAIL_FROM` | From address | `support@yourapp.com` |

---

## Project Structure

```
social-media/
├── README.md
├── source_Back-end/
│   ├── source_BE/                     # Main REST API server
│   │   ├── .env.example
│   │   ├── package.json
│   │   └── src/
│   │       ├── index.js               # Entry point
│   │       ├── app.js                 # Express app setup
│   │       ├── config/                # Configuration (env, passport, upload, etc.)
│   │       ├── models/                # Mongoose models
│   │       ├── controllers/           # Route controllers
│   │       ├── routes/v1/             # API routes (all under /v1)
│   │       ├── middlewares/           # Auth, validation, error handling
│   │       ├── services/              # Business logic
│   │       ├── validations/           # Joi validation schemas
│   │       ├── utils/                 # Utilities (ApiError, catchAsync, etc.)
│   │       └── docs/                  # Swagger YAML definitions
│   │
│   └── source_BE_socket/              # Socket.IO server
│       ├── package.json
│       └── src/
│           ├── index.js               # Entry point
│           ├── app.js                 # Express app
│           ├── socket/index.js         # Socket.IO event handlers
│           ├── config/                # Configuration
│           ├── models/                # Mongoose models (subset)
│           └── middlewares/           # Auth middleware
│
└── source_Front-end/                  # React frontend
    ├── package.json
    └── src/
        ├── index.js                   # React entry point
        ├── App.js                     # Root component
        ├── routes/                    # Route definitions & guards
        ├── store/                     # Redux store
        ├── reducers/                  # Redux reducers
        ├── axiosApi/                  # API modules
        ├── containers/                # Page-level components
        ├── components/                # Reusable UI components
        ├── components-Admin/          # Admin panel components
        ├── layout/                    # Layout wrappers
        ├── skeletons/                 # Loading skeletons
        └── css/                       # Stylesheets
```

---

## API Endpoints

All endpoints are prefixed with `/v1`. Swagger docs available at `/v1/docs` in development mode.

### Authentication (`/v1/auth`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/register` | Register new user |
| POST | `/login` | User login |
| POST | `/logout` | Logout (invalidate refresh token) |
| POST | `/refresh-tokens` | Refresh access token |
| POST | `/forgot-password` | Send password reset email |
| POST | `/reset-password` | Reset password with token |
| POST | `/send-verification-email` | Send email verification |
| POST | `/verify-email` | Verify email with token |
| POST | `/check-token` | Check token validity |
| POST | `/check-auth-v` | Check token + email verified |

### Admin Auth (`/v1/auth/admin`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/login` | Admin login |
| PUT | `/change-password` | Admin change password |

### Users (`/v1/users`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/` | Create user (admin only) |
| GET | `/` | Get all users (search, paginate) |
| GET | `/:userId` | Get user by ID |
| PATCH | `/:userId` | Update user |
| DELETE | `/:userId` | Delete user |

### Profile (`/v1/profile`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| PUT | `/changeAvatar` | Upload new avatar |
| PUT | `/change-profile` | Update profile info |
| GET | `/:id` | Get profile by ID |
| PUT | `/change-password` | Change password |
| GET | `/get-summary/:id` | Get profile summary |

### Posts (`/v1/post`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/create-post-file` | Create post with file |
| POST | `/create-post-text` | Create text-only post |
| PUT | `/like` | Like/unlike post |
| POST | `/like` | Check if post is liked |
| PUT | `/comment` | Comment on post |
| GET | `/` | Get all posts (paginated) |
| GET | `/get-my-post` | Get own posts |
| DELETE | `/` | Delete post |
| PUT | `/` | Edit post text |

### Comments (`/v1/comment`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| PUT | `/like` | Like/unlike comment |
| GET | `/` | Get comments |

### Conversations (`/v1/conversation`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Get user's conversations |
| POST | `/private` | Get/create private conversation |
| POST | `/create-group` | Create group conversation |
| PUT | `/add-member` | Add member to group |
| PUT | `/out-group` | Leave group |

### Messages (`/v1/message`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/` | Send text message |
| POST | `/like/:conversationId` | Send like reaction |
| POST | `/love/:conversationId` | Send love reaction |
| POST | `/media` | Send media message |
| GET | `/:conversationId` | Get messages from conversation |
| PUT | `/` | Recall (unsend) message |

### Notifications (`/v1/notification`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Get notifications |
| DELETE | `/` | Delete notification |

### Follow (`/v1/follow`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| PUT | `/` | Follow/unfollow user |
| GET | `/:id` | Find followers/following |

### Files & Images (`/v1/file`, `/v1/image`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/v1/file/:id` | Get file by ID |
| GET | `/v1/image/:id` | Get image by ID |
| DELETE | `/v1/image/:id` | Delete image |

### Admin (`/v1/admin`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/createAdmin` | Create new admin |
| PUT | `/blockUser/:userId` | Block/unblock user |
| DELETE | `/post` | Delete any post |

---

## Database Models

| Model | Description |
|-------|-------------|
| `User` | User accounts (fullname, email, password, role, avatar, story) |
| `Post` | Posts (owner, text, file attachment, likes) |
| `Comment` | Comments (user, text, post reference, likes) |
| `Conversation` | Conversations (private/group, members) |
| `Message` | Messages (conversation, sender, type, content) |
| `Notification` | Notifications (recipient, text, triggering user) |
| `Follow` | Follow relationships (followers, following) |
| `Group` | Groups (name, users, admin) |
| `Image` | Image metadata (name, type, GridFS file ID) |
| `Token` | Tokens (refresh, reset password, verify email) |
| `Admin` | Admin accounts (name, password, role) |

### File Storage

Files are stored in **GridFS** with separate MongoDB databases for each type:
- **Images:** 5MB limit (jpeg, jpg, png, gif)
- **Audio:** 20MB limit (mp3, mpeg, mp4, wav, wma, aac)
- **Video:** 500MB limit (mp4, mov, wmv, avi, flv, mkv, webm)
- **Generic Files:** 500MB limit (any type)

---

## Real-time Events (Socket.IO)

### Chat Events
| Event | Description |
|-------|-------------|
| `sendMessage` / `getMessage` | Text messages |
| `sendMedia` / `getMedia` | Media messages |
| `sendIcon` / `getIcon` | Reaction icons (like, love) |
| `sendRecall` / `getRecall` | Message recall (unsend) |
| `typing` / `untyping` | Typing indicators |
| `online` | Online status checking |
| `upload` | File upload progress |
| `send-file` / `unsend-file` | File send/unsend notifications |

### WebRTC Call Events
| Event | Description |
|-------|-------------|
| `callUser` / `getCallUser` | Initiate call |
| `answerCall` / `callAccepted` | Accept call |
| `rejectCall` / `callRejected` | Reject call |
| `offer` / `answer` / `ice-candidate` | WebRTC SDP/ICE signaling |
| `video-on/off`, `audio-on/off`, `screen-on/off` | Media state toggles |
| `callEnded` | Call termination |

---

## Security

- **JWT-based authentication** with access tokens (30 min) and refresh tokens (30 days)
- **Passport JWT strategy** for both REST API and Socket.IO
- **Role-based access control** — Three roles: user, admin, superadmin
- **Rate limiting** — 15 requests per 15 minutes on auth endpoints
- **Helmet** for security headers
- **bcrypt** password hashing (cost 8)
- **Blocked user check** at auth middleware level
- **Content filtering** — Server-side (bad-words) and client-side (nsfwjs + TensorFlow.js)

---

## Deployment

- **Frontend:** Surge.sh (`vn-smxh.surge.sh`) and Azure Container Instances
- **Backend:** Azure Container Instances
- **Process Manager:** PM2

---

## Contributing

This is a graduation thesis project. Contributions are not expected, but feel free to fork and learn from the code.

---

## License

This project is for educational purposes. No license is specified.
