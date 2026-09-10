# 🎗️ CancApp

CancApp is a Flutter mobile application designed to support cancer patients through every stage of their treatment journey. It brings health record management, medication and appointment reminders, doctor-patient communication, and a supportive community into a single, multi-role app for **patients, doctors, pharmacists, psychiatrists, and volunteers**.

> Built with Clean Architecture, Bloc/Cubit state management, and a fully localized (English/Arabic) experience.

## ✨ Key Features

- **Multi-Role Authentication** — Sign-up and login for five user types (Patient, Doctor, Pharmacist, Psychiatrist, Volunteer), with OTP email verification, password recovery, and biometric login.
- **Community Hub** — A social feed for sharing updates, images, comments, and reactions in a supportive space.
- **Push Notifications (FCM)** — Community activity (new likes, comments, and replies) triggers real-time push notifications via Firebase Cloud Messaging, so users stay engaged even when the app is in the background.
- **Real-time Chat** — Direct messaging between roles (e.g. patient ↔ doctor).
- **AI Chatbot** — An in-app assistant for instant answers to patient questions.
- **Medication & Appointment Reminders** — Local notifications with flexible schedules (daily, specific days, custom intervals), built on `flutter_local_notifications` and `timezone`.
- **Health Records** — Upload and organize medical documents, lab results, prescriptions, and scans.
- **Find Nearest Pharmacies** — Google Maps-based search for nearby pharmacies using live device location.
- **Profile Management** — Edit profile details, change passwords, and secure the app with fingerprint/Face ID.
- **Multi-language Support** — Fully localized UI in English and Arabic (`intl_en.arb`, `intl_ar.arb`).

## 📱 Screenshots
<img width="3000" height="1688" alt="image" src="https://github.com/user-attachments/assets/5d84821c-f7a0-495d-a09f-31003191bb89" />
<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/d6514ebe-6169-480a-83ff-0dac1a064c21" />
<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/07687d63-e2a5-43b1-9982-2457686ba67a" />
<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/5906af1a-f71c-44e8-86e9-55f4074d3f13" />
<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/ab7e1ca1-2883-4711-9cc8-78a2401f7eb1" />
<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/bd8aa604-95e7-405b-a91f-323d2feae57f" />
<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/509b337e-39ad-401b-a91d-2b4342088dcf" />
<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/0e34046a-7507-4c2d-b8b4-9daef0040c9e" />
<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/b198c1e7-36a2-47b6-ab0e-1e98578c7e33" />
<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/bf512ea8-533f-4f2b-af42-d5f216c03ff5" />

> Doctor View — Patient Records : This screen lets doctors quickly access a patient's profile and view their medical records in one place, including scans, lab results, prescriptions, and documents. From the doctor's own profile, they can manage accepted patient requests, edit their profile, change their password, or log out. Tapping into a patient (like Omar Ahmed) opens a categorized record view, making it easy to review a patient's full medical history at a glance.

<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/d03fda86-d4c4-46f5-bce1-cda4add4bbcb" />

## 📂 Project Structure

```
lib
├── core/                        # Shared logic and utilities
│   ├── cubits/                  # Global (app-wide) state management
│   ├── di/                      # get_it dependency injection setup
│   ├── helpers/                 # Utilities, extensions, DB helpers
│   ├── models/                  # Core data models (e.g. UserModel)
│   ├── networking/              # Dio client, endpoints, interceptors, error models
│   ├── routing/                 # go_router configuration and route names
│   ├── services/                # Background services (notifications, location)
│   ├── shared_feature/          # Features shared across roles:
│   │   ├── login/ · sign_up/ · otp/ · forgot_password/
│   │   ├── onboarding/ · who/ (role selection)
│   │   ├── chat/ · community/
│   │   ├── edit_profile/ · change_password/
│   ├── theming/                 # Colors, text styles, app-wide theme
│   └── widgets/                 # Reusable shared widgets
│
├── users/                       # Role-specific features
│   ├── patient/                 # Fully implemented
│   │   ├── chat/ · chatbot/ · home/ · profile/ · record/ · reminder/
│   ├── doctor/                  # Views and logic for doctors
│
├── l10n/                        # Localization source files (intl_en.arb, intl_ar.arb)
├── generated/                   # Auto-generated localization code
└── main.dart                    # App entry point
```

Each `data`/`presentation` pair under `shared_feature/` and `users/patient/` follows the same Clean Architecture split: `data/` for models and repositories, `presentation/` for Cubits, screens, and widgets.

## 🛠️ Tech Stack & Architecture

The app follows **Clean Architecture**, organized by feature with a clear separation between data and presentation:

- **Data layer** — Remote data via `dio`, local persistence via `hive` / `shared_preferences` / `flutter_secure_storage`.
- **Presentation layer** — Widgets driven by `flutter_bloc` / `Cubit` state management.

| Concern | Package(s) |
|---|---|
| State management | `flutter_bloc`, `equatable` |
| Navigation | `go_router` |
| Networking | `dio` (with auth & token-refresh interceptors) |
| Dependency injection | `get_it` |
| Local storage | `hive`, `hive_flutter`, `shared_preferences`, `flutter_secure_storage` |
| Environment config | `flutter_dotenv` |
| Maps & location | `google_maps_flutter`, `location` |
| Notifications | `flutter_local_notifications`, `timezone` |
| Auth & security | `local_auth` (biometrics), `pinput` (OTP) |
| Media & files | `image_picker`, `file_picker`, `cached_network_image`, `flutter_svg` |
| UI polish | `shimmer`, `redacted`, `bot_toast`, `persistent_bottom_nav_bar`, `easy_date_timeline`, `iconly`, `font_awesome_icon_class` |
| Localization | `flutter_localizations`, `intl`, `flutter_intl` |
| Misc | `dartz` (functional error handling), `uuid`, `audioplayers`, `translator` |

**Fonts:** Poppins, Almarai (Arabic), Righteous.
**Platforms:** Android, iOS, Web, and Windows targets are present in the repo.
