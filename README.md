# Owlhead: Study Website

Owlhead is a colorful, multi-page study dashboard built with plain HTML, CSS and JavaScript. There are no frameworks and no build step. Open it in a browser and go.

Built by Ananya Jaiswal.

## Pages

The site flows like this: **Landing page → Home → Flashcards / Notes / Games / Resources**, and clicking the bus on Home rides over to the **Dashboard**.

### Landing page (`homepage.html`)
A "Welcome to Owlhead" screen with a typing animation that cycles through what you can do ("Make flashcards", "Write notes", "Play games", ...) and a **Start** button that opens Home.

### Home (`screen-1.html`)
- **Music player**: play/pause, previous/next, a clickable progress bar with timers, a playlist drawer, and a repeat button that cycles through *loop playlist*, *loop song* and *shuffle*
- **Quote of the Day**: click *New Quote* for a fresh quote and author
- **Study links**: Flashcards, Notes, Games and Additional Resources, each with its own hover animation
- **To-do list**: add, check off and delete tasks
- **Calculator**: `+ - × ÷`, decimals, clear
- **Animated background**: a scrolling city skyline and a clickable bus

### Dashboard (`screen-2.html`)
- **Calendar**: browse months, jump to a month with `mm/yyyy`, add events with a name and time range
- **Stopwatch**: start, stop and reset, down to hundredths of a second
- **Countdown timer**: click the timer icon, enter minutes (under 60), then press play
- **Digital clock**
- **Weather**: temperature in °C and °F plus a description for any city (defaults to Chicago)

### Flashcards (`flashcards.html`)
Create question/answer cards, click a card to reveal the answer, and delete cards one at a time or all at once. Includes a mini music player.

### Notes (`notes.html`)
- A **daily notebook** with a date picker. Today's note saves automatically as you type.
- **Three scratch boxes** that save automatically
- A mini music player and a floating UFO animation

### Additional Resources (`aditional.html`)
Pick a subject from the dropdown and get a list of study links (Khan Academy, CrashCourse, CK-12 and more).

## Project Structure

```
.
├── homepage.html / .css / .js     # Landing page and typing effect
├── screen-1.html / .css           # Home page
├── script1.js                     # Home: music player, to-do list, calculator, bus
├── playlist.js                    # Song list (defines allMusic)
├── quotes.js                      # Quotes and the generate() function
├── screen-2.html / .css / .js     # Dashboard: calendar, stopwatch, timer, clock, weather
├── flashcards.html / .css / .js   # Flashcards
├── notes.html / .css / .js        # Notes
├── aditional.html / .css / .js    # Additional resources finder
├── test.js                        # Loaded by Flashcards and Notes (mini player)
├── songs/                         # Audio files (.mp4)
├── images/                        # Cover art (.gif), one per song
├── images1/                       # Icons (search1, delete, waves, ufo)
└── bus.png, city1.png, light.png  # Background art
```

## Getting Started

1. Download or clone the project.
2. Open `homepage.html` in a modern browser.
3. To use the weather widget, add your own API key (see below).

An internet connection is needed for fonts, icons, jQuery, Moment.js and weather data.

### Weather API key

