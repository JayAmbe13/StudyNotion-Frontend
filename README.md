# 📚 StudyNotion — EdTech Frontend

> A full-featured EdTech platform frontend built with **React.js**, enabling students to discover and enroll in courses, and instructors to create and manage their own content.

![React](https://img.shields.io/badge/React-18.2.0-61DAFB?style=for-the-badge&logo=react)
![Redux](https://img.shields.io/badge/Redux_Toolkit-1.9.5-764ABC?style=for-the-badge&logo=redux)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.2.7-38B2AC?style=for-the-badge&logo=tailwind-css)
![React Router](https://img.shields.io/badge/React_Router-6.9.0-CA4245?style=for-the-badge&logo=react-router)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Pages & Routes](#-pages--routes)
- [State Management (Redux)](#-state-management-redux)
- [API Integration](#-api-integration)
- [User Roles](#-user-roles)
- [Authentication Flow](#-authentication-flow)
- [Dashboard Features](#-dashboard-features)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Available Scripts](#-available-scripts)

---

## 🌟 Overview

**StudyNotion** is a modern EdTech web application similar to Udemy or Coursera. It has a dark-themed, responsive UI built with React and TailwindCSS. The platform supports three types of users — **Students**, **Instructors**, and **Admins** — each with their own dedicated dashboard and feature set.

The frontend communicates with a REST API backend (Node.js/Express) for all data operations including authentication, course management, payments, and profile management.

---

## ✨ Features

### 🎓 For Students
- Browse and explore courses by category
- View detailed course information (description, sections, reviews, instructor info)
- Add courses to cart and purchase via **Razorpay** payment gateway
- Access enrolled courses and watch video lectures
- Track lecture completion progress
- Rate and review courses
- Manage profile, change password, update display picture

### 🧑‍🏫 For Instructors
- Create and publish courses with rich details (thumbnail, description, price, tags)
- Build course content using sections and sub-sections
- Upload video lectures for each sub-section
- Edit or delete existing courses
- View instructor dashboard with earnings and student statistics (chart)
- Manage profile and account settings

### 🔒 For All Users
- Sign up with OTP email verification
- Secure login with JWT token-based authentication
- Forgot Password / Reset Password via email link
- Profile settings: update info, change password, delete account

---

## 🛠 Tech Stack

| Technology | Purpose |
|---|---|
| **React 18** | UI library |
| **React Router DOM v6** | Client-side routing |
| **Redux Toolkit** | Global state management |
| **Axios** | HTTP requests to backend API |
| **TailwindCSS** | Utility-first CSS styling |
| **React Hook Form** | Form state and validation |
| **React Hot Toast** | Toast notifications |
| **React Icons** | Icon library |
| **Swiper.js** | Course/review carousels/sliders |
| **Chart.js + react-chartjs-2** | Instructor earnings chart |
| **video-react** | Video player for course lectures |
| **react-type-animation** | Typing animation on homepage |
| **react-otp-input** | OTP input component for email verification |
| **react-dropzone** | Drag-and-drop file upload (thumbnails/videos) |
| **react-markdown + showdown** | Render markdown course descriptions |
| **react-rating-stars-component** | Star rating display |
| **@ramonak/react-progress-bar** | Progress bar for course completion |

---

## 📁 Project Structure

```
studynotion-edtech-project-main/
│
├── public/                        # Static assets (favicon, index.html, logos)
│
├── src/
│   ├── App.jsx                    # Root component — defines all routes
│   ├── App.css                    # Global styles
│   ├── index.js                   # React app entry point
│   │
│   ├── assets/                    # Images, logos, SVGs, video
│   │   ├── Images/                # Page images (banner, about, login, signup etc.)
│   │   ├── Logo/                  # StudyNotion logos (light/dark variants)
│   │   └── TimeLineLogo/          # SVG icons used in the About timeline
│   │
│   ├── components/
│   │   ├── Common/                # Shared/reusable components
│   │   │   ├── Navbar.jsx         # Top navigation bar
│   │   │   ├── Footer.jsx         # Site-wide footer
│   │   │   ├── ConfirmationModal.jsx  # Reusable confirm/cancel modal
│   │   │   ├── IconBtn.jsx        # Button with icon support
│   │   │   ├── RatingStars.jsx    # Star rating display component
│   │   │   ├── ReviewSlider.jsx   # Swiper carousel for reviews
│   │   │   └── Tab.jsx            # Tab switcher (Student/Instructor)
│   │   │
│   │   └── core/                  # Feature-specific components
│   │       ├── Auth/              # Login, Signup, OTP, Route Guards
│   │       ├── AboutPage/         # About page sections
│   │       ├── Catalog/           # Course card and slider for catalog
│   │       ├── ContactUsPage/     # Contact form and details
│   │       ├── Course/            # Course accordion, details card
│   │       ├── HomePage/          # Hero section, features, timeline
│   │       ├── Dashboard/         # All dashboard panels (student + instructor)
│   │       └── ViewCourse/        # Video player and course sidebar
│   │
│   ├── pages/                     # Top-level page components (mapped to routes)
│   │   ├── Home.jsx
│   │   ├── About.jsx
│   │   ├── Contact.jsx
│   │   ├── Catalog.jsx
│   │   ├── CourseDetails.jsx
│   │   ├── Login.jsx
│   │   ├── Signup.jsx
│   │   ├── VerifyEmail.jsx
│   │   ├── ForgotPassword.jsx
│   │   ├── UpdatePassword.jsx
│   │   ├── Dashboard.jsx
│   │   ├── ViewCourse.jsx
│   │   └── Error.jsx              # 404 page
│   │
│   ├── data/                      # Static data files
│   │   ├── navbar-links.js        # Navbar navigation link definitions
│   │   ├── dashboard-links.js     # Sidebar link definitions per role
│   │   ├── footer-links.js        # Footer column link data
│   │   ├── homepage-explore.js    # Explore section course data
│   │   └── countrycode.json       # Country dialing codes for contact form
│   │
│   ├── hooks/                     # Custom React hooks
│   │   ├── useOnClickOutside.js   # Detect clicks outside an element
│   │   └── useRouteMatch.js       # Active route detection helper
│   │
│   ├── reducer/
│   │   └── index.js               # Combines all Redux slices into root reducer
│   │
│   ├── slices/                    # Redux Toolkit state slices
│   │   ├── authSlice.js           # Auth state (token, loading, signupData)
│   │   ├── profileSlice.js        # User profile state
│   │   ├── cartSlice.js           # Cart items and total count
│   │   ├── courseSlice.js         # Course creation/editing state
│   │   └── viewCourseSlice.js     # Active course viewing state
│   │
│   ├── services/
│   │   ├── apiConnector.js        # Axios instance wrapper
│   │   ├── apis.js                # All API endpoint URLs
│   │   ├── formatDate.js          # Date formatting utility
│   │   └── operations/            # API call functions (thunks)
│   │       ├── authAPI.js         # Login, signup, OTP, password reset
│   │       ├── profileAPI.js      # Get user details, enrolled courses
│   │       ├── courseDetailsAPI.js# Course CRUD, sections, subsections
│   │       ├── studentFeaturesAPI.js  # Payment, lecture completion
│   │       ├── pageAndComponntDatas.js # Catalog page data
│   │       └── SettingsAPI.js     # Profile picture, update profile, delete
│   │
│   └── utils/
│       ├── constants.js           # ACCOUNT_TYPE and COURSE_STATUS enums
│       ├── avgRating.js           # Average rating calculation helper
│       └── dateFormatter.js       # Human-readable date formatting
│
├── tailwind.config.js             # TailwindCSS config (custom colors, fonts)
├── package.json                   # Dependencies and scripts
└── .env                           # Environment variables (not committed)
```

---

## 🗺 Pages & Routes

| Route | Component | Access |
|---|---|---|
| `/` | `Home` | Public |
| `/about` | `About` | Public |
| `/contact` | `Contact` | Public |
| `/login` | `Login` | Guest only |
| `/signup` | `Signup` | Guest only |
| `/verify-email` | `VerifyEmail` | Guest only |
| `/forgot-password` | `ForgotPassword` | Guest only |
| `/update-password/:id` | `UpdatePassword` | Guest only |
| `/catalog/:catalogName` | `Catalog` | Public |
| `/courses/:courseId` | `CourseDetails` | Public |
| `/dashboard/my-profile` | `MyProfile` | Logged in |
| `/dashboard/Settings` | `Settings` | Logged in |
| `/dashboard/cart` | `Cart` | Student only |
| `/dashboard/enrolled-courses` | `EnrolledCourses` | Student only |
| `/dashboard/instructor` | `Instructor` | Instructor only |
| `/dashboard/my-courses` | `MyCourses` | Instructor only |
| `/dashboard/add-course` | `AddCourse` | Instructor only |
| `/dashboard/edit-course/:courseId` | `EditCourse` | Instructor only |
| `/view-course/:courseId/section/:sectionId/sub-section/:subSectionId` | `VideoDetails` | Student only |
| `*` | `Error` (404) | Public |

> **OpenRoute** — redirects logged-in users away from auth pages (login, signup).  
> **PrivateRoute** — redirects unauthenticated users to the login page.

---

## 🗃 State Management (Redux)

The app uses **Redux Toolkit** with 5 slices combined in `src/reducer/index.js`:

### `authSlice`
| State | Description |
|---|---|
| `token` | JWT auth token (persisted in `localStorage`) |
| `loading` | Auth operation loading state |
| `signupData` | Temporary signup data stored during OTP verification |

### `profileSlice`
| State | Description |
|---|---|
| `user` | Full user object (name, email, accountType, image, etc.) |
| `loading` | Profile fetch loading state |

### `cartSlice`
| State | Description |
|---|---|
| `cart` | Array of course objects in cart (persisted in `localStorage`) |
| `totalItems` | Number of items in cart |
| `total` | Total price of cart items |

### `courseSlice`
| State | Description |
|---|---|
| `course` | Course being created/edited |
| `editCourse` | Boolean — whether we're editing an existing course |
| `step` | Current step in the multi-step course creation form (1, 2, or 3) |
| `paymentLoading` | Payment processing state |

### `viewCourseSlice`
| State | Description |
|---|---|
| `courseSectionData` | Sections + sub-sections for the currently viewed course |
| `courseEntireData` | Full course details |
| `completedLectures` | Array of completed sub-section IDs |
| `totalNoOfLectures` | Total number of lectures in the course |

---

## 🔌 API Integration

All API calls go through `src/services/apiConnector.js`, which is a thin wrapper around **Axios**. The base URL is set via the `REACT_APP_BASE_URL` environment variable.

### Endpoint Groups (`src/services/apis.js`)

| Group | Endpoints |
|---|---|
| **Auth** | Send OTP, Sign Up, Log In, Reset Password Token, Reset Password |
| **Profile** | Get User Details, Get Enrolled Courses, Instructor Dashboard Data |
| **Courses** | Get All Courses, Course Details, Create/Edit/Delete Course, Sections & Sub-sections |
| **Students** | Capture Payment, Verify Payment, Send Payment Success Email |
| **Categories** | Show All Categories |
| **Catalog** | Get Category Page Details |
| **Ratings** | Get All Reviews |
| **Contact** | Submit Contact Form |
| **Settings** | Update Picture, Update Profile, Change Password, Delete Account |

### API Operations (`src/services/operations/`)

Each file exports async thunk functions that:
1. Show a loading spinner/toast
2. Make the API call via `apiConnector`
3. Handle success (dispatch state update, navigate, show success toast)
4. Handle errors (show error toast, log to console)

---

## 👤 User Roles

The app has **3 account types** defined in `src/utils/constants.js`:

```js
ACCOUNT_TYPE = {
  STUDENT: "Student",
  INSTRUCTOR: "Instructor",
  ADMIN: "Admin",
}
```

Role-based access is enforced both in **routing** (App.jsx) and **UI rendering** (Navbar, Dashboard Sidebar).

---

## 🔐 Authentication Flow

```
1. User visits /signup
   └─ Enters name, email, password, role (Student/Instructor)
   └─ Clicks "Create Account"
   └─ OTP sent to email → stored in signupData Redux state

2. User visits /verify-email
   └─ Enters 6-digit OTP
   └─ On success → account created → redirected to /login

3. User visits /login
   └─ Enters email + password
   └─ Receives JWT token → stored in localStorage + Redux
   └─ User profile fetched and stored in Redux
   └─ Redirected to /dashboard/my-profile

4. Token persisted across page refresh
   └─ App.jsx reads token from localStorage on mount
   └─ Calls getUserDetails() to restore session

5. Forgot Password flow:
   └─ /forgot-password → enter email → receive reset link
   └─ /update-password/:id → enter new password → updated
```

---

## 🖥 Dashboard Features

The Dashboard uses a **Sidebar layout** (`Dashboard.jsx` + `Sidebar.jsx`) with role-based navigation links.

### Student Dashboard
| Panel | Description |
|---|---|
| **My Profile** | View profile info, enrolled course count, account details |
| **Enrolled Courses** | List of purchased courses with progress bars |
| **Cart** | Review courses in cart, view total price, proceed to payment |
| **Settings** | Update profile picture, personal info, password, or delete account |

### Instructor Dashboard
| Panel | Description |
|---|---|
| **Dashboard** | Overview: total courses, students, earnings + pie/bar chart |
| **My Courses** | Table of all created courses with edit/delete actions |
| **Add Course** | 3-step form: Course Info → Course Builder → Publish |
| **Edit Course** | Pre-filled form to update existing course content |
| **Settings** | Same as student settings |

### Course Creation (3 Steps)
```
Step 1 — Course Information
  ├─ Title, description, price, category, tags
  ├─ Thumbnail image upload (drag & drop)
  ├─ What you'll learn (benefits), requirements
  └─ Course language, level

Step 2 — Course Builder
  ├─ Add/edit/delete Sections
  └─ Add/edit/delete Sub-sections (each has title, description, video upload)

Step 3 — Publish
  └─ Toggle course status (Draft / Published) and submit
```

---

## 🚀 Getting Started

### Prerequisites
- **Node.js** v16+ (v24 recommended)
- **npm** v8+
- A running **StudyNotion backend** server

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/JayAmbe13/StudyNotion-Frontend.git
cd StudyNotion-Frontend

# 2. Install dependencies
npm install

# 3. Create the environment file
cp .env.example .env
# Edit .env and set your backend URL (see Environment Variables below)

# 4. Start the development server
npm start
```

The app will open at **http://localhost:3000**

---

## 🔧 Environment Variables

Create a `.env` file in the root of the project:

```env
REACT_APP_BASE_URL=http://localhost:4000/api/v1
```

| Variable | Description |
|---|---|
| `REACT_APP_BASE_URL` | Base URL of your StudyNotion backend REST API |

> ⚠️ Never commit your `.env` file — it's already listed in `.gitignore`.

---

## 📜 Available Scripts

| Command | Description |
|---|---|
| `npm start` | Starts the React development server at `localhost:3000` |
| `npm run build` | Builds the optimized production bundle in `/build` |
| `npm test` | Runs the test suite with React Testing Library |
| `npm run eject` | Ejects from Create React App (irreversible) |

---

## 🎨 Design System

The app uses a custom **TailwindCSS** configuration with:

- **Font**: `Inter` (via Google Fonts)
- **Color palette**: `richblack` (dark grays), `richblue`, `yellow`, `pink`, `caribbeangreen` — all defined in `tailwind.config.js`
- **Max content width**: `1360px` (`max-w-maxContent`)
- **Dark theme** throughout the entire application

---

## 📦 Key Dependencies

```json
{
  "react": "^18.2.0",
  "react-router-dom": "^6.9.0",
  "@reduxjs/toolkit": "^1.9.5",
  "react-redux": "^8.0.5",
  "axios": "^1.3.5",
  "react-hook-form": "^7.43.9",
  "react-hot-toast": "^2.4.0",
  "swiper": "^9.3.1",
  "chart.js": "^4.3.0",
  "video-react": "^0.16.0",
  "tailwindcss": "^3.2.7"
}
```

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add some amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

---

## 📄 License

This project is for educational purposes. Feel free to use it as a reference or learning resource.

---

<div align="center">
  <p>Built with ❤️ by <a href="https://github.com/JayAmbe13">JayAmbe13</a></p>
</div>
