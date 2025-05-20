 step-by-step tutorial** for Dockerizing a **React app** (only build, no Nginx).

---

### ✅ 1. **React Project Structure (example)**

```
my-react-app/
├── public/
├── src/
├── package.json
├── package-lock.json
├── Dockerfile
```

---

### 🐳 2. **Create Dockerfile** in the root folder

```Dockerfile
# Step: Build the React app
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy rest of the app and build
COPY . .
RUN npm run build
```

---

### 🛠️ 3. **Build the Docker Image**

Open terminal in the root folder (where Dockerfile is located), then run:

```bash
docker build -t react-app-builder .
```

---

### 🔍 4. **Verify the build folder exists in the container**

```bash
docker run --rm -it react-app-builder ls /app/build
```

---

### 📦 5. **Extract the build folder to your local machine (optional)**

```bash
docker create --name temp-builder react-app-builder
docker cp temp-builder:/app/build ./build
docker rm temp-builder
```

Now you’ll have a local `build/` folder with your React production build.

---

### 🎯 Result

You now have a **Dockerized React build environment** – this container builds your app and exits. It’s useful for:

* CI/CD pipelines
* Custom deployment flows
* Manual serving (e.g., via Express, Nginx, S3, etc.)

Let me know if you want to **serve the build manually or using another server.**