The weather widget uses [OpenWeatherMap](https://openweathermap.org/api). Create a free account, generate a key, and set `apiKey` near the bottom of `screen-2.js`.

> **Do not publish your key.** Anything in front-end JavaScript can be read by anyone who opens the page. If you push this project to a public repository, regenerate the key afterwards, and never reuse a key that was already shared.

## Customizing

- **Add songs**: add an entry to `allMusic` in `playlist.js` with a `name`, `artist` and `src`. The `src` must match `songs/<src>.mp4` and `images/<src>.gif`, and should use only letters, numbers and dashes (not starting with a digit).
- **Add quotes**: edit `quotes.js`.
- **Add study resources**: add a subject to the `resources` object in `aditional.js` (and a matching `<option>` in `aditional.html`).
- **Change the typing messages**: edit the `words` array in `homepage.js`.
- **Change colors**: edit the CSS variables at the top of `screen-1.css`.

## How data is saved

Everything is stored in your browser's `localStorage`. Nothing leaves your device, and clearing site data erases it.

| Key | Used for |
| --- | --- |
| `todos` | To-do list |
| `items` | Flashcards |
| `events` | Calendar events |
| `noteContent_<date>` | Daily notes |
| `textBoxContent1` to `3` | Notes scratch boxes |
| `objectMoved` | Remembers the bus moved when you switched pages |

## Built With

- HTML, CSS and JavaScript, jQuery, Moment.js
- Bootstrap (5.3.2 on Home and Dashboard, 4.3.1 on Notes)
- Material Icons and Font Awesome
- Google Fonts: Quicksand, Poppins, Shadows Into Light
- OpenWeatherMap for weather data

## Credits

<!-- Fill in the blanks below. Keep only the lines that apply. -->

**Code and tutorials**
- Calendar: adapted from an Open Source Coding tutorial (YouTube). *Confirm the exact video and license before sharing.*
- Stopwatch: *add source or "original"*
- Countdown timer: *add source or "original"*
- Weather widget: *add source or "original"*
- Music player: *add source or "original"*
- Landing page background animation (floating circles): *add source or "original"*
- Typing effect: *add source or "original"*

**Libraries and services**
- [Bootstrap](https://getbootstrap.com/), [jQuery](https://jquery.com/), [Moment.js](https://momentjs.com/), [Font Awesome](https://fontawesome.com/), [Material Icons](https://fonts.google.com/icons), [Google Fonts](https://fonts.google.com/), [OpenWeatherMap](https://openweathermap.org/)

**Art and media**
- Bus, city skyline, UFO, light and icon images: *add creator or "made by me"*
- Cover art (`images/`): *add creator*
- Songs (`songs/`): *add artists and licenses*

**Study resources linked on the Additional Resources page**
- Khan Academy, Wolfram Alpha, CrashCourse, CK-12, HHMI BioInteractive, Utah Genetics Learn, The Concord Consortium, Amoeba Sisters, Kurzgesagt and others

## Known Issues and To-Do

**Bugs**
- [ ] **Flashcards "Delete Cards" wipes everything.** It calls `localStorage.clear()`, which also deletes your to-do list, calendar events and notes. Use `localStorage.removeItem('items')` instead.
- [ ] **Notes: the Clear button doesn't exist.** `notes.js` looks for `#clear-button`, but `notes.html` has no such element, so the page logs an error. Add the button or remove that code.
- [ ] **Notes: past dates aren't saved.** You can type in an older day's note, but only today's note is saved, so the text is lost. Disable the textarea for other dates, or save them all.
- [ ] **Additional Resources is only partly filled in.** Physics, English, Government and Geography are in the dropdown but show "No resources found". Chemistry currently links to NASA and Khan Academy Science, and the History and Biology CrashCourse links point to the same page.
- [ ] Typo: "Amobea Sisters" should be "Amoeba Sisters".

**Security and cleanup**
- [ ] The weather API key is hard-coded in `screen-2.js`. Move it out before publishing.
- [ ] External links use `target="_blank"` without `rel="noopener noreferrer"`.
- [ ] The **Games** button links to `flashcards.html`. Point it to a real games page.
- [ ] Rename `aditional.html` and its files to `additional` (and update every link) if the spelling is a typo.
- [ ] `notes.html` is titled "Title" and the Dashboard has two `<title>` tags.
- [ ] `homepage.html` has content inside `<head>`, a nested `<body>`, and a script in the middle of the page.
- [ ] `screen-1.html` and `screen-2.html` are missing the `<html>` tag and have stray or nested tags.
- [ ] Calculator buttons need semicolons in `&times;` and `&divide;`.
- [ ] Load each page's own stylesheet after Bootstrap so Bootstrap doesn't override it.
- [ ] Use one Bootstrap version across all pages.
- [ ] The calculator uses `eval()`. That is fine for a personal project, but replace it if you ever accept input from others.
- [ ] `homepage.css`, `screen-2.css`, `flashcards.css`, `notes.css` and `aditional.css` may need the same responsive treatment as `screen-1.css`.

## License

Add a license here (for example MIT) if you plan to share the project.
