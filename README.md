# OrthoNow Developer Assignment

**Loom Walkthrough Video:** [https://www.loom.com/share/10dfda5ffb40471f890fe4bfd359e0c3](https://www.loom.com/share/10dfda5ffb40471f890fe4bfd359e0c3)

*(Please watch this video for a detailed technical walkthrough of the implementation.)*

## Live Demo

**Project Deployed on Netlify:** [https://neon-kelpie-2c5df7.netlify.app/]

*The landing page is fully deployed and optimized for high-performance delivery via Netlify’s global CDN.*

---

## Task 01: GTM Event Schema

This task defines the tracking infrastructure to measure user engagement and funnel progression.

* **Core Approach**: I have designed custom events to track the 3-step booking funnel, enabling accurate drop-off analysis.
* **Key Events**:
* `booking_step_complete`: Tracks progress at each form step.
* `call_button_click` & `wa_chat_click`: Tracks high-intent engagement buttons.


* **Implementation**: The schema ensures that GA4 receives granular data (step number, specialty, location) for detailed Funnel Exploration reports.

## Task 02: Performance Audit

The landing page is optimized for speed and user experience.

* **Performance Score**: 100/100 (Tested via PageSpeed Insights).
* **Status**: Mobile-Optimized & Fast Loading.

## Task 03: Integration Design

### 1. Integration Architecture

I utilized **Make (formerly Integromat)** to orchestrate the lead data flow due to its robust visual workflow builder and API handling capabilities.

* **Workflow**: Landing Page Form Submission -> Webhook (Make) -> HubSpot CRM (Contact Search/Create/Update) -> Karix WhatsApp API (Immediate Notification) -> Google Ads API (Offline Conversion Tracking).

### 2. CRM Deduplication Strategy

HubSpot’s default deduplication relies on email addresses, which are frequently unavailable in our target demographic.

* **Solution**: I implemented a Search API check using the user's Phone Number as the unique identifier. The workflow queries HubSpot for an existing contact with that number; if found, it updates the record, preventing duplicate lead generation.

### 3. Failure & Monitoring

* **Fallback Strategy**: I utilized Error Handler modules in Make. If an API call fails, the system triggers an automated retry mechanism (3 attempts) and logs the error.
* **SLA Compliance**: To ensure WhatsApp messages are sent within the 2-minute SLA, I monitor the "Execution Time" in Make’s history logs. Any execution exceeding 60 seconds triggers an automated alert for manual investigation.
