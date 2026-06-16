# DBX Web API Documentation

## Base URL
```
/api/DBXWebApi
```

## Authentication
All endpoints require an `api_key` (GUID) to be passed in the request body. The API key is validated against the PayAtTable repository.

**Header:**
```
Content-Type: application/json
```

---

## Endpoints

### 1. Keep Booking Alive
**Endpoint:** `POST /api/DBXWebApi/KeepBookingAlive`

**Description:** Extends the time for a booking that is currently in progress.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "pending_booking_guid": "00000000-0000-0000-0000-000000000000",
  "keep_alive_minutes": 15
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": ""
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Booking not found"` - Booking GUID doesn't exist
- `"Booking already deleted"` - Booking status is 255 or not Booked/InProgress
- `"Booking not in progress"` - Booking status is not InProgress
- `"Failed to keep booking alive"` - Database update failed

---

### 2. Delete Booking
**Endpoint:** `POST /api/DBXWebApi/DeleteBooking`

**Description:** Deletes a pending or in-progress booking.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "suppress_email": false,
  "suppress_sms": false
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": ""
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Booking for guid: [guid] not found"` - Booking doesn't exist
- `"Booking delete failed"` - Booking status prevents deletion

---

### 3. Get Promotions
**Endpoint:** `POST /api/DBXWebApi/GetPromotions`

**Description:** Retrieves available promotions for a booking.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "date": "2026-05-15",
  "covers": 4,
  "session_guid": "00000000-0000-0000-0000-000000000000"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "available_promotions_list": [
    {
      "promotion_guid": "00000000-0000-0000-0000-000000000000",
      "promotion_label": "Summer Special",
      "promotion_description": "20% off for groups of 4+",
      "promotion_colour": "#FF5733"
    }
  ]
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Invalid Client"` - Client GUID not found
- `"No Location record Matches given LocationGuid"` - Location doesn't exist

---

### 4. Get Booking
**Endpoint:** `POST /api/DBXWebApi/GetBooking`

**Description:** Retrieves details of a specific booking including deposit information.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "booking_id": 12345,
  "deposit_due": 50.00,
  "deposit_paid": 25.00,
  "deposit_outstanding": 25.00
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Booking not found"` - Booking GUID doesn't exist

---

### 5. Get Locations
**Endpoint:** `POST /api/DBXWebApi/GetLocations`

**Description:** Retrieves all web-enabled locations for a site.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "site_guid": "00000000-0000-0000-0000-000000000000"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "site": "Main Restaurant",
  "time_zone": "Europe/London",
  "start_of_day": "06:00:00",
  "loyalty_site_id": "LOYALTY001",
  "locations": [
    {
      "location_id": 1,
      "location_name": "Main Floor",
      "location_guid": "00000000-0000-0000-0000-000000000000"
    }
  ]
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Invalid Client"` - Client GUID not found
- `"No site Matches for GUID"` - Site doesn't exist
- `"Fatal in GetLocations"` - Server error

---

### 6. Get Pre-Auth Details
**Endpoint:** `POST /api/DBXWebApi/GetPreAuthDetails`

**Description:** Retrieves payment processor pre-authentication details for a site.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "site_guid": "00000000-0000-0000-0000-000000000000"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "elavon_secret_key": "secret_key_value",
  "elavon_public_key": "public_key_value",
  "elavon_merchant_alias": "MERCHANT123",
  "elavon_processor_id": "PROC001",
  "elavon_api_url": "https://api.elavon.com",
  "elavon_hpp_url": "https://hpp.elavon.com"
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"No site Matches for GUID"` - Site doesn't exist

---

### 7. Get Sites
**Endpoint:** `POST /api/DBXWebApi/GetSites`

**Description:** Retrieves all available sites for a client.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "client": "Restaurant Group Name",
  "sites": [
    {
      "site_id": 1,
      "site_name": "London Branch",
      "site_guid": "00000000-0000-0000-0000-000000000000"
    }
  ]
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Invalid Client"` - Client GUID not found

