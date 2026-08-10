# 📋 MessMate — Project State (v2.0)

> **Last Updated:** 2026-07-29  
> **Version:** 2.0.0+1  
> **Flutter SDK:** ^3.9.2 / Dart ^3.9  
> **Architecture:** Clean Architecture + Riverpod (feature-first)  
> **Backend:** Firebase (Firestore, Auth, Messaging, Storage, Cloud Functions)

---

## 🏗️ Architecture Pattern

```
features/<feature>/
├── domain/
│   └── models/         # Data classes with toMap/fromMap serialization
├── presentation/
│   ├── providers/      # Riverpod StateNotifier providers
│   ├── screens/        # Full-page screen widgets
│   └── widgets/        # Reusable feature-specific UI components
```

- **State Management:** `flutter_riverpod` (StateNotifier pattern)
- **Routing:** `go_router` with 21 routes (v2.0 routing integration complete)
- **Theme:** Material 3 with custom `AppColors`, `AppTypography`, `AppTheme` (light + dark, scheduled auto-switching)
- **Serialization:** Manual `toMap()` / `fromMap()` (no code generation, no freezed)

---

## 📦 Current Dependencies

| Package | Version | Purpose |
|---|---|---|
| `flutter_riverpod` | ^2.6.1 | State management |
| `go_router` | ^14.8.0 | Declarative routing |
| `google_fonts` | ^6.2.1 | Typography (Outfit, Inter) |
| `intl` | ^0.20.2 | Date/time formatting |
| `fl_chart` | ^0.70.2 | Statistics bar charts |
| `shared_preferences` | ^2.5.2 | Local settings persistence |
| `uuid` | ^4.5.1 | Unique ID generation |
| `qr_flutter` | ^4.1.0 | QR code rendering |
| `mobile_scanner` | ^6.0.4 | QR code camera scanning |
| `flutter_local_notifications` | ^18.0.1 | Local notification scheduling |
| `timezone` | ^0.10.1 | Timezone-aware scheduling |
| `firebase_core` | ^3.12.0 | Firebase initialization |
| `firebase_auth` | ^5.5.1 | Authentication |
| `cloud_firestore` | ^5.6.5 | Realtime database |
| `firebase_messaging` | ^15.2.4 | FCM push notifications |
| `firebase_storage` | ^12.4.4 | File/image storage |
| `confetti` | ^0.8.0 | Confetti animations for badges |
| `lottie` | ^3.3.1 | Lottie illustrations |
| `share_plus` | ^10.1.4 | Sharing wrapped statistics |
| `hive` | ^2.2.3 | Offline key-value database caching |
| `hive_flutter` | ^1.1.0 | Offline Flutter storage wrapper |
| `connectivity_plus` | ^6.1.4 | Network monitoring |
| `url_launcher` | ^6.3.1 | Launch external links |
| `home_widget` | ^0.7.0 | Home screen widget support |

---

## 🗂️ Feature Module Status

