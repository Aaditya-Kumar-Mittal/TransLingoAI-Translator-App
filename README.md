# TransLingoAI Translator App

## Table of Contents

- [TransLingoAI Translator App](#translingoai-translator-app)
  - [Table of Contents](#table-of-contents)
  - [About](#about)
  - [Features](#features)
  - [Technologies Used](#technologies-used)
  - [Setup and Installation](#setup-and-installation)
  - [Project Phases](#project-phases)
    - [Phase 1: English to Hindi Translator](#phase-1-english-to-hindi-translator)
      - [**Implementation Code**](#implementation-code)
  - [How to Use](#how-to-use)
  - [License](#license)

## About

TransLingoAI is an AI-powered **English-Hindi Language Translator App** that converts **English to Hindi**, the official language of India. This can be used by **government organizations** and **official websites** for translations.

## Features

- AI-based **English to Hindi** translation
- Uses **Google ML Kit Translate API**
- Offline translation support
- Simple and intuitive UI

## Technologies Used

- **Kotlin** (Android Development)
- **Google ML Kit Translate API**
- **Android SDK**

## Setup and Installation

1. Clone this repository:

   ```sh
   git clone https://github.com/your-repo/TransLingoAI.git
   ```

2. Open the project in **Android Studio**.
3. Add the ML Kit dependency in `build.gradle`:

   ```gradle
   implementation("com.google.mlkit:translate:17.0.3")
   ```

4. Build and run the app on an **Android device or emulator**.

## Project Phases

### Phase 1: English to Hindi Translator

The first phase of the project focuses on implementing an **English to Hindi** translator using **Google ML Kit's Translation API**.

#### **Implementation Code**

```kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var englishHindiTranslator: Translator

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val inputText = findViewById<EditText>(R.id.inputText)
        val outputText = findViewById<TextView>(R.id.outputText)
        val translateButton = findViewById<Button>(R.id.translateButton)

        // Configure the translator (English to Hindi)
        val options = TranslatorOptions.Builder()
            .setSourceLanguage(TranslateLanguage.ENGLISH)
            .setTargetLanguage(TranslateLanguage.HINDI)
            .build()

        englishHindiTranslator = Translation.getClient(options)
        val conditions = DownloadConditions.Builder()
            .requireWifi()
            .build()

        englishHindiTranslator.downloadModelIfNeeded(conditions)
            .addOnSuccessListener {
                // Model downloaded successfully, enable translation button
                translateButton.setOnClickListener {
                    translateText(inputText.text.toString(), outputText)
                }
            }
            .addOnFailureListener { exception ->
                Log.e("Download Error", exception.toString())
                outputText.text = "Download Error!"
            }
    }

    private fun translateText(inputText: String, outputText: TextView) {
        englishHindiTranslator.translate(inputText)
            .addOnSuccessListener { translatedText ->
                outputText.text = translatedText
            }
            .addOnFailureListener { exception ->
                Log.e("Translation Error", exception.toString())
                outputText.text = "Translation Error!"
            }
    }

    override fun onDestroy() {
        super.onDestroy()
        englishHindiTranslator.close()
    }
}
```

## How to Use

1. **Open the App**
2. **Enter text in English** in the input field.
3. **Click the "Translate" button**.
4. **View the Hindi translation** in the output field.

## License

This project is licensed under the **MIT License**
