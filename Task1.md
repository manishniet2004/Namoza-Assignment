# Task 01: GTM Event Schema

| Event Name | Trigger Type | Key Parameters | GA4 Report |
| :--- | :--- | :--- | :--- |
| `booking_step_complete` | Custom Event | step_number, step_name, clinic_location | Funnel Exploration |
| `call_button_click` | Click (Just Links) | button_location, phone_number, page_path | Engagement |
| `wa_chat_click` | Click (All Elements) | click_url, button_location, device_type | Traffic Source |
| `pdf_download` | Click (Just Links) | file_name, file_type, source_page | Content Performance |

### 3-Step Booking Form: DataLayer Implementation
I will manually implement the `dataLayer.push` in the frontend code for each form step.

**Example JSON for Step 1:**
```json
{
  "event": "booking_step_complete",
  "step_number": 1,
  "step_name": "location_specialty_selected",
  "clinic_location": "Bengaluru",
  "specialty": "Orthopaedics"
}