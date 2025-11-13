# UniHub – A Modern Campus Companion

UniHub is an Android mobile application designed to streamline and enhance the campus experience for students. It serves as a comprehensive platform where users can easily discover and engage with various campus events and clubs, ensuring they stay informed and involved in the vibrant community life. Additionally, UniHub offers a robust feature for managing notes. The app also provides timely notifications, keeping users updated on important announcements and deadlines. Furthermore, UniHub simplifies the process of registering for activities, making it convenient for students to participate in extracurricular events. All these functionalities are delivered through a fast and polished Material 3 user interface, ensuring a seamless and visually appealing user experience. 

---

## Tech Stack 

- Platforms: Android
- Frontend: Flutter (Material 3, Impeller, Dynamic Color)
- Backend: Spring Boot (recommendations/search)
- Cloud: Firebase (Auth, Firestore, Messaging)

---

## Highlights

- Beautiful, responsive UI
  - Dynamic Color (Material You), custom themes, micro‑interactions
  - Shimmer skeletons for fast‑perceived performance
  - SlideUpPageRoute transitions and interactive cards
- Events
  - Browse, details, registration CTA, add‑to‑calendar with robust fallbacks (native intent → Google Calendar web → ICS share)
- Clubs
  - Grid/list browsing, details, membership actions
- Notes
  - Branch‑aware recommendations
  - Branch‑scoped search and fast downloads
- Notifications
  - FCM push, foreground/background handling
- Reliability & performance
  - Firestore offline persistence
  - Centralized error handling with AppException/Result, retry with backoff, connectivity‑aware UI
  - RepaintBoundary and constraint‑aware layouts to avoid jank/overflows

---

## Screenshots

**Authentication**

|<img width="200" alt="ForgotPassword" src="https://github.com/user-attachments/assets/3f552d99-e29c-4d6d-a880-0d7c616e6d63" />| |<img width="200" alt="Register" src="https://github.com/user-attachments/assets/90c3f266-f37b-429f-a72f-c5517bf4f2ea" />| |<img width="200" alt="Login" src="https://github.com/user-attachments/assets/3e50c142-0235-47de-ada3-2a00b02802cd" />|

---

**Dashboard** 

|<img src="https://github.com/user-attachments/assets/98812901-3b92-41c8-81fd-584f0abeb920" alt="Dashboard1" width="200" />| |<img width="200" alt="Dashboard2" src="https://github.com/user-attachments/assets/f77eee52-31c4-4885-b6e5-fcd2fc8a65c0" />|

---

**Events**

|<img width="200" alt="Events" src="https://github.com/user-attachments/assets/428abdea-bce1-41c8-aa45-6e08fdba7cec" />| |<img width="200" alt="Event_details" src="https://github.com/user-attachments/assets/fa07f9ef-bed3-4deb-ae2f-fc51b73ac2c4" />| |<img width="200" alt="Event_create" src="https://github.com/user-attachments/assets/a4fc4622-8659-4aaf-8c12-e498a21fae78" />|

---

**Notes**

|<img width="200" alt="Notes_upload" src="https://github.com/user-attachments/assets/8b793dfc-aed8-4f2c-8435-87a5752f55f9" />| |<img width="200" alt="Notes_browse2" src="https://github.com/user-attachments/assets/8594f6f8-cabe-4277-bc89-c1f2af4f5e55" />| |<img width="200" alt="Notes_browse1" src="https://github.com/user-attachments/assets/e9ef21ba-8eda-4954-986d-eafd0c2f67ce" />|

---

**Clubs** 

|<img width="200" alt="Clubs" src="https://github.com/user-attachments/assets/3b910f97-c16d-439d-ab76-85d25b07c6be" />| |<img width="200" alt="Club_details" src="https://github.com/user-attachments/assets/c5054c4f-6e79-4496-b8c6-914de569bb61" />| |<img width="200" alt="Club_gallery" src="https://github.com/user-attachments/assets/693de090-2d9f-4174-8cdc-b6ce410f44bd" />| |<img width="200" alt="Club_feed" src="https://github.com/user-attachments/assets/0bfd55b2-27cf-4bf7-bd38-4dd54adbe5d1" />|

---

**Profile** 

|<img width="200" alt="Profile" src="https://github.com/user-attachments/assets/68b9ec3e-e0b6-48d2-b9bf-c05f0eb5b200" />|

---

**More**

|<img width="200" alt="More" src="https://github.com/user-attachments/assets/2f4337e8-16ef-42b8-8bd5-17b7a8e4b5e1" />|

---

**Faculty Contact**

---

|<img width="200" alt="FaclutyContact" src="https://github.com/user-attachments/assets/e037511c-70d3-4662-923c-dfb6f31e881c" />|

---

**Notification Settings**

---

|<img width="200" alt="Notification" src="https://github.com/user-attachments/assets/1dcda71a-6541-433b-bf72-e7c92d17012b" />|

---

**SGPA Calculator**

