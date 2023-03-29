Task Collection

## Objective
Using JavaScript and Vue, your assignment is to implement a responsive task viewer component.

## Brief
Build out the project using the designs inside the `/design` folder as a guide. You can use any vue component framework to help you complete the challenge. 

## Tasks
Implement the assignment using:
  - language: JavaScript
  - framework: Vue / React
  - frontend state management: 
    - Vue: Pinia
    - React: coders choice
  - testing libraries: Jest / Mocha / Cyprus

## Expected Behaviour
- On initial load, make a call to the backend using the `GET /tasks` endpoint provided and display the response to the user
- Once the tasks have been loaded automatically trigger the `GET /tasks/:id` call for the first task
- On clicking a task in the task list trigger the `GET /tasks/:id` call to get the selected task
- Form display uses the supplied column sizing for different devices
- Form validation uses supplied field validation
- On submit button click trigger the `POST /tasks/:id` call and submit the form to the API
- When a task has been completed the user is no longer able to modify or resubmit the form
- The user can use the filter/search input provided to filter the list of tasks visible to them

## Extra Notes
- The design is not final you may alter the design as you see fit, to facilitate this you can add content to the mock responses from the backend
- Feel free to add to the list of behaviour requirements and add in any library usage that you feel could benefit the flow and design
- Comments on functionality and design decisions to help us understand your thought process would be a benefit

## Evaluation Criteria
- JavaScript/Vue best practices
- Show your work through commit history
- Demonstrate how to structure components in a small program
- Design and interpretation of mobile view and layout
- Completeness: Did you complete the features?
- Correctness: Does the functionality act in sensible, thought-out ways?
- Creativity: Did you go above and beyond the requirements?
- Maintainability: Is it written in a clean, maintainable way?
- Testing: Is the system adequately tested?

## Folder Structure
This project is broken down to 4 separate areas:
- frontend: where the coding challenge should be completed
- backend: serves as a fake server containing JSON files to simulate API interaction
- design: mockups of different forms
- assets: image assets and postman collection to test API

# Backend Setup
## Navigate to Backend Folder
```
cd ./backend
```

## Install NPM Packages
```
npm install
```

## Run Backend
```
node server
```

# Frontend Setup
## Navigate to Backend Folder
```
cd ./frontend
```

## Install NPM Packages
```
npm install
```

## Run Frontend
```
npm run serve
```
