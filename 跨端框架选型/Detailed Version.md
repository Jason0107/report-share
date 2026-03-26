# Circuit Mobile Technology Selection Report

## 1. Background

Circuit is an AI Q&A platform (RAG) that also supports multimodal capabilities.
 It currently has a Web App and now needs to further support both iOS and Android.

The focus of this evaluation is to assess the feasibility and cost-effectiveness of mobile solutions based on the existing Web capabilities, and to choose an appropriate implementation path for Circuit.

------

## 2. Overview of Mobile Technology Options

Mobile technology options can generally be divided into three categories: **Web App, Cross-Platform, and Native**.

### 2.1 Web App

A Web App is built directly with front-end web technologies, mainly HTML, CSS, and JavaScript.
 The same codebase is adapted for both desktop and mobile, and users access it through a browser, where the code runs.

### 2.2 Cross-Platform

Cross-platform means writing one primary codebase to cover both iOS and Android.
 It does not run directly in the browser. Instead, it relies on a cross-platform framework to map business logic and UI to mobile platform capabilities.

Common solutions include React Native, Flutter, Kotlin Multiplatform, and Ionic.

### 2.3 Native

Native development means building directly for each platform.
 iOS is mainly developed with Swift / Objective-C, while Android is mainly developed with Kotlin / Java.
 The code runs directly in the native operating system environment, with UI components, system capabilities, and performance scheduling all directly integrated with the platform itself.

------

## 3. Comparison of the Three Approaches

Since Circuit already has a Web App, the Web approach already provides a baseline capability.
 This evaluation therefore focuses mainly on comparing **Cross-Platform** and **Native**, while using Web App as a reference.

### 3.1 Comparison of the Three Mobile Approaches

| Dimension              | Web App | Cross-Platform App | Native App |
| ---------------------- | ------- | ------------------ | ---------- |
| Performance            | ★★☆☆☆   | ★★★★☆              | ★★★★★      |
| Development Efficiency | ★★★★★   | ★★★★☆              | ★★☆☆☆      |
| Cost                   | ★★★★★   | ★★★★☆              | ★★☆☆☆      |
| Talent Availability    | ★★★★★   | ★★★★☆              | ★★☆☆☆      |

### 3.2 Summary

Web App has clear advantages in development speed, low cost, and strong reuse of existing web capabilities, but it has the lowest ceiling in performance and system-level capabilities.
 Native offers the strongest performance, user experience, and system integration, but also comes with the highest development cost and usually requires maintaining separate iOS and Android implementations.
 Cross-platform sits between the two, offering a good balance across performance, efficiency, and cost.

Considering Circuit’s business characteristics, such as AI Q&A and multimodal upload/playback scenarios, the product does not have extremely high requirements for graphics performance. In most cases, **a cross-platform solution is sufficient to support the core business needs**.

------

## 4. Comparison of Cross-Platform Solutions

The current mainstream cross-platform options include **React Native, Flutter, Ionic, and Kotlin Multiplatform**.

Among them, the current app solution is based on **Ionic**,
 which means the app shell embeds a WebView that loads the Web App internally.

### 4.1 Overall Ranking

**React Native > Flutter > Ionic > Kotlin Multiplatform**

### 4.2 Solution Comparison

| Solution                 | Performance | Ecosystem | Hiring | Maintenance Cost |
| ------------------------ | ----------- | --------- | ------ | ---------------- |
| **React Native**         | ★★★★☆       | ★★★★★     | ★★★★★  | ★★★★☆            |
| **Flutter**              | ★★★★★       | ★★★★☆     | ★★★☆☆  | ★★★☆☆            |
| **Ionic**                | ★★☆☆☆       | ★★★☆☆     | ★★★★★  | ★★★★★            |
| **Kotlin Multiplatform** | ★★★★☆       | ★★☆☆☆     | ★★☆☆☆  | ★★☆☆☆            |

### 4.3 Brief Summary of Each Option

**React Native**
 The most balanced overall option. It performs well across performance, ecosystem, hiring, and long-term maintainability. It is also the most friendly to a front-end team, with relatively low migration cost.

**Flutter**
 Strong performance and high UI consistency, but it requires introducing Dart and the full Flutter technology stack. The team learning curve and hiring threshold are both higher than React Native.

**Ionic**
 The best option if the goal is to continue iterating on the current WebView-based wrapper with maximum reuse of existing web assets. However, it is still fundamentally a Web App running inside a WebView, so its ceiling for performance and native experience is the lowest.

**Kotlin Multiplatform**
 More suitable for native teams that want to share business logic. It is not a typical front-end cross-platform UI solution. Given the current team structure, the adoption threshold is relatively high and its short-term cost-effectiveness is not strong.

### 4.4 Summary

Given Circuit’s current team capabilities, existing web foundation, and future cost of supporting both platforms, **React Native is the most balanced cross-platform option at this stage**.
 Flutter is more suitable for teams willing to rebuild the technical stack and pursue stronger UI control.
 Ionic is more suitable for continuing with a low-cost short-term strategy.
 Kotlin Multiplatform is not recommended as the primary option for now.

------

## 5. Additional Notes on the Native Approach

If a Native route is chosen, **Swift** would mainly be used for iOS and **Kotlin** for Android.
 In practical implementation, if resources are limited, teams usually prioritize building the iOS side first and then evaluate the pace of Android investment.

The main advantage of Swift is that, even though cross-platform frameworks can get close to iOS style, there are still differences in default component systems, interaction details, and overall platform consistency.
 Swift makes it easier to achieve a fully native iOS experience.

Therefore, Native is better suited for handling the following capabilities:

- App shell
- Login and app launch flow
- Push notifications
- Audio recording and playback
- Image / video selection and upload
- Permission management
- Performance monitoring and crash handling
- System-level sharing, clipboard, file handling, and related capabilities

------

## 6. Recommended Direction

### 6.1 Recommended Main Path

**Recommended approach: hybrid development, cross-platform as the main path, with native as fallback support.**

That means:

- Main business pages and interactions are built with a cross-platform solution
- App shell and key system-level capabilities are handled natively
- Avoid continuing down a pure WebView-wrapper path as the long-term solution

### 6.2 Why This Approach

Looking at common practices of leading AI apps such as Doubao and Yuanbao, the mainstream industry approach is not a pure WebView route, but rather:

**retain native client capabilities + use native as fallback for critical flows + improve iteration efficiency at the business layer through cross-platform development**

For a product like Circuit, this approach usually delivers better cost-effectiveness because it is:

- faster than full Native
- better in experience than pure WebView
- lower cost than building two fully native apps
- more scalable in the long run than continuing to rely heavily on Ionic

### 6.3 Recommended Conclusion

**Primary recommendation: React Native with native capability fallback**

It is not recommended to continue treating Ionic / WebView as the long-term primary path.
 Native should be used as a supplement for the shell and key capabilities, rather than rebuilding the entire product as two fully native apps.

------

## 7. Final Conclusion

Taking into account the business scenario, existing technical foundation, development efficiency, cost, and long-term scalability, the most suitable approach for Circuit is:

**a hybrid development model with React Native as the main solution and native support as fallback.**

This approach provides a good balance among performance, user experience, development efficiency, and team feasibility, and is well suited to serve as the primary path for Circuit’s mobile development.