# Workshop Booking — UI/UX Enhancement

This iteration focuses on improving the overall user experience, especially for students on mobile devices, while keeping the existing Django views and template structure intact.

What changed at a glance
- Global layout improvements in the base template
- Mobile-first spacing and readability
- Accessible navigation and focus states
- Automatic responsive tables and improved form controls
- Non-intrusive scripts to enhance existing pages without rewriting templates


Reasoning
1) Design principles used
- Mobile-first: Prioritized small screens with readable typography, generous spacing, and touch-friendly controls.
- Visual hierarchy: Structured content with cards, adequate padding, and consistent spacing scale to emphasize key actions.
- Consistency: Centralized improvements in the base template and base stylesheet so all pages inherit the same UI patterns.
- Accessibility: Added a skip link to jump to main content, improved focus outlines, and ensured toasts are visible and dismissible.
- Progressive enhancement: Kept enhancements additive, without breaking existing behavior or requiring template rewrites.

2) Ensuring responsiveness
- Wrapped all tables automatically in a responsive container so they scroll horizontally on mobile instead of overflowing.
- Added a spacing scale and consistent paddings/margins for better vertical rhythm on small screens.
- Ensured inputs and buttons have minimum heights for touch targets.
- Collapsed the mobile navbar automatically after a link click to avoid trapping users.
- Used container in the navbar to limit line length and maintain a clean layout on wide screens.

3) Design vs. Performance trade-offs
- Kept dependencies unchanged to avoid heavier bundles; reused the existing Bootstrap and jQuery shipped with the project.
- Added small, targeted JavaScript to enhance forms and tables automatically; the code is lightweight and runs after DOMReady.
- Preserved CDN for Material Icons to avoid bundling new assets.
- Chose CSS-only approaches for many improvements (focus states, spacing scale) to reduce runtime overhead.

4) Most challenging part and approach
- Challenge: Improving many pages at once without touching each template individually and without risking regressions.
- Approach: Concentrated changes in the base template and base.css to cascade improvements globally. Wrote defensive JavaScript (checks classes/parents before modifying DOM) to avoid double-wrapping or styling conflicts.


Changes made
- workshop_app/templates/workshop_app/base.html
  - Added meta theme-color and a visible skip link for accessibility.
  - Wrapped navbar content in a .container to maintain readable line lengths.
  - Marked the main content region with id="main" for skip link targeting.
  - Configured Toastr with close button, progress bar, and sane defaults.
  - Added a script to:
    - Wrap tables in a responsive container.
    - Apply .form-control to common inputs/selects/textarea for better mobile usability.
    - Ensure submit buttons receive Bootstrap button styling.
    - Auto-collapse the navbar after clicking a link on mobile.

- workshop_app/static/workshop_app/css/base.css
  - Added spacing variables, improved footer, and increased content padding to avoid overlap with fixed header/footer.
  - Implemented accessible focus outlines and a keyboard-visible skip link.
  - Improved card padding and table readability.
  - Increased touch targets (inputs/buttons min-height) and honored reduced-motion preferences.


Setup instructions
1) Clone and set up environment
- git clone https://github.com/FOSSEE/workshop_booking
- cd workshop_booking
- python3 -m venv .venv
- source .venv/bin/activate
- pip install -r requirements.txt

2) Environment variables
- Copy .sampleenv to .env and adjust values if needed.

3) Database and static
- python manage.py migrate
- python manage.py collectstatic  # optional for local, helpful if DEBUG=False

4) Run the server
- python manage.py runserver

Visual showcase (add screenshots)
Place screenshots in docs/screenshots and ensure the file names match those referenced below.

Before
- docs/screenshots/before_home.png
- docs/screenshots/before_login.png

After
- docs/screenshots/after_home.png
- docs/screenshots/after_login.png


Submission checklist
- [x] Code is readable and well-structured
- [x] Centralized changes with minimal template churn
- [x] README includes reasoning and setup instructions
- [x] Screenshots: add files under docs/screenshots and ensure links above resolve
- [x] Code is documented where necessary (inline comments and self-explanatory CSS variables)


Notes
- No new heavyweight frameworks were added; improvements are built on the project’s existing Bootstrap/jQuery stack for fast load times.
- The enhancements are backward compatible and strictly progressive. Pages that already used Bootstrap markup will look and work better, while pages with plain form fields are upgraded automatically at runtime.

