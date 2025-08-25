[![Releases](https://img.shields.io/github/v/release/savanbadani98/MERN-task-manager?label=Releases&color=2b9348)](https://github.com/savanbadani98/MERN-task-manager/releases)

# MERN Task Manager — Secure Task App with React, Node & Mongo

Build and run a simple task manager app built on the MERN stack. Manage tasks, sign in with JWT, and see a clean React UI. The app pairs a Node/Express API with MongoDB and a React front end. Use the link above to download the release asset and run it on your machine.

🚀 Live demo: open the Releases page to get the packaged build and server binary.  
(If you are on this page, download the release file and execute it per the steps in the Releases section below.)

---

![task-manager-hero](https://images.unsplash.com/photo-1515879218367-8466d910aaa4?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80)

Table of contents
- Features
- Tech stack
- Architecture
- Screenshots
- Install (local)
- Run (production bundle)
- Environment
- API overview
- Front end notes
- Auth and security
- Contributing
- Releases
- License
- FAQ
- Acknowledgements

Features
- User auth with JWT and bcryptjs for password hashing.
- Full CRUD for tasks: create, read, update, delete.
- Protected API routes with Express middleware.
- Global state with Redux and async flows via redux-thunk.
- React Hooks across the client.
- Form validation and client-side feedback via react-toastify.
- Tailwind CSS for utility-first styling and responsive UI.
- Axios for HTTP requests.
- MongoDB + Mongoose for data modeling.

Tech stack
- Front end: React, Redux, react-router-dom, react-toastify, Tailwind CSS.
- Back end: Node.js, Express.js, JWT, bcryptjs.
- Database: MongoDB with Mongoose.
- Tools: Axios, eslint (optional), nodemon (dev).

Architecture
- Client: React SPA. Routes: /, /auth, /dashboard, /tasks/:id.
- Server: REST API. Routes: /api/auth, /api/tasks, /api/users.
- Auth: JSON Web Tokens. The server issues a token on login. The client stores it in localStorage and sends it via Authorization header.
- State: Redux stores auth and tasks. Thunks fetch data and handle side effects.

Screenshots
- Login and register screens
![login-screen](https://images.unsplash.com/photo-1542744173-8e7e53415bb0?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80)
- Task list and filters
![tasks-screen](https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80)
- Mobile responsive layout
![mobile-screen](https://images.unsplash.com/photo-1519389950473-47ba0277781c?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=60)

Install (local development)
Follow these steps to run the app locally. You need Node.js (v16+) and MongoDB.

1. Clone the repo
```bash
git clone https://github.com/savanbadani98/MERN-task-manager.git
cd MERN-task-manager
```

2. Install dependencies for server and client
```bash
# server
cd server
npm install

# open a new terminal for client
cd ../client
npm install
```

3. Create a .env file in server
```text
# server/.env
PORT=5000
MONGO_URI=mongodb://localhost:27017/mern_task_manager
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRE=7d
```

4. Run server and client in parallel
```bash
# server
cd server
npm run dev

# client
cd client
npm start
```

The React app runs on http://localhost:3000. The server runs on http://localhost:5000.

Run (production bundle)
You can build the client and serve it with the server in production mode.

1. Build the client
```bash
cd client
npm run build
```

2. Start the server in production
```bash
cd ../server
npm run start
```

The server serves the static client build and the REST API.

Releases (download and execute)
Use the Releases page to get pre-built packages and executables.

- Visit the Releases link at the top or here:
  https://github.com/savanbadani98/MERN-task-manager/releases

- The Releases page contains packaged builds. Download the asset that matches your platform. After download, extract and execute the file. Example commands for a Linux tarball:
```bash
# example: adjust filename to what you downloaded
tar -xzf mern-task-manager-1.0.0-linux.tar.gz
cd mern-task-manager
./run-server.sh
```

On Windows you may get a zipped archive. Extract and run the provided .bat script or run the Node server using node:

```powershell
# if the release provides a node bundle
cd mern-task-manager
node server/index.js
```

If the Releases link fails or the file is missing, check the Releases tab on the GitHub repo for assets and instructions:
https://github.com/savanbadani98/MERN-task-manager/releases

Environment variables
Server (.env)
- PORT — port for the server.
- MONGO_URI — MongoDB connection string.
- JWT_SECRET — secret used to sign tokens.
- JWT_EXPIRE — token expiry (e.g., 7d).

Client (.env.local)
- REACT_APP_API_URL — API base URL (ex: http://localhost:5000/api).

API overview
Auth
- POST /api/auth/register
  - body: { name, email, password }
  - returns: token, user

- POST /api/auth/login
  - body: { email, password }
  - returns: token, user

Tasks (protected)
- GET /api/tasks
  - returns array of tasks for the user.

- POST /api/tasks
  - body: { title, description, status }
  - creates a task.

- GET /api/tasks/:id
  - returns single task.

- PUT /api/tasks/:id
  - body: changes, updates a task.

- DELETE /api/tasks/:id
  - removes a task.

Auth header: set Authorization: Bearer <token>.

Front end notes
- Redux slices: auth and tasks.
- Thunks handle async calls via axios.
- Token middleware attaches Authorization header for protected requests.
- Forms use controlled inputs and basic validation.
- Toasts display success and error messages.

Auth and security
- Passwords use bcryptjs for hashing.
- The server rejects unauthenticated requests to task routes.
- JWT tokens expire per JWT_EXPIRE.
- Use HTTPS in production and set secure cookies if you change storage strategy.
- Sanitize inputs on server. Use Mongoose validators and escape user text when rendering.

Testing
- Manual testing: use Postman or Insomnia to hit the API endpoints.
- Front end: run the app and test auth flows and CRUD operations.
- Add unit tests for reducers and API helpers in future work.

Contributing
- Fork the repo.
- Create a branch: git checkout -b feature/my-change
- Commit: git commit -m "feat: add ..."
- Push and open a pull request.

Guidelines
- Keep code style consistent.
- Use small commits.
- Add tests for new logic.
- Open issues for major changes or feature requests.

License
This project uses the MIT License. See LICENSE file.

FAQ
Q: Where does the data store live?
A: The app uses MongoDB. Use a local MongoDB instance or a hosted MongoDB Atlas URI.

Q: How do I reset the database?
A: Drop the mern_task_manager database in MongoDB or remove collections via a Mongo client.

Q: I see CORS errors. What to do?
A: Ensure the server enables CORS for the client origin. The server uses the cors middleware.

Q: Can I run the server and client in one container?
A: Yes. You can build the client and serve static files from Express. The repo includes a sample Dockerfile in examples/ (create one if missing).

Acknowledgements
- React and Redux for front-end primitives.
- Express and Mongoose for server and database.
- Tailwind CSS for styling utilities.
- img.shields.io for badges.

Contact
- Issues: open a GitHub issue on the repo.
- Pull requests: open a PR against main.

Release link (again)
[Download releases and run the packaged file](https://github.com/savanbadani98/MERN-task-manager/releases)