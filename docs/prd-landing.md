[Section 1: Page Overview]
This document specifies the requirements for the site's main landing page, located at the root (/).

Purpose: To act as a fast, clean, and direct "root navigator." Its primary function is to guide visitors who land on the root domain to one of the three main portfolio sections or provide immediate contact information.

File Path: src/pages/index.astro

[Section 2: Page-Specific User Flows]
[Flow: ContactNavigation]

GIVEN a user is on the Landing Page.

WHEN the user clicks the "Contact Me" button within the [Component: PrimaryNav] element.

THEN the browser executes a smooth scroll animation to the [Component: Footer] element.

[Section 3: Component Requirements & Specifications]
This section details the specific components required to construct the landing page.

[Component: IntroText]
Description: A static text block that serves as the primary heading and introduction.

Placement: Top-left of the main content area.

Content:

Hello there,
I am Advay Inabathini...
How can I help you?
Design Specs:

Typography: Adhere to Body Text token from prd-main.md. (Tailwind: text-base text-white).

Technical Implementation Notes:

For v1 simplicity, this content will be placed directly within the src/pages/index.astro file. It does not require a separate component file.

[Component: PrimaryNav]
Description: The main navigation hub, consisting of four interactive buttons.

Placement: Below the [Component: IntroText].

Design Specs:

Layout: A grid with a 16px gap (gap-4). On desktop (md: breakpoint and up), it's a 2x2 grid (grid-cols-2). On mobile, it's a 4x1 vertical stack (grid-cols-1).

Styling: Each button must have 12px vertical padding (py-3), 24px horizontal padding (px-6), and a 1px solid border (border border-white).

Behavior: On hover, buttons must smoothly transition background-color and color as per the accent-hover tokens in prd-main.md.

Behavioral Specs (Links):

"Photography" button navigates to /photography.

"Design" button navigates to /design.

"Tech" button navigates to /tech.

"Contact Me" button navigates to #contact, triggering [Flow: ContactNavigation].

Technical Implementation Notes:

Component Name: PrimaryNav.astro

Location: src/components/PrimaryNav.astro

[Component: LandingPageGrid]
Description: A purely visual, decorative grid of photos that sits in the page background to provide immediate visual interest.

Placement: Occupies the background of the page. Its exact layout relative to the foreground content will be determined during implementation, but it should not interfere with the readability of the text.

Content: The grid will render a static, pre-defined list of 8-10 images.

Design Specs:

Layout: A responsive masonry-style grid with a 16px gap (gap-4). Use varying column and row spans to achieve the asymmetrical look from the Figma design.

Example Layout: On a 4-column grid, some items might have col-span-2 or row-span-2.

Technical Implementation Notes:

Component Name: LandingPageGrid.astro

Location: src/components/LandingPageGrid.astro

Data Source: Must import its list of images from a dedicated file: src/data/landingPagePhotos.js.

Image Optimization: Must use the Astro <Image /> component for every photo to ensure performance.

[Component: Footer]
Description: The global site footer.

Placement: At the bottom of the page viewport.

Page-Specific Requirement: The root element of this component must have an id="contact" attribute to serve as the scroll anchor for the "Contact Me" button.

Technical Implementation Notes:

Component Name: Footer.astro

Location: src/components/Footer.astro

All other content and behavioral requirements are defined in prd-main.md.

[Section 4: Page Layout & Responsiveness]
Desktop (md: and up): The page should have a primary content area on the left, containing the [Component: IntroText] and [Component: PrimaryNav]. The [Component: LandingPageGrid] serves as a background element.

Mobile (<md): All content should stack vertically in a single column for easy readability. The order should be: IntroText, PrimaryNav, Footer. The LandingPageGrid remains a background element.