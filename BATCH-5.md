Long links are hard to share, so the service creates short codes for them.

Build POST /shorten, which accepts a url.

Rules

The URL must start with http:// or https://, or return 400.
Generate a random 6-character code using letters and digits.
If the code already exists in urls.csv, generate a new one.
If the same URL was shortened before, return its existing code instead of creating a new one.
Save the code, the URL, the creation time, and clicks=0.

Build GET /{code}, which redirects (302) to the original URL and increases its click count by 1. An unknown code returns 404.

Build GET /stats/{code}, which returns the URL, its creation time, and its click count.

Done when: shortening the same URL twice returns the same code, and opening the link 3 times shows 3 clicks.