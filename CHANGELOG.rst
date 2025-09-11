Changelog
#########

All notable changes to this project will be documented in this file.
The format is based on Keep a Changelog (https://keepachangelog.com/en/1.1.0/),
and this project adheres to Semantic Versioning (https://semver.org/spec/v2.0.0.html).

Version 19.1.1 (2025-09-11)
***************************

Changed
=======

- Removed unnecesary entry in ingress.

Version 19.1.0 (2025-09-08)
***************************

Added
=====

* Problem creation endpoints and logic for multiple problem types:
  - Support for dropdown problems with XML generation
  - Enhanced XML generation for multiple choice problems with input validation and escaping
  - ``POST /add_problem_content`` endpoint for problem integration
* Content publishing functionality:
  - ``POST /publish`` endpoint for publishing courses and units
  - Content publishing logic with modulestore integration
* XBlock management capabilities:
  - ``POST /delete_xblock`` endpoint for removing course components
  - Delete XBlock logic with modulestore integration
* Certificate management enhancements:
  - Toggle certificate logic for managing certificate active status
  - Certificate activation/deactivation integration in course configuration
  - Simplified certificate activation logic without certificate_id requirement

Version 19.0.1 (2025-08-27)
***************************

Changed
=======

- Fixed condition to enable chat widget.

Version 19.0.0 (2025-08-27)
**********

Added
=====

* DRF ViewSets and endpoints for analytics: ``overview``, ``enrollments``, ``discussions``, ``detailed`` under ``/owly-analytics/`` (see ``openedx_owly_apis/views/analytics.py``).
* Course management endpoints under ``/owly-courses/`` (see ``openedx_owly_apis/views/courses.py``):
  - ``POST /create``: create course.
  - ``POST /structure``: create/edit course structure (chapters, subsections, verticals).
  - ``POST /content/html``: add HTML component to vertical.
  - ``POST /content/video``: add Video component to vertical.
  - ``POST /content/problem``: add Problem component to vertical.
  - ``POST /content/discussion``: add Discussion component to vertical.
  - ``POST /settings/update``: update course settings (dates/details/etc.).
  - ``POST /settings/advanced``: update advanced settings.
  - ``POST /certificates/configure``: enable/configure certificates.
  - ``POST /units/availability/control``: control unit availability and due dates.
* Roles endpoint under ``/owly-roles/me`` to determine effective user role (see ``openedx_owly_apis/views/roles.py``).
* Authentication via ``JwtAuthentication``, ``BearerAuthenticationAllowInactiveUser``, and ``SessionAuthentication`` across ViewSets.

