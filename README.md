# Wonder Words
The app is WonderWords, an insightful quotes archive. Users can
explore, upvote, downvote and mark their favorite quotes.

![image](https://user-images.githubusercontent.com/20933055/236761160-016d419c-0c41-4801-b39b-5efc5ec9f605.png)

![image](https://user-images.githubusercontent.com/20933055/236761227-b83215f1-d9c0-4713-8559-8718eafb280f.png)

# Features: 
search, pagination, forms, authentication, deep links,
internationalization, dark mode, analytics, feature flags, automated tests, CI/CD
# Architecture

![image](https://user-images.githubusercontent.com/20933055/236761616-64a454e5-2779-4bd6-8098-bff5dc4429b0.png)

This architecture is the result of Package-by-layer and Package-by-feature architecture, some packages are feature-based, like `quote_list`, `quote_details`
and `sign_in`. In contrast, all the other packages represented above are layerbased, like `key_value_storage` and `component_library`.
What is a feature?
we consider a feature to be either:
1. A screen.
2. A dialog that executes I/O calls, like networking and databases.
WonderWords’ `forgot_password` package falls into this category.
Other than that, if it’s just a regullar UI component that we want to share
between two or more screens, like a search bar, we should place it inside the
`component_library` package.
* component_library: Holds UI components that either are, or have the
potential to be, reused across different screens.

* fav_qs_api: Since both user_repository and quote_repository talk to your
remote API, it makes sense to create a separate package for it.

* key_value_storage: Same story as fav_qs_api, but this one wraps your local
storage.

* domain_models: You can expect that repositories will need to start sharing
models or custom exceptions at some point. Therefore, it’s a good thing to

have a separate package for your domain models right from the start.
* form_fields: Contains field validation logic that different features share.

# API
FavQs.com is an online quote repository with both web and mobile apps.
We stored API in compile time variable.
Navigate to *packages/fav_qs_api/lib/src* and open *fav_qs_api.dart*.
Look at setUpAuthHeaders at the end of the file:
```dart
void setUpAuthHeaders(UserTokenSupplier userTokenSupplier) {
 final appToken = const String.fromEnvironment(
 _appTokenEnvironmentVariableKey,
 );
 options = BaseOptions(headers: {
 'Authorization': 'Token token=$appToken',
 });
 // ...
}
```
It’s telling Dart to look up a value inside a compile-time variable called fav-qs-app-token .We do that by specifying the dart-define
parameter when using flutter run to run your app, like so:
`flutter run --dart-define=fav-qs-app-token=YOUR_FavQs.com_DEVELOPER_KEY`
# Firebase
WonderWords relies on Firebase for all the typical use cases in mobile apps:
dynamic links, analytics, crash reporting, feature flags and A/B tests.Start by opening Firebase’s console and signing in with a Google account. Then,
click Create a project or Add project if you have a project before.

# Install
To use this app from restricted area you may use VPN.
Here is the fat apk file to install and explore the application.
[app-release.zip](https://github.com/m8811163008/wonderWords/files/11418976/app-release.zip)
