# Aurora Player - Spotify-Style Web Music App

A fully offline-capable, browser-based music player inspired by Spotify. Upload your MP3 files, create playlists, and enjoy seamless playback with customizable crossfade transitions—all running entirely in your browser with no external dependencies.

## Features

### 🎵 Core Music Playback
- **Play/Pause/Next/Previous** controls
- **Seek bar** with current time and duration display
- **Volume control** with Web Audio API integration
- **Persistent bottom player bar** that stays visible across all views
- **Queue system** with visual queue drawer
- **Auto-play next song** when current track ends

### 📤 Music Upload & Management
- **Multiple MP3 uploads** at once
- **Large file support** without crashing (handles files of any size)
- **Automatic metadata extraction** (title, artist, duration)
- **Upload progress** indicators
- **Library view** with album-style cards
- All songs stored locally in **IndexedDB** for offline access

### 📋 Playlists
- **Create custom playlists**
- **Add/remove songs** from playlists
- **Reorder tracks** with up/down buttons
- **Play directly** from playlists
- **JSON import/export** for sharing playlists
- All playlists stored locally in **IndexedDB**

### 🔄 Crossfade & Transitions
- **Adjustable crossfade duration** (0-10 seconds)
- **Smooth audio crossfade** using Web Audio API
- **UI animation speed control** (slow/normal/fast)
- Settings apply instantly across the app

### 📱 Offline Support
- **Full offline functionality** using Service Workers
- **IndexedDB storage** for audio files and metadata
- **Automatic online/offline detection**
- **Offline indicator** banner when disconnected
- All features work seamlessly offline

### 🎨 UI/UX
- **Dark theme** inspired by Spotify
- **Responsive design** for desktop and mobile
- **Smooth animations** and transitions
- **Clean, modern interface**

## Tech Stack

- **Frontend**: React + TypeScript + Vite
- **Styling**: Tailwind CSS
- **Audio**: HTML5 Audio API + Web Audio API (for crossfade)
- **Storage**: IndexedDB (for songs, playlists, queue state)
- **Offline**: Service Worker + Cache API

## Getting Started

### Running on Replit

1. **Fork or import** this repository into Replit
2. **Install dependencies**:
   ```bash
   npm install
   ```
3. **Start the development server**:
   ```bash
   npm run dev
   ```
4. Replit will automatically open the app in a new tab. If not, click the "Open in new tab" button in the preview pane.

### Running Locally

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd "Spotify Ish APP"
   ```
2. **Install dependencies**:
   ```bash
   npm install
   ```
3. **Start the development server**:
   ```bash
   npm run dev
   ```
4. Open your browser to `http://localhost:5173` (or the port shown in the terminal)

### Building for Production

```bash
npm run build
```

The built files will be in the `dist` directory. You can serve them with any static file server.

## How to Use

### Uploading Music

1. Click the **"Upload Songs"** button in the header (available on all views)
2. Select one or multiple MP3 files from your computer
3. The app will automatically:
   - Extract metadata (title, artist, duration)
   - Store the audio files in IndexedDB
   - Add them to your library
4. Uploaded songs appear in the **Library** view immediately
5. Songs are available **offline** after upload

### Playing Music

- **Click any song** in the Library or Playlists view to play it immediately
- Use the **bottom player bar** controls:
  - Play/Pause button
  - Previous/Next buttons
  - Seek bar to jump to any position
  - Volume slider (desktop only)
- Songs will **auto-play the next track** in the queue when finished

### Managing the Queue

1. **Add songs to queue**:
   - Click the **"Add to Queue"** button on any song card in the Library
   - Or click **"Queue"** button in the bottom player bar to open the queue drawer
2. **View queue**:
   - Click the **"Queue (X)"** button in the bottom player bar
   - The queue drawer slides in from the right
3. **Reorder queue**:
   - In the queue drawer, use the **↑** and **↓** buttons to move tracks up or down
4. **Remove from queue**:
   - Click the **✕** button next to any track in the queue drawer

### Creating Playlists

