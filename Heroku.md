### Heroku

#### Deploy a React and Express app

Recently I want to deploy an React + Express.js app to Heroku. I thought it would be a breeze but turned out hitting some road blocks. One of the main issues is Heroku somehow doesn't work well with Yarn.

__STEPS__

- create an Express app using NPM
- create an React using `create-react-app client --typescript --use-npm`
- set up a proxy in the React app package.json `"proxy": "http://localhost:5000"`
- set up a script in the Express app package.json `"heroku-postbuild": "cd client && npm install && npm run build"`
- push your code to Heroku `git push heroku master`
