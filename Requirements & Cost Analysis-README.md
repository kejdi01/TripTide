RouteMuse - Requirements & Cost Analysis
This document outlines the necessary software, accounts, skills, and potential costs for the RouteMuse project.
I. Technical Requirements
Software & Tools

Programming Languages: Python (3.8+), JavaScript (ES6+).
Package Managers: pip (Python), npm or yarn (Node.js).
Version Control: Git.
Code Editor: VS Code (recommended, with Python & JavaScript extensions) or any preferred IDE.
Web Browser: Modern browser for testing (Chrome, Firefox).
Operating System: Windows, macOS, or Linux.

Accounts & API Keys

GitHub Account: For version control and showcasing.
Mapping API:
Mapbox Account: (Recommended)
Access Token for Directions API, Geocoding API, Static Tiles/Styles API, (Optionally) Places API.
Free tier is generous for development (e.g., 50,000 map loads, 100,000 directions requests per month typically).


OR Google Cloud Platform Account:
API Keys for Google Maps JavaScript API, Directions API, Geocoding API, Places API.
Requires enabling billing, but offers a monthly free credit (e.g., $200). Be careful with usage.




Weather API:
OpenWeatherMap Account:
API Key for One Call API (or other relevant forecast APIs).
Free tier typically allows 1,000 calls/day and 60 calls/minute for One Call API 3.0.




Hosting Platforms (for deployment):
Vercel Account: For frontend deployment (generous free tier).
Heroku Account: For backend & Redis (free tier available, but might have limitations like dyno sleeping).
OR Render Account: Alternative for backend & Redis (free tier for web services and Redis).
OR Railway Account: Another alternative (offers starter plan with some free usage credits).



Python Libraries (Main Ones)

Flask
Flask-CORS
requests
transformers
torch (or tensorflow if preferred for Hugging Face)
celery
redis (Python client for Redis)
python-dotenv (for managing environment variables)
gunicorn (for production deployment)

JavaScript Libraries (Main Ones)

react
react-dom
vite (as build tool)
tailwindcss
Mapping library:
react-map-gl (for Mapbox)
OR google-maps-react (for Google Maps)


axios (or use native fetch)
(Optional state management: zustand or valtio)

II. Knowledge Prerequisites (Assumed Proficiency)

Python: Intermediate (comfortable with functions, classes, modules, virtual environments, pip).
Flask: Basic to Intermediate (routing, request handling, basic templates or API responses, blueprints).
JavaScript: Intermediate (ES6+ syntax, DOM manipulation, asynchronous operations - promises, async/await).
React: Intermediate (components, props, state, hooks - useState, useEffect, useContext, basic forms, calling APIs).
HTML/CSS: Basic to Intermediate. Tailwind CSS experience is a plus but can be learned.
Git & GitHub: Basic (commit, push, pull, branching).
REST APIs: Understanding of how to consume and design basic RESTful APIs.
Command Line / Terminal: Comfortable navigating and running commands.
AI Concepts (Basic): Understanding what sentiment analysis and keyword extraction are. No need to train models, just use Hugging Face pipelines.

III. Cost Analysis (for MVP Portfolio Project)
The goal is to keep costs at $0 or very close to $0 for the MVP.
API Usage

Mapbox: Free tier is usually sufficient for development and a low-traffic demo.
Potential Cost: If you exceed free tier limits (unlikely for solo dev project).


Google Maps Platform: Free $200 monthly credit. Stay within this.
Potential Cost: If you exceed the $200 credit. Monitor usage closely in Google Cloud Console.


OpenWeatherMap: Free tier (1,000 calls/day for One Call API) should be enough.
Potential Cost: If you need more calls (unlikely for MVP).


Hugging Face Models: Free to download and use pre-trained models locally.
Potential Cost: None for inference on your own machine/deployment server. If using Hugging Face Inference API in production beyond free limits, that would be a cost.



Hosting

Vercel (Frontend): Generous free tier ("Hobby" plan) is perfect. Cost: $0.
Heroku (Backend + Redis):
Web Dyno (Flask app): Free tier sleeps after inactivity. For a portfolio piece, this is usually fine.
Redis: Heroku Data for Redis offers a free plan (e.g., 25MB). Sufficient for Celery broker/backend for MVP.
Cost: $0.


Render (Backend + Redis):
Web Service (Flask): Free instance available (can also sleep, shared CPU/RAM).
Redis: Free instance available (25MB).
Cost: $0.


Railway (Backend + Redis):
Offers a starter plan that includes some free usage hours/credits per month. Could cover a small Flask app + Redis.
Cost: Potentially $0 if usage stays within free credits.


Domain Name (Optional):
You can use the default *.vercel.app or *.herokuapp.com / *.onrender.com domains for free.
Custom Domain: ~$10-15/year if you want one (e.g., from Namecheap, Google Domains). Not essential for MVP.


Development Software:
VS Code, Python, Node, Git, etc., are all free. Cost: $0.



Total Estimated Cost for MVP: $0
(Assuming careful use of free tiers).
Strategies to Stay Within Free Tiers

Implement Caching: Cache API responses (especially mapping/POI data that doesn't change rapidly) to reduce calls.
Rate Limiting on Your End: If your app allows users to make many requests, consider adding some light rate limiting in your backend.
Lazy Loading/On-Demand Fetching: Only fetch detailed POI/weather when a user interacts or a route is finalized.
Efficient API Queries: Request only the data fields you need from external APIs.
Monitor Usage: Regularly check your API usage dashboards on Mapbox/Google Cloud/OpenWeatherMap.
During Development: Hardcode some responses or use mock data services to avoid hitting API limits while building UI components.

If the project were to scale to many users, then paid tiers for APIs and hosting would become necessary. But for a portfolio piece, $0 is a realistic target.