### ✅ Auth (`features/auth/`)
| Layer | Files | Status |
|---|---|---|
| **Model** | [user_model.dart](file:///c:/projecct%201/messapp/lib/features/auth/domain/models/user_model.dart) | ✅ Complete — gamification fields added |
| **Provider** | `auth_provider.dart` | ✅ Exists |
| **Screens** | `splash_screen.dart`, `login_screen.dart`, `register_screen.dart` | ✅ 3 screens |

**Gamification fields added to UserModel:** totalBadgesEarned, longestStreak, totalMealsAttended, nudgesSent, nudgesReceived

---

### ✅ Onboarding (`features/onboarding/`)
| Layer | Files | Status |
|---|---|---|
| **Screens** | `onboarding_carousel_screen.dart`, `select_hostel_screen.dart`, `join_create_group_screen.dart` | ✅ 3 screens |

---

### ✅ Home (`features/home/`)
| Layer | Files | Status |
|---|---|---|
| **Screens** | [home_screen.dart](file:///c:/projecct%201/messapp/lib/features/home/presentation/screens/home_screen.dart) | ✅ Contextual greetings, RSVP card added |
| **Widgets** | `meal_card.dart` (Hero & ratings), `live_countdown_widget.dart`, `quick_action_bar.dart` | ✅ 3 widgets |

---

### ✅ Meals (`features/meals/`)
| Layer | Files | Status |
|---|---|---|
| **Models** | `rsvp_model.dart`, `rating_model.dart`, `meal_model.dart`, `attendance_model.dart` | ✅ RSVP & Rating integrations complete |
| **Providers** | `rsvp_provider.dart`, `rating_provider.dart` | ✅ RSVP, Rating logic |
| **Screens** | `rsvp_screen.dart`, `meal_details_screen.dart` | ✅ Complete |
| **Widgets** | `rsvp_card.dart`, `rating_bottom_sheet.dart`, `meal_rating_summary.dart` | ✅ Complete |

---

### ✅ Gamification (`features/gamification/`)
| Layer | Files | Status |
|---|---|---|
| **Models** | `badge_model.dart`, `nudge_model.dart` | ✅ Badge & nudge structures |
| **Providers** | `badge_provider.dart`, `nudge_provider.dart`, `leaderboard_provider.dart` | ✅ Real-time data & rankings |
| **Screens** | `badges_screen.dart`, `leaderboard_screen.dart` | ✅ Complete |
| **Widgets** | `badge_card.dart`, `nudge_button.dart`, `badge_unlock_overlay.dart` | ✅ Complete |

---

### ✅ Chat (`features/chat/`)
| Layer | Files | Status |
|---|---|---|
| **Model** | [chat_message_model.dart](file:///c:/projecct%201/messapp/lib/features/chat/domain/models/chat_message_model.dart) | ✅ Reactions, reply, poll support |
| **Provider** | `chat_provider.dart` | ✅ sendMessage, createPoll, addReaction, voteOnPoll |
| **Screens** | `chat_screen.dart` | ✅ Integrates poll cards, reaction overlays |
| **Widgets** | `reaction_picker.dart`, `reaction_bar.dart`, `poll_message_card.dart`, `create_poll_sheet.dart`, `status_board_header.dart` | ✅ Complete |

---

### ✅ Statistics (`features/statistics/`)
| Layer | Files | Status |
|---|---|---|
| **Models** | `stats_model.dart`, `wrapped_model.dart` | ✅ Fully live data modeling |
| **Provider** | `stats_provider.dart` | ✅ Live Firestore aggregation |
| **Screens** | `statistics_screen.dart`, `wrapped_screen.dart` | ✅ Complete |
| **Widgets** | `heatmap_calendar.dart`, `companion_card.dart`, `popularity_chart.dart` | ✅ Complete |

---

### ✅ Complaints (`features/complaints/`)
| Layer | Files | Status |
|---|---|---|
| **Model** | `complaint_model.dart` | ✅ Categories and status tracker enums |
| **Provider** | `complaint_provider.dart` | ✅ Admin resolution logic |
| **Screens** | `complaint_screen.dart`, `complaint_list_screen.dart` | ✅ Complete |
| **Widgets** | `complaint_status_tracker.dart` | ✅ Vertical stepper |

---

### ✅ Expenses (`features/expenses/`)
| Layer | Files | Status |
|---|---|---|
| **Model** | `expense_model.dart` | ✅ Split-wise tracking |
| **Provider** | `expense_provider.dart` | ✅ Balance aggregation |
| **Screens** | `expense_screen.dart`, `add_expense_screen.dart` | ✅ Complete |
| **Widgets** | `balance_card.dart` | ✅ Net status card |

---

### ✅ Settings (`features/settings/`)
| Layer | Files | Status |
|---|---|---|
| **Provider** | `settings_provider.dart` | ✅ Auto-schedule dark mode added |
| **Screens** | `settings_screen.dart` | ✅ Complete |

---

## 🔥 Firestore Collections (v2.0)

| Collection | Document Key | Trigger Functions | Security Rules |
|---|---|---|---|
| `users` | `{userId}` (= UID) | `checkBadgeProgress` | Owner-write only |
| `groups` | `{groupId}` | None | Admin/Moderator write |
| `meals` | `{mealId}` | `onMealTimingChange` | Authenticated read/write |
| `attendance` | `{attendanceId}` | `onMemberDeparture` | Authenticated read/write |
| `messages` | `{messageId}` | None | Owner-write/delete |
| `rsvp` | `rsvp_{userId}_{YYYYMMDD}_{mealType}` | `onRsvpDeadline` | Owner-write/delete |
| `ratings` | `rating_{userId}_{mealId}_{YYYYMMDD}` | `onRatingSubmitted` | Owner-create, immutable |
| `badges` | `badge_{userId}_{badgeType}` | None | Read-only for users |
| `nudges` | `nudge_{nudgeId}` | `onNudgeSent` | Owner-create, immutable |
| `complaints` | `complaint_{complaintId}` | `onComplaintCreated` | Authenticated read/write |
| `expenses` | `expense_{expenseId}` | None | Authenticated read/write |

---

## ☁️ Cloud Functions (v2.0)

| Function | Trigger | Purpose |
|---|---|---|
| `sendMealReminder` | PubSub (every 15 min) | Push notification before meals |
| `onMemberDeparture` | Firestore `attendance` onUpdate | "X has left Room Y" notification |
| `onMealTimingChange` | Firestore `meals` onUpdate | Timing change alert |
| `onRsvpDeadline` | PubSub (10 PM daily) | Lock RSVPs, notify non-responders |
| `onRatingSubmitted` | Firestore `ratings` onCreate | Re-aggregates and updates average ratings |
| `onNudgeSent` | Firestore `nudges` onCreate | Sends nudge push alert to target user |
| `checkBadgeProgress` | Firestore `users` onUpdate | Validates and unlocks earned badges |
| `generateMonthlyWrapped` | PubSub (1st of month) | Compiles stats wrapped report data |
| `onComplaintCreated` | Firestore `complaints` onCreate | Notifies admins of new issues |

---

## 🛣️ Routes (21 current)

| Route | Screen |
|---|---|
| `/splash` | SplashScreen |
| `/login` | LoginScreen |
| `/register` | RegisterScreen |
| `/onboarding-intro` | OnboardingCarouselScreen |
| `/select-hostel` | SelectHostelScreen |
| `/join-group` | JoinCreateGroupScreen |
| `/home` | HomeScreen |
| `/meal-details` | MealDetailsScreen |
| `/rsvp` | RsvpScreen |
| `/members` | GroupMembersScreen |
| `/admin` | AdminPanelScreen |
| `/chat` | ChatScreen |
| `/profile` | ProfileScreen |
| `/badges` | BadgesScreen |
| `/leaderboard` | LeaderboardScreen |
| `/statistics` | StatisticsScreen |
| `/wrapped` | WrappedScreen |
| `/notifications` | NotificationsScreen |
| `/settings` | SettingsScreen |
| `/complaints` | ComplaintScreen |
| `/complaints/list` | ComplaintListScreen |
| `/expenses` | ExpenseScreen |
| `/expenses/add` | AddExpenseScreen |

---

## 🚧 Version 2.0 Improvements
1. **Offline database caching** implemented via Hive service.
2. **Dynamic system stats** load live Firestore metrics (heatmap, companion besties, and dishes).
3. **Immutability of ratings** and locking constraints at 10 PM.
4. **Scheduled dark mode** adjusts theme dynamically.
