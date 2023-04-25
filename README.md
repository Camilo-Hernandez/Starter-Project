# Starter Project

Plantilla para todo proyecto Android que fuera a crearse desde cero

Pasos a seguir para adaptar el proyecto nuevo:
1. Crear el proyecto desde la plantilla Empty Activity con Compose

![image](https://user-images.githubusercontent.com/36543483/234294026-e197a7a2-9250-4a44-8def-74d8d054aedd.png)

2. Pegar el build.gradle a nivel de proyecto
```groovy
buildscript {
    ext {
        compose_version = '1.4.3'
        hilt_version = '2.45'
    }
}
// Top-level build file where you can add configuration options common to all sub-projects/modules.
plugins {
    id 'com.android.application' version '8.0.0' apply false
    id 'com.android.library' version '8.0.0' apply false
    id 'org.jetbrains.kotlin.android' version '1.8.10' apply false
    id 'com.google.dagger.hilt.android' version "$hilt_version" apply false
}
```

3. Pegar los siguientes campos del build.gradel a nivel de app
```groovy
plugins {
    ... // Se agregan a lo que ya está
    id 'kotlin-kapt'
    id 'dagger.hilt.android.plugin'
}

// Se reemplaza todo
compileOptions {
    sourceCompatibility JavaVersion.VERSION_17
    targetCompatibility JavaVersion.VERSION_17
}
kotlinOptions {
    jvmTarget = '17'
}
composeOptions {
    kotlinCompilerExtensionVersion compose_version
}

dependencies {
    implementation 'androidx.core:core-ktx:1.10.0'
    implementation 'androidx.lifecycle:lifecycle-runtime-ktx:2.6.1'
    implementation 'androidx.activity:activity-compose:1.7.1'
    implementation platform('androidx.compose:compose-bom:2022.10.00')
    implementation 'androidx.compose.ui:ui'
    implementation 'androidx.compose.ui:ui-graphics'
    implementation 'androidx.compose.ui:ui-tooling-preview'
    implementation 'androidx.compose.material3:material3'
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.5'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
    androidTestImplementation platform('androidx.compose:compose-bom:2022.10.00')
    androidTestImplementation 'androidx.compose.ui:ui-test-junit4'
    debugImplementation 'androidx.compose.ui:ui-tooling'
    debugImplementation 'androidx.compose.ui:ui-test-manifest'

    // Compose dependencies
    implementation "androidx.lifecycle:lifecycle-viewmodel-compose:2.6.1"
    // Lifecycle
    implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:2.6.1"

    // -- Dependencias para usar Hilt, una biblioteca que simplifica la inyección de dependencias en Android
    // Dagger Hilt
    implementation "com.google.dagger:hilt-android:$hilt_version"
    kapt "com.google.dagger:hilt-android-compiler:$hilt_version"
    implementation "com.google.dagger:hilt-android:$hilt_version"
    kapt "com.google.dagger:hilt-compiler:$hilt_version"
    // Androidx Hilt
    implementation 'androidx.hilt:hilt-navigation-compose:1.0.0'
    kapt "androidx.hilt:hilt-compiler:1.0.0"
    implementation "androidx.hilt:hilt-lifecycle-viewmodel:1.0.0-alpha03" // TODO: Aún no sé cuándo implementarlo
    // For instrumentation tests
    androidTestImplementation  "com.google.dagger:hilt-android-testing:$hilt_version"
    kaptAndroidTest "com.google.dagger:hilt-compiler:$hilt_version"
    // For local unit tests
    testImplementation "com.google.dagger:hilt-android-testing:$hilt_version"
    kaptTest "com.google.dagger:hilt-compiler:$hilt_version"

    // Accompanist: Dependencia para cargar imágenes
    implementation "io.coil-kt:coil-compose:2.2.2"

    // Dependencias para usar Coroutines, una biblioteca que permite escribir código asíncrono de forma secuencial y sin bloqueos
    def coroutines_version = '1.6.4'
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:$coroutines_version"
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:$coroutines_version"

    // Retrofit
    def retrofit_version = '2.9.0'
    implementation "com.squareup.retrofit2:retrofit:$retrofit_version"
    implementation "com.squareup.retrofit2:converter-gson:$retrofit_version"
    implementation "com.squareup.okhttp3:okhttp:5.0.0-alpha.2"

    // Dependencias para usar Room, una biblioteca que provee una capa de abstracción sobre SQLite para facilitar el acceso a datos persistentes
    def room_version = "2.5.1"
    implementation "androidx.room:room-runtime:$room_version"
    kapt "androidx.room:room-compiler:$room_version"
    // Kotlin Extensions and Coroutines support for Room
    implementation "androidx.room:room-ktx:$room_version"

}
```

4. Agregar el permiso de internet en el AndroidManifest.xml (Cuando se quiere acceder a una API remota)
```xml
    <uses-permission android:name="android.permission.INTERNET"/>
```
