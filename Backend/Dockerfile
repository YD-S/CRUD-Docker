# Use the official Node.js 14 image as the base image
FROM node:latest

RUN apt-get update && apt-get install -y \
	curl git

# Set the working directory in the container
RUN git clone https://github.com/YD-S/CRUD.git /app

RUN cd /app

RUN git checkout backend

# Install dependencies
RUN npm install

# Expose the port on which the Express.js application will run
EXPOSE 3000

# Start the application
CMD ["npm", "run" ,"start"]