1. Go to the **Playlists** view (sidebar)
2. Click **"New Playlist"**
3. Enter a name when prompted
4. **Add tracks**:
   - Select your playlist from the list
   - Click **"Add from Library"**
   - Enter the track number (shown in Library view) to add
5. **Reorder tracks**:
   - Use **↑** and **↓** buttons next to each track
6. **Remove tracks**:
   - Click the **✕** button next to any track
7. **Delete playlist**:
   - Click **"Delete"** in the playlist header

### Sharing Playlists

#### Export a Playlist

1. Go to **Playlists** view
2. Select the playlist you want to share
3. Click **"Export selected as JSON"**
4. A `playlist.json` file will download containing:
   - Playlist metadata (name, timestamps)
   - Track information (title, artist, duration)
   - **Note**: Audio files are NOT included (to avoid copyright issues)

#### Import a Playlist

1. Go to **Playlists** view
2. Click **"Import playlist JSON"**
3. Select a `.json` file exported from this app
4. The playlist will be added to your list
5. **Important**: You'll need to upload your own audio files and manually add tracks to match the imported playlist

### Settings

Go to the **Settings** view to adjust:

- **Crossfade Duration**: Control how long the transition between songs lasts (0-10 seconds)
  - Set to 0 to disable crossfade
  - Higher values create longer, smoother transitions
- **UI Animation Speed**: Choose slow, normal, or fast for UI animations

Settings are saved automatically and apply instantly.

## Offline Mode

### How It Works

1. **Service Worker** caches the app shell (HTML, CSS, JS) on first visit
2. **IndexedDB** stores all uploaded music and playlists locally
3. When you go offline:
   - The app continues to work normally
   - An **offline indicator** banner appears at the top
   - All uploaded music remains accessible
   - Playlists and queue continue to function

### Offline Limitations

- You cannot upload new files while offline (requires file system access)
- The app must be visited at least once online to cache the service worker

### Clearing Offline Data

To clear all stored music and playlists:

1. Open browser DevTools (F12)
2. Go to **Application** tab → **Storage**
3. Click **"Clear site data"** or manually delete IndexedDB data

## Project Structure

```
src/
├── components/          # React components
│   ├── LibraryView.tsx  # Library/upload view
│   ├── PlaylistsView.tsx # Playlist management
│   ├── PlayerBar.tsx     # Bottom player controls
│   ├── QueueDrawer.tsx   # Queue management drawer
│   ├── SettingsView.tsx  # Settings UI
│   ├── Sidebar.tsx       # Navigation sidebar
│   ├── UploadDialog.tsx  # File upload modal
│   └── OfflineIndicator.tsx # Online/offline banner
├── context/
│   └── PlayerContext.tsx # Global player state & logic
├── services/
│   └── db.ts            # IndexedDB operations
├── types.ts             # TypeScript type definitions
├── App.tsx              # Main app component
└── main.tsx             # Entry point + service worker registration

public/
└── service-worker.js    # Service worker for offline support
```

## Browser Compatibility

- **Chrome/Edge**: Full support (recommended)
- **Firefox**: Full support
- **Safari**: Full support (iOS 11.3+)
- **Opera**: Full support

**Note**: Service Workers require HTTPS (or localhost) to work. Replit provides HTTPS automatically.

## Troubleshooting

### Songs won't play
- Check browser console for errors
- Ensure audio files are valid MP3 format
- Try refreshing the page

### Upload fails
- Check file size (very large files may take time)
- Ensure files are audio format (MP3, etc.)
- Check browser console for errors

### Offline mode not working
- Ensure you've visited the app at least once online
- Check that Service Worker is registered (DevTools → Application → Service Workers)
- Try clearing cache and reloading

### Playlist import fails
- Ensure JSON file is valid format exported from this app
- Check browser console for error messages

## Development

### Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint

### Adding Features

The codebase is modular and well-commented:
- **Player logic**: `src/context/PlayerContext.tsx`
- **Database operations**: `src/services/db.ts`
- **UI components**: `src/components/`

## License

This project is provided as-is for educational and personal use. Ensure you have rights to any music you upload.

## Credits

Built with:
- React
- Vite
- Tailwind CSS
- Web Audio API
- IndexedDB

---

**Enjoy your music! 🎵**
