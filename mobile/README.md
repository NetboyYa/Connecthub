# Mobile App README

A modern, feature-rich mobile application built with React Native and Expo, providing seamless real-time communication for communities, friends, gaming groups, and more.

## Tech Stack

- **Framework**: React Native with Expo
- **State Management**: Zustand
- **Networking**: Axios + Socket.io client
- **Real-time**: WebSocket for live updates
- **Storage**: AsyncStorage for local caching
- **Navigation**: React Navigation (Bottom Tabs, Stack)
- **UI Components**: React Native Paper / Custom components
- **Forms**: React Hook Form with validation
- **Testing**: Jest + React Native Testing Library

## Getting Started

### Prerequisites
- Node.js 16+
- npm or yarn
- Expo CLI: `npm install -g expo-cli`

### Installation

```bash
cd mobile
npm install
npm start
```

### Run on Devices

```bash
npm run ios      # iOS simulator
npm run android  # Android emulator
npm run web      # Web browser
```

## Available Scripts

```bash
npm start        # Start development server
npm run ios      # Run on iOS
npm run android  # Run on Android
npm run web      # Run on web
npm test         # Run tests
npm run lint     # Run linter
npm run format   # Format code
```

## Project Structure

```
mobile/
├── src/
│   ├── components/          # Reusable UI components
│   ├── screens/             # Screen components
│   ├── navigation/          # Navigation configuration
│   ├── services/            # API and Socket.io services
│   ├── store/               # Zustand store
│   ├── hooks/               # Custom React hooks
│   ├── utils/               # Helper functions
│   ├── constants/           # App constants
│   ├── types/               # TypeScript types
│   └── App.tsx              # Root component
├── assets/                  # Images, fonts, etc.
├── app.json                 # Expo configuration
├── package.json
└── README.md
```

## Bottom Navigation Tabs

1. **Home** - Main feed with recent servers/DMs
2. **Friends** - Friend list, requests, search
3. **Servers** - Browse and manage servers
4. **Notifications** - Unified notifications
5. **Profile** - User profile and settings

## Key Features

- ✅ Real-time messaging
- ✅ Voice and video calls
- ✅ Server and channel management
- ✅ Friend system with activity status
- ✅ Push notifications
- ✅ Dark mode support
- ✅ Message search and reactions
- ✅ File attachments
- ✅ User profiles and customization

## Environment Setup

Create `.env` file in mobile directory:

```env
REACT_APP_API_URL=https://api.connecthub.app/v1
REACT_APP_SOCKET_URL=https://socket.connecthub.app
REACT_APP_GOOGLE_CLIENT_ID=your_google_client_id
REACT_APP_APPLE_CLIENT_ID=your_apple_client_id
```

## Testing

```bash
npm test                    # Run all tests
npm test -- --watch        # Watch mode
npm test -- --coverage     # With coverage report
```

## Troubleshooting

### Metro bundler cache issues
```bash
npm start -- --reset-cache
```

### Dependency conflicts
```bash
rm -rf node_modules package-lock.json
npm install
```

### Emulator/simulator issues
- iOS: Try `npm run ios` or open in Xcode
- Android: Ensure emulator is running

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines.

## Learn More

- [React Native](https://reactnative.dev)
- [Expo](https://docs.expo.dev)
- [React Navigation](https://reactnavigation.org)
