---
title: "Multiple College Library Management System"
excerpt: "A Django-based web application to support library operations across multiple colleges. This system helps manage book inventory, track student book issues/returns, handle staff records, and manage relationships among students, colleges, and books through a relational database."
collection: portfolio
---
**Duration:** January 2021 – May 2021  
**Tech Stack:** Python · Django · MySQL · HTML/CSS · Bootstrap  

## Project Overview  

A Django-based web application to support library operations across multiple colleges. This system helps manage book inventory, track student book issues/returns, handle staff records, and manage relationships among students, colleges, and books through a relational database.

## Roles & Features  

- **User roles & authentication:**  
  - Admin, Employee, and Student roles  
  - Profile management, role-based access  

- **Book & Inventory Management:**  
  - CRUD operations for books (add, update, delete)  
  - Inventory tracking across multiple colleges  

- **Issue/Return Workflow:**  
  - Students can request, issue, or return books  
  - Admin/employee approval workflows  
  - Payment or fine capture for overdue books  

- **Student & College Entities:**  
  - Student registration and membership tied to a specific `college_id`  
  - Interlinked relationships between student, book, issue records, and staff  

- **Admin Dashboard & Utilities:**  
  - Approval dashboard for book requests  
  - Reports of issued books, pending requests, inventory distribution  


## Code Structure & Key Paths  

- **Project entry points:**  
  - `djangoProject1/settings.py`, `djangoProject1/urls.py`, `manage.py`  
- **Accounts module:**  
  - `accounts/models.py`  
  - `accounts/views.py`  
  - `accounts/urls.py`  
  - `accounts/migrations/`  
- **Library module:**  
  - `library/models.py`  
  - `library/views.py`  
  - `library/urls.py`  
  - `library/migrations/`  
- **Templates:**  
  - Stored in `templates/` (e.g. `add_book.html`, `request_book.html`, `return_book.html`, `admin_home.html`, `student_home.html`)  
- **Static assets:**  
  - Stored in `static/` (CSS, JS, images)  
- **Dependencies:**  
  - `requirements.txt`


## Demo / Access & Contact  

To view the full source code and live demo, please check the repository linked below or **contact me directly** for access:

**Repository:**  
[Multiple_college_lib_mgmt_sys on GitHub](https://github.com/prasadboi/Multiple_college_lib_mgmt_sys)
