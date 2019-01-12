---
title: API Error Codes
---

Error Code | HTTP Code | Response Msg                          | Description
---------- | --------- | ------------                          | -----------
105        | 503       | Service currently unavailable         | The requested service is temporarily unavailable.
110        | 404       | API Version "XXX" not found.          | The requested API version was not found.
111        | 404       | Format "XXX" not found.               | The requested response format was not found.
112        | 404       | Method "XXX" not found.               | The requested method was not found.
115        | 404       | Missing required parameter            | Parameters which are required have not been sent.
120        | 404       | Parameter "XXX" has an invalid value. | The provided parameter value is not valid.
140        | 400       | Endpoint "XXX" not found.             | The requested endpoint was not found
150        | 400       | Language with ISO2 code: "XX" is not yet supported in the API | Response requested in an unsupported language.
160        | 400       | Filtering data-set on an indicator value without indicating a date range is meaningless and is not allowed. | You need to indicate date-range if you want to filter by an indicator value.
199        | 500       | Unexpected error                      | An unexpected error was encountered while processing the request.
