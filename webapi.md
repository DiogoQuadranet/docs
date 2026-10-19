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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "client": "Example Client",
  "loyalty_brand_id": 1,
  "sites": [
    {
      "site": "Example Site",
      "time_zone": "Europe/London",
      "start_of_day": "06:00:00",
      "default_start_of_day": true,
      "site_guid": "00000000-0000-0000-0000-000000000000",
      "loyalty_site_id": 1,
      "locations": [
        {
          "location": "Restaurant",
          "location_guid": "00000000-0000-0000-0000-000000000000",
          "advanced_months": 3,
          "max_covers": 12,
          "cut_off": 60
        }
      ]
    }
  ]
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "day_message": "",
  "session_list": [
    {
      "session_friendly_name": "Dinner",
      "session_guid": "00000000-0000-0000-0000-000000000000",
      "first_time_slot": "17:00:00",
      "last_time_slot": "22:00:00",
      "session_message": ""
    }
  ]
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "day_message": "",
  "session_message": "",
  "available_promotions_list": [
    {
      "promotion_label": "Offer",
      "promotion_description": "Example offer",
      "promotion_guid": "00000000-0000-0000-0000-000000000000",
      "promotion_colour": "#008000"
    }
  ],
  "availability_list": [
    {
      "start_time": "19:00:00",
      "end_time": "20:30:00",
      "is_available": true,
      "timeslot_message": "",
      "deposit_due": 20.0,
      "deposit_per_cover": true,
      "deposit_per_cover_amount": 5.0,
      "deposit_paid": 0.0,
      "deposit_outstanding": 20.0,
      "deposit_name": "Deposit",
      "preauth_required": false,
      "deposit_description": "Required deposit",
      "total_available": 10,
      "promotion_guids": [
        "00000000-0000-0000-0000-000000000000"
      ],
      "duration": 90,
      "friendly_duration": "1 hour 30 minutes",
      "start_time_datetime": "2026-05-15T19:00:00"
    }
  ]
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "pending_booking_guid": "00000000-0000-0000-0000-000000000000",
  "deposit_due": 20.0,
  "deposit_per_cover": true,
  "deposit_per_cover_amount": 5.0,
  "deposit_paid": 0.0,
  "deposit_outstanding": 20.0,
  "deposit_name": "Deposit",
  "deposit_description": "Required deposit",
  "preauth_required": false,
  "available_promotion_list": [
    {
      "promotion_label": "Offer",
      "promotion_description": "Example offer",
      "promotion_guid": "00000000-0000-0000-0000-000000000000",
      "promotion_colour": "#008000"
    }
  ]
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "booking_guid": "00000000-0000-0000-0000-000000000000",
  "deposit_due": 20.0,
  "deposit_per_cover": true,
  "deposit_per_cover_amount": 5.0,
  "deposit_paid": 0.0,
  "deposit_outstanding": 20.0,
  "deposit_name": "Deposit",
  "deposit_description": "Required deposit",
  "preauth_required": false
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "surname": "Doe",
  "forename": "John",
  "booking_message": "Special occasion",
  "session_guid": "00000000-0000-0000-0000-000000000000",
  "session_name": "Dinner",
  "booking_datetime": "2026-05-15T19:00:00",
  "booking_datetime_raw": "2026-05-15T19:00:00",
  "covers": 4,
  "promotion": "Offer",
  "site": "Example Site",
  "location": "Restaurant",
  "client": "Example Client",
  "loyalty_site_id": 1,
  "loyalty_brand_id": 1,
  "duration": 90,
  "deposit_description": "Required deposit",
  "deposit_name": "Deposit",
  "deposit_due": 20.0,
  "deposit_per_cover": 5.0,
  "deposit_rule_id": 1,
  "deposit_type": 1,
  "deposit_paid": 0.0,
  "deposit_outstanding": 20.0,
  "preauth_required": false,
  "preauth_taken": false,
  "booking_promotion_guid": "00000000-0000-0000-0000-000000000000",
  "booking_promotion_label": "Offer",
  "booking_promotion_description": "Example offer",
  "booking_promotion_colour": "#008000",
  "booking_promotion_status": 1,
  "confirmation_status": 1,
  "confirmation_status_label": "Confirmed",
  "friendly_duration": "1 hour 30 minutes",
  "customer_message": "Birthday",
  "guest_request": "Window table",
  "booking_tags": [
    {
      "booking_booking_tag_guid": "00000000-0000-0000-0000-000000000000",
      "booking_tag_guid": "00000000-0000-0000-0000-000000000000",
      "booking_tag_name": "VIP",
      "guest_name": "John Doe",
      "added_online": true,
      "booking_tag_group_name": "Tags",
      "background_colour": "#000000",
      "text_colour": "#FFFFFF"
    }
  ],
  "customer_tags": [
    {
      "customer_customer_tag_guid": "00000000-0000-0000-0000-000000000000",
      "customer_tag_guid": "00000000-0000-0000-0000-000000000000",
      "customer_tag_name": "Member",
      "added_online": true,
      "customer_tag_group_name": "Tags",
      "background_colour": "#000000",
      "text_colour": "#FFFFFF"
    }
  ],
  "order_guid": [
    "00000000-0000-0000-0000-000000000000"
  ]
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": ""
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "error_code": 0
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": ""
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": ""
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