---

### 8. Get Sessions
**Endpoint:** `POST /api/DBXWebApi/GetSessions`

**Description:** Retrieves available sessions for a specific date and location.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "date": "2026-05-15"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "day_message": "Busy evening expected",
  "session_list": [
    {
      "session_guid": "00000000-0000-0000-0000-000000000000",
      "session_friendly_name": "Lunch Service",
      "first_time_slot": "12:00:00",
      "last_time_slot": "14:30:00",
      "session_message": "Lunch only on weekdays"
    }
  ]
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Invalid Client"` - Client GUID not found
- `"Location GUID: [guid] location id: [id]. Location is not present or doesnt allow web."` - Invalid location
- `"No Sessions"` - No sessions available for date

---

### 9. Get Sessions Range
**Endpoint:** `POST /api/DBXWebApi/GetSessionsRange`

**Description:** Retrieves available sessions for a date range.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "date_from": "2026-05-15",
  "date_to": "2026-05-22"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "days": [
    {
      "date": "2026-05-15",
      "day_message": "Fully booked",
      "day_bookings_stopped": false,
      "sessions": [
        {
          "session_guid": "00000000-0000-0000-0000-000000000000",
          "session_friendly_name": "Dinner",
          "first_time_slot": "17:00:00",
          "last_time_slot": "22:00:00",
          "session_message": "",
          "session_bookings_stopped": false
        }
      ]
    }
  ]
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Invalid Client"` - Client GUID not found
- `"Start date must be before end date"` - Invalid date range

---

### 10. Get Availability
**Endpoint:** `POST /api/DBXWebApi/GetAvailability`

**Description:** Retrieves available time slots for a booking.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "date": "2026-05-15",
  "covers": 4,
  "return_totals": true,
  "booking_guid": null,
  "table_ids": [],
  "override_duration": null
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "day_message": "",
  "session_message": "",
  "availability_list": [
    {
      "start_time": "17:00:00",
      "end_time": "18:30:00",
      "is_available": true,
      "slot_colour": "#00FF00",
      "slot_text_colour": "#000000"
    }
  ],
  "available_promotions_list": []
}
```

**Error Responses:**
- `"Requested date [date] is more than 10 years in the future"` - Date too far in future
- `"Invalid api_key"` - API key validation failed
- `"Invalid Client"` - Client GUID not found
- `"Session GUID: [guid] location id: [id]. Session is not valid for given location and date."` - Invalid session

---

### 11. Make Booking
**Endpoint:** `POST /api/DBXWebApi/MakeBooking`

**Description:** Creates a new pending booking.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "booking_datetime": "2026-05-15T19:00:00",
  "covers": 4,
  "booking_source": "Website",
  "promotion_guid": null,
  "override_duration": null,
  "booking_guid_list": []
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "pending_booking_guid": "00000000-0000-0000-0000-000000000000",
  "deposit_due": 50.00,
  "deposit_per_cover": true,
  "deposit_per_cover_amount": 12.50,
  "deposit_paid": 0.00,
  "deposit_outstanding": 50.00,
  "deposit_name": "Deposit Required",
  "deposit_description": "A deposit is required to confirm this booking",
  "preauth_required": false,
  "available_promotion_list": []
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Invalid Client"` - Client GUID not found
- `"Location GUID: [guid] location id: [id]. Location is not present or doesnt allow web."` - Invalid location
- `"Invalid Session"` - Session GUID not valid
- `"Booking date time is in the past"` - Cannot book in past
- `"Booking cannot be made this close to its start time"` - Web cut-off time exceeded
- `"Online Bookings are not permitted less than [X] mins before the start of session"` - Session cut-off exceeded
- `"Online bookings are not permitted less than [X] day(s) in advance"` - Booking too soon
- `"Online bookings are not permitted for more than [X] people."` - Exceeds max covers
- `"Online bookings are not permitted more than [X] months in advance"` - Booking too far ahead
- `"Location closed"` - Location has a stop message
- `"Total covers for time slot would be exceeded"` - Time slot full
- `"Total covers for session would be exceeded"` - Session full
- `"Invalid Promotion"` - Promotion not valid for this booking

