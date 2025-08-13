# CopilotUI Flight Booking Application

**ALWAYS follow these instructions first and only fallback to additional search and context gathering if the information here is incomplete or found to be in error.**

CopilotUI is a simple, responsive HTML5/CSS3/JavaScript web application that provides a flight booking interface. The entire application is contained in a single `index.html` file with embedded styles and scripts.

## Working Effectively

### Quick Start (Essential Commands)
```bash
# Serve the application (choose one method):
cd /home/runner/work/CopilotUI/CopilotUI
python3 -m http.server 8000              # Method 1: Python HTTP server
# OR
npm install -g live-server && live-server --port=8080 --host=localhost --no-browser  # Method 2: Live-server with auto-reload
```

### Development Setup
- **Install development tools**: `npm install -g live-server htmlhint jshint prettier eslint` (takes 60-90 seconds total)
- **Serve application**: Choose Python HTTP server (instant) or live-server (auto-reload, ~2-3 second startup)
- **Access application**: `http://localhost:8000` (Python) or `http://localhost:8080` (live-server)

### Code Validation (ALWAYS run before committing)
```bash
cd /home/runner/work/CopilotUI/CopilotUI

# HTML validation - takes ~11ms, NEVER CANCEL
htmlhint index.html

# JavaScript validation - takes ~100ms, NEVER CANCEL  
echo '{"esversion": 6, "browser": true, "devel": true}' > .jshintrc
jshint --extract=always index.html
rm .jshintrc  # Clean up temporary config

# Code formatting check - takes ~170ms, NEVER CANCEL
prettier --check index.html

# Format code (optional) - takes ~170ms, NEVER CANCEL
prettier --write index.html
```

### Manual Validation Scenarios (REQUIRED after changes)
**ALWAYS test these scenarios after making any changes:**

1. **Server startup validation**:
   ```bash
   # Start server and verify response
   python3 -m http.server 8000 &
   SERVER_PID=$!
   sleep 2
   curl -I http://localhost:8000  # Should return HTTP/1.0 200 OK
   kill $SERVER_PID
   ```

2. **Application functionality validation**:
   ```bash
   # Verify HTML content loads correctly  
   curl -s http://localhost:8000 | grep -q "Discover your next flight"
   
   # Verify JavaScript functions are present
   curl -s http://localhost:8000 | grep -q "function searchFlights"
   curl -s http://localhost:8000 | grep -q "function swapLocations"
   
   # Verify form validation exists
   curl -s http://localhost:8000 | grep -q "Please enter both departure and destination"
   ```

3. **Complete user workflow validation**:
   - Load application in browser: `http://localhost:8000`
   - Verify flight booking form displays correctly
   - Test trip type radio buttons (Round-trip, One-way, Multi-city)
   - Test class selection dropdown (Economy, Premium Economy, Business, First Class)
   - Test direct flights checkbox
   - Enter departure location (e.g., "New York")
   - Enter destination location (e.g., "Los Angeles")  
   - Click swap button (⇄) to verify locations swap
   - Click "Search" button to verify form validation works
   - Verify alert shows flight search details

## Timing Expectations

**NEVER CANCEL any of these operations:**
- **Server startup**: 2-3 seconds for live-server, instant for Python HTTP server
- **HTML validation**: ~11ms (instant)
- **JavaScript validation**: ~100ms (instant)
- **Code formatting**: ~170ms (instant)
- **Application loading**: ~16ms response time (instant)
- **Tool installation**: 60-90 seconds total for all development tools

## Repository Structure

```
CopilotUI/
├── README.md           # Brief project description
├── index.html          # Complete application (HTML + CSS + JavaScript)
└── .github/
    └── copilot-instructions.md  # This file
```

## Common Tasks

### Adding New Features
1. **ALWAYS** start the development server first
2. **ALWAYS** validate existing functionality works before making changes
3. Edit `index.html` directly - all code is in this single file
4. **ALWAYS** test in browser after changes
5. **ALWAYS** run validation commands before committing

### Debugging Issues
1. Check browser console for JavaScript errors: F12 → Console tab
2. Verify server is running: `curl -I http://localhost:8000`
3. Validate HTML structure: `htmlhint index.html`
4. Validate JavaScript syntax: `jshint --extract=always index.html`

### Key Code Locations in index.html
- **CSS styles**: Lines 7-267 (embedded in `<style>` tag)
- **HTML structure**: Lines 270-343 (flight booking form)
- **JavaScript functions**: Lines 345-386 (embedded in `<script>` tag)
  - `swapLocations()`: Lines 346-352 (swaps departure/destination)
  - `searchFlights()`: Lines 355-377 (validates and processes search)
  - Event listeners: Lines 380-386 (trip type change handlers)

## Technology Stack
- **Frontend**: HTML5, CSS3 (with Flexbox/Grid), Vanilla JavaScript (ES6)
- **Styling**: CSS Grid, Flexbox, CSS custom properties, responsive design
- **No build tools**: Direct editing, no compilation required
- **No frameworks**: Pure vanilla JavaScript, no dependencies
- **No testing framework**: Manual validation only

## Development Best Practices
- **ALWAYS** test changes in browser before committing
- **ALWAYS** run HTML and JavaScript validation before committing  
- **NEVER** remove the responsive design CSS classes
- **ALWAYS** maintain accessibility attributes (labels, proper form structure)
- **ALWAYS** test on both desktop and mobile viewports
- **NEVER** add external dependencies without strong justification

## Troubleshooting

### Server won't start
- Check if port is in use: `lsof -i :8000` or `lsof -i :8080`
- Try different port: `python3 -m http.server 8001`

### JavaScript errors  
- Check syntax: `jshint --extract=always index.html`
- Check browser console for runtime errors
- Verify ES6 features are supported in target browsers

### Styling issues
- Verify CSS syntax is valid
- Check responsive design with browser dev tools (F12 → Device toolbar)
- Test on mobile viewport: 768px and below

### Form not working
- Verify all required form elements have correct IDs
- Check JavaScript event handlers are attached
- Verify form validation logic in `searchFlights()` function

Remember: This is a simple static web application. No build process, no package management, no server-side code. Focus on HTML/CSS/JavaScript fundamentals and browser compatibility.