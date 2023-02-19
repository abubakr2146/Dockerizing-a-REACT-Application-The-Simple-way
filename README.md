# Dockerizing-a-REACT-Application-The-Simple-way
You might have heard the term Docker many times on the internet. But alot of people just float over it instead of delving deeper.

For an easy definition:

Docker is a tool that helps software developers build, package, and run their applications in a way that makes them easy to move from one computer environment to another.

Think of it like a shipping container for software. Just as a shipping container can be loaded with goods, transported across oceans, and then unloaded at a different port, Docker can package up an application, move it between different computer environments, and then “unload” it in a way that makes it easy to run.

This is useful because it means that software developers can build applications on their own computers, package them up with all the necessary files and dependencies, and then easily move them to other computers for testing, deployment, or production.

In other words, Docker helps make the process of building and deploying software more efficient and streamlined.

Now let’s move on the techincal part. What parts in a REACT app do we need to focus on while containerizing our application.

In a React app the essentials are:

Package.json

The package.json file is a small but essential file that provides important information and configuration for a JavaScript-based project, including dependencies, scripts, and metadata.

Package-lock .json

The package-lock.json file is a small but crucial file that keeps track of the exact versions of all the dependencies installed in a Node.js project, along with their dependencies and sub-dependencies. It ensures that everyone working on the project is using the same versions of dependencies, which helps to prevent issues caused by version mismatches or conflicts.

src folder

The src folder is the main source directory that contains the source code for the application

public folder

The public folder is the top-level directory that contains static assets that are not processed by the Webpack bundler.

For this part I am assuming that you have Docker desktop already setup on your system.


Now what I want you to do is go into the directory of your REACT application and create a file by the name of “TestReactDockerfile”. This is the file in which we will write the code for creating a docker image from our application.

Now in this file you will write the following:

FROM node:lts-alpine AS react-frontend
WORKDIR /usr/local/app

CMD ["yarn", "yarn install && yarn start"]

COPY package.json yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn build
Basically what this snippet is doing is:

Fetching an image from Docker Hub with Node pre-installed
Changing the directory from root to “/usr/local/app”
Startup and installing dependencies
copying package.json,package-lock.json,src and public folder into the approriate locations.
Running the build command for your REACT app.
Now we have written the docker file but how will we create a docker image?

Well that is pretty simple with the “docker build -t myapp:latest .” command.You need to run this command in the same directory as the docker file.

And after this your docker image should have been created.


Now we just need to use the “docker run image id” command and your docker container will have started. You can open docker desktop and click on the port specified to access your React application.


Hopefully you found this to be helpful and it helped you gained an understanding of the power of Docker.
