RouteMuse - Learning Resources & TODO List
This document provides targeted learning resources and a checklist for tracking progress.
I. Targeted Learning Resources
Flask

Official Flask Tutorial: Flask Tutorial - Good for core concepts.
Miguel Grinberg's Flask Mega-Tutorial (Parts for API): Flask Mega-Tutorial - Excellent, though comprehensive. Focus on API parts if not building traditional web pages.
Building RESTful APIs with Flask: Search for "Flask REST API tutorial" (e.g., PrettyPrinted on YouTube, or various blog posts).

React

Official React Tutorial: React Tutorial - The new docs are great.
Vite Documentation: Vite Getting Started
Tailwind CSS: Tailwind CSS Docs

Mapping Libraries (Choose one track)

Mapbox GL JS & react-map-gl:
react-map-gl Documentation: visgl.github.io/react-map-gl/
Mapbox GL JS Documentation (underlying library): docs.mapbox.com/mapbox-gl-js/api/
Mapbox Directions API Docs: docs.mapbox.com/api/navigation/directions/
Mapbox Geocoding API Docs: docs.mapbox.com/api/search/geocoding/
Mapbox Isochrone API (Might be useful for "places within X minutes"): docs.mapbox.com/api/navigation/isochrone/


Google Maps & google-maps-react:
google-maps-react (example usage): Search GitHub for examples, or simple NPM page. (Note: this is one of many community libraries, check activity). react-google-maps/api is another popular one.
Google Maps JavaScript API Docs: developers.google.com/maps/documentation/javascript/overview
Google Directions API: developers.google.com/maps/documentation/directions/overview
Google Geocoding API: developers.google.com/maps/documentation/geocoding/overview
Google Places API: developers.google.com/maps/documentation/places/web-service/overview



Weather API

OpenWeatherMap One Call API 3.0 Docs: openweathermap.org/api/one-call-3

Hugging Face Transformers

Pipelines Documentation: huggingface.co/docs/transformers/main_classes/pipelines - This is key for easy use.
Model Hub (for finding models): huggingface.co/models
Sentiment: nlptown/bert-base-multilingual-uncased-sentiment
Zero-Shot: facebook/bart-large-mnli



Celery & Redis with Flask

Celery Official Docs (First Steps with Celery): docs.celeryq.dev/en/stable/getting-started/first-steps-with-celery.html
Using Celery with Flask: docs.celeryq.dev/en/stable/getting-started/first-steps-with-celery.html#using-celery-with-flask
Search for "Flask Celery Redis tutorial" - many blog posts available.

Deployment

Vercel Docs: vercel.com/docs (for React frontend)
Heroku Dev Center (Python): devcenter.heroku.com/categories/python-support
Render Docs (Python): render.com/docs/deploy-flask

II. RouteMuse - Granular TODO List
(Corresponds to the Roadmap)
Phase 1: Foundations & Core Mapping (Weeks 1-4)
Week 1: Project Setup & Basic Backend/Frontend Communication

 Install Python, Node.js, Git
 Set up Python virtual environment
 Initialize Git repository
 Install Flask, Flask-CORS
 Create basic Flask app (app.py)
 Implement Flask /api/ping endpoint
 Create React project (Vite)
 Install Axios, Tailwind CSS for React
 Configure Tailwind CSS
 Create basic React App layout component
 Implement React frontend call to /api/ping & display response
 Create initial README.md

Week 2: Mapping API Integration - Displaying a Static Route

 Sign up for Mapping API (Mapbox/Google) & get API key
 Store API key securely (e.g., .env file)
 Backend: Install requests
 Backend: Create Flask endpoint /api/route (hardcoded coords initially)
 Backend: Implement Mapping API Directions call
 Backend: Parse route geometry (polyline) from API response
 Backend: Return route geometry
 Frontend: Install react-map-gl or chosen map library
 Frontend: Set up basic map component
 Frontend: Fetch route geometry from /api/route
 Frontend: Render polyline on map

Week 3: Dynamic Route Input & Weather API Basics

 Frontend: Create input fields for Start/Destination addresses
 Frontend: On submit, send addresses to backend /api/route
 Backend: Modify /api/route to accept addresses
 Backend: Implement Geocoding API call to convert addresses to coords
 Backend: Use geocoded coords for Directions API call
 Backend: Return route geometry AND total duration
 Sign up for OpenWeatherMap & get API key
 Store Weather API key securely
 Backend: Create test endpoint /api/weather_test (takes lat/lon)
 Backend: Implement OpenWeatherMap API call for current weather
 Backend: Return basic weather info
 Frontend: Test /api/weather_test with route midpoint & display