---

### 12. Add Customer
**Endpoint:** `POST /api/DBXWebApi/AddCustomer`

**Description:** Adds customer details to a pending booking and confirms it.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "pending_booking_guid": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "booking_datetime": "2026-05-15T19:00:00",
  "covers": 4,
  "customer_details": {
    "forename": "John",
    "surname": "Doe",
    "email": "john@example.com",
    "phone": "07700900000",
    "consent": 1,
    "customer_message": "Birthday celebration",
    "member_id": null,
    "swipe_id": null,
    "booking_guid": null,
    "customer_tag_guids": ["00000000-0000-0000-0000-000000000000"]
  },
  "booking_message": "Special occasion",
  "guest_request": "Window table if possible",
  "booking_source": "Website",
  "promotion_guid": null,
  "booking_tags": [
    {
      "booking_tag_guid": "00000000-0000-0000-0000-000000000000",
      "guest_name": "John Doe"
    }
  ],
  "deposit_amount": 0,
  "deposit_reference": null,
  "deposit_processor": null,
  "advert": null,
  "referrer": null,
  "promotion": null,
  "suppress_email": false,
  "suppress_sms": false
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "deposit_due": 50.00,
  "deposit_per_cover": true,
  "deposit_per_cover_amount": 12.50,
  "deposit_paid": 0.00,
  "deposit_outstanding": 50.00,
  "deposit_name": "Deposit Required",
  "deposit_description": "A deposit is required",
  "preauth_required": false
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"No pending_booking_guid supplied"` - Booking GUID required
- `"booking not found for supplied pending_booking_guid: [guid]"` - Booking doesn't exist
- `"This booking has been deleted"` - Booking status is 255
- `"Preauth token cannot be null"` - Token required if provided
- `"No customer details supplied"` - Customer data required
- `"Must supply a surname"` - Surname required
- `"Must supply a forename"` - Forename required if no member ID
- `"Invalid email address"` - Email validation failed
- `"member_id/surname not found"` - Member not found
- `"swipe_id/surname not found"` - Swipe ID not found
- `"Invalid Promotion"` - Promotion not valid for booking

---

### 13. Update Customer
**Endpoint:** `POST /api/DBXWebApi/UpdateCustomer`

**Description:** Updates customer information on a booking.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "customer_guid": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "consent": 1,
  "forename": "Jane",
  "surname": "Doe",
  "email": "jane@example.com",
  "phone": "07700900001"
}
```

**Response:**
```json
{
  "success": true,
  "error_message": ""
}
```

**Error Responses:**
- `"Api key required"` - API key missing
- `"Both customer and booking guid cannot both be unspecified"` - At least one GUID required
- `"Consent field required in request"` - Consent value required
- `"Invalid api_key"` - API key validation failed

---

### 14. Update Booking
**Endpoint:** `POST /api/DBXWebApi/UpdateBooking`

**Description:** Updates booking details including date, time, covers, and notes.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "booking_datetime": "2026-05-15T20:00:00",
  "covers": 5,
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "booking_message": "Updated note",
  "replace_booking_message": false,
  "booking_source": "Website",
  "promotion_guid": null,
  "guest_request": "Early seating preferred",
  "replace_guest_request": false,
  "booking_tags": [],
  "customer_tags": [],
  "deposit_amount": 25.00,
  "deposit_reference": "DEP123",
  "deposit_processor": "Stripe",
  "preauth_token": "token123",
  "suppress_email": false,
  "suppress_sms": false
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "Booking details updated",
  "error_code": 3
}
```

**Error Response Codes:**
- `error_code: 1` - Invalid deposit amount
- `error_code: 2` - Booking updated but deposit failed
- `error_code: 3` - Success
- Messages:
  - `"Invalid api_key"` - API key validation failed
  - `"Booking for guid:[guid] not found"` - Booking doesn't exist
  - `"Booking has been deleted"` - Booking status is 255
  - `"Booking cannot be changed"` - Booking status not editable
  - `"Location not found"` - Location doesn't exist
  - `"Site not found"` - Site doesn't exist
  - `"Changes to online bookings are not permitted this close to its start time"` - Edit cut-off exceeded

---

### 15. Update Booking Confirmation Status
**Endpoint:** `POST /api/DBXWebApi/UpdateBookingConfirmationStatus`

**Description:** Updates the confirmation status of a booking.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "confirmation_status": 1,
  "suppress_email": false,
  "suppress_sms": false
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "ConfirmationStatus updated with success"
}
```

