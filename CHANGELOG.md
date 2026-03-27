# Changelog

All notable changes to this project will be documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Unreleased

- feat: align local development automation with the shared Tutor plugin `Makefile` targets, including `clean` and `PYTHON` override support
- feat: align dev/test requirements and GitHub Actions workflows with the shared plugin maintenance setup
- ref: restrict supported Python versions to 3.11 and 3.12 in packaging metadata
- chore: ignore generated Tutor `config.yml` and `env/` artifacts from local test runs

## Version 20.0.0 (2026-03-26)

### Added

- Automated release publishing from GitHub Actions when a pushed tag matches `vX.X.X` and the full test workflow passes.

### Changed

- Removed the `OWLY_ENABLE_CHAT` setting and its MFE-side gate so chat loads whenever the plugin is enabled, while keeping the backend chat flag endpoint configuration.
- Updated the bundled Django app dependency to `openedx-owly-apis==2.0.1`.
- Pass deterministic Owly loader context into Open edX MFEs through both `window.OwlyChatbotContext` and script `data-*` attributes.
- Inject `platformType="openedx"` and `baseUrl=LMS_BASE_URL` for frontend runtime platform resolution instead of relying on hostname inference.
- Auto-bootstrap the Owly loader from shared MFE config so pages without footer slots, including authn, can still load the chat script.
- Converted the changelog to Markdown.

### Fixed

- Made `make test` build distribution artifacts before running `twine check dist/*`.
- Removed an unused MFE config import from the build-time patch.

## Version 20.0.0 (2026-03-20)

### Changed

- Declared Tutor 20 support.
- Relaxed `Requires-Python` to `>=3.9` to match Tutor 20 supported Python versions.
- Moved Owly frontend integration to Tutor 20 compatible MFE build-time configuration and plugin slots.

### Added

- GitHub Actions coverage for automated test runs on pushes and pull requests.
- Initial GitHub Actions publishing workflow for PyPI releases.

## Version 19.6.1 (2025-12-15)

Updated Django app to use version `openedx-owly-apis==1.6.3`.

## Version 19.6.0 (2025-12-11)

Updated Django app to use version `openedx-owly-apis==1.6.0`.


## Version 19.5.0 (2025-10-31)

Updated Django app to use version `openedx-owly-apis==1.5.0`.

## Version 19.4.0 (2025-10-22)

Updated Django app to use version `openedx-owly-apis==1.4.0`.

## Version 19.2.1 (2025-09-23)

### Changed

- Updated MFE platform repo to use version `owly/sumac.2.1`.


## Version 19.2.0 (2025-09-23)

### Added

- Owly chat feature flag endpoint:
  `GET /owly-config/enable_owly_chat`: Check if the Owly chat feature is enabled via waffle flag.
- Advanced problem creation:
  `POST /owly-courses/content/problem/create`: Create any problem component with structured data (e.g., multiple select, numerical input, text input, etc.).
- Content publishing endpoint:
  `POST /owly-courses/content/publish`: Publish a course or course component (unit, subsection, etc.).
- XBlock management:
  `POST /owly-courses/xblock/delete`: Delete an XBlock component from a course.
- Course staff management endpoints:
  `POST /owly-courses/staff/manage`: Add or remove a user from a course staff role (`staff` or `course_creator`).
  `GET /owly-courses/staff/list?course_id=<course-key>`: List users with staff roles for a given course.


## Version 19.1.1 (2025-09-11)

### Changed

- Removed unnecesary entry in ingress.

## Version 19.1.0 (2025-09-08)

### Added

- Problem creation endpoints and logic for multiple problem types:
  Support for dropdown problems with XML generation
  Enhanced XML generation for multiple choice problems with input validation and escaping
  `POST /add_problem_content` endpoint for problem integration
- Content publishing functionality:
  `POST /publish` endpoint for publishing courses and units
  Content publishing logic with modulestore integration
- XBlock management capabilities:
  `POST /delete_xblock` endpoint for removing course components
  Delete XBlock logic with modulestore integration
- Certificate management enhancements:
  Toggle certificate logic for managing certificate active status
  Certificate activation/deactivation integration in course configuration
  Simplified certificate activation logic without certificate_id requirement

## Version 19.0.1 (2025-08-27)

### Changed

- Fixed condition to enable chat widget.

## Version 19.0.0 (2025-08-27)

### Added

- DRF ViewSets and endpoints for analytics: `overview`, `enrollments`, `discussions`, `detailed` under `/owly-analytics/` (see `openedx_owly_apis/views/analytics.py`).
- Course management endpoints under `/owly-courses/` (see `openedx_owly_apis/views/courses.py`):
  `POST /create`: create course.
  `POST /structure`: create/edit course structure (chapters, subsections, verticals).
  `POST /content/html`: add HTML component to vertical.
  `POST /content/video`: add Video component to vertical.
  `POST /content/problem`: add Problem component to vertical.
  `POST /content/discussion`: add Discussion component to vertical.
  `POST /settings/update`: update course settings (dates/details/etc.).
  `POST /settings/advanced`: update advanced settings.
  `POST /certificates/configure`: enable/configure certificates.
  `POST /units/availability/control`: control unit availability and due dates.
- Roles endpoint under `/owly-roles/me` to determine effective user role (see `openedx_owly_apis/views/roles.py`).
- Authentication via `JwtAuthentication`, `BearerAuthenticationAllowInactiveUser`, and `SessionAuthentication` across ViewSets.