Week 4: Route Segmentation & Time-Adjusted Weather Display

 Backend: Logic to segment route into ~5-7 points
 Backend: For each segment point, calculate coordinates and ETA
 Backend: Create service get_weather_for_eta(lat, lon, eta_timestamp)
 Backend: get_weather_for_eta calls OpenWeatherMap hourly forecast for ETA
 Backend: /api/route calls get_weather_for_eta for each segment
 Backend: Bundle route, segments (coords, ETA, weather) in response
 Frontend: Parse enhanced /api/route response
 Frontend: Display weather icon & temp on map for each weather-enabled segment
 Frontend: Implement basic loading states for API calls

Phase 2: POI Integration & Basic AI (Weeks 5-8)
Week 5: Basic POI Fetching (Mapping API)

 Backend: Decide on MVP POI categories
 Backend: For selected points along route, call Mapping API's Places/Nearby Search
 Backend: Filter POIs by category, extract name, location, category
 Backend: Add fetched POI data to /api/route response (or a new POI endpoint)
 Frontend: Display POIs as markers on map
 Frontend: POI marker click shows popup with name/category

Week 6: Hugging Face Setup & First AI Model (Sentiment for POIs)

 Backend: Install transformers, torch/tensorflow
 Backend: Choose & download/cache sentiment model (e.g., nlptown/...)
 Backend: Create ai_services.py module
 Backend: Implement analyze_sentiment(text) function
 Backend: Determine POI text source for sentiment (API reviews, description, or demo text)
 Backend: Integrate analyze_sentiment into POI processing logic
 Backend: Store sentiment score/label with POI data
 Frontend: Visually indicate POI sentiment on map/popup

Week 7: Asynchronous Task Processing (Celery Introduction)

 Backend: Install Celery & Redis (and Python Redis client)
 Backend: Configure Celery with Flask app & Redis broker
 Backend: Define Celery task for fetching weather (single point)
 Backend: Define Celery task for fetching POIs (single location)
 Backend: Define Celery task for sentiment analysis (single POI)
 Backend: Refactor /api/route to dispatch Celery tasks
 Backend: Implement polling endpoint (e.g., /api/route_status/<task_id>)
 Frontend: Implement polling logic to fetch updates
 Frontend: Update map with data as Celery tasks complete
 Frontend: Add "processing..." indicators

Week 8: AI for POI Tagging (Keyword/Zero-Shot - Basic)

 Backend: Choose & download/cache keyword/zero-shot model
 Backend: Implement get_poi_tags(description_or_reviews, candidate_labels) in ai_services.py
 Backend: Define candidate labels for zero-shot (if using)
 Backend: Create Celery task for POI tagging
 Backend: Store tags with POI data
 Frontend: Display 1-2 top tags in POI popup
 Frontend: (Optional) Filter POIs by AI-generated tags

Phase 3: Refinement, User Experience & Deployment (Weeks 9-12)
Week 9: AI-Powered Suggestion Logic & UI for Suggestions

 Backend: Define criteria for a "good POI suggestion"
 Backend: Implement logic to identify 1-3 suggested POIs
 Backend: Add "suggested_pois" to API response
 Frontend: Highlight suggested POIs on map
 Frontend: Create "Route Suggestions" panel/section

Week 10: UI/UX Polish & Error Handling

 Frontend: Refine map interactions (zoom, popups)
 Frontend: Ensure consistent Tailwind CSS styling
 Frontend: Implement basic responsive design
 Frontend: Add clear visual feedback for actions & loading
 Frontend: Implement user-friendly error messages for API failures
 Backend: Implement robust error catching & logging
 Backend/Frontend: Handle edge cases (no route, API key issues)

Week 11: Testing & Final Touches

 Manual E2E testing: Various routes, browsers
 Backend: Write basic unit tests for critical services (pytest)
 Frontend: (Optional) Basic component tests
 Code cleanup: Remove unused code, add comments, format
 Basic performance check

Week 12: Deployment & Documentation

 Choose hosting platforms (Vercel, Heroku/Render/Railway)
 Configure production environment variables
 Prepare Procfile / gunicorn for Flask backend
 Deploy frontend to Vercel
 Deploy backend (+ Redis if needed) to Heroku/Render/Railway
 Test live application thoroughly
 Update GitHub README.md: Description, demo link, screenshots, tech stack, setup, AI/API info, limitations, future ideas.
 Prepare portfolio talking points/presentation.


This set of documents should give you a very clear, structured, and actionable path forward for building RouteMuse! Remember to be flexible; if one part takes longer, adjust the scope of a later part to stay within your timeline for the MVP.
