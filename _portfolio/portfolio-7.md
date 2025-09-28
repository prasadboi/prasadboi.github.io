---
title: "T-N-T"
excerpt: "Inventory Management Mobile app with scheduling, reminders, and to-do lists features"
collection: portfolio
---
**Timeline:** August 2020 - November 2020
**Tech Stack:** Android Studio, Java, Firebase (Authentication, Firestore)

**Description:**

The T-N-T mobile app was developed to assist users with inventory management, meeting scheduling, reminders, and to-do lists. The application leverages Firebase for authentication and data storage.

**Key Features:**

* **Inventory Management:** The app provides functionality to manage inventories, likely within specific categories such as "Kitchen Appliances," as suggested by the code.
* **Meeting Scheduling and Reminders:** Users can schedule meetings, set reminders, and receive notifications. The app uses the `AlarmManager` to trigger notifications.
* **To-Do List Creation:** Users can create and manage to-do lists with tasks, descriptions, dates, and times. This data is stored in Firebase.
* **User Authentication:** The app uses Firebase Authentication for user registration and login, including phone number verification and OTP verification.
* **Dashboard:** The `DashboardMainActivity` serves as the main screen, potentially displaying categories or other relevant information.
* **Email Verification:** The app includes functionality for email verification.

**Application Component Behavior:**

* **MainScreen:** This activity handles phone number input and redirects users to the registration screen.
* **Register:** This activity handles user registration, storing user data (username, email, phone, profession) in Firebase. It also sets up default categories.
* **PhoneVerification:** This activity handles phone number verification using Firebase.
* **verify\_otp:** This activity handles OTP verification.
* **DashboardMainActivity:** This activity likely displays the main dashboard with different categories.
* **ToDoListActivity:** This activity displays the user's to-do list.
* **Add\_events:** This activity allows users to add new events or tasks to their to-do list, including setting dates, times, and descriptions.  It also integrates with the `AlarmManager` to set reminders.
* **details:** This activity displays the details of a selected to-do list item.