# Spark (SmartClass)

A client-side classroom management app with face-recognition login, GPS-verified attendance, batch timetables, an intelligent class rescheduler, and a Gemini-powered chat assistant.

Built as a single-page app in vanilla HTML, CSS, and JavaScript — no backend required. All data is stored in the browser via `localStorage`.

## Features

### Authentication & security

- **Face recognition** — register and log in using [face-api.js](https://github.com/justadudewhohacks/face-api.js) (TensorFlow.js models)
- **Liveness detection** — blink, movement, and zoom checks to reduce photo/video spoofing
- **Location verification** — attendance only counts when the device is within a configurable radius of the classroom (Haversine distance)

### Student

- Dashboard with attendance stats, today's schedule, and activity feed
- Face + location attendance marking
- Weekly timetable (Mon–Fri) with live status (upcoming / ongoing / completed) and PDF export
- Profile management (photo, skills, interests, career goals)
- AI study suggestions based on profile
- Daily routine view

### Teacher

- Attendance session management
- **Class rescheduler** — define classes and subjects, mark absent teachers, auto-regenerate schedules with conflict resolution, export CSV
- **Timetable management** — create and edit batch timetables from the teacher dashboard

### Admin

- Add and remove students and teachers
- Create batches and assign students
- Build weekly timetables per batch (grid editor with time, subject, and room)

### AI assistant

- Floating Gemini chat widget for in-app help and content generation

## Tech stack

| Layer | Technology |
|-------|------------|
| UI | HTML5, CSS3, [Tailwind CSS](https://tailwindcss.com) (CDN) |
| Logic | Vanilla JavaScript (ES6+) |
| Face recognition | [face-api.js](https://github.com/justadudewhohacks/face-api.js) 0.22.2 |
| PDF export | [jsPDF](https://github.com/parallax/jsPDF) 2.5.1 |
| Icons | [Font Awesome](https://fontawesome.com) 6.4.0 |
| AI | Google Gemini (Generative AI SDK) |
| Storage | Browser `localStorage` |
| Hosting | [Vercel](https://vercel.com) (`vercel.json` SPA routing) |

## Project structure

```
sparkuuu/
├── index.html      # Entire application (UI, styles, and logic)
├── vercel.json     # SPA route fallback for deployment
└── README.md
```

## Getting started

### Prerequisites

- A modern browser (Chrome or Firefox recommended)
- Webcam access for face recognition
- Location services enabled for attendance
- Internet connection (CDN models and libraries load at runtime)

### Run locally

Clone the repo and serve the folder with any static file server:

```bash
git clone https://github.com/hemannt003/sparkuuu.git
cd sparkuuu
```

**Python**

```bash
python -m http.server 8000
```

**Node.js**

```bash
npx serve
```

Open [http://localhost:8000](http://localhost:8000) and allow camera and location permissions when prompted.

> **Note:** Some browsers restrict camera access on `file://` URLs. Use a local server.

### Deploy to Vercel

1. Import the GitHub repository in Vercel.
2. Vercel picks up `vercel.json` automatically — all routes serve `index.html`.
3. Deploy on push to your default branch.

## Usage

1. **Choose a role** — Student, Teacher, or Admin on the landing screen.
2. **Register** — enter a username, capture your face, and (for students) select a batch.
3. **Log in** — face match + liveness check; students also need to be within the classroom geofence for attendance.

### Mark attendance (student)

1. Open the **Attendance** tab.
2. Click **Mark Attendance with Face Recognition**.
3. Complete the liveness check (natural movement, 2+ blinks, ~6 seconds).
4. On success, face match and GPS verification run automatically.

### Reschedule classes (teacher)

1. Open **Rescheduler**.
2. Add classes, subjects, teachers, and period counts.
3. Mark absent teachers.
4. Click **Regenerate Schedule** and preview or export the result.

### Manage the system (admin)

1. Add users by email and type.
2. Create batches and assign students.
3. Select a batch and build its weekly timetable in the grid editor.

## Configuration

Edit values directly in `index.html`:

| Setting | Location | Default |
|---------|----------|---------|
| Classroom GPS | `CLASSROOM_LOCATION` in student dashboard init | `22.681432, 75.879018` |
| Attendance radius | `RADIUS_METERS` | `49` meters |
| Face match threshold | login/attendance handlers | Euclidean distance `< 0.6` |
| Gemini API key | `API_KEY` in `<head>` | Set your own key |

**Security note:** The Gemini API key is embedded in client-side code. For production, proxy requests through a backend or use environment-based injection at build time. Never commit real API keys to a public repository.

## Data storage

All persistence is local to the browser:

| Key | Contents |
|-----|----------|
| `userProfile` | Current user profile and preferences |
| `faceDescriptors` | Face recognition descriptors by username |
| `attendanceData` | Attendance history |
| `adminUsers` | Registered students and teachers |
| `adminBatches` | Batch membership |
| `batchTimetables` | Per-batch weekly schedules |
| `timetableData` | Student timetable cache |

Clearing site data or switching browsers resets all records. There is no server sync.

## Troubleshooting

| Issue | What to try |
|-------|-------------|
| Camera not working | Grant camera permission; use HTTPS or localhost |
| Face match fails | Improve lighting; center face 1–2 ft from camera |
| Location denied | Enable location for the site in browser settings |
| Models not loading | Check network; face-api models load from CDN on first use |
| Storage full | Clear old data — `localStorage` is typically limited to ~5–10 MB |

## Limitations

- Single-browser, single-device data — no multi-user server or sync
- Face descriptors and attendance live in `localStorage`, not a secure database
- GPS accuracy varies by device and environment
- Client-exposed API keys are visible to anyone who views the page source

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes
4. Open a pull request

## Author

**Hemanth** — [@hemannt003](https://github.com/hemannt003)

## Acknowledgments

- [face-api.js](https://github.com/justadudewhohacks/face-api.js) for face detection and recognition
- [Tailwind CSS](https://tailwindcss.com), [Font Awesome](https://fontawesome.com), [jsPDF](https://github.com/parallax/jsPDF)
- [Google Gemini](https://ai.google.dev/) for the chat assistant
