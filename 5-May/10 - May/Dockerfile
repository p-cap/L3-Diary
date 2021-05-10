# We build from an official Node image from Docker
FROM node:10

# Create app directory
# This will create /app folder inside the image
# Everything from here will be copied to /app
WORKDIR /app

# create package.json
RUN npm init -y

# install express as dependency
RUN npm install express

# Create index.js
RUN touch index.js

# Add code inside index.js
RUN ["/bin/bash", "-c",  "echo -e \"const express = require('express');\nconst app = express();\napp.get('/', (req, res) => {\nres.send('Server is running');\n});\napp.listen(5000, () => {\nconsole.log('Server started at 5000');\n});\n\" > index.js"]

#Expose the port that our Node Express server will run
EXPOSE 5000

# running the server
# Define the runtime command
# This will execute when we run our docker image
CMD ["node", "index.js"]