**Confirmation Status Values:**
- `0` - Unconfirmed
- `1` - Confirmed
- `2` - Auto Confirmed

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Booking for guid: [guid] not found"` - Booking doesn't exist
- `"Booking has been deleted"` - Booking status is 255
- `"Booking cannot be changed"` - Booking status not editable
- `"Fail, Confirmation Status must be between 0 and 2"` - Invalid status value

---

### 16. Add Deposit
**Endpoint:** `POST /api/DBXWebApi/AddDeposit`

**Description:** Records a deposit payment for a booking.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "deposit_amount": 50.00,
  "deposit_reference": "DEP123456",
  "deposit_processor": "Stripe",
  "suppress_email": false,
  "suppress_sms": false
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "Deposit Saved with success"
}
```

**Error Responses:**
- `"Invalid api_key"` - API key validation failed
- `"Booking for guid:[guid] not found"` - Booking doesn't exist
- `"Booking has been deleted"` - Booking status is 255
- `"Booking cannot be changed"` - Booking status not editable
- `"Booking record not added to table BookingDepositPush"` - Database error
- `"Fail to Add Deposit"` - Deposit amount is 0 or negative

---

### 17. Get Booking Tags
**Endpoint:** `POST /api/DBXWebApi/GetBookingTags`

**Description:** Retrieves available booking tags for a client.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "booking_tag_list": [
    {
      "booking_tag_group_guid": "00000000-0000-0000-0000-000000000000",
      "booking_tag_group_name": "Occasions",
      "booking_tag_group_sort_order": 1,
      "background_colour": "#FF5733",
      "text_colour": "#FFFFFF",
      "booking_tags": [
        {
          "booking_tag_guid": "00000000-0000-0000-0000-000000000000",
          "booking_tag_name": "Birthday",
          "booking_tag_sort_order": 1
        }
      ]
    }
  ]
}
```

**Error Responses:**
- `"Invalid Api Key"` - API key validation failed
- `"Invalid Client Number provided"` - Client GUID not found
- `"No Booking Tags Groups Found"` - No tags available

---

### 18. Get Customer Tags
**Endpoint:** `POST /api/DBXWebApi/GetCustomerTags`

**Description:** Retrieves available customer tags for a client.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "customer_tag_list": [
    {
      "customer_tag_group_guid": "00000000-0000-0000-0000-000000000000",
      "customer_tag_group_name": "VIP Levels",
      "customer_tag_group_sort_order": 1,
      "background_colour": "#FFD700",
      "text_colour": "#000000",
      "customer_tags": [
        {
          "customer_tag_guid": "00000000-0000-0000-0000-000000000000",
          "customer_tag_name": "Platinum",
          "customer_tag_sort_order": 1
        }
      ]
    }
  ]
}
```

**Error Responses:**
- `"Invalid Api Key"` - API key validation failed
- `"Invalid Client Number provided"` - Client GUID not found
- `"No Customer Tags Groups Found"` - No tags available

---

### 19. Get Booking Sources
**Endpoint:** `POST /api/DBXWebApi/GetBookingSources`

**Description:** Retrieves available booking sources for a client.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "booking_source_list": [
    {
      "source_id": 1,
      "source_name": "Website",
      "source_guid": "00000000-0000-0000-0000-000000000000"
    },
    {
      "source_id": 2,
      "source_name": "Phone",
      "source_guid": "00000000-0000-0000-0000-000000000000"
    }
  ]
}
```

