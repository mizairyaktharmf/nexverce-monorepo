# Nexverce Platform

![Status](https://img.shields.io/badge/Status-Private-red.svg)
![Version](https://img.shields.io/badge/Version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/License-Proprietary-orange.svg)

**Your Solution Platform - Discover, Compare & Buy Smarter**

> ⚠️ **PRIVATE REPOSITORY** - This is a proprietary monorepo containing all Nexverce platform code. All repositories are private and confidential.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Repositories](#repositories)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Development Workflow](#development-workflow)
- [Deployment](#deployment)
- [Environment Setup](#environment-setup)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

Nexverce is a full-stack affiliate marketing and content management platform that helps users discover solutions through expert reviews, AI-generated comparisons, and deal tracking. The platform consists of three main applications:

1. **Backend API** - RESTful API server with MongoDB database
2. **Admin Panel** - Content management dashboard for staff and admins
3. **Client Website** - Public-facing platform for end users

### Key Features

- 🔐 **Secure Authentication** - JWT-based auth with single device login
- 📝 **Block-Based Content Editor** - Advanced WYSIWYG editor with 15+ block types
- 📊 **Analytics & Tracking** - Real-time analytics with country/device tracking
- 🔔 **Real-Time Notifications** - Socket.IO powered notification system
- 📋 **Task Management** - Complete task system with assignments and permissions
- 📱 **Telegram Integration** - Post to Telegram channel with multiple images (album support)
- 🔗 **LinkedIn Integration** - Auto-post content to LinkedIn with AI-generated captions
- 📧 **Newsletter Management** - Email subscription and bulk operations
- 💼 **Career Portal** - Job postings with application tracking
- 🎯 **Referral System** - Affiliate link request and approval workflow
- 🤖 **AI-Powered Features** - OpenAI integration for SEO, captions, and content generation

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      Nexverce Platform                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐   │
│  │   Client    │    │    Admin    │    │   Backend   │   │
│  │  (Public)   │◄───┤   (Staff)   │◄───┤     API     │   │
│  │   React     │    │    React    │    │  Express.js │   │
│  │   Vite      │    │    Vite     │    │   MongoDB   │   │
│  └─────────────┘    └─────────────┘    └─────────────┘   │
│       ▲                    ▲                    ▲          │
│       │                    │                    │          │
│       └────────────────────┴────────────────────┘          │
│                   Socket.IO (Real-time)                    │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│                   External Services                         │
├─────────────────────────────────────────────────────────────┤
│  MongoDB Atlas │ Cloudinary │ OpenAI │ Telegram Bot API │  │
│  LinkedIn API │ Socket.IO Server │ Cron Jobs Scheduler      │
└─────────────────────────────────────────────────────────────┘
```

---

## 📦 Repositories

### 🔧 [Backend API](./nexverce-backend/)

**Private Repository** - RESTful API server powering the entire platform.

- **Tech Stack**: Node.js, Express.js, MongoDB (Mongoose)
- **Features**: JWT Auth, REST API, Socket.IO, Cloudinary, OpenAI, LinkedIn API
- **Deployment**: Render.com
- **Port**: 5000 (Development)

**Quick Links:**
- 📖 [Backend README](./nexverce-backend/README.md)
- 🚀 Production: `https://nexverce-backend.onrender.com`
- 📚 [API Documentation](./nexverce-backend/README.md#api-documentation)

**Key Endpoints:**
```
/api/auth          - Authentication
/api/blogs         - Blog posts
/api/products      - Product posts
/api/tasks         - Task management
/api/analytics     - Analytics tracking
/api/linkedin      - LinkedIn integration
/api/users         - User management
```

---

### 🎨 [Admin Panel](./nexverce-admin/)

**Private Repository** - Content management dashboard for staff and administrators.

- **Tech Stack**: React 18, Vite, Tailwind CSS, shadcn/ui
- **Features**: Block Editor, Analytics Dashboard, Task System, Real-time Notifications
- **Deployment**: Render
- **Port**: 5174 (Development)

**Quick Links:**
- 📖 [Admin README](./nexverce-admin/README.md)
- 🚀 Production: `https://admin.nexverce.com`
- 📖 [Block Editor Training Guide](./BLOCK_EDITOR_TRAINING_GUIDE.html)

**Admin Features:**
- 📝 **Block-Based Content Editor** with Collapse All/Expand All
- 📊 **Analytics Dashboard** with filters and date ranges
- 👥 **User Management** (create, edit, suspend, delete)
- 📋 **Task Management** with real-time notifications
- 🔗 **LinkedIn Auto-Posting** with analytics
- 💼 **Career Posts Management**
- 📧 **Newsletter Management**
- 🎯 **Referral Request Approvals**

---

### 🌐 [Client Website](./nexverce-client/)

**Private Repository** - Public-facing platform for end users.

- **Tech Stack**: React 18, Vite, Tailwind CSS, shadcn/ui, Framer Motion
- **Features**: Solutions Page, Blog System, Product Finder, Career Portal
- **Deployment**: Vercel
- **Port**: 5173 (Development)

**Quick Links:**
- 📖 [Client README](./nexverce-client/README.md)
- 🚀 Production: `https://www.nexverce.com`
- 🔗 Social: [Instagram](https://instagram.com/nexverce) | [LinkedIn](https://linkedin.com/company/nexverce)

**Client Features:**
- 🏠 **Hero Section** with animated blobs
- 🎯 **Solutions Page** for problem-solving
- 📱 **Product Finder** interactive quiz
- 📝 **Blog System** with categories
- 💼 **Career Posts** job listings
- 📧 **Newsletter Subscription**
- 📄 **Legal Pages** (Privacy, Terms)

---

## 🛠️ Tech Stack

### Frontend (Admin + Client)
- **Framework**: React 18
- **Build Tool**: Vite 5
- **Styling**: Tailwind CSS 3
- **UI Library**: shadcn/ui (Radix UI)
- **Icons**: Lucide React, React Icons
- **Routing**: React Router DOM v6
- **State**: React Context API
- **Animations**: Framer Motion
- **Forms**: React Hook Form
- **HTTP**: Axios
- **Real-time**: Socket.io Client

### Backend
- **Runtime**: Node.js v18+
- **Framework**: Express.js v4
- **Database**: MongoDB v6 (Mongoose ODM)
- **Authentication**: JWT (jsonwebtoken)
- **Password**: bcrypt
- **File Upload**: Cloudinary
- **Real-time**: Socket.IO
- **Email**: Nodemailer
- **AI**: OpenAI API
- **Social**: LinkedIn API

### DevOps & Deployment
- **Backend Hosting**: Render.com
- **Admin Hosting**: Render
- **Client Hosting**: Vercel
- **Database**: MongoDB Atlas
- **CDN**: Cloudinary
- **Version Control**: Git
- **CI/CD**: GitHub Actions (optional)

---

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have:

- **Node.js** v18 or higher ([Download](https://nodejs.org/))
- **npm** v9 or higher
- **MongoDB** v6.0+ (Local or [MongoDB Atlas](https://www.mongodb.com/cloud/atlas))
- **Git** installed
- **Cloudinary Account** ([Sign up](https://cloudinary.com/))
- **OpenAI API Key** ([Get Key](https://platform.openai.com/))
- **LinkedIn App** (for LinkedIn integration)

### Quick Start

#### 1. Clone the Repository

```bash
git clone <repository-url>
cd nexverce
```

#### 2. Install All Dependencies

**Option A: Install All at Once**
```bash
# Backend
cd nexverce-backend
npm install

# Admin
cd ../nexverce-admin
npm install

# Client
cd ../nexverce-client
npm install
```

**Option B: Use npm workspaces** (if configured)
```bash
npm install
```

#### 3. Set Up Environment Variables

Create `.env` files in each directory:

**Backend** (`nexverce-backend/.env`):
```env
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb://localhost:27017/nexverce
JWT_SECRET=your-super-secret-jwt-key
CLOUDINARY_CLOUD_NAME=your-cloud-name
CLOUDINARY_API_KEY=your-api-key
CLOUDINARY_API_SECRET=your-api-secret
OPENAI_API_KEY=sk-your-openai-api-key
LINKEDIN_CLIENT_ID=your-linkedin-client-id
LINKEDIN_CLIENT_SECRET=your-linkedin-client-secret
LINKEDIN_ACCESS_TOKEN=your-access-token
LINKEDIN_ORGANIZATION_ID=your-organization-id
CLIENT_URL=http://localhost:5173
ADMIN_URL=http://localhost:5174
CORS_ORIGINS=http://localhost:5173,http://localhost:5174
```

**Admin** (`nexverce-admin/.env`):
```env
VITE_API_URL=http://localhost:5000/api
VITE_SOCKET_URL=http://localhost:5000
```

**Client** (`nexverce-client/.env`):
```env
VITE_API_URL=http://localhost:5000/api
VITE_GA_MEASUREMENT_ID=G-VLX41C874Q
```

#### 4. Run All Applications

Open **3 terminals**:

**Terminal 1 - Backend:**
```bash
cd nexverce-backend
npm run dev
# Running on http://localhost:5000
```

**Terminal 2 - Admin:**
```bash
cd nexverce-admin
npm run dev
# Running on http://localhost:5174
```

**Terminal 3 - Client:**
```bash
cd nexverce-client
npm run dev
# Running on http://localhost:5173
```

#### 5. Access Applications

- **Backend API**: http://localhost:5000
- **Admin Panel**: http://localhost:5174
- **Client Website**: http://localhost:5173

### Default Admin Credentials

```
Email: admin@nexverce.com
Password: admin123
```

**⚠️ IMPORTANT**: Change these credentials immediately after first login!

---

## 📁 Project Structure

```
nexverce/
├── nexverce-backend/          # Backend API (Private)
│   ├── Config/                # Database configuration
│   ├── Controllers/           # Route controllers
│   ├── Models/                # Mongoose schemas
│   ├── Routes/                # API routes
│   ├── Middleware/            # Auth, error handling
│   ├── Utils/                 # Helper functions
│   ├── server.js              # Entry point
│   ├── package.json
│   └── README.md
│
├── nexverce-admin/            # Admin Panel (Private)
│   ├── src/
│   │   ├── Components/
│   │   │   ├── BlocksEditor/ # Content editor
│   │   │   ├── Dashboard/
│   │   │   ├── Blogs/
│   │   │   ├── Tasks/
│   │   │   ├── Users/
│   │   │   └── ...
│   │   ├── Context/
│   │   ├── Utils/
│   │   └── App.jsx
│   ├── package.json
│   └── README.md
│
├── nexverce-client/           # Client Website (Private)
│   ├── src/
│   │   ├── Components/
│   │   │   ├── HeroSection/
│   │   │   ├── Solutions/
│   │   │   ├── Blog/
│   │   │   ├── Career/
│   │   │   └── ...
│   │   └── App.jsx
│   ├── package.json
│   └── README.md
│
├── .gitignore                 # Git ignore rules
├── README.md                  # This file
└── BLOCK_EDITOR_TRAINING_GUIDE.html  # Staff training guide
```

---

## 🔄 Development Workflow

### Branch Strategy

```bash
main           # Production-ready code
├── develop    # Integration branch
├── feature/*  # New features
├── fix/*      # Bug fixes
└── hotfix/*   # Emergency fixes
```

### Commit Convention

```bash
feat:     # New feature
fix:      # Bug fix
docs:     # Documentation update
style:    # Code formatting
refactor: # Code refactoring
test:     # Add tests
chore:    # Maintenance tasks
```

**Examples:**
```bash
git commit -m "feat: add collapse all blocks feature to editor"
git commit -m "fix: resolve LinkedIn API authorization issue"
git commit -m "docs: update README with deployment instructions"
```

### Development Process

1. **Create Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make Changes** - Follow coding standards

3. **Test Locally** - Ensure all features work

4. **Commit Changes**
   ```bash
   git add .
   git commit -m "feat: your feature description"
   ```

5. **Push Branch**
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Create Pull Request** - Request code review

7. **Merge to Develop** - After approval

8. **Deploy to Production** - From `main` branch

---

## 🌐 Deployment

### Backend (Render.com)

**Build Command:**
```bash
npm install
```

**Start Command:**
```bash
npm start
```

**Environment Variables:**
- All `.env` variables set in Render dashboard
- `NODE_ENV=production`

**Production URL:** `https://nexverce-backend.onrender.com`

---

### Admin Panel (Render)

**Build Command:**
```bash
npm install && npm run build
```

**Start Command:**
```bash
npm run preview
```

**Environment Variables:**
- `VITE_API_URL=https://nexverce-backend.onrender.com/api`
- `VITE_SOCKET_URL=https://nexverce-backend.onrender.com`

**Production URL:** `https://admin.nexverce.com`

---

### Client Website (Vercel)

**Build Command:**
```bash
npm run build
```

**Output Directory:**
```
dist
```

**Environment Variables:**
- `VITE_API_URL=https://nexverce-backend.onrender.com/api`
- `VITE_GA_MEASUREMENT_ID=G-VLX41C874Q`

**Production URL:** `https://www.nexverce.com`

**Deployment:**
- Automatic on push to `main`
- Vercel auto-detects Vite configuration
- Custom domain configured: `www.nexverce.com`

---

## 🔐 Environment Setup

### Generate Secure Secrets

**JWT Secret:**
```bash
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
```

**Session Secret:**
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

### MongoDB Atlas Setup

1. Create cluster at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Whitelist deployment platform IPs
3. Create database user
4. Get connection string
5. Update `MONGO_URI` in environment variables

### Cloudinary Setup

1. Sign up at [Cloudinary](https://cloudinary.com/)
2. Get Cloud Name, API Key, API Secret
3. Update environment variables

### LinkedIn API Setup

1. Create LinkedIn App at [LinkedIn Developers](https://www.linkedin.com/developers/)
2. Get Client ID and Client Secret
3. Set up OAuth redirect URL
4. Generate Access Token
5. Get Organization ID

### OpenAI API Setup

1. Sign up at [OpenAI Platform](https://platform.openai.com/)
2. Create API Key
3. Add credits to account
4. Update `OPENAI_API_KEY` in environment

---

## 🔒 Security

### Implemented Security Measures

- ✅ **JWT Authentication** - Secure token-based auth (7-day expiry)
- ✅ **Password Hashing** - bcrypt with 10 salt rounds
- ✅ **CORS Protection** - Configured allowed origins
- ✅ **Rate Limiting** - Prevent brute force attacks
- ✅ **Input Validation** - Sanitize all user inputs
- ✅ **MongoDB Injection Prevention** - Mongoose validation
- ✅ **Helmet.js** - HTTP security headers
- ✅ **HTTPS Only** - SSL/TLS encryption in production
- ✅ **Environment Variables** - Sensitive data protection
- ✅ **Role-Based Access Control** - Admin/Staff permissions
- ✅ **Session Management** - Single device login enforcement
- ✅ **XSS Protection** - Content sanitization
- ✅ **CSRF Protection** - Token validation

### Security Best Practices

1. **Never commit `.env` files** to version control
2. **Use strong, unique secrets** for production
3. **Rotate API keys** regularly
4. **Monitor logs** for suspicious activity
5. **Keep dependencies updated** (npm audit)
6. **Use HTTPS** for all production URLs
7. **Implement rate limiting** on all endpoints
8. **Validate all inputs** on client and server

---

## 👥 Contributing

**This is a private repository.** Only authorized team members can contribute.

### Team Access

- **Admins**: Full access to all repositories
- **Developers**: Read/Write access to assigned repositories
- **Reviewers**: Read access + PR review permissions

### Code Review Process

1. All PRs require at least 1 approval
2. Tests must pass before merging
3. No direct commits to `main` or `develop`
4. Follow coding standards and conventions

---

## 📄 License

**Proprietary and Confidential**

This codebase is the exclusive property of **Nexverce**. Unauthorized copying, distribution, or use is strictly prohibited.

**© 2026 Nexverce. All rights reserved.**

Powered by **NexCode Nova**

---

## 📞 Support & Contact

### Production URLs
- **Client Website**: https://www.nexverce.com
- **Admin Panel**: https://admin.nexverce.com
- **Backend API**: https://nexverce-backend.onrender.com

### Contact
- **Email**: contact@nexverce.com
- **Support Email**: admin@nexverce.com
- **Telegram**: https://t.me/nexverce

### Social Media
- **Instagram**: https://www.instagram.com/nexverce
- **LinkedIn**: https://www.linkedin.com/company/nexverce
- **Facebook**: https://www.facebook.com/nexverce

### Documentation
- **Backend API Docs**: [nexverce-backend/README.md](./nexverce-backend/README.md)
- **Admin Panel Docs**: [nexverce-admin/README.md](./nexverce-admin/README.md)
- **Client Website Docs**: [nexverce-client/README.md](./nexverce-client/README.md)
- **Block Editor Training**: [BLOCK_EDITOR_TRAINING_GUIDE.html](./BLOCK_EDITOR_TRAINING_GUIDE.html)

---

## 🔄 Changelog

### Version 1.0.0 (January 2026)

**Backend Features:**
- ✅ Complete RESTful API with 30+ endpoints
- ✅ JWT authentication with single device login
- ✅ MongoDB database with 15+ models
- ✅ Socket.IO real-time notifications
- ✅ LinkedIn auto-posting integration
- ✅ OpenAI-powered SEO and content generation
- ✅ Cloudinary image upload and management
- ✅ Email notifications with Nodemailer
- ✅ Task management system
- ✅ Analytics tracking (views, clicks, devices, countries)

**Admin Panel Features:**
- ✅ Block-based content editor with 15+ block types
- ✅ **Collapse All / Expand All blocks** feature
- ✅ Real-time dashboard with analytics
- ✅ User management (CRUD, suspend, delete)
- ✅ Task management with notifications
- ✅ LinkedIn post scheduling and analytics
- ✅ Referral request approval system
- ✅ Career posts management
- ✅ Newsletter subscriber management
- ✅ Advanced analytics with filters

**Client Website Features:**
- ✅ Responsive landing page with hero section
- ✅ Solutions page for problem-solving
- ✅ Interactive product finder quiz
- ✅ Blog system with categories and search
- ✅ Career portal with job listings
- ✅ Newsletter subscription
- ✅ SEO optimization (meta tags, Schema.org)
- ✅ SSL badge and security features
- ✅ Mobile-first responsive design

---

## 📊 Statistics

- **Total Lines of Code**: ~50,000+
- **Components**: 100+ React components
- **API Endpoints**: 30+ RESTful endpoints
- **Database Models**: 15+ Mongoose schemas
- **Block Types**: 15+ content block types
- **Team Members**: 5+ developers
- **Deployment Platforms**: 3 (Render, Vercel, MongoDB Atlas)

---

## 🎯 Roadmap

### Q1 2026
- [ ] Mobile app (React Native)
- [ ] Advanced analytics dashboard
- [ ] AI-powered content recommendations
- [ ] Multi-language support

### Q2 2026
- [ ] Payment gateway integration
- [ ] Subscription management
- [ ] Advanced SEO tools
- [ ] API rate limiting dashboard

---

## ⚠️ Important Notes

1. **All repositories are PRIVATE** and non-visible to the public
2. This is a **monorepo structure** with 3 separate applications
3. Each repository has its own **README.md** with detailed documentation
4. **Never commit sensitive data** (API keys, passwords, tokens)
5. **Always use environment variables** for configuration
6. **Test locally** before deploying to production
7. **Follow the commit convention** for all changes
8. **Request code review** before merging to develop/main

---

**Built with ❤️ by the Nexverce Team | Powered by NexCode Nova**

---

## 🚨 Repository Privacy Notice

**PRIVATE REPOSITORIES:**
- `nexverce-backend` - ⚠️ Private
- `nexverce-admin` - ⚠️ Private
- `nexverce-client` - ⚠️ Private

**These repositories are NOT visible on GitHub publicly.** Access is restricted to authorized team members only.

For access requests, contact: **mizairyakthar@nexverce.com**
