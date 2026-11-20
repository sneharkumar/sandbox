# End-to-End Web Analytics and Lead Capture Infrastructure
A functional portfolio sandbox featuring a clean front-end interface, an automated serverless spreadsheet database backend, 
and a verified event-tracking pipeline using Google Analytics 4 (GA4) and Google Tag Manager (GTM).

# Demo
Website URL: https://sneharkumar.github.io/sandbox/

# Tech Stack
- Front-end: Static HTML 5 / CSS3
- Tag management: GTM
- Analytics engine: GA4
- Backend database: Google Apps Script API + Google Sheets

# Measurement Plan and Implementation Strategy
(to avoid generic tracking limitations)

Objective 1: Asset Engagement 
KPI or Action: Clicks "Download Resume" > resume_download GA4 Event name > Click - All Elements GTM trigger type > click_id, page_location

Objective 2: Lead Generation
KPI or Action: Submits email address > form_submit GA4 Event name > Custom Event GTM trigger type > form_id


# Key Technical Challenges Overcome
1. The page-reload data loss: standard HTML form submissions on static hosts like GitHub Pages trigger aggressive page refreshes or error redirects. This completely clears the browser's active memory
   before GTM has enough time to bundle up and dispatch data packets.
2. Added an HTML event override ("onsubmit="return false;") directly into the form container tag. This safely gets the submission, keeping the page layout frozen and stable.
3. Because the page layout remains frozen during the submission, GTM has a window of stability to capture the button click and successfully send the data packets over to GA4 without any dropping.

# Verification Proof
1. Custom reporting was enabled inside the GA4 Admin panel.
2. Active conversion tracking, classified as key events.
3. Used GTM preview mode and GA4 DebugView to visually verify data packets arriving instantly with no delay.

Note: I originally mapped out a window.datalayer.push framework for the lead form. But, due to the static hosting constraints
of GitHub Pages, the async execution was conflicting with the browser session and dropping packets.
To stabilize the page layout I included "onsubmit=return false;" and tracked the click element instead. 
It taught me that data accuracy matters more than complex code.


