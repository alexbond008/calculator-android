# Kotlin Compose Calculator

A simple yet functional calculator application built for Android using Kotlin and Jetpack Compose. This project demonstrates basic MVVM-like architecture principles and modern Android development practices.

## Features

*   **Basic Arithmetic Operations:** Addition, Subtraction, Multiplication, Division.
*   **Decimal Input:** Support for numbers with decimal points.
*   **Clear (AC):** Resets the entire calculation and display.
*   **Delete (Del):** Removes the last entered digit or operation.
*   **Responsive UI:** Adapts to different screen orientations.
*   **Clear Display:** Shows the current numbers and operation being entered.

## Screenshots

*(Placeholder: Add a screenshot or GIF of the app in action here. For example:)*
<!-- ![Calculator Screenshot](app/src/main/res/drawable/screenshot.png) -->
<!-- You can add a screenshot to a drawable folder and reference it like the example above -->

## Tech Stack & Architecture

*   **Language:** [Kotlin](https://kotlinlang.org/)
*   **UI Toolkit:** [Jetpack Compose](https://developer.android.com/jetpack/compose) for building a declarative UI.
*   **Architecture:** Follows an MVVM-like pattern:
    *   **ViewModel (`CalculatorViewModel.kt`):** Manages the calculator's state and business logic. It exposes state to the UI and handles user actions.
    *   **State (`CalculatorState.kt`):** A data class representing the current state of the calculator (e.g., `number1`, `number2`, `operation`).
    *   **Actions (`CalculatorAction.kt`):** A sealed class defining all possible user interactions (e.g., entering a number, selecting an operation, calculating).
    *   **Operations (`CalculatorOperation.kt`):** A sealed class representing the types of mathematical operations.
    *   **UI Components (`Calculator.kt`, `CalculatorButton.kt`):** Composable functions responsible for rendering the calculator's interface.
*   **Build System:** [Gradle](https://gradle.org/)

## Project Structure

The main components of the application are located in `app/src/main/java/com/example/calculator/`:

```
.
├── Calculator.kt         # Main Composable for the calculator UI layout
├── CalculatorAction.kt   # Sealed class for user actions
├── CalculatorButton.kt   # Composable for individual calculator buttons
├── CalculatorOperation.kt# Sealed class for mathematical operations
├── CalculatorState.kt    # Data class for the calculator's state
├── CalculatorViewModel.kt# ViewModel handling logic and state
├── MainActivity.kt       # Entry point of the Android application
└── ui/theme/             # Jetpack Compose theme files (Color.kt, Theme.kt, Type.kt)
```

## Getting Started

To get a local copy up and running, follow these simple steps:

### Prerequisites

*   Android Studio (latest stable version recommended, e.g., Hedgehog, Iguana or newer)
*   Kotlin configured with Android Studio
*   An Android Emulator or a physical Android device

### Installation & Running

1.  **Clone the repository:**
    ```sh
    git clone <your-repository-url> 
    ```
    *(Replace `<your-repository-url>` with the actual URL if you host this on GitHub, GitLab, etc.)*
2.  **Open the project in Android Studio:**
    *   In Android Studio, select "Open an Existing Project".
    *   Navigate to the cloned directory and select it.
3.  **Let Gradle sync:**
    Android Studio will automatically sync the project with Gradle. This might take a few minutes.
4.  **Run the application:**
    *   Select an emulator or connect a physical device.
    *   Click the "Run 'app'" button (green play icon) in Android Studio.

## How It Works

The calculator operates based on a unidirectional data flow principle:

1.  **User Interaction:** The user taps a button on the `Calculator` UI (defined in `Calculator.kt`).
2.  **Action Triggered:** The `onClick` lambda for the `CalculatorButton` calls the `onAction` function (which is a reference to `viewModel::onAction`) in the `CalculatorViewModel`, passing a specific `CalculatorAction` (e.g., `CalculatorAction.Number(5)`, `CalculatorAction.Operation(CalculatorOperation.Add)`).
3.  **ViewModel Logic:** The `CalculatorViewModel` receives the action. Its `onAction` method uses a `when` statement to determine the type of action and calls the appropriate private function (e.g., `enterNumber()`, `enterOperation()`, `performCalculation()`). These functions update the `state` property of the ViewModel.
4.  **State Update:** The `state` property in `CalculatorViewModel` is a `MutableState<CalculatorState>` (`mutableStateOf`). When its value (an instance of `CalculatorState`) is replaced with a new one (e.g., via `state = state.copy(...)`), Jetpack Compose is notified of the change.
5.  **UI Re-renders:** The `Calculator` composable function in `Calculator.kt` observes this `state`. When the state changes, Compose intelligently recomposes only the parts of the UI that depend on the changed state, ensuring the display (like the `Text` view showing numbers and operations) and button appearances are updated.

*   The `MAX_NUM_LENGTH` constant in `CalculatorViewModel` limits the length of numbers that can be entered.
*   The logic for handling decimal points, preventing multiple operations from being entered consecutively, and clearing/deleting input is all managed within the `CalculatorViewModel`.

---

This README provides a solid foundation. You can further enhance it with:
*   A "Contributing" section if you plan for others to contribute.
*   A "License" section (e.g., MIT, Apache 2.0).
*   More detailed explanations of complex logic if necessary.