|<img width="200" alt="SGPA_calculator" src="https://github.com/user-attachments/assets/2cc1bb10-966d-49ab-bbec-f65f51f5c44a" />| |<img width="200"  alt="CGPA_calculator" src="https://github.com/user-attachments/assets/6f43f696-5b70-4218-b45a-bf25b7ab6eea" />|

---

**Lost & Found**

<img width="200"  alt="Lost_found1" src="https://github.com/user-attachments/assets/e306b8d9-1594-4b4d-9313-93d83c4d168d" />
<img width="200"  alt="Lost_found2" src="https://github.com/user-attachments/assets/35ae0926-1597-4c32-9531-1a76992c423f" />
<img width="200"  alt="Lost_found3" src="https://github.com/user-attachments/assets/ff9aafed-6ae9-459e-9676-82ea2948c452" />

---

## Architecture

- Presentation
  - Screens (feature pages)
  - Widgets (reusable components: shimmer, error state, offline banner)
  - Navigation via MaterialApp + global NavigationService
- Domain/Services
  - EventService, NoteService, SearchService, ApiService
  - ConnectivityService (online/offline stream)
- Core
  - Error model: AppException with mappers (Firebase/HTTP/Platform)
  - Result<T> (Success/Failure)
  - safeFuture/toResultStream wrappers, retry with exponential backoff + jitter
- Platform
  - Firebase initialization, notifications, timezones
  - Android calendar integration with manifest queries (Android 11+)

Folder sketch (abbreviated):
```
lib/
  core/
    errors/app_exception.dart
    result.dart
    safe_execute.dart
    retry.dart
  services/
    api_service.dart
    event_service.dart
    note_service.dart
    search_service.dart
    connectivity_service.dart
    navigation_service.dart
  screens/
    dashboard_screen.dart
    modern_home_screen.dart
    events_screen.dart
    clubs_screen.dart
    notes_screen.dart
    event_details_screen.dart
    login_screen.dart
    register_screen.dart
    splash_screen.dart
  widgets/
    shimmer_loading.dart
    error_state.dart
    offline_banner.dart
    retry_on_reconnect.dart
  utils/
    error_to_message.dart
  theme/
    app_theme.dart
main.dart
```

---

## Key UX/Engineering Features

- ShimmerLoading
  - Grid/list shimmers sized by layout constraints to avoid overflows
- AnimatedInteractiveCard + SlideUpPageRoute
  - Micro‑interactions for lists and smooth page transitions
- Error handling
  - Consistent ErrorState/SmallInlineError with friendly messages
  - Global hooks: runZonedGuarded, FlutterError.onError, PlatformDispatcher.onError
  - Auto‑retry on reconnect via RetryOnReconnect + connectivity stream
- Performance
  - Impeller (Vulkan/Metal), image caching, const widgets, RepaintBoundary
  - Debounced search, no heavy work in build
- Calendar fallback chain
  - Native add intent → Google Calendar web template → ICS share

---

## Getting Started

Prerequisites:
- Flutter 3.29.3, Dart SDK 3.7.2
- Android Studio , Java 17+
- Firebase project (Auth + Firestore + Messaging)

1) Clone front/back
```
git clone https://github.com/sumukh1203/unihub.git
git clone https://github.com/sumukh1203/unihub-backend.git
```

2) Backend (Spring Boot)
- Set in application.properties:
```
server.port=8080
server.address=0.0.0.0
```
- Run:
```
cd unihub_backend
./mvnw spring-boot:run
```

3) Firebase setup (frontend)
- Add google-services.json (Android) and GoogleService-Info.plist (iOS)
- Or run FlutterFire CLI to generate firebase_options.dart
- Ensure AndroidManifest allows cleartext during dev if using http:
```
android:usesCleartextTraffic="true"
```

4) Run on Android emulator
```
cd unihub_frontend
flutter pub get
flutter run -d emulator --dart-define=API_BASE_URL=http://10.0.2.2:8080
```

Notes:
- 10.0.2.2 works only on Android emulator.
- Keep secrets out of the repo (service files, API keys).

---

## Testing

Run unit/widget tests:
```
flutter test
```

Included samples:
- Result and safeFuture behavior
- error_to_message mapping
- ErrorState widget (retry disabled state)

---

## Notable Implementations

- Branch‑scoped Notes
  - Recommendations and search are restricted to the user’s branch; downloads supported with progress
- Connectivity‑aware UI
  - OfflineBanner across the app; retries disabled while offline and auto‑retry on reconnect
- Robust “Add to Calendar”
  - Android manifest queries for calendar apps (Android 11+)
  - Web intent fallback and ICS export as last resort

---

## Tech Stack

- Flutter: Material 3, Dynamic Color, Impeller
- Firebase: Auth, Firestore (offline persistence), FCM
- Backend: Spring Boot (Java), personalized recommendations API

---

## License

This repository is for portfolio/demo use. Do not commit private keys or organization data.

---

## Contact
**SUMUKH H**
|sumukh122004@gmail.com|
