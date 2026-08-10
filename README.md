# MessMate - Modern Hostel Mess Departure & Meal Coordination App 🍽️🚀

**MessMate** is a production-ready mobile application designed for hostel students living on campus. It solves the common daily hassle of calling multiple friends individually before every meal (Breakfast, Lunch, Snacks, Dinner) by providing real-time departure sync, automated push & offline notifications, countdown timers, group status updates, lightweight chat, and student statistics.

---

## 🌟 Key Features

### 🔐 Multi-Provider Authentication & Profile
- **Login Options**: Google Sign-In, Phone OTP modal verification, and Email/Password.
- **Student Profile**: Stores UID, Name, Profile Picture, Hostel Name, Block, Floor, Room Number, Department, Year, and Phone Number.

### 🏢 Hierarchical Onboarding
- **Stepped Selection**: Hostel Building ➔ Hostel Block ➔ Floor Number ➔ Room Number.
- **Group Join Options**:
  - **QR Code Scanning**: Scan a room/wing mate's screen using built-in scanner (`mobile_scanner`).
  - **Invitation Code**: Enter unique code (e.g. `MESS-210-CS`).
  - **Create Group**: Generate new group with instant QR generation (`qr_flutter`).

### ⏰ Home Screen & Live Meal Countdown
- Greeting header ("Hello, Suraj") with active meal departure streak counter.
- **Today's Meals**: Breakfast, Lunch, Snacks, Dinner cards displaying start/end timings, menu items, and live status.
- **Live Tabular Countdown**: Real-time counter (e.g. `00:09:45`) updating every second.

### 🟢 Live Group Status & Quick Actions
- **Instant Status Selection**:
  - `I'm Coming` (Emerald badge ✔)
  - `Wait 10 Minutes` (Amber badge ⏳ - Broadcasts arrival delay notice to group)
  - `Skip Today` (Terracotta badge ❌)
- **Departure Mode**: Tap `I'm Leaving Room Now!` to broadcast instant alert (*"Nirmal has left Room 210 for BVC Hostel Mess. Est arrival: 2 minutes"*).
- **Group Summary**: Real-time counts of Total Coming, Waiting, and Absent friends.

### 💬 Group Chat & Announcement Notice
- Lightweight group messaging supporting meal discussion tags, pinned admin announcements, typing indicators, and read receipts.

### 📊 Attendance Statistics & Analytics
- **FL Chart Integration**: Interactive bar charts for attendance rate % by meal type.
- **Student Metrics**: Meals Attended, Late Arrivals, Current Streak, Average Response Time, and **"Most Active Mess Companion"** award card.

### ⚙️ Settings & Notification Controls
- **Reminder Time Offset**: Select 5, 10, 15, or 20 minutes before meal starts.
- **Alarm Volume & Sound**: Sound selector & volume slider.
- **Privacy Mode**: Approximate hostel location sharing toggle (no continuous background location tracking).
- **Theme**: Material 3 Dark / Light Mode support.

---

## 🏗 Project Architecture (Clean Architecture + Riverpod)

```
c:\projecct 1\messapp\
├── android/
├── ios/
├── functions/                     # Firebase Cloud Functions (Node.js)
│   ├── index.js                   # FCM push triggers & Firestore triggers
│   └── package.json
├── firestore.rules                # Production Firestore security rules
├── firestore.indexes.json         # Composite database indexes
├── firebase.json                  # Firebase configuration
├── pubspec.yaml                   # Package dependencies
├── test/
│   └── widget_test.dart           # Unit & widget test suite
└── lib/
    ├── main.dart                  # Entry point with ProviderScope
    ├── app/
    │   ├── constants/             # AppConstants, hostel metadata
    │   ├── router/                # GoRouter with 14 full screens
    │   └── theme/                 # AppColors, AppTypography, AppTheme (M3)
    ├── core/
    │   ├── services/              # LocalNotificationService, FirebaseService, QRService
    │   ├── utils/                 # DateTimeUtils (HH:MM:SS formatters)
    │   └── widgets/               # CustomButton, CustomTextField, StatusBadge, LoadingSkeleton
    └── features/
        ├── auth/                  # Login, Register, Splash, User Model & AuthProvider
        ├── onboarding/            # Select Hostel, Join/Create Group, QR Scanner
        ├── home/                  # Home Screen, Meal Card, Live Countdown, Quick Action Bar
        ├── meals/                 # Meal Details, Meal Model, Attendance Model & Provider
        ├── group/                 # Group Members, Admin Panel & Group Provider
        ├── chat/                  # Group Chat, Message Model & Chat Provider
        ├── profile/               # Student Profile & Streaks
        ├── statistics/            # FL Chart analytics & User Stats
        ├── notifications/         # Push & Local Notification Log
        └── settings/              # Dark Mode, Reminder Offsets & Privacy
```

