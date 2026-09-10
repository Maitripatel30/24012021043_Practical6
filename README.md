# Practical 6 — Frame by Frame Animation and Splash Screen

## 📱 Aim

Create an Android application to demonstrate **Frame by Frame Animation** and a **Splash Screen** with **Twin Animation** using Kotlin and XML.

---

## 📚 Study

The following Android concepts are studied and implemented in this practical:

* ImageView
* Frame by Frame Animation
* Twin Animation
* Immersive Mode
* Edge-to-Edge Content Display
* SplashScreen
* AnimationDrawable
* `animation-list`
* `oneShot` attribute
* `<set>` tag
* `startOffset`
* `duration`
* `<scale>` tag
* `<translate>` tag
* `<rotate>` tag
* `<alpha>` tag
* `onWindowFocusChanged()` method
* `AnimationUtils` class
* `loadAnimation()` method
* `setAnimationListener()` method
* `overridePendingTransition()` method
* `finish()` method
* `anim` folder in `res`
* Creating XML files from SVG/vector resources
* Gradient drawable using `<gradient>` inside `<shape>`

---

## ❓ What is Frame by Frame Animation?

**Frame by Frame Animation** displays a sequence of different images one after another to create the effect of movement.

In Android, it can be implemented using **AnimationDrawable** and an `<animation-list>` XML resource.

For example:

```xml
<animation-list android:oneshot="false">
    <item
        android:drawable="@drawable/frame1"
        android:duration="200" />

    <item
        android:drawable="@drawable/frame2"
        android:duration="200" />

    <item
        android:drawable="@drawable/frame3"
        android:duration="200" />
</animation-list>
```

Each image acts as one frame of the animation.

---

## ❓ What is Twin Animation?

**Twin Animation** is also called **View Animation** or **Tween Animation**.

It changes the properties of a view over a period of time, such as:

* Position
* Size
* Rotation
* Transparency

Android provides four main tween animation types:

| Animation | Purpose                    |
| --------- | -------------------------- |
| Scale     | Changes the size of a view |
| Translate | Moves a view               |
| Rotate    | Rotates a view             |
| Alpha     | Changes transparency       |

These animations can be combined using the `<set>` tag.

---

## 🌐 Edge-to-Edge Content Display

Edge-to-edge display allows the application content to extend behind the system bars and use the complete screen area.

It can be enabled using:

```kotlin
WindowCompat.setDecorFitsSystemWindows(window, false)
```

This allows the application UI to draw behind the status bar and navigation bar.

The application can then handle system bar insets according to the UI requirements.

---

# 🎨 Splash Screen

The application contains a separate `SplashActivity` that is displayed when the application starts.

The splash screen uses a **radial gradient rectangle**.

The background is created using the `<gradient>` tag inside the `<shape>` tag.

Example:

```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">

    <gradient
        android:type="radial"
        android:centerX="0.9"
        android:centerY="0.9"
        android:gradientRadius="1500"
        android:startColor="#FFC0CB"
        android:endColor="#0000FF" />

</shape>
```

### Gradient Properties

* Shape: Rectangle
* Gradient Type: Radial
* Center X: `0.9`
* Center Y: `0.9`
* Radius: `1500`
* Start Color: Pink
* End Color: Blue

---

# ✨ Animations Used

The practical demonstrates the following animation tags.

### 1. Scale Animation

The `<scale>` tag changes the size of a view.

```xml
<scale
    android:fromXScale="0.0"
    android:toXScale="1.0"
    android:fromYScale="0.0"
    android:toYScale="1.0"
    android:duration="1000" />
```

### 2. Translate Animation

The `<translate>` tag moves a view from one position to another.

```xml
<translate
    android:fromXDelta="0"
    android:toXDelta="0"
    android:fromYDelta="100"
    android:toYDelta="0"
    android:duration="1000" />
```

### 3. Rotate Animation

The `<rotate>` tag rotates a view.

```xml
<rotate
    android:fromDegrees="0"
    android:toDegrees="360"
    android:duration="1000" />
```

### 4. Alpha Animation

The `<alpha>` tag changes the transparency of a view.

```xml
<alpha
    android:fromAlpha="0.0"
    android:toAlpha="1.0"
    android:duration="1000" />
```

---

# 🔗 Animation Set

Multiple animations can be combined using the `<set>` tag.

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">

    <scale
        android:fromXScale="0.0"
        android:toXScale="1.0"
        android:fromYScale="0.0"
        android:toYScale="1.0"
        android:duration="1000" />

    <rotate
        android:fromDegrees="0"
        android:toDegrees="360"
        android:duration="1000" />

</set>
```

The `<set>` tag allows multiple animations to run together.

---

# ⏱️ startOffset and duration

### `android:startOffset`

`startOffset` specifies how long an animation waits before starting.

Example:

```xml
android:startOffset="100"
```

This means the animation starts after a **100 millisecond delay**.

### `android:duration`

`duration` specifies how long the animation takes to complete.

Example:

```xml
android:duration="1000"
```

This means the animation takes **1000 milliseconds (1 second)**.

---

# 🔁 AnimationDrawable

`AnimationDrawable` is used for **Frame by Frame Animation**.

Example:

```kotlin
val animationDrawable =
    imageView.drawable as AnimationDrawable

