<div align="center">

# 📚 Vocab ZX

### A Premium Vocabulary & Spelling Learning Web Application

**Built with Django · HTMX · Alpine.js**

[![Python](https://img.shields.io/badge/Python-3.13-blue?style=flat-square&logo=python)](https://python.org)
[![Django](https://img.shields.io/badge/Django-4.2-green?style=flat-square&logo=django)](https://djangoproject.com)
[![HTMX](https://img.shields.io/badge/HTMX-1.9-orange?style=flat-square)](https://htmx.org)
[![Alpine.js](https://img.shields.io/badge/Alpine.js-3.13-teal?style=flat-square)](https://alpinejs.dev)
[![License](https://img.shields.io/badge/License-MIT-purple?style=flat-square)](LICENSE)

*A dark-mode-first, eye-safe spelling trainer with 4 interactive game modes, 326+ vocabulary words, and real-time audio pronunciation.*

</div>

---

## 📸 Features at a Glance

| Feature | Details |
|---------|---------|
| 🎯 MCQ Spelling | 40 questions/session · countdown timer · green/red glow feedback |
| ⌨️ Typing Spelling | Audio cues · real-time char feedback · WPM speed tracking |
| 📖 Learn Spelling | Flashcard lessons · pronunciation · searchable word library |
| 🧩 Spelling Recorrection | Scrambled letter blocks · drag-to-arrange gameplay |
| ⚙️ System Settings | Dark/Light mode · screen dimmer · timer adjust · CSV/JSON upload |
| 🏆 Leaderboard | Per-mode score tracking with username ranking |
| 🔊 Audio Pronunciation | Native Web Speech API (no external API needed) |
| 📂 Custom Vocab Import | Upload your own wordlist via `.csv` or `.json` |

---

## 🌙 Design Philosophy

Vocab ZX is built with **eye safety first**. The interface features:

- **Dark-mode by default** — deep slate palette reduces eye strain during extended study sessions
- **Eyestrain Dimmer Slider** — applies a transparency overlay on top of the screen, dimming beyond monitor limits
- **High-contrast glow states** — emerald green for correct answers, crimson red for incorrect
- **Glassmorphism UI** — frosted glass cards with smooth backdrop-filter blur effects
- **Premium typography** — Outfit + Space Grotesk from Google Fonts
- **Micro-animations** — fade-in reveals, card hover lifts, and smooth state transitions

---

## 🚀 Quick Start

### Prerequisites

- Python 3.13+
- Django 4.2+
- pip

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/vocab-zx.git
cd vocab-zx

# 2. (Optional but recommended) Create a virtual environment
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install django

# 4. Apply database migrations
python3 manage.py migrate

# 5. Seed the database with built-in vocabulary
python3 manage.py seed_vocab

# 6. (Optional) Import the APEUni advanced PTE vocabulary (326 words)
python3 import_apeuni.py

# 7. Create an admin superuser
python3 manage.py createsuperuser

# 8. Run the development server
python3 manage.py runserver
```

Then open your browser and visit **[http://127.0.0.1:8000/](http://127.0.0.1:8000/)**

### Docker Installation

You can also run the project entirely within Docker. This requires having Docker and Docker Compose installed.

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/vocab-zx.git
cd vocab-zx

# 2. Build and start the container
docker-compose up -d

# 3. Apply database migrations (runs inside container)
docker-compose exec web python manage.py migrate

# 4. Seed the database with built-in vocabulary
docker-compose exec web python manage.py seed_vocab

# 5. Create an admin superuser
docker-compose exec web python manage.py createsuperuser
```

Then open your browser and visit **[http://127.0.0.1:8000/](http://127.0.0.1:8000/)**

---

## 🗂️ Project Structure

```
vocab ZX/
│
├── manage.py                        # Django management entry point
├── import_apeuni.py                 # APEUni PTE advanced vocab importer
├── db.sqlite3                       # SQLite database
│
├── vocab_zx/                        # Django project configuration
│   ├── settings.py                  # App settings (INSTALLED_APPS, STATIC, etc.)
│   ├── urls.py                      # Root URL routing
│   └── wsgi.py                      # WSGI entry point
│
├── core/                            # Main application
│   ├── models.py                    # Word + UserScore models & distractor generator
│   ├── views.py                     # Game views, score endpoints, CSV/JSON parser
│   ├── urls.py                      # App URL routes
│   ├── admin.py                     # Django Admin registrations
│   ├── tests.py                     # 7 unit tests (models, API, file parsers)
│   │
│   ├── management/
│   │   └── commands/
│   │       └── seed_vocab.py        # Built-in seed command (65 curated words)
│   │
│   └── templates/core/
│       ├── base.html                # Global layout + Alpine store + settings modal
│       ├── home.html                # Dashboard with mode cards + leaderboard
│       ├── mcq.html                 # MCQ Spelling game
│       ├── typing.html              # Typing Spelling game
│       ├── learn.html               # Learn vocabulary browser
│       ├── recorrection.html        # Spelling Recorrection block game
│       └── partials/
│           └── leaderboard.html     # HTMX-rendered results + rankings partial
│
└── static/
    ├── css/
    │   └── style.css                # Custom CSS (dark/light themes, glassmorphism)
    └── js/
        ├── htmx.min.js              # HTMX 1.9.10
        └── alpine.min.js            # Alpine.js 3.13.5
```

---

## 🎮 Game Modes

### 🎯 MCQ Spelling
- Presents the **definition + example sentence** as cues
- Generates **4 choices** — the correct spelling plus 3 algorithmically generated misspellings (letter swaps, phonetic substitutions, duplications)
- **Countdown timer** (default 20s, adjustable from 5s to 60s in Settings)
- Colour-coded feedback: **green glow** = correct, **red glow** = incorrect
- Correct answer always revealed after selection
- Score + username saved and shown on leaderboard at completion

### ⌨️ Typing Spelling
- Word auto-pronounced via **Web Speech API** on load (no server audio processing)
- Repeat audio by clicking the speaker button
- **Real-time character feedback** as you type — green for correct letters, red for mismatches, grey for remaining
- Submit to check, then view the correct spelling and example sentence
- **WPM (Words Per Minute)** calculated from active typing time
- Final score + speed shown in the leaderboard

### 📖 Learn Spelling
- Browse all **326+ words** in a responsive card grid
- Each card shows: word, difficulty badge, definition, and example sentence
- Click **Listen** to hear the word spoken aloud via Web Speech API
- **Live search filter** — instantly narrows results as you type in the search box

### 🧩 Spelling Recorrection
- Presents definition and example cues
- Letters of the target word are **scrambled** into clickable blocks
- Click scrambled letters to place them in the arrangement area
- Click placed letters to return them to the pool
- **Reset** button to start arrangement over
- Green/red border feedback on the arrangement box after submission
- Word is spoken aloud on each answer reveal

---

## ⚙️ System Settings (Three-Dot Menu)

Click the **⋮** icon in the top-right header to open the Settings panel:

| Setting | Description |
|---------|-------------|
| **Dark / Light Mode** | Toggles full theme; preference saved to `localStorage` |
| **Screen Glare Dimmer** | 0–80% opacity overlay using CSS `mix-blend-mode: multiply` for safe screen dimming |
| **MCQ Timer Duration** | Slide between 5s and 60s per question |
| **Custom Vocabulary Upload** | Upload `.csv` or `.json` file — words added to the live database instantly |

### Custom Vocabulary File Format

**CSV:**
```csv
spelling,definition,example_sentence,difficulty,image_url
ephemeral,Lasting for a very short time,Beauty is ephemeral.,Hard,
```

**JSON:**
```json
[
  {
    "spelling": "ephemeral",
    "definition": "Lasting for a very short time.",
    "example_sentence": "Beauty is ephemeral.",
    "difficulty": "Hard"
  }
]
```

> Existing words are **updated** (not duplicated) when re-uploaded.

---

## 🗃️ Database Models

### `Word`
| Field | Type | Description |
|-------|------|-------------|
| `spelling` | `CharField` | The target word (unique) |
| `definition` | `TextField` | Meaning of the word |
| `example_sentence` | `TextField` | Usage in context |
| `image_url` | `URLField` | Optional image cue URL |
| `difficulty` | `CharField` | Easy / Medium / Hard |

### `UserScore`
| Field | Type | Description |
|-------|------|-------------|
| `username` | `CharField` | Player's chosen name |
| `score` | `IntegerField` | Number of correct answers |
| `total_questions` | `IntegerField` | Questions attempted |
| `game_mode` | `CharField` | MCQ Spelling / Typing Spelling / Spelling Recorrection |
| `wpm` | `FloatField` | Words per minute (Typing mode only) |
| `date_played` | `DateTimeField` | Auto-set timestamp |

---

## 📦 Vocabulary Sources

| Source | Words | Notes |
|--------|-------|-------|
| Built-in seed (`seed_vocab.py`) | 65 | Curated commonly misspelled English words |
| APEUni PTE Advanced Vocab | 261 | Real-world academic vocabulary from PTE reading Fill-in-the-Blank |
| **Total** | **326+** | Grows with custom uploads |

---

## 🧪 Running Tests

```bash
python3 manage.py test
```

**7 tests** covering:
- ✅ Word model creation and `__str__` representation
- ✅ Distractor generator uniqueness (3 unique, never equal to correct word)
- ✅ `get_choices()` returns exactly 4 options including correct answer
- ✅ MCQ score submission and database persistence
- ✅ Typing score submission with WPM storage
- ✅ CSV vocabulary file upload and parsing
- ✅ JSON vocabulary file upload and parsing

---

## 🔐 Django Admin

Access the admin panel to manage words and scores directly:

| | |
|--|--|
| **URL** | http://127.0.0.1:8000/admin/ |
| **Default username** | `admin` |

Create your superuser with:
```bash
python3 manage.py createsuperuser
```

Admin features:
- Browse and edit all vocabulary words
- Search words by spelling or definition
- Filter by difficulty (Easy / Medium / Hard)
- View all player score records with mode and date filters

---

## 🛠️ Tech Stack

| Technology | Version | Role |
|------------|---------|------|
| **Python** | 3.13 | Runtime |
| **Django** | 4.2 | Backend framework, ORM, templating |
| **HTMX** | 1.9.10 | Dynamic HTML responses (score submission, partial updates) |
| **Alpine.js** | 3.13.5 | Client-side reactivity (game state, settings store, timer) |
| **SQLite** | — | Default database (zero-config, swap to PostgreSQL for production) |
| **Web Speech API** | Native | Browser-native text-to-speech for pronunciation |
| **Google Fonts** | — | Outfit + Space Grotesk typography |
| **Vanilla CSS** | — | Full custom design system (no Tailwind, no Bootstrap) |

---

## 🌐 URL Routes

| URL | View | Description |
|-----|------|-------------|
| `/` | `home` | Dashboard with mode cards and leaderboard |
| `/mcq/` | `mcq_start` | MCQ game start |
| `/mcq/submit/` | `mcq_submit` | POST: save MCQ score, return leaderboard HTML |
| `/typing/` | `typing_start` | Typing game start |
| `/typing/submit/` | `typing_submit` | POST: save typing score + WPM |
| `/learn/` | `learn_home` | Vocabulary browser |
| `/recorrection/` | `recorrection_start` | Block arrangement game |
| `/recorrection/submit/` | `recorrection_submit` | POST: save recorrection score |
| `/upload-vocab/` | `upload_vocab` | POST: ingest CSV or JSON file |
| `/admin/` | Django Admin | Word and score management |

---

## 🎨 Customisation

### Changing the Colour Palette
Edit CSS variables in [`static/css/style.css`](static/css/style.css):

```css
:root {
    --color-primary: hsl(263, 85%, 62%);    /* Indigo/violet */
    --color-secondary: hsl(190, 90%, 50%);  /* Cyan */
    --color-success: hsl(142, 70%, 45%);    /* Emerald */
    --color-error: hsl(346, 84%, 60%);      /* Crimson */
}
```

### Swapping to PostgreSQL
In `vocab_zx/settings.py`:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'vocabzx',
        'USER': 'youruser',
        'PASSWORD': 'yourpassword',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 🙏 Acknowledgements

- [APEUni](https://www.apeuni.com/) — Advanced PTE vocabulary word list
- [HTMX](https://htmx.org/) — for making server-side HTML dynamic without heavy JavaScript
- [Alpine.js](https://alpinejs.dev/) — for lightweight reactive game state management
- [Django](https://www.djangoproject.com/) — the web framework for perfectionists with deadlines
- [Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API) — browser-native pronunciation without API costs

---

<div align="center">

Made with ❤️ for English learners everywhere

**[⬆ Back to Top](#-vocab-zx)**

</div>
