# 🛠️ Formint — Multi-Tenant HR SaaS Platform

> Formint is a modern HR SaaS platform built with React.js, Tailwind CSS, shadcn/ui, Supabase, etc.
> It streamlines employee onboarding, recruitment, leave management, and team operations while providing real-time validations, dynamic forms, and secure data handling for modern HR workflows.

## 🚀 Live Demo

[👉 Click here to check out the live version](https://formint.vercel.app/auth/login)

---

## 🧭 Table of Contents

1. [Overview](#-overview)
2. [Key Highlights](#-key-highlights)
3. [Key Features](#-key-features)
4. [App Experience & UI](#-app-experience--ui)
5. [Architecture & Tech Stack](#-architecture--tech-stack)
6. [Authentication & Multi-Tenant Flow](#-authentication--multi-tenant-flow)
7. [Role-Based Access Control](#-role-based-access-control)
8. [Security & Data Isolation](#-security--data-isolation)
9. [📸 Screenshots](#-screenshots)
10. [Project Structure & Conventions](#-project-structure--conventions)
11. [Developer Setup](#-developer-setup)
12. [Testing](#-testing)
13. [Production Deployment](#-production-deployment)
14. [Author](#-author)
15. [Contact](#-contact)
16. [License](#-license)
17. [Developer Note](#-developer-note)
18. [Additional Notes](#-additional-notes)
19. [Closing Note](#-closing-note)
20. [Thank You](#-thank-you)

---

## 📝 Overview

**Formint** is a multi-tenant HR SaaS solution designed for modern companies to manage their HR operations, including employee onboarding, leave management and team collaboration, while ensuring **secure and isolated tenant environments**.

Each company gets its `own secure tenant environment`, enabling `Admins, Managers, Recruiters, and Employees` to manage their workforce efficiently.

The platform focuses on:

- Auth Flow
- Clear onboarding pipelines
- Leave Management
- Role-based access control
- Real-time analytics
- Scalable architecture

---

## 🌟 Key Highlights

✅ HR SaaS Application  
✅ Multi-tenant Architecture  
✅ Supabase Auth & RLS Policies  
✅ Role-based Access Control (RBAC)  
✅ Team Management & Invites  
✅ Leave Management  
✅ Onboarding Flow  
✅ Real-time Dashboard & Analytics  
✅ Scalable Component Architecture
✅ Responsive/Mobile-friendly UI

---

## 🧩 Key Features

- **Multi-Tenant Architecture** — Each company acts as a tenant and has its own workspace.
- **Full Authentication** — Password + passwordless login/signup, forgot/update password, and secure session management via Supabase Auth.
- **Role-Based Access Control (RBAC)** — Admin, Manager, Recruiter, and Employee roles with scoped permissions.
- **Admin Signup & Tenant Setup** — First user automatically becomes the admin and sets up the company.
- **Invite-Based Employee Signup** — Admins can invite members, and new members join with roles through secure invite links.
- **Team Management** — Invite, and view members (Active, Pending, Expired) with advanced table features like pagination, filtering, and sorting.
- **Leave Management** — A complete module to handle all employee leave operations:
  - **Apply Leave** — Employees can apply for leaves with validations.
  - **Leave Approvals** — Admins and Managers can review, approve, or reject leave requests through an intuitive table and drawer-based interface.
  - **Leave Types** — Admins can create, edit, enable/disable, and delete leave types for better organizational structuring.
  - **My Leaves (History)** — Employees can track their leave status (Pending, Approved, Rejected, Cancelled) with applied dates and remarks.
  - **Leave Entitlements** — Admins can define or assign leave balances per employee or role, view entitlements, and manage limits with inline warnings.
- **Onboarding Forms** — Fully validated forms for employee onboarding with file upload support.
- **Dashboard Analytics** — Stats for onboarding submissions, members, and pending invites with interactive charts.
- **Advanced Tables** — Sort, filter, paginate, update columns visibility, and view details seamlessly.
- **Tenant-Level Data Isolation** — RLS policies and Supabase Edge Functions ensure secure access.
- **Notifications & Emails** — Integrated email invites via SendGrid and in-app toast notifications.
- **Modern UI/UX** — Responsive, accessible, and clean design with Tailwind CSS, shadcn components, and, custom components.

---

## 🖼️ App Experience & UI

Instead of listing only pages, Formint focuses on **user-centric workflows** across HR functions:

- **Dashboard** – Real-time overview of Onboarding and leave stats, charts, and quick access to recent activity including **View All** & **View Details**.
- **Team Management** – Centralized member management and invite handling.
- **Onboarding Flow** – Smooth employee onboarding with structured workflows.
- **Leave Management** – Comprehensive leave lifecycle including:
  - Manage Leave Types
  - Apply Leave
  - Leave Approvals
  - Leave Entitlements
  - My Leaves (History)
- **Data Table & Drawers** – Unified interface for CRUD operations and record details with pagination, filtering, sorting, and detailed viewing of submissions.

---

## 🏗️ Architecture & Tech Stack

- **Frontend**: React + Vite, Tailwind CSS, shadcn UI, TanStack Table, Recharts, Lucide icons
- **Backend**: Supabase (Auth, Postgres DB, Storage, Edge Functions, RLS policies)
- **Email & Notifications**: SendGrid, Sonner toast
- **State Management**: Context API & Custom hooks
- **Forms**: React Hook Form
- **Routing**: React Router
- **Validation**: Yup
- **Hosting**: Vercel for frontend, Supabase for backend
- **Security**: Row Level Security (RLS) and Edge Functions for secure operations
- **Trello**: Tracking development tasks, feature roadmap, and internal tickets

---

## 🔐 Authentication & Multi-Tenant Flow

- First signup creates a **Tenant** and sets the user as **Admin**.
- Admin completes **Company Setup**.
- Admin invites members from **Team Page**.
- Invite is sent via email with a secure token.
- New members sign up via the invite link and are **auto-linked** to the tenant with assigned roles.
- RLS ensures that users only access their own tenant data.

### 1️⃣ Two-Step Company Sign-Up

1. **Create Account** – An admin first signs up with email & password or a magic link.
2. **Setup Company** – After verifying email, the admin completes company onboarding:

   - **Company Name** (unique slug auto-generated)
   - **Your Full Name** (optional; defaults to email prefix)

Once complete, a tenant row is created in the `tenants` table and the admin’s profile is inserted with the `admin` role in the `members` table.

---

### 2️⃣ Invite Team Members

- From the **Team** page (`/dashboard/team`), admins can send invites.
- Each invite generates a secure, time-limited email link.

---

### 3️⃣ Member Sign-Up

- Invited users click their email link, landing on **Member Signup Page**.
- They create their account and are automatically linked to the correct tenant in the `members` table.

---

### 4️⃣ Team Management

- The **Team** page lists all members in a data table (sortable & responsive).

---

**Step by step flow**:  
`Admin Signup` → `Verify` → `Company Setup` → `Invite Member` → `Accept Invite` → `Member Signup` → `Login & Use Formint`

---

## 🧑‍💼 Role-Based Access Control

| Role          | Capabilities                                              |
| ------------- | --------------------------------------------------------- |
| **Admin**     | Full control over tenant, invites, analytics, and data    |
| **Manager**   | Manage features like onboarding flows (under development) |
| **Employee**  | Limited access, can view assigned data and submit forms   |
| **Recruiter** | Dedicated to recruitment activities (future scope)        |

---

## 🛡️ Security & Data Isolation

- All tenant-specific data is isolated using Supabase **RLS Policies**.
- Users can only access records belonging to their tenant.
- Certain privileged actions like **invite creation** use **Supabase Edge Functions** with `service_role`.
- Files (images, PDFs) are stored securely in **Supabase Storage** with path references in the database.

---

## 📸 Screenshots

Screenshots or UI previews will be added soon.

---

## 🧭 Project Structure & Conventions

- Clear separation of components, hooks, contexts, services, and layouts
- Centralized logic for file uploads and validation
- Reusable UI components and form inputs
- Protected routes and layouts for authenticated sections
- Tenant ID attached to all tenant-scoped operations

---

## 🧰 Developer Setup

> ⚠️ Note: This repository is currently private. The instructions below are informational.

1. **Clone the repository**
2. **Install dependencies**
3. **Setup Supabase** project with RLS policies, Edge functions, and, Storage bucket.
4. **Configure environment variables** for both Vercel and Supabase in production.
5. **Run the project locally**
6. **Deploy Edge Functions** for secure invite handling

---

## 🧪 Testing

**Suggested flow for exploring the application**:

1. Admin signs up and creates tenant
2. Dashboard loads with empty stats
3. Submit a onboarding form to populate data
4. Send an invite to a new member and find it reflected in Team table
5. Accept invite as new member and login
6. Ensure RBAC differences between Admin and Employee
7. Test table filters, sorting, and details pages

---

## ☁️ Production Deployment

- **Frontend**: Deployed on Vercel
- **Backend**: Supabase project with configured RLS & Edge Functions
- **Email**: SendGrid API key
- **Monitoring**: Supabase Dashboard & Logs, Vercel deployments, Github, and SendGrid activity

---

## 🧑‍💻 Author

Developed by [Shahnawaz Khan](https://shahnawazkhan.vercel.app/)  
Senior Frontend Developer | React Developer

---

## 📫 Contact

Email: 1990.shahnawaz@gmail.com  
[Portfolio](https://shahnawazkhan.vercel.app/) • [Linkedin](https://www.linkedin.com/in/sk-shahnawazkhan) • [Github](https://github.com/sk-shahnawazkhan)

---

## 📄 License

This repository contains a project summary for Formint SaaS application. The content is shared solely for demonstration and portfolio purposes.

Its is **not intended for reuse, redistribution, or commercial use**. Because copying or using this documentation elsewhere may not be appropriate or meaningful.

---

## ✍️ Developer Note

This project is actively being designed, developed, and maintained solely by me.  
I’m continuously improving its architecture, UI, and features to make it more robust and scalable.  
Suggestions and feedback are always welcome!

---

## 📝 Additional Notes

This file is reviewed and maintained on a regular basis. However, as the project is still actively being developed, you may occasionally encounter text inconsistencies or slight variations in meaning.  
Also, some UI elements may not be fully optimized for all themes — particularly in default device dark mode — which may result in a less-than-ideal viewing experience.

## 🙌 Closing Note

More features and improvements on the way 🚀

---

## 🤝 Thank You

Thank you for reading and visiting this project summary.  
Feel free to reach out if you'd like to know more or discuss the project further.
