# Errors

The MyRIACompliance API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong or has expired.
403 | Forbidden -- Your API key does not allow access to this endpoint.
404 | Not Found -- The specified endpoint could not be found.
406 | Not Acceptable -- You requested a format that isn't json.
429 | Too Many Requests -- You've reached your limit of 500 requests for the day.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