---

## 🗄️ Firestore Database Design

### `users` Collection
```json
{
  "uid": "user_101",
  "name": "Suraj Thakur",
  "email": "suraj.thakur@hostel.edu",
  "phoneNumber": "+91 98765 43210",
  "profilePic": "https://i.pravatar.cc/150?img=11",
  "hostelName": "BVC Hostel (Boys)",
  "block": "Block B",
  "floor": "2nd Floor",
  "roomNumber": "210",
  "department": "Computer Science & Engineering",
  "year": "3rd Year",
  "groupId": "group_csec_210",
  "isGroupAdmin": true,
  "createdAt": "2026-07-28T22:00:00.000Z"
}
```

### `groups` Collection
```json
{
  "id": "group_csec_210",
  "name": "Bvc Boys Mess Squad 🚀",
  "hostelName": "bvc Hostel (Boys)",
  "inviteCode": "MESS-210-CS",
  "qrCodeData": "messmate://group/group_csec_210",
  "adminId": "user_101",
  "moderatorIds": ["user_102"],
  "memberIds": ["user_101", "user_102", "user_103", "user_104"],
  "pinnedNotice": "📢 Dinner starts at 7:30 PM today! Special Paneer Tikka menu."
}
```

### `meals` Collection
```json
{
  "id": "meal_dinner",
  "type": "dinner",
  "title": "Dinner",
  "startTime": "07:30 PM",
  "endTime": "09:00 PM",
  "menuItems": ["Shahi Paneer", "Butter Roti", "Veg Biryani", "Raita", "Ice Cream"],
  "status": "current"
}
```

### `attendance` Collection
```json
{
  "userId": "user_101",
  "userName": "Suraj Thakur",
  "userPhoto": "https://i.pravatar.cc/150?img=11",
  "roomNumber": "210",
  "mealId": "meal_dinner",
  "status": "coming",
  "waitMinutes": 0,
  "departureNote": null,
  "updatedAt": "2026-07-28T22:15:00.000Z"
}
```

---

## ⚡ Firebase Cloud Functions & Push Notifications

Firebase Cloud Functions are configured in `functions/index.js`:

1. **`sendMealReminder`**: PubSub cron trigger running every 15 minutes before scheduled meals. Broadcasts FCM push message:
   > 🍽 *Dinner starts in 15 minutes. 7 friends are joining. Come to the mess together.*
2. **`onMemberDeparture`**: Firestore trigger on `attendance` document update. When a student clicks *"I'm Leaving"*, triggers push notification:
   > 🏃‍♂️ *Rahul has left Room 210. Estimated arrival: 2 minutes.*
3. **`onMealTimingChange`**: Firestore trigger on `meals` document update. Sends real-time timing sync alert to all group members when admin updates mess timings.

---

## 🚀 Installation & Setup Guide

### 1. Prerequisites
- Flutter SDK (v3.35.4+ / Dart 3.9+)
- Node.js (v18+) & Firebase CLI (`npm install -g firebase-tools`)

### 2. Install Dependencies
```bash
git clone <repository_url>
cd messapp
flutter pub get
```

### 3. Run Application locally
```bash
# Run on connected phone, emulator, or Chrome browser
flutter run
```

### 4. Deploy Firebase Security Rules & Cloud Functions
```bash
firebase login
firebase init
firebase deploy --only firestore:rules,functions
```

---

## 🧪 Testing Guide

Run automated unit and widget tests:
```bash
flutter test
```

Run code analysis to confirm zero errors or lints:
```bash
flutter analyze
```

---

## 🔮 Future Improvements & Roadmap

1. **Mess Rating & Food Quality Feedback**: Post-meal 5-star rating system with feedback logs for hostel wardens.
2. **Special Menu Voting**: Weekly poll widget for students to vote on Sunday special menus.
3. **Live Hostel Map & Approximate Geofencing**: Low-energy Bluetooth beacon or Wi-Fi SSID check when entering mess hall to automatically mark attendance as "Arrived".
