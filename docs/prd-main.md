# What The Application Does (Vision & Goals)
Vision: A professional online platform showcasing Advay Inabathini's multi-disciplinary skills in Photography, Graphic Design, and Technology.

v1 Goal: Launch an MVP with a landing page and a functional photography portfolio to support freelance client acquisition.

Target Audience: Potential freelance clients (photo/design) and tech industry recruiters.

# 2. Required Technologies (Global Tech Stack)
Framework: Astro

Styling: Tailwind CSS

Page Transitions: Astro View Transitions

Image Handling: Astro Image Component (<Image />)

Version Control: Git & GitHub

Deployment: GitHub Pages via GitHub Actions

# 3. Design Patterns & Conventions (Project-Wide Rules)
This section defines the rules to be followed for all generated code to ensure consistency and maintainability.

## 3.1. Architectural Pattern:

The project will use Astro's Islands Architecture.

Most components will be static, presentational .astro files.

Client-side JavaScript should be used sparingly and only within isolated components ("islands") when interactivity is essential.

## 3.2. Data Handling Pattern:

Content and data (e.g., lists of photos, project details) should be decoupled from the UI.

All project data will be stored in JavaScript objects/arrays within the src/data/ directory (e.g., src/data/photos.js).

Components should import data from this directory rather than containing hard-coded content.

## 3.3. Component Structure Pattern:

Components should be created to be reusable and single-purpose where possible.

All reusable components will be located in src/components/.

All full-page layouts will be located in src/layouts/.

## 3.4. Styling Pattern:

Styling will be implemented exclusively with Tailwind CSS utility classes applied directly in the HTML structure.

Custom CSS via <style> tags should be avoided unless absolutely necessary for a complex, unique element.

## 3.5. File & Code Conventions:

Component Files: PascalCase (e.g., PrimaryNav.astro).

JavaScript Variables: camelCase (e.g., photoList).

Responsiveness: Mobile-first approach. Base styles should target mobile, with sm:, md:, lg: prefixes for larger screens.

# 4. Technical Specifications (Feature-Specific Docs)
The detailed technical specifications, user flows, and component breakdowns for each major feature are located in their respective "spoke" documents.

Landing Page: See docs/prd-landing.md

Photography Page: See docs/prd-photography.md

(Future documents will be added here)