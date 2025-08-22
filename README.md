// ...existing code...

# Chatify

Lightweight real-time chat application (React + Express + MongoDB + Socket.IO).

## Quick links
- Backend entry: [server/index.js](server/index.js) — starts the Express app and Socket.IO server.
- Frontend entry: [public/src/App.js](public/src/App.js).
- Frontend API routes: [public/src/utils/APIRoutes.js](public/src/utils/APIRoutes.js).

## Features
- User registration, login, avatar setup and logout ([`register`](server/controllers/userController.js), [`login`](server/controllers/userController.js), [`setAvatar`](server/controllers/userController.js), [`logOut`](server/controllers/userController.js))
- Real-time messaging via Socket.IO with online-user tracking ([server/index.js](server/index.js))
- Message persistence in MongoDB ([server/models/messageModel.js](server/models/messageModel.js)) and retrieval ([`getMessages`](server/controllers/messageController.js), [`addMessage`](server/controllers/messageController.js))
- React frontend with pages and components:
  - Pages: [public/src/pages/Login.jsx](public/src/pages/Login.jsx), [public/src/pages/Register.jsx](public/src/pages/Register.jsx), [public/src/pages/Chat.jsx](public/src/pages/Chat.jsx)
  - Components: [public/src/components/ChatContainer.jsx](public/src/components/ChatContainer.jsx), [public/src/components/ChatInput.jsx](public/src/components/ChatInput.jsx), [public/src/components/Contacts.jsx](public/src/components/Contacts.jsx), [public/src/components/SetAvatar.jsx](public/src/components/SetAvatar.jsx), [public/src/components/Logout.jsx](public/src/components/Logout.jsx), [public/src/components/Welcome.jsx](public/src/components/Welcome.jsx)

## Project layout
- server/
  - [index.js](server/index.js) — server bootstrap and Socket.IO logic
  - [controllers/userController.js](server/controllers/userController.js) — user auth and profile functions
  - [controllers/messageController.js](server/controllers/messageController.js) — message CRUD: [`getMessages`](server/controllers/messageController.js), [`addMessage`](server/controllers/messageController.js)
  - [models/userModel.js](server/models/userModel.js), [models/messageModel.js](server/models/messageModel.js)
  - [routes/auth.js](server/routes/auth.js), [routes/messages.js](server/routes/messages.js)
  - [.env.example](server/.env.example), [package.json](server/package.json)
- public/ (React app)
  - [src/App.js](public/src/App.js), [src/index.js](public/src/index.js), [src/index.css](public/src/index.css)
  - [src/utils/APIRoutes.js](public/src/utils/APIRoutes.js) — frontend endpoints like `loginRoute`, `registerRoute`, `sendMessageRoute`, `recieveMessageRoute`, `setAvatarRoute`
  - pages and components under [public/src/pages/](public/src/pages) and [public/src/components/](public/src/components)
  - [public/.env.example](public/.env.example), [public/package.json](public/package.json), [public/public/index.html](public/public/index.html)

## Environment
- Backend: copy `server/.env.example` → `server/.env` and set:
  - PORT (default in example: 5000)
  - MONGO_URL (MongoDB connection string)
- Frontend: copy `public/.env.example` → `public/.env` and set:
  - REACT_APP_LOCALHOST_KEY (localStorage key used by the app)

## Run locally

1. Start backend
   - cd server
   - npm install
   - npm start
   - Server file: [server/index.js](server/index.js)

2. Start frontend
   - cd public
   - npm install
   - npm start
   - Frontend entry: [public/src/App.js](public/src/App.js)

Frontend expects backend at http://localhost:5000 (see [public/src/utils/APIRoutes.js](public/src/utils/APIRoutes.js)).

## API endpoints (overview)
- Auth
  - POST /api/auth/register → handled by [`register`](server/controllers/userController.js) via [server/routes/auth.js](server/routes/auth.js)
  - POST /api/auth/login → handled by [`login`](server/controllers/userController.js)
  - GET /api/auth/allusers/:id → [`getAllUsers`](server/controllers/userController.js)
  - POST /api/auth/setavatar/:id → [`setAvatar`](server/controllers/userController.js)
  - GET /api/auth/logout/:id → [`logOut`](server/controllers/userController.js)
- Messages
  - POST /api/messages/addmsg → [`addMessage`](server/controllers/messageController.js) (stores message)
  - POST /api/messages/getmsg → [`getMessages`](server/controllers/messageController.js) (retrieves conversation)

Routes are mounted in [server/index.js](server/index.js) via:
- [server/routes/auth.js](server/routes/auth.js)
- [server/routes/messages.js](server/routes/messages.js)

## Storage
- MongoDB models:
  - [server/models/userModel.js](server/models/userModel.js) — Users collection
  - [server/models/messageModel.js](server/models/messageModel.js) — Messages collection

## Notes & tips
- Socket.IO online user tracking occurs in [server/index.js](server/index.js) using a global Map named `onlineUsers`.
- Frontend socket logic lives in [public/src/pages/Chat.jsx](public/src/pages/Chat.jsx) and messaging events are emitted/listened in [public/src/components/ChatContainer.jsx](public/src/components/ChatContainer.jsx).
- Avatar images are generated and encoded on the frontend by [public/src/components/SetAvatar.jsx](public/src/components/SetAvatar.jsx) (uses `@multiavatar/multiavatar`).

## Tests
- No tests included. See [public/package.json](public/package.json) and [server/package.json](server/package.json) for scripts.

## License
- Add a LICENSE file to the project root if needed.

## Useful files
- Root .gitignore: [.gitignore](.gitignore)
- Frontend README: [public/README.md](public/README.md)
- Public assets: [public/public/index.html](public/public/index.html) and