# Flutter & Dart Project Structure Guide for Copilot

This guide helps GitHub Copilot understand the project structure and conventions used in this Flutter/Dart project, based on the best practices from Code with Andrea (https://codewithandrea.com/articles/flutter-project-structure/).

## Project Directory Structure

### Core Directories

- **lib/**: Main application code
  - **main.dart**: Entry point of the application
  - **models/**: Data models and classes
  - **services/**: Business logic, API calls, database operations
  - **providers/**: State management (Riverpod, Provider, etc.)
  - **screens/**: Full page widgets
  - **widgets/**: Reusable UI components
  - **utils/**: Utility functions and constants
  - **config/**: App configuration and constants

- **test/**: Unit and widget tests
- **integration_test/**: Integration tests
- **assets/**: Images, fonts, and other static files
- **android/**: Android-specific code (Kotlin/Java)
- **ios/**: iOS-specific code (Swift/Objective-C)
- **web/**: Web-specific code
- **windows/**, **macos/**, **linux/**: Platform-specific code

## Naming Conventions

### File Naming
- Use snake_case for all Dart file names: `user_model.dart`, `auth_service.dart`
- One main class per file
- Keep filenames descriptive

### Class & Variable Naming
- Use PascalCase for classes: `UserModel`, `AuthService`
- Use camelCase for variables and functions: `userName`, `fetchUserData()`
- Use UPPER_SNAKE_CASE for constants: `API_BASE_URL`, `DEFAULT_TIMEOUT`

## File Organization Guidelines

### Models Directory
```
lib/models/
├── user_model.dart
├── product_model.dart
├── response_model.dart
└── exceptions.dart
```

### Services Directory
```
lib/services/
├── auth_service.dart
├── api_service.dart
├── database_service.dart
├── local_storage_service.dart
└── notification_service.dart
```

### Providers/State Management
```
lib/providers/
├── auth_provider.dart
├── user_provider.dart
├── product_provider.dart
└── app_state_provider.dart
```

### Screens Directory
```
lib/screens/
├── auth/
│   ├── login_screen.dart
│   ├── signup_screen.dart
│   └── forgot_password_screen.dart
├── home/
│   ├── home_screen.dart
│   └── home_widgets.dart
└── profile/
    └── profile_screen.dart
```

### Widgets Directory (Reusable Components)
```
lib/widgets/
├── common/
│   ├── app_button.dart
│   ├── app_text_field.dart
│   ├── app_card.dart
│   └── custom_app_bar.dart
└── loading/
    ├── loading_indicator.dart
    └── shimmer_loading.dart
```

### Utils Directory
```
lib/utils/
├── constants.dart
├── app_colors.dart
├── app_text_styles.dart
├── app_dimensions.dart
├── validators.dart
├── extensions.dart
└── helpers.dart
```

## Code Style & Best Practices

### Imports Organization
- Organize imports in three groups separated by blank lines:
  1. Dart imports
  2. Flutter imports
  3. Package imports
  4. Relative imports

```dart
import 'dart:async';
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

import 'package:your_app/models/user_model.dart';
import 'package:your_app/services/auth_service.dart';

import '../widgets/custom_app_bar.dart';
import 'home_widgets.dart';
```

### State Management Best Practices
- Use providers for state management (Riverpod is recommended)
- Keep business logic separate from UI code
- Use sealed classes for union types
- Implement proper error handling

### Error Handling
```dart
// Always handle exceptions in services
try {
  final data = await service.fetchData();
} catch (e) {
  // Log and rethrow with meaningful message
  throw CustomException('Failed to fetch data: $e');
}
```

### Testing Structure
```
test/
├── models/
├── services/
├── providers/
└── widgets/

integration_test/
├── app_test.dart
└── flow_test.dart
```

## Asset Organization

### Images
```
assets/
├── images/
│   ├── svg/
│   ├── png/
│   └── jpg/
├── fonts/
└── animations/
```

In `pubspec.yaml`:
```yaml
flutter:
  assets:
    - assets/images/
    - assets/images/svg/
  fonts:
    - family: CustomFont
      fonts:
        - asset: assets/fonts/CustomFont-Regular.ttf
        - asset: assets/fonts/CustomFont-Bold.ttf
          weight: 700
```

## Platform-Specific Code

### Android (Kotlin)
```
android/app/src/main/kotlin/com/example/app/
├── MainActivity.kt
└── services/
```

### iOS (Swift)
```
ios/Runner/
├── GeneratedPluginRegistrant.swift
├── AppDelegate.swift
└── Services/
```

## Common Patterns

### Repository Pattern
```dart
abstract class IUserRepository {
  Future<User> getUser(String id);
  Future<List<User>> getAllUsers();
  Future<void> createUser(User user);
}

class UserRepository implements IUserRepository {
  // Implementation
}
```

### Service Layer
- Keep services focused on single responsibility
- Return clean data models from services
- Handle all error cases

### Provider Pattern (Riverpod)
```dart
final userProvider = FutureProvider((ref) async {
  final service = ref.watch(userServiceProvider);
  return service.getUser();
});
```

## Dependencies Organization in pubspec.yaml

```yaml
dependencies:
  flutter:
    sdk: flutter  
  
  # State Management
  flutter_riverpod: ^latest  
  
  # Networking
  dio: ^latest  
  
  # Local Storage
  shared_preferences: ^latest
  hive: ^latest  
  
  # UI
  google_fonts: ^latest  
  cached_network_image: ^latest  
  
  # Utilities
  intl: ^latest
  logger: ^latest  
  
dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^latest
```

## Copilot Instructions

When generating code for this project:

1. Follow the directory structure above when suggesting file locations
2. Use appropriate state management (Riverpod recommended)
3. Separate business logic from UI widgets
4. Always organize imports correctly (dart, flutter, packages, relative)
5. Use proper naming conventions (snake_case for files, PascalCase for classes)
6. Suggest error handling and proper exception management
7. Include proper type annotations (avoid dynamic when possible)
8. For reusable components, suggest placing in lib/widgets/common/
9. For utilities, organize by functionality in lib/utils/
10. Suggest tests for services and providers

## Additional Resources

- [Code with Andrea - Flutter Project Structure](https://codewithandrea.com/articles/flutter-project-structure/)
- [Effective Dart Style Guide](https://dart.dev/guides/language/effective-dart/style)
- [Flutter Architecture Samples](https://github.com/brianegan/flutter_architecture_samples)
- [Riverpod Documentation](https://riverpod.dev/)