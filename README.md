# dockerazation-frontend

**step-by-step Dockerization tutorial for a React App**

---

## 🚀 Dockerize a React App – Step-by-Step Tutorial

### 📁 **Step 1: Create a React App**

Step 1: Install a build tool 
The first step is to install a build tool like vite, parcel, or rsbuild. These build tools provide features to package and run source code, provide a development server for local development and a build command to deploy your app to a production server.

Vite 
Vite is a build tool that aims to provide a faster and leaner development experience for modern web projects.

 
npm create vite@latest my-app -- --template react

Vite is opinionated and comes with sensible defaults out of the box. Vite has a rich ecosystem of plugins to support fast refresh, JSX,  Babel/SWC, and other common features. See Vite’s React plugin or React SWC plugin and React SSR example project to get started.

Vite is already being used as a build tool in one of our recommended frameworks: React Router.

Parcel 
Parcel combines a great out-of-the-box development experience with a scalable architecture that can take your project from just getting started to massive production applications.


npm install --save-dev parcel

Parcel supports fast refresh, JSX, TypeScript, Flow, and styling out of the box. See Parcel’s React recipe to get started.

Rsbuild 

Rsbuild is an Rspack-powered build tool that provides a seamless development experience for React applications. It comes with carefully tuned defaults and performance optimizations ready to use.


npx create-rsbuild --template react

Rsbuild includes built-in support for React features like fast refresh, JSX, TypeScript, and styling. See Rsbuild’s React guide to get started.

Note
Metro for React Native 
If you’re starting from scratch with React Native you’ll need to use Metro, the JavaScript bundler for React Native. Metro supports bundling for platforms like iOS and Android, but lacks many features when compared to the tools here. We recommend starting with Vite, Parcel, or Rsbuild unless your project requires React Native support.

---

### 🛠️ **Step 2: Create a Production Build**

```bash
npm run build
```

This generates a `build/` folder with optimized static files.

---

### 📄 **Step 3: Create Dockerfile**

In the root of your project, create a file named `Dockerfile`:

# Step: Build the React app
FROM node:18-alpine AS builder
WORKDIR /app

# Copy and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the code and build
COPY . .
RUN npm run build

# Optional: Define output if needed for CI/CD
# For example, to copy build artifacts to host, use:
# docker

---

### 📄 **Step 4: Create .dockerignore File**

```bash
touch .dockerignore
```

Add these lines:

```
node_modules
build
.dockerignore
Dockerfile
```

---

### 🧱 **Step 5: Build Docker Image**

```bash
docker build -t my-react-app .
```

---

### ▶️ **Step 6: Run Docker Container**

```bash
docker run -p 3000:80 my-react-app
```

Visit [http://localhost:3000](http://localhost:3000) in your browser 🚀

---

### 📦 Bonus: Docker Compose (Optional)

Create a `docker-compose.yml`:

```yaml
version: '3'
services:
  frontend:
    build: .
    ports:
      - '3000:80'
```

Run with:

```bash
docker-compose up --build
```

---

Let me know if you want a dev setup (with live reload), Nginx config customizations, or images for this tutorial!
