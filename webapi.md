<div align="center">
  <img src="./assets/36741914-c89c-425b-a6fe-4f4685ea1ab4.png" alt="DBX Logo" width="300">
</div>

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

## Endpoints (ordered)

### Get Sites
**Endpoint:** `POST /api/DBXWebApi/GetSites`

**Description:** Returns sites for a client.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

### Get Sessions
**Endpoint:** `POST /api/DBXWebApi/GetSessions`

**Description:** Returns sessions for a location and date.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "date": "2026-05-15"
}
```

---

### Get Availability
**Endpoint:** `POST /api/DBXWebApi/GetAvailability`

**Description:** Returns availability for a session/location/date/covers.

**Request:**
```json
{
  "booking_guid": null,
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "covers": 4,
  "date": "2026-05-15",
  "override_duration": null,
  "return_totals": false,
  "table_ids": [],
  "promotion_guid": null
}
```

---

### Make Booking
**Endpoint:** `POST /api/DBXWebApi/MakeBooking`

**Description:** Create a booking.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "covers": 4,
  "booking_datetime": "2026-05-15T19:00:00",
  "override_duration": null,
  "booking_guid_list": [],
  "table_ids": [],
  "booking_source": "Website",
  "promotion_guid": null
}
```

---

### Add Customer
**Endpoint:** `POST /api/DBXWebApi/AddCustomer`

**Description:** Add customer details to a pending booking or create a booking with customer.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "covers": 4,
  "booking_datetime": "2026-05-15T19:00:00",
  "pending_booking_guid": null,
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
    "customer_tag_guids": [
      "00000000-0000-0000-0000-000000000000"
    ]
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
  "suppress_sms": false,
  "preauth_token": null
}
```

---

### Get Booking
**Endpoint:** `POST /api/DBXWebApi/GetBooking`

**Description:** Get booking details by booking GUID.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

### Delete Booking
**Endpoint:** `POST /api/DBXWebApi/DeleteBooking`

**Description:** Delete a booking (pending or in-progress).

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "suppress_sms": false,
  "suppress_email": false
}
```

---

### Update Booking
**Endpoint:** `POST /api/DBXWebApi/UpdateBooking`

**Description:** Update an existing booking.

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
  "deposit_amount": 25.0,
  "deposit_reference": "DEP123",
  "deposit_processor": "Stripe",
  "preauth_token": "token123",
  "suppress_email": false,
  "suppress_sms": false
}
```

---

### Update Booking Confirmation Status
**Endpoint:** `POST /api/DBXWebApi/UpdateBookingConfirmationStatus`

**Description:** Update the confirmation status of a booking.

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

---

### Add Deposit
**Endpoint:** `POST /api/DBXWebApi/AddDeposit`

**Description:** Add a deposit to a booking.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "deposit_amount": 50.0,
  "deposit_reference": "DEP123456",
  "deposit_processor": "Stripe",
  "suppress_email": false,
  "suppress_sms": false
}
```

---

### Update Customer
**Endpoint:** `POST /api/DBXWebApi/UpdateCustomer`

**Description:** Update customer details. Subapp is resolved by booking_guid or customer_guid.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "customer_guid": "SPR0UTID_OR_CUSTOMER_GUID",
  "consent": 1
}
```

---

### Get Promotions
**Endpoint:** `POST /api/DBXWebApi/GetPromotions`

**Description:** Get available promotions for the given location/session/date/covers.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "session_guid": null,
  "covers": 4,
  "date": "2026-05-15"
}
```

---

### Get Booking Sources
**Endpoint:** `POST /api/DBXWebApi/GetBookingSources`

**Description:** Get available booking sources for a client.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

### Get Booking Tags
**Endpoint:** `POST /api/DBXWebApi/GetBookingTags`

**Description:** Get booking tags for a client.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

### Get Customer Tags
**Endpoint:** `POST /api/DBXWebApi/GetCustomerTags`

**Description:** Get customer tags for a client.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

### Get Locations
**Endpoint:** `POST /api/DBXWebApi/GetLocations`

**Description:** Get locations for a site.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "site_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

### Get Sessions Range
**Endpoint:** `POST /api/DBXWebApi/GetSessionsRange`

**Description:** Get sessions across a date range for a location.

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

---

### Get Pre-Auth Details
**Endpoint:** `POST /api/DBXWebApi/GetPreAuthDetails`

**Description:** Get pre-auth configuration for a site.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "site_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

### Keep Booking Alive
**Endpoint:** `POST /api/DBXWebApi/KeepBookingAlive`

**Description:** Extend the time for a booking that is in progress.

**Request:**
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "pending_booking_guid": "00000000-0000-0000-0000-000000000000",
  "keep_alive_minutes": 15
}
```

---

## Common Response Fields
(Responses retained as previously documented; for detailed responses see the repo examples.)

## Date/Time Formats
(As previously documented.)

## Validation Rules / Troubleshooting / Rate Limiting / Support
(As previously documented.)