**Response:**
```json
{
  "success": true,
  "error_message": ""
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "available_promotions_list": [
    {
      "promotion_label": "Offer",
      "promotion_description": "Example offer",
      "promotion_guid": "00000000-0000-0000-0000-000000000000",
      "promotion_colour": "#008000"
    }
  ]
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

**Response:**
```json
{
  "succeeded": true,
  "booking_source_list": [
    {
      "booking_source_name": "Website"
    }
  ],
  "error_message": ""
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

**Response:**
```json
{
  "succeeded": true,
  "booking_tag_list": [
    {
      "booking_tag_group_name": "Tags",
      "booking_tag_group_guid": "00000000-0000-0000-0000-000000000000",
      "booking_tag_group_sort_order": 1,
      "background_colour": "#000000",
      "text_colour": "#FFFFFF",
      "booking_tags": [
        {
          "booking_tag_name": "VIP",
          "booking_tag_guid": "00000000-0000-0000-0000-000000000000",
          "booking_tag_sort_order": 1
        }
      ]
    }
  ],
  "error_message": ""
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

**Response:**
```json
{
  "succeeded": true,
  "customer_tag_list": [
    {
      "customer_tag_group_name": "Tags",
      "customer_tag_group_guid": "00000000-0000-0000-0000-000000000000",
      "customer_tag_group_sort_order": 1,
      "background_colour": "#000000",
      "text_colour": "#FFFFFF",
      "customer_tags": [
        {
          "customer_tag_name": "Member",
          "customer_tag_guid": "00000000-0000-0000-0000-000000000000",
          "customer_tag_sort_order": 1
        }
      ]
    }
  ],
  "error_message": ""
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "site": "Example Site",
  "time_zone": "Europe/London",
  "start_of_day": "06:00:00",
  "default_start_of_day": true,
  "loyalty_site_id": 1,
  "locations": [
    {
      "location": "Restaurant",
      "location_guid": "00000000-0000-0000-0000-000000000000",
      "advanced_months": 3,
      "max_covers": 12,
      "cut_off": 60
    }
  ]
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "days": [
    {
      "date": "2026-05-15",
      "day_bookings_stopped": false,
      "day_message": "",
      "sessions": [
        {
          "session_friendly_name": "Dinner",
          "session_guid": "00000000-0000-0000-0000-000000000000",
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": "",
  "elavon_secret_key": "secret",
  "elavon_public_key": "public",
  "elavon_merchant_alias": "merchant",
  "elavon_processor_id": "processor",
  "elavon_api_url": "https://example.invalid/api",
  "elavon_hpp_url": "https://example.invalid/hpp"
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

**Response:**
```json
{
  "succeeded": true,
  "error_message": ""
}
```

---

## Common Response Fields
(Responses retained as previously documented; for detailed responses see the repo examples.)

## Date/Time Formats
(As previously documented.)

## Validation Rules / Troubleshooting / Rate Limiting / Support
(As previously documented.)

---

<!-- Redundant schema matrix retained in source temporarily; endpoint-level schemas above are canonical.

## Complete request and response schemas

The examples above are introductory payloads. This section is the complete field-level contract, taken from the controller's DTOs. A `?` indicates a nullable DTO value; fields without `?` can still have a JSON default if omitted by the caller.

### Request DTOs

| Request DTO | All fields |
|---|---|
| `GetSitesRequest` | `api_key: GUID`, `client_guid: GUID` |
| `GetWebSessionRequest` | `api_key: GUID`, `client_guid: GUID`, `location_guid: GUID`, `date: date-time` |
| `GetWebSessionsRangeRequest` | `api_key: GUID`, `client_guid: GUID`, `location_guid: GUID`, `date_from: date-time`, `date_to: date-time` |
| `GetWebAvailabilityRequest` | `booking_guid: GUID?`, `api_key: GUID`, `client_guid: GUID`, `location_guid: GUID`, `session_guid: GUID`, `covers: integer`, `date: date-time`, `override_duration: integer?`, `return_totals: boolean`, `table_ids: integer[]`, `promotion_guid: GUID?` |
| `MakeBookingRequest` | `api_key: GUID`, `client_guid: GUID`, `location_guid: GUID`, `session_guid: GUID`, `covers: integer`, `booking_datetime: date-time`, `override_duration: integer?`, `booking_guid_list: GUID[]`, `table_ids: integer[]`, `booking_source: string`, `promotion_guid: GUID?` |
| `AddCustomerRequest` | `api_key: GUID`, `client_guid: GUID`, `location_guid: GUID`, `session_guid: GUID`, `covers: integer`, `booking_datetime: date-time`, `pending_booking_guid: GUID?`, `customer_details: WebCustomerInfo`, `booking_message: string`, `advert: string`, `referrer: string`, `promotion: string`, `promotion_guid: GUID?`, `booking_tags: BookingTagGuids[]`, `analyitics: string`, `guest_request: string`, `deposit_amount: number`, `deposit_processor: string`, `deposit_reference: string`, `booking_source: string`, `suppress_email: boolean`, `suppress_sms: boolean`, `preauth_token: string` |
| `GetWebBookingRequest` | `api_key: GUID`, `booking_guid: GUID?` |
| `DeleteBookingRequest` | `api_key: GUID`, `booking_guid: GUID`, `suppress_sms: boolean`, `suppress_email: boolean` |
| `UpdateBookingRequest` | `api_key: GUID`, `booking_guid: GUID`, `booking_datetime: date-time?`, `session_guid: GUID?`, `covers: integer?`, `booking_message: string`, `guest_request: string`, `replace_booking_message: boolean`, `replace_guest_request: boolean`, `deposit_amount: number`, `deposit_processor: string`, `deposit_reference: string`, `booking_source: string`, `suppress_email: boolean`, `suppress_sms: boolean`, `promotion_guid: GUID?`, `booking_tags: UpdateBookingBookingTag[]`, `customer_tags: UpdateBookingCustomerTags[]`, `preauth_token: string` |
| `UpdateBookingConfirmationStatusRequest` | `api_key: GUID`, `booking_guid: GUID`, `confirmation_status: integer`, `suppress_email: boolean`, `suppress_sms: boolean` |
| `AddDepositRequest` | `api_key: GUID`, `booking_guid: GUID`, `deposit_amount: number`, `deposit_processor: string`, `preauth_token: string`, `deposit_reference: string`, `suppress_email: boolean`, `suppress_sms: boolean` |
| `WebApiUpdateCustomerRequest` | `api_key: GUID`, `booking_guid: GUID`, `customer_guid: string`, `consent: integer` |
| `GetPromotionsRequest` | `api_key: GUID`, `client_guid: GUID`, `location_guid: GUID`, `session_guid: GUID?`, `covers: integer?`, `date: date-time?` |
| `GetBookingSourceRequest` | `api_key: GUID`, `client_guid: GUID` |
| `GetBookingTagsRequest` | `api_key: GUID`, `client_guid: GUID` |
| `GetCustomerTagsRequest` | `api_key: GUID`, `client_guid: GUID` |
| `GetLocationsWebApiRequest` | `api_key: GUID`, `client_guid: GUID`, `site_guid: GUID` |
| `GetPreauthDetailsReq` | `api_key: GUID`, `site_guid: GUID` |
| `KeepBookingAliveRequest` | `api_key: GUID`, `pending_booking_guid: GUID`, `keep_alive_minutes: integer` |

### Response DTOs

| Response DTO | All fields |
|---|---|
| `GetSitesResponse` | `succeeded: boolean`, `error_message: string`, `client: string`, `loyalty_brand_id: integer?`, `sites: WebSiteInfo[]` |
| `GetWebSessionsResponse` | `succeeded: boolean`, `error_message: string`, `day_message: string`, `session_list: WebSessionInfo[]` |
| `GetWebSessionsRangeResponse` | `succeeded: boolean`, `error_message: string`, `days: GetWebSessionsRangeResponse_Day[]` |
| `GetWebAvailabilityResponse` | `succeeded: boolean`, `error_message: string`, `day_message: string`, `session_message: string`, `available_promotions_list: AvailablePromotions[]`, `availability_list: WebAvailabilityInfo[]` |
| `MakeBookingResponse` | `succeeded: boolean`, `error_message: string`, `pending_booking_guid: GUID`, `deposit_due: decimal?`, `deposit_per_cover: boolean?`, `deposit_per_cover_amount: decimal?`, `deposit_paid: decimal?`, `deposit_outstanding: decimal?`, `deposit_name: string`, `deposit_description: string`, `preauth_required: boolean`, `available_promotion_list: AvailablePromotions[]` |
| `AddCustomerResponse` | `succeeded: boolean`, `error_message: string`, `booking_guid: GUID`, `deposit_due: decimal?`, `deposit_per_cover: boolean?`, `deposit_per_cover_amount: decimal?`, `deposit_paid: decimal?`, `deposit_outstanding: decimal?`, `deposit_name: string`, `deposit_description: string`, `preauth_required: boolean` |
| `GetWebBookingResponse` | `succeeded: boolean`, `error_message: string`, `surname: string`, `forename: string`, `booking_message: string`, `session_guid: GUID`, `session_name: string`, `booking_datetime: date-time`, `booking_datetime_raw: string`, `covers: integer`, `promotion: string`, `site: string`, `location: string`, `client: string`, `loyalty_site_id: integer?`, `loyalty_brand_id: integer?`, `duration: integer`, `deposit_description: string`, `deposit_name: string`, `deposit_due: decimal?`, `deposit_per_cover: decimal?`, `deposit_rule_id: integer?`, `deposit_type: integer?`, `deposit_paid: decimal?`, `deposit_outstanding: decimal?`, `preauth_required: boolean`, `preauth_taken: boolean`, `booking_promotion_guid: GUID?`, `booking_promotion_label: string`, `booking_promotion_description: string`, `booking_promotion_colour: string`, `booking_promotion_status: integer?`, `confirmation_status: integer?`, `confirmation_status_label: string`, `friendly_duration: string`, `customer_message: string`, `guest_request: string`, `booking_tags: GetBookingBookingTags[]`, `customer_tags: GetBookingCustomerTags[]`, `order_guid: GUID[]` |
| `DeleteBookingResponse` | `succeeded: boolean`, `error_message: string` |
| `UpdateBookingResponse` | `succeeded: boolean`, `error_message: string`, `error_code: integer` |
| `UpdateBookingConfirmationStatusResponse` | `succeeded: boolean`, `error_message: string` |
| `AddDepositResponse` | `succeeded: boolean`, `error_message: string` |
| `WebApiUpdateCustomerResponse` | `success: boolean`, `error_message: string` |
| `GetPromotionsRespose` | `succeeded: boolean`, `error_message: string`, `available_promotions_list: AvailablePromotions[]` |
| `GetBookingSourceResponse` | `succeeded: boolean`, `booking_source_list: WebBookingApiBookingSoruce[]`, `error_message: string` |
| `GetBookingTagsResponse` | `succeeded: boolean`, `booking_tag_list: BookingTagGroup[]`, `error_message: string` |
| `GetCustomerTagsResponse` | `succeeded: boolean`, `customer_tag_list: WebApiCustomerTagGroup[]`, `error_message: string` |
| `GetLocationsWebApiResponse` | `succeeded: boolean`, `error_message: string`, `site: string`, `time_zone: string`, `start_of_day: time?`, `default_start_of_day: boolean`, `loyalty_site_id: integer?`, `locations: WebLocation[]` |
| `GetPreauthDetailsRes` | `succeeded: boolean`, `error_message: string`, `elavon_secret_key: string`, `elavon_public_key: string`, `elavon_merchant_alias: string`, `elavon_processor_id: string`, `elavon_api_url: string`, `elavon_hpp_url: string` |
| `KeepBookingAliveResponse` | `succeeded: boolean`, `error_message: string` |

### Nested DTOs

| DTO | All fields |
|---|---|
| `WebCustomerInfo` | `surname: string`, `forename: string`, `email: string`, `phone: string`, `customer_message: string`, `consent: integer`, `member_id: integer?`, `swipe_id: string`, `booking_guid: GUID?`, `customer_tag_guids: string[]` |
| `BookingTagGuids` | `booking_tag_guid: string`, `guest_name: string` |
| `UpdateBookingBookingTag` | `action_type: integer`, `booking_booking_tag_guid: GUID`, `booking_tag_guid: string`, `guest_name: string` |
| `UpdateBookingCustomerTags` | `action_type: integer`, `customer_tag_guid: string`, `customer_customer_tag_guid: GUID` |
| `WebSiteInfo` | `site: string`, `time_zone: string`, `start_of_day: time`, `default_start_of_day: boolean`, `site_guid: GUID`, `loyalty_site_id: integer?`, `locations: WebLocation[]` |
| `WebLocation` | `location: string`, `location_guid: GUID`, `advanced_months: integer?`, `max_covers: integer?`, `cut_off: integer?` |
| `WebSessionInfo` | `session_friendly_name: string`, `session_guid: GUID`, `first_time_slot: time`, `last_time_slot: time`, `session_message: string` |
| `GetWebSessionsRangeResponse_Day` | `date: string`, `day_bookings_stopped: boolean`, `day_message: string`, `sessions: GetWebSessionsRangeResponse_Session[]` |
| `GetWebSessionsRangeResponse_Session` | `session_friendly_name: string`, `session_guid: GUID`, `first_time_slot: time`, `last_time_slot: time`, `session_message: string`, `session_bookings_stopped: boolean` |
| `AvailablePromotions` | `promotion_label: string`, `promotion_description: string`, `promotion_guid: GUID`, `promotion_colour: string` |
| `WebAvailabilityInfo` | `start_time: time`, `end_time: time`, `is_available: boolean`, `timeslot_message: string`, `deposit_due: decimal?`, `deposit_per_cover: boolean?`, `deposit_per_cover_amount: decimal?`, `deposit_paid: decimal?`, `deposit_outstanding: decimal?`, `deposit_name: string`, `preauth_required: boolean`, `deposit_description: string`, `total_available: integer?`, `promotion_guids: GUID[]`, `duration: integer`, `friendly_duration: string`, `start_time_datetime: string` |
| `GetBookingBookingTags` | `booking_booking_tag_guid: GUID`, `booking_tag_guid: GUID`, `booking_tag_name: string`, `guest_name: string`, `added_online: boolean`, `booking_tag_group_name: string`, `background_colour: string`, `text_colour: string` |
| `GetBookingCustomerTags` | `customer_customer_tag_guid: GUID`, `customer_tag_guid: GUID`, `customer_tag_name: string`, `added_online: boolean`, `customer_tag_group_name: string`, `background_colour: string`, `text_colour: string` |
| `WebBookingApiBookingSoruce` | `booking_source_name: string` |
| `BookingTagGroup` | `booking_tag_group_name: string`, `booking_tag_group_guid: GUID`, `booking_tag_group_sort_order: integer`, `background_colour: string`, `text_colour: string`, `booking_tags: BookingTagList[]` |
| `BookingTagList` | `booking_tag_name: string`, `booking_tag_guid: GUID`, `booking_tag_sort_order: integer` |
| `WebApiCustomerTagGroup` | `customer_tag_group_name: string`, `customer_tag_group_guid: GUID`, `customer_tag_group_sort_order: integer`, `background_colour: string`, `text_colour: string`, `customer_tags: WebApiCustomerTagList[]` |
| `WebApiCustomerTagList` | `customer_tag_name: string`, `customer_tag_guid: GUID`, `customer_tag_sort_order: integer` |

### Date and time values

Use ISO 8601 date-time values, for example `2026-05-15T19:00:00`. `time` values are .NET `TimeSpan` values, normally represented as `HH:mm:ss`.
-->
