# 🏏 Cricket Auction System

A full-stack web application for running live cricket player auctions. Organizers can set up tournaments, register teams, build player pools, and run a real-time auction room where teams bid for players within their budgets.

Built with **Next.js 16 (App Router)**, **React 19**, **MongoDB/Mongoose**, and **Tailwind CSS**.

---

## ✨ Features

- **Authentication** — JWT-based register/login/logout with access tokens and HTTP-only refresh-token cookies.
- **Tournament setup** — Create tournaments with budgets, min/max player counts, role-based pricing, and rules.
- **Team registration** — Register teams with owners and unique short codes.
- **Player pools** — Maintain a player roster (with profile images via Cloudinary) and map players to tournaments.
- **Live auction room** — Run the auction, place bids, and "hammer down" sales to the winning team.
- **Bid history** — Track every bid placed during an auction.
- **Organizer isolation** — Players, teams, and tournaments are scoped to the organizer who created them.

---

## 🛠 Tech Stack

| Layer        | Technology                                          |
| ------------ | --------------------------------------------------- |
| Framework    | Next.js 16 (App Router), React 19                   |
| Language     | TypeScript (UI) / JavaScript (API & models)         |
| Database     | MongoDB with Mongoose                                |
| Auth         | JWT (`jsonwebtoken`) + `bcryptjs`                    |
| State        | Zustand                                             |
| Styling      | Tailwind CSS v4                                      |
| Media        | Cloudinary (player image uploads)                   |
| HTTP / UX    | Axios, react-hot-toast, Framer Motion, lucide-react |

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18.18+ (or 20+)
- A MongoDB instance (local or Atlas)
- A Cloudinary account (for player image uploads)

### Installation

```bash
# Install dependencies
npm install

# Configure environment variables (see below)
cp .env.example .env.local

# Run the development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Environment Variables

Create a `.env.local` file in the project root:

```env
# Database
MONGODB_URI=your_mongodb_connection_string

# Auth
ACCESS_TOKEN_SECRET=your_access_token_secret
REFRESH_TOKEN_SECRET=your_refresh_token_secret

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

> Confirm exact variable names in `lib/db.js`, `lib/token.js`, and `lib/cloudinary.js`.

---

## 📜 Scripts

| Command         | Description                          |
| --------------- | ------------------------------------ |
| `npm run dev`   | Start the development server         |
| `npm run build` | Build the app for production         |
| `npm run start` | Run the production build             |
| `npm run lint`  | Lint the codebase with ESLint        |

---

## 📁 Project Structure

```
auction-system/
├── app/
│   ├── api/                # Route handlers (auth, tournaments, teams, players, auction)
│   │   ├── auth/           # register / login / logout
│   │   ├── tournaments/    # CRUD + roles dropdown
│   │   ├── teams/          # team management
│   │   ├── players/        # player roster
│   │   ├── tournament-players/  # player ↔ tournament mapping
│   │   ├── auction-room/   # live auction state
│   │   └── hammer-down/    # finalize a sale
│   ├── auction-room/       # live auction UI
│   ├── dashboard/          # organizer dashboard
│   ├── setup-tournament/   # tournament creation
│   ├── register-teams/     # team registration
│   ├── player-pools/       # player pool management
│   ├── host/               # host controls
│   ├── login/ signup/      # auth pages
│   ├── components/         # shared UI components
│   ├── hooks/ store/ lib/  # React hooks, Zustand stores, API helpers
│   └── page.tsx            # landing page
├── lib/                    # auth, db, token, cloudinary helpers
├── models/                 # Mongoose models
├── docs/                   # BRD, ERD, and API documentation
└── public/                 # static assets
```

### Data Models

- **User** — organizers who run auctions
- **Tournament** — auction event with budget, player limits, and role pricing
- **Team** — bidding teams (name, owner, unique short code)
- **Player** — player roster with profile image (unique per organizer by phone)
- **TournamentPlayer** — association mapping players to tournaments
- **BidHistory** — record of bids placed during auctions

---

## 📚 API Documentation

Full API reference — including endpoints, request/response shapes, and error codes — lives in [docs/BRD.md](docs/BRD.md).

### Authentication

All protected endpoints require an access token:

```
Authorization: Bearer <accessToken>
```

The refresh token is issued as an HTTP-only cookie on login/register and cleared on logout.

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes
4. Push and open a pull request

---

## 📄 License

Private project — all rights reserved.
