<p align="center">
  <img src="https://i.imgur.com/iKiDgs0.png" alt="Heroic Logo" />
  <br>
  <b>Habbo.com — optimized for retro development!</b>
</p>

<p align="center">
  <a href="https://www.youtube.com/watch?v=AbhmPUCEyMU" target="_blank">
    <img src="https://img.youtube.com/vi/AbhmPUCEyMU/maxresdefault.jpg" alt="Heroic Video Preview" width="700">
  </a>
  <br>
  <i>Click the image above to watch the preview on YouTube</i>
</p>

---

# Pre Requistes

Before setting up and running Heroic, ensure you have the following installed and configured:

- **Node.js** and **npm**
- **MySQL / MariaDB** (Compatible with Arcturus DB or Holo DB)
- **Gulp CLI** (Installed globally: `npm install -g gulp-cli`)
- **PM2** (For production use: `npm install -g pm2`)

---

# Local Use

Follow these steps to run Heroic locally for development:

### 1. Database Configuration
Ensure your MySQL server is running. Edit `config.json` in the project root:

```json
{
  "database": {
    "host": "127.0.0.1",
    "user": "root",
    "password": "your_password",
    "database": "arcturus"
  },
  "installation": {
    "completed": true
  }
}
```

### 2. Frontend Setup & Build
Install frontend dependencies and compile assets:

```bash
cd Website/Frontend
npm install
gulp build-complete
```

> **Tip:** While actively editing frontend files, run `gulp watch` to auto-rebuild on file changes.

### 3. Backend Setup & Run
Install backend dependencies and start the development server:

```bash
cd Website/Backend
npm install
npm start
```

The development server uses `nodemon` and `babel-node` to automatically restart on changes. Once launched, open `http://localhost` in your browser.

---

# Prod Use

For production environments, compile both frontend and backend distributions, then manage the Node process using **PM2** for high availability and automatic restarts.

### 1. Build Frontend
Compile and minify all client assets:

```bash
cd Website/Frontend
npm install
gulp build-complete
```

### 2. Build Backend
Compile ES6+ source code to the `dist` directory:

```bash
cd Website/Backend
npm install
npm run build
```

### 3. Process Management with PM2
Install PM2 globally if not already installed:

```bash
npm install -g pm2
```

Start the compiled backend server:

```bash
cd Website/Backend
pm2 start dist/boot.js --name "heroic"
```

#### Common PM2 Management Commands:
- **Status check:** `pm2 status`
- **View logs:** `pm2 logs heroic`
- **Restart service:** `pm2 restart heroic`
- **Stop service:** `pm2 stop heroic`
- **Save process list to restart on system reboot:**
  ```bash
  pm2 save
  pm2 startup
  ```
