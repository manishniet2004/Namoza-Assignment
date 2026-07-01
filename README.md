# Namoza Developer Assignment

## Project Overview
This repository contains the solution for the Namoza Developer Assignment for **OrthoNow**. The project focuses on high-performance landing page development, event tracking using Google Tag Manager (GTM), and automated CRM integration.

## Deliverables
- **Task 01:** [GTM Event Schema](./Task1.md)
- **Task 02:** [Landing Page](./index.html)
- **Task 03:** [Integration Design](#task-03-integration-design)

---

## Task 01: GTM Event Schema
This task defines the tracking infrastructure to measure user engagement and funnel progression.
* **Core Approach:** I have designed custom events to track the 3-step booking funnel, enabling accurate drop-off analysis.
* **Key Events:** 
    * `booking_step_complete`: Tracks progress at each form step.
    * `call_button_click` & `wa_chat_click`: Tracks high-intent engagement buttons.
* **Implementation:** The schema ensures that GA4 receives granular data (step number, specialty, location) for detailed Funnel Exploration reports.

---

## Task 02: Performance Audit
The landing page is optimized for speed and user experience.
* **Performance Score:** 100/100 (Tested via PageSpeed Insights)
* **Status:** Mobile-Optimized & Fast Loading
![PageSpeed Score](./images/pagespeed-score.png)

---

## Task 03: Integration Design

### 1. Integration Architecture
I would use **Make (formerly Integromat)** to orchestrate the lead data flow due to its robust visual workflow builder and API handling capabilities.
* **Workflow:** Landing Page Form Submission -> Webhook (Make) -> HubSpot CRM (Contact Search/Create/Update) -> Karix WhatsApp API (Immediate Notification) -> Google Ads API (Offline Conversion Tracking).

### 2. CRM Deduplication Strategy
HubSpot’s default deduplication relies on email addresses, which are frequently unavailable in our target demographic.
* **Solution:** I will implement a **Search API check** using the user's **Phone Number** as the unique identifier. The workflow will first query HubSpot for an existing contact with that number. If found, it updates the record; otherwise, it creates a new entry, preventing duplicate lead generation.

### 3. Failure & Monitoring
* **Fallback Strategy:** I will utilize **Error Handler** modules in Make. If an API call (HubSpot or Karix) fails, the system will trigger an automated retry mechanism (3 attempts) and log the error.
* **SLA Compliance:** To ensure WhatsApp messages are sent within the **2-minute SLA**, I will monitor the **"Execution Time"** in Make’s history logs. Any execution exceeding 60 seconds will trigger an automated alert to the development team for manual investigation.