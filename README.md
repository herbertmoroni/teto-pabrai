# Overview

Teto Pabrai is a native Android application that helps value investors quickly evaluate whether a stock is trading below its fair entry price using Mohnish Pabrai's investment framework. 

The user enters a ticker symbol, the company's forward earnings per share two years out, and the current stock price. The app sends this data to GitHub Models (GPT-4o), which classifies the company type, suggests a conservative price-to-earnings multiple, generates a four-sentence investment thesis, and evaluates the company against an eight-criterion checklist. 

The app then calculates the Pabrai ceiling price (Fair Value × 0.80) and displays the complete analysis as a shareable result card.

The purpose of this project was to take my first steps into native Android development with Kotlin, learn how to structure a real mobile app with XML layouts and an Activity-based architecture, integrate a third-party AI API into a mobile interface, and practice handling asynchronous network calls cleanly. As a software engineer, I wanted to build something I would actually use rather than a generic tutorial project — this app maps directly to the manual workflow I follow when researching stocks for my personal investing.


[Software Demo Video](https://youtu.be/_6TxPvNJJP8)

# Development Environment

The app was developed in Android Studio Panda 4 (2025.3.4) on Windows. The target was the Android emulator running a Pixel 7 with API level 34 (Android 14). The minimum supported SDK is API 26 (Android 8.0), which covers the vast majority of devices in use today.

The project is written entirely in Kotlin using XML-based layouts (Empty Views Activity template), not Jetpack Compose. The networking layer uses OkHttp for HTTP requests and the org.json library for parsing the AI response. 

The GitHub Models API token is loaded from a `local.properties` file at build time and exposed to the code as a `BuildConfig` constant, keeping it out of version control.


# Useful Websites

* [Android Developers — Build Your First App](https://developer.android.com/training/basics/firstapp)
* [GitHub Models Marketplace](https://github.com/marketplace/models)
* [OkHttp Documentation](https://square.github.io/okhttp/)
* [Mohnish Pabrai investment framework](https://www.youtube.com/results?search_query=mohnish+pabrai+investment+framework)


# Future Work

* Integrate a real-time financial data API (such as Financial Modeling Prep or Alpha Vantage) so the user no longer needs to manually look up forward EPS and current price — this was the biggest limitation discovered during the sprint, since GitHub Models has no built-in web access
* Add local history so previously analyzed tickers can be revisited without spending another API call
* Polish the loading state with a spinner instead of just disabling the button


# AI Disclosure

I used AI to help translate a visual design prototype into Android XML layouts, since converting CSS-style designs to Android resources was new to me.

I asked for help structuring the OkHttp call and the JSON response parsing, since this was my first time working with HTTP libraries on Android. I also asked for help when my parser broke on AI responses that wrapped JSON in markdown code fences — the fix was a defensive function that extracts whatever sits between the first `{` and last `}` in the response.

The AI integration in the app itself uses GitHub Models (GPT-4o), and the prompt was designed iteratively to produce reliable structured JSON output for the analysis card. Working through the prompt engineering, JSON parsing edge cases, and markdown-fence stripping was a meaningful learning experience in working with LLM APIs in production code.

I can explain every line of the final code and justify the design decisions.

Since English is not my first language (Portuguese is my native language), I also used AI to proofread the README.
