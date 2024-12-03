# Dealership Review Website

A web application for customers to browse dealership branches by state and view or submit reviews for each branch. This project aims to increase transparency and build trust between customers and the dealership network.

---

## Table of Contents

- [About the Project](#about-the-project)
  - [Key Features](#key-features)
  - [Solution Architecture](#solution-architecture)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
  - [Installation](#installation)
- [Usage](#usage)
- [Development and Deployment](#development-and-deployment)

---

## About the Project

The **Dealership Review Website** is designed for a national car dealership to allow customers to:
- Access a central database of dealership reviews.
- View branch information filtered by state.
- Submit reviews for specific dealership branches.

This project leverages a hybrid cloud strategy, combining private and public cloud services for scalability and robustness.

### Key Features

- **User Management**: Authentication and account management using Django and React.
- **Dealer and Review Management**: Back-end services built with Node.js and MongoDB.
- **Sentiment Analysis**: IBM Code Engine for analyzing the sentiment of customer reviews.
- **Dynamic Pages**:
  - List all dealerships.
  - Display reviews for selected dealerships.
  - Allow customers to add reviews.
- **Continuous Integration/Deployment (CI/CD)**: Automated workflows with GitHub Actions.

### Solution Architecture

1. **Frontend**:
   - A React-based interface for user interaction.
   - Dynamic pages rendered using Django templates.

2. **Django Application**:
   - Manages user authentication and car model/make data (SQLite database).
   - Acts as a proxy for dealer and review services.

3. **Dealership and Reviews Service**:
   - An Express-based service (Node.js) with MongoDB for storing dealer and review data.
   - Runs in a Docker container.

4. **Sentiment Analysis Service**:
   - Deployed on IBM Code Engine.
   - Analyzes review sentiment (positive, negative, neutral).
  
![v2 capstone-dealership-architecture](https://github.com/user-attachments/assets/276086a1-6f32-42dd-b24f-db30d46ec656)

---

## Tech Stack

- **Frontend**: React, Django Templates
- **Backend**: Django, Node.js (Express)
- **Database**: SQLite, MongoDB
- **Containerization**: Docker
- **Cloud Services**: IBM Cloud Code Engine
- **CI/CD**: GitHub Actions
- **Deployment**: Kubernetes

---

## Getting Started

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/jakeleesh/xrwvm-fullstack_developer_capstone.git
   cd dealers
   ```

2. Set up Django environment:
   ```bash
   cd /xrwvm-fullstack_developer_capstone/server
   pip install virtualenv
   virtualenv djangoenv
   source djangoenv/bin/activate
   python3 -m pip install -U -r requirements.txt
   ```

3. Perform model migrations:
   ```bash
   python3 manage.py makemigrations
   python3 manage.py migrate
   python3 manage.py runserver
   ```

4. Build front end:
   ```bash
   cd /xrwvm-fullstack_developer_capstone/server/frontend
   npm install
   npm build
   ```

5. Build Docker app:
   ```bash
   cd /xrwvm-fullstack_developer_capstone/server/database
   docker build . -t nodeapp
   docker-compose up
   ```

---

## Usage

1. Navigate to `http://localhost:8000` to access the Django application.
2. Use the following API endpoints:
   - `get_cars/`: Retrieve a list of all car models and makes.
   - `get_dealers/`: Retrieve a list of all dealerships.
   - `get_dealers/:state`: Retrieve dealers filtered by state.
   - `dealer/:id/`: Retrieve details for a specific dealer by ID.
   - `review/dealer/:id/`: Retrieve reviews for a specific dealer by ID.
   - `add_review/`: Submit a new review for a dealer.
3. Interact with the sentiment analysis feature when submitting a review, which determines if the review sentiment is positive, negative, or neutral.

---

## Development and Deployment

### CI/CD

- GitHub Actions is used for:
  - Linting code to ensure adherence to best practices.
  - Running automated tests for reliability.
  - Managing deployment pipelines.

### Deployment

- The application is deployed on Kubernetes for scalability and container orchestration.
- Docker images for the `Dealership and Reviews Service` are pushed to a container registry for use in Kubernetes deployments.
