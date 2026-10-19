# DBX WebApi Controller - Endpoints & Requests

**Base URL:** `/api/DBXWebApi/{Action}`  
**Method:** POST  
**Content-Type:** application/json

---

## Get Sites
**Endpoint:** `/api/DBXWebApi/GetSites`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## Get Sessions
**Endpoint:** `/api/DBXWebApi/GetSessions`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "location_guid": "00000000-0000-0000-0000-000000000000",
  "date": "2026-05-15"
}
```

---

## Get Availability
**Endpoint:** `/api/DBXWebApi/GetAvailability`
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

## Make Booking
**Endpoint:** `/api/DBXWebApi/MakeBooking`
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

## Add Customer
**Endpoint:** `/api/DBXWebApi/AddCustomer`
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
    "customer_tag_guids": []
  },
  "booking_message": "Special occasion",
  "guest_request": "Window table if possible",
  "booking_source": "Website",
  "promotion_guid": null,
  "booking_tags": [],
  "deposit_amount": 0,
  "deposit_reference": null,
  "deposit_processor": null,
  "suppress_email": false,
  "suppress_sms": false,
  "preauth_token": null
}
```

---

## Get Booking
**Endpoint:** `/api/DBXWebApi/GetBooking`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## Delete Booking
**Endpoint:** `/api/DBXWebApi/DeleteBooking`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "suppress_sms": false,
  "suppress_email": false
}
```

---

## Update Booking
**Endpoint:** `/api/DBXWebApi/UpdateBooking`
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

## Update Booking Confirmation Status
**Endpoint:** `/api/DBXWebApi/UpdateBookingConfirmationStatus`
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

## Add Deposit
**Endpoint:** `/api/DBXWebApi/AddDeposit`
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

## Update Customer
**Endpoint:** `/api/DBXWebApi/UpdateCustomer`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "customer_guid": "SPR0UTID_OR_CUSTOMER_GUID",
  "consent": 1
}
```

---

## Get Promotions
**Endpoint:** `/api/DBXWebApi/GetPromotions`
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

## Get Booking Sources
**Endpoint:** `/api/DBXWebApi/GetBookingSources`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## Get Booking Tags
**Endpoint:** `/api/DBXWebApi/GetBookingTags`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## Get Customer Tags
**Endpoint:** `/api/DBXWebApi/GetCustomerTags`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## Get Locations
**Endpoint:** `/api/DBXWebApi/GetLocations`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "client_guid": "00000000-0000-0000-0000-000000000000",
  "site_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## Get Sessions Range
**Endpoint:** `/api/DBXWebApi/GetSessionsRange`
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

## Get Pre-Auth Details
**Endpoint:** `/api/DBXWebApi/GetPreAuthDetails`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "site_guid": "00000000-0000-0000-0000-000000000000"
}
```

---

## Keep Booking Alive
**Endpoint:** `/api/DBXWebApi/KeepBookingAlive`
```json
{
  "api_key": "00000000-0000-0000-0000-000000000000",
  "pending_booking_guid": "00000000-0000-0000-0000-000000000000",
  "keep_alive_minutes": 15
}
```
