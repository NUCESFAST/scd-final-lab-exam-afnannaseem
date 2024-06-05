# Use Node.js base image
FROM node:14

# Set the working directory in the container
WORKDIR /1124_backend2

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the port the app runs on
EXPOSE 3125

# Command to run the app
CMD ["node", "index.js"]
