# Salah and Deen Case Study

## Project Summary

Salah and Deen is a React Native and Expo mobile app that brings several daily Islamic utilities into one place: prayer times, Qibla direction, Tasbih counter, Quran browsing, Islamic calendar, and settings.

The project focuses on reliability and practical mobile UX. The app should still be useful when the network is unreliable, when location access is denied, or when some device sensors are unavailable.

## Problem

Many utility apps depend heavily on live APIs or device capabilities. For a daily-use religious utility app, that can create a poor experience if:

- the network is slow
- location permission is denied
- the device compass is unavailable or inaccurate
- cached data is missing
- native APIs receive unexpected values

The goal was to build an app that handles those situations without crashing.

## What I Built

The app includes:

- prayer times with cached-first loading and Aladhan API refresh
- Qibla compass using the device magnetometer when available
- Tasbih counter for daily dhikr
- Islamic calendar with Hijri date formatting
- Quran browsing with remote fetch and local fallback data
- manual city selection with persisted location preferences
- local prayer reminder scheduling through Expo Notifications

## Architecture

```text
Screens
    -> reusable components
    -> services for APIs, sensors, location, and notifications
    -> storage utilities
    -> fallback data and formatting helpers
```

The app is organized around screens, services, constants, utilities, and shared theme state.

## Key Technical Decisions

### Cached-first prayer times

Prayer times are important daily data. Instead of showing a blank screen while waiting for the network, the app first tries to show cached timings, then refreshes from the API.

This makes the UX feel faster and more reliable.

### Defensive native integration

Mobile apps can crash when JavaScript values are passed incorrectly to native modules. One important fix was coercing coordinates to numeric values before passing them to location or sensor-related logic.

### Fallback behavior

The app includes fallbacks for cases where APIs, location, or device sensors are not available. This is important because a useful mobile app should degrade gracefully instead of failing silently.

### Expo for fast iteration

Expo made it easier to build and test the app quickly, especially for location, sensors, and notifications. The tradeoff is that some notification behavior needs a development build or standalone build for complete testing.

## Evidence

The project can be demonstrated through:

- home screen with prayer times and quick actions
- prayer-time screen and calculation-method modal
- Qibla compass screen
- Tasbih counter screen
- Quran browsing screen
- Islamic calendar screen
- settings screen with theme and notification controls

## Current Limitations

- Full Android notification behavior is better tested in a development build instead of Expo Go.
- Qibla accuracy depends on the physical device magnetometer.
- Some API-backed features require fallback handling when the network is unavailable.

## What I Learned

This project helped me understand that mobile reliability is not only about features. A good app must handle missing data, denied permissions, device differences, slow networks, and native module expectations. The app became stronger through defensive coding and fallback design.

