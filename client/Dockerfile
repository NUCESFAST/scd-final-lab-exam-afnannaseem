# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory
WORKDIR /1124_frontend

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Bundle app source inside Docker image
COPY . .

# Build the app
RUN npm run build

# Use serve to serve the app on port 1124
RUN npm install -g serve
CMD ["serve", "-s", "build", "-l", "1124"]
