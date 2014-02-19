# Views

Best practices for creating Drupal views.

1. **Reject unexpected sub-paths.** By default, Views displays that register router items, such as pages and feeds, respond not only to the exact paths registered but to "sub-paths" as well--e.g., a view at a path of `/example` will also respond to `/example/1` and `/example/1/2` with an HTTP 200 response and the same content. This can lead to unexpected site behavior, confusing user experience, cache bypass vulnerabilities, and duplicate content issues with the search engines. It can be prevented with a simple trick: add a "Global: Null" contextual filter (formerly known as "arguments") and set it to "Fail basic validation if any argument is given". This will cause anything at more than the expected path depth to return a 404. This approach offers complete and granular control, and it doesn't have the unexpected side effects or performance issues associated with common module-based approaches.