animationDrawable.start()
```

The drawable contains multiple images that are displayed sequentially.

---

# 🎬 AnimationUtils

`AnimationUtils` is used to load an animation XML resource.

Example:

```kotlin
val animation = AnimationUtils.loadAnimation(
    this,
    R.anim.animation
)
```

The animation can then be applied to a view:

```kotlin
imageView.startAnimation(animation)
```

---

# 👂 Animation Listener

An animation listener can be used to perform an action when an animation starts, repeats, or ends.

```kotlin
animation.setAnimationListener(object :
    Animation.AnimationListener {

    override fun onAnimationStart(animation: Animation?) {
    }

    override fun onAnimationEnd(animation: Animation?) {
    }

    override fun onAnimationRepeat(animation: Animation?) {
    }
})
```

---

# 🪟 onWindowFocusChanged()

`onWindowFocusChanged()` is called when the window gains or loses focus.

It can be used to start an animation after the activity becomes visible.

Example:

```kotlin
override fun onWindowFocusChanged(hasFocus: Boolean) {
    super.onWindowFocusChanged(hasFocus)

    if (hasFocus) {
        // Start animation
    }
}
```

---

# 🔄 overridePendingTransition()

`overridePendingTransition()` is used to apply an animation while switching between activities.

Example:

```kotlin
overridePendingTransition(
    R.anim.fade_in,
    R.anim.fade_out
)
```

It can make activity transitions smoother.

---

# ❌ finish()

`finish()` closes the current Activity.

For example, after moving from `SplashActivity` to `MainActivity`:

```kotlin
startActivity(Intent(this, MainActivity::class.java))
finish()
```

`finish()` prevents the user from returning to the splash screen using the Back button.

---

# 📁 Project Structure

```text
Practical6/
│
├── app/
│   └── src/
│       └── main/
│           ├── java/
│           │   └── .../
│           │       ├── MainActivity.kt
│           │       └── SplashActivity.kt
│           │
│           └── res/
│               ├── anim/
│               │   ├── scale.xml
│               │   ├── translate.xml
│               │   ├── rotate.xml
│               │   ├── alpha.xml
│               │   └── ...
│               │
│               ├── drawable/
│               │   ├── splash_background.xml
│               │   └── animation frames
│               │
│               ├── layout/
│               │   ├── activity_main.xml
│               │   └── activity_splash.xml
│               │
│               └── ...
│
└── README.md
```

---

# 🖥️ Application Flow

```text
        App Starts
            ↓
     SplashActivity
            ↓
    Splash Animation
            ↓
     Twin Animation
            ↓
    Animation Completed
            ↓
       MainActivity
            ↓
   Frame by Frame Animation
```

---

# 🧩 Main Components

### SplashActivity

Responsible for:

* Displaying the splash screen
* Showing the gradient background
* Performing twin animations
* Applying activity transition
* Opening `MainActivity`

### MainActivity

Responsible for:

* Displaying the main application UI
* Demonstrating Frame by Frame Animation
* Starting the `AnimationDrawable`

---

# 📱 Features Demonstrated

* ✅ Custom Splash Screen
* ✅ Radial Gradient Background
* ✅ Frame by Frame Animation
* ✅ Tween/Twin Animation
* ✅ Scale Animation
* ✅ Translate Animation
* ✅ Rotate Animation
* ✅ Alpha Animation
* ✅ Animation Set
* ✅ Animation Listener
* ✅ Activity Transition Animation
* ✅ Edge-to-Edge UI
* ✅ Immersive UI concepts
* ✅ AnimationDrawable
* ✅ AnimationUtils

---

# 🛠️ Technologies Used

* **Android Studio**
* **Kotlin**
* **XML**
* **Android SDK**
* **AnimationDrawable**
* **Android Animation Framework**

---

# ▶️ How to Run

1. Clone this repository.
2. Open the project in **Android Studio**.
3. Wait for Gradle synchronization to complete.
4. Connect an Android device or start an emulator.
5. Click **Run ▶**.
6. The `SplashActivity` will appear first.
7. After the splash animation, `MainActivity` will open.
8. The main screen demonstrates Frame by Frame Animation.

---

# 🎯 Learning Outcomes

After completing this practical, we understand:

1. How Frame by Frame Animation works in Android.
2. How to use `AnimationDrawable`.
3. How to create Tween/Twin animations.
4. How to use Scale, Translate, Rotate and Alpha animations.
5. How to combine animations using `<set>`.
6. How to create an animated Splash Screen.
7. How to create a radial gradient background.
8. How to use `AnimationUtils`.
9. How to use animation listeners.
10. How to perform animated Activity transitions.
11. How to display content edge-to-edge.
12. How to organize animation XML files inside the `res/anim` folder.

---

# 📌 Conclusion

This practical successfully demonstrates **Frame by Frame Animation** and **Twin Animation** in an Android application. A custom animated Splash Screen is created using a radial gradient background and multiple animation techniques. The application also demonstrates `AnimationDrawable`, animation XML resources, Activity transitions, and edge-to-edge content display.

---

## 🔗 GitHub Repository

**Practical 6 — Frame by Frame Animation and Splash Screen**

https://github.com/Maitripatel30/24012021043_Practical6

**👩‍💻 Author**

**Maitri Patel**