**Error Responses:**
- `"Invalid Api Key"` - API key validation failed
- `"Invalid Client Number provided"` - Client GUID not found
- `"Fatal in GetBookingSources"` - Server error

---

## Common Response Fields

### Success Response Pattern
All successful responses follow this pattern:
```json
{
  "succeeded": true,
  "error_message": ""
}
```

### Error Response Pattern
All error responses include:
```json
{
  "succeeded": false,
  "error_message": "Description of error"
}
```

---

## Date/Time Formats

- **Date Format:** `YYYY-MM-DD` (ISO 8601)
  - Example: `2026-05-15`

- **DateTime Format:** `YYYY-MM-DDTHH:mm:ss` (ISO 8601)
  - Example: `2026-05-15T19:00:00`

- **TimeSpan Format:** `HH:mm:ss`
  - Example: `19:00:00`

---

## Booking Status Codes

| Code | Status | Description |
|------|--------|-------------|
| 1 | Booked | Confirmed booking |
| 2 | InProgress | Customer currently dining |
| 3 | Seated | Customer seated |
| 255 | Deleted | Booking has been deleted |

---

## Confirmation Status Codes

| Code | Status |
|------|--------|
| 0 | Unconfirmed |
| 1 | Confirmed |
| 2 | Auto Confirmed |

---

## Deposit Type Values

| Code | Type | Description |
|------|------|-------------|
| 1 | Fixed | Fixed deposit amount |
| 2 | ByCovers | Per-cover deposit amount |

---

## HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | OK - Request successful |
| 400 | Bad Request - Invalid request format |
| 500 | Internal Server Error - Server error occurred |

---

## Authentication Notes

1. All requests must include a valid `api_key` in the request body
2. The API key is validated against the PayAtTable repository
3. Invalid or missing API keys will return: `"Invalid api_key"`
4. API keys must be valid GUIDs in the format: `00000000-0000-0000-0000-000000000000`

---

## Validation Rules

### Booking Dates & Times
- Booking datetime cannot be in the past
- Booking must respect web cutoff times (time before start time)
- Booking must respect cutoff days (minimum advance booking)
- Max advance booking (in months) is configurable per location

### Covers
- Must be positive integer
- Cannot exceed max covers per location
- Must not exceed session capacity
- Must not exceed timeslot capacity

### Customer Details
- Surname is required
- Forename is required (unless member ID provided)
- Email must be valid format (if validation is enabled)
- Consent value required for UpdateCustomer

### Promotions
- Promotion GUID must be valid for the booking date/time/location/session
- Promotion must be active and applicable

---

## Troubleshooting

### Common Issues

**Issue:** "Invalid api_key"
- **Solution:** Verify API key is correct GUID format and is registered in the system

**Issue:** "Invalid Client"
- **Solution:** Ensure client_guid matches a registered client in the system

**Issue:** "Booking cannot be made this close to its start time"
- **Solution:** Check location's WebCutOff setting; increase advance booking time

**Issue:** "Online bookings are not permitted less than X day(s) in advance"
- **Solution:** Check location's WebCutOffDays setting; allow more advance booking time

**Issue:** "Total covers for session would be exceeded"
- **Solution:** Session is fully booked; suggest alternative time or reduce covers

**Issue:** "Location closed"
- **Solution:** Day message indicates location is stopped; choose different date

---

## Rate Limiting

Currently, there are no rate limits enforced. However, it's recommended to:
- Implement reasonable request spacing
- Cache responses where possible
- Batch requests when appropriate

---

## Support

For API support or issues, contact the development team with:
- API key used
- Request/response JSON
- Timestamp of request
- Error message received
