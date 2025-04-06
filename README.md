# DevSecOps Pipeline Implementation for Tic Tac Toe Game

![Screenshot 2025-03-04 at 7 16 48 PM](https://github.com/user-attachments/assets/7ed79f9c-9144-4870-accd-500085a15592)

![image](https://github.com/user-attachments/assets/5b2813a5-f493-4665-8964-77359b5be93a)

## Features

- 🎮 Fully functional Tic Tac Toe game
- 📊 Score tracking for X, O, and draws
- 📜 Game history with timestamps
- 🏆 Highlights winning combinations
- 🔄 Reset game and statistics
- 📱 Responsive design for all devices

## Technologies Used

- React 18
- TypeScript
- Tailwind CSS
- Lucide React for icons

## Project Structure

```
src/
├── components/
│   ├── Board.tsx       # Game board component
│   ├── Square.tsx      # Individual square component
│   ├── ScoreBoard.tsx  # Score tracking component
│   └── GameHistory.tsx # Game history component
├── utils/
│   └── gameLogic.ts    # Game logic utilities
├── App.tsx             # Main application component
└── main.tsx           # Entry point
```

## Game Logic

The game implements the following rules:

1. X goes first, followed by O
2. The first player to get 3 of their marks in a row (horizontally, vertically, or diagonally) wins
3. If all 9 squares are filled and no player has 3 marks in a row, the game is a draw
4. Winning combinations are highlighted
5. Game statistics are tracked and displayed

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/devsecops-demo.git
   cd devsecops-demo
   ```

2. Install dependencies:
   ```bash
   npm install
   # or
   yarn
   ```

3. Start the development server:
   ```bash
   npm run dev
   # or
   yarn dev
   ```

4. Open your browser and navigate to `http://localhost:5173`

## Building for Production

To create a production build:

```bash
npm run build
# or
yarn build
```

The build artifacts will be stored in the `dist/` directory.



Docker file
- Download dependency
- Build the image, this is done using npm command as instructed by the developer
- Copy the dist folder form the build into a webserver to seve the content
- Start the webserver, most likely nginx
   - FROM (statement to include a base image) if its multi stage then "as build"
   - WORKDIR (a folder in the docker image)
   - COPY (usually dependency file)
   - RUN (maybe the command to install the dependencies)
   - COPY (the entire application will be copied into docker image)
   - RUN (run the application)

   - FROM (include the webserver)
   - COPY (copy the built file in the dist folder into the nginx webserver folder... dont forget to specify that it is copying from the built stage)
   - EXPOSE (expose the port number)
   - CMD (command to start the nginx server)

Run docker build -t appname:vrsion
To run your application use - docker run -d -p 9099:80 appname:version


DEVSECOPS pipeline
Once a developer pushes to the repo, the github actions workflow is activated. 

Unit test
static code analysis
build 
docker -> build -> scan -> push to GHCR


CI/CD Pipeline Yaml file

name: (can provide any name)

on: (describes when it will be triggered)
   push: (when a push is made to the repo)
      branches: (which branch to trigger the action)
         - main
   pull_request: (when a pull request is made)2

jobs: (jobs to be executed)
   test:
      name: (name of the job)
      runs-on: ubuntu-latest 
      steps: (steps to be executed)
         - name: Checkout code
           uses: actions/checkout@v2
         - name: Install dependencies
           run: npm install
         - name: Run tests
           run: npm test
   static_code_analysis:
   build:
   docker_build:
   docker_scan:
   docker_push:
