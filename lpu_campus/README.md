# 🎓 LPU Smart Campus Management System

**Course:** Python and Full Stack | **Project II**
**Framework:** Django | **Database:** SQLite

---

## 📌 Project Overview

A **Smart Campus Management System** for Lovely Professional University focused on the **Make-Up Class & Remedial Code Module**.

### Features

**Faculty Portal:**
- Schedule make-up / remedial classes
- Generate unique 6-character remedial codes per session (with expiry timer)
- View real-time attendance as students mark in
- Manage class status (Upcoming → Active → Completed)
- Edit / delete classes

**Student Portal:**
- Mark attendance by entering the remedial code
- View full separate attendance records for all make-up classes
- Visual 6-box code entry UI

---

## 🛠️ How to Run

### 1. Clone / Download the project
```bash
cd lpu_campus
```

### 2. Install Django
```bash
pip install -r requirements.txt
```

### 3. Run migrations (creates the SQLite database)
```bash
python manage.py makemigrations
python manage.py migrate
```

### 4. Create a superuser (for Django admin panel)
```bash
python manage.py createsuperuser
```

### 5. Start the server
```bash
python manage.py runserver
```

### 6. Open in browser
```
http://127.0.0.1:8000/
```

---

## 📂 Project Structure

```
lpu_campus/
│
├── lpu_campus/          ← Django project config
│   ├── settings.py      ← Settings (SQLite, apps, timezone)
│   ├── urls.py          ← Root URL configuration
│   └── wsgi.py
│
├── attendance/          ← Main Django app
│   ├── models.py        ← UserProfile, MakeUpClass, RemedialCode, MakeUpAttendance
│   ├── views.py         ← All view logic (auth, faculty, student)
│   ├── forms.py         ← Django forms
│   ├── urls.py          ← App URL patterns
│   ├── admin.py         ← Admin panel registration
│   └── templates/
│       └── attendance/
│           ├── base.html           ← Base layout with navbar + sidebar
│           ├── login.html
│           ├── register.html
│           ├── dashboard.html      ← Different UI for faculty vs student
│           ├── faculty_classes.html
│           ├── schedule_class.html
│           ├── class_detail.html   ← Code generation + attendance tracking
│           ├── mark_attendance.html ← Student code entry
│           ├── my_attendance.html
│           └── confirm_delete.html
│
├── manage.py
├── requirements.txt
└── README.md
```

---

## 🔑 How the Remedial Code System Works

1. **Faculty** schedules a make-up class
2. On the day, faculty opens the class detail page and clicks **Generate Remedial Code**
3. A **unique 6-character code** (e.g. `AB1C2D`) is generated with an expiry (15 min / 30 min / 1 hr / 2 hrs)
4. Faculty shares the code verbally or on the projector
5. **Students** go to "Mark Attendance", enter the code
6. System validates: Is it active? Not expired? Not already used by this student?
7. Attendance is recorded in a **separate table** (`MakeUpAttendance`) — independent from regular attendance
8. Faculty can see all students who marked attendance in real-time

---

## 🧠 Python / Django Concepts Used

- **Django ORM** — Models, ForeignKey, OneToOneField, QuerySets
- **Class-based relationships** — UserProfile extending `auth.User`
- **Django Forms** — ModelForms, custom validation in `clean()`
- **Django Auth** — `login()`, `logout()`, `@login_required`
- **Django Messages** — Flash messages for user feedback
- **`timezone.now()`** — Timezone-aware datetime for code expiry
- **`random.choices()`** — Unique code generation
- **AJAX / JSON response** — `JsonResponse` for live code countdown
- **Django Admin** — Full admin registration

---

## 👥 User Roles

| Role | Can Do |
|------|--------|
| Faculty | Schedule classes, generate codes, view attendance |
| Student | Mark attendance via code, view own records |
| Admin (superuser) | Full access via `/admin/` |

---

*Built for LPU Project II — Python and Full Stack*
