---
title: "Dyslexia Farm: Educational Game for Spelling Disabilities"
date: 2023-02-28T10:00:00+03:00
draft: false
toc: true
images:
  - "https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/Dyslexic.png"
tags:
  - Educational Games
  - Dyslexia
  - JavaFX
  - SQL
  - Learning Disabilities
---

<img src="https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/Dyslexic.png" width=3000 height=500>

<br>

[Github Repo](https://github.com/Mohaddz/dyslexiaGame)
<img style="float: left;margin-right: 20px;" src="https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/github-mark-white.svg" width="30" height="30"/> 

## Project Overview

Dyslexia Farm is an educational game designed to help children with spelling disabilities, particularly dyslexia. The game provides an attractive and interactive platform for children to practice spelling and word recognition, aiming to improve their reading and writing skills.

### Key Features

- Two main games: Words Game and Spelling Game
- User-friendly interface designed for children
- Multilingual support (English and Arabic)
- Performance tracking and reporting
- Adjustable difficulty levels

## Technology Stack

- Frontend: JavaFX
- Backend: SQL (for data storage and retrieval)

## Project Structure

The project consists of several Java classes and FXML files, each serving a specific purpose in the game's functionality:

1. **DyslexiaFXMLController.java**: Controls the main game interface for the Words Game.

2. **EndScreenFXMLController.java**: Manages the end screen displayed after completing a game.

3. **LoginController.java**: Handles user authentication and login process.

4. **SpillingFXMLController.java**: Controls the Spelling Game interface and logic.

5. **mainMenuController.java**: Manages the main menu interface and navigation.

6. **reportsController.java**: Handles the display of user performance reports.

7. **rhymeWords.java**: Likely manages the word database or logic for rhyming words in the games.

8. **dyslexiaFXMain.java**: The main class that launches the application.

FXML Files (UI Layouts):
- SpillingFXML.fxml
- dyslexiaFXML.fxml
- endSreenFXML.fxml
- loginPage.fxml
- mainMenu.fxml
- reports.fxml

Resource Files:
- _ar.properties: Arabic language resources
- _en.properties: English language resources
- derby.properties: Database configuration

## Game Features

### 1. Login System

![Login Page](https://user-images.githubusercontent.com/93622996/228839584-99f8cdd7-d038-4ecd-ab8c-39f2f91dfc47.png)

The login page allows users to:
- Enter username and password
- Choose between English and Arabic languages
- Access the game upon successful authentication

### 2. Main Menu

![Main Menu](https://user-images.githubusercontent.com/93622996/228839927-86e31846-cd28-47c9-bf7b-4d69aad0bbbb.png)

The main menu provides access to:
- Words Game
- Spelling Game
- Performance Reports
- Exit option

### 3. Words Game

![Words Game](https://user-images.githubusercontent.com/93622996/228840080-c9d84c1d-1db1-4f2b-b69e-fd44991876be.png)

Features:
- Helps players differentiate between commonly mistaken words
- Child-friendly interface with background music
- Three difficulty levels for sound

### 4. Spelling Game

![Spelling Game](https://user-images.githubusercontent.com/93622996/228840161-c68f1e25-e827-4005-a4e2-91e7aee449a4.png)

Features:
- Focuses on letter sounds and spelling
- Three difficulty levels
- Real-time score tracking (points and misses)

### 5. Performance Reporting

![Report Page](https://user-images.githubusercontent.com/93622996/228840227-dcd6223f-5105-4d9b-9881-510b6c4b65d4.png)

- Retrieves and displays user performance data from the database
- Shows high scores for each game

## Database Structure

![Database Structure](https://user-images.githubusercontent.com/93622996/228840493-16fea405-adc8-4b25-a167-c1f3072a48e5.png)

The database table includes:
- User information (username, password)
- Game performance data (points, misses) for both games
- Date records for high scores

## Conclusion

Dyslexia Farm demonstrates an innovative approach to helping children with dyslexia and other spelling disabilities. By combining educational content with game-like interactions, it provides an engaging platform for learning and practice. The project's use of JavaFX for the frontend and SQL for data management showcases a well-rounded application of software development skills in creating an educational tool.