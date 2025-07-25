[Section 1: Page Overview]
Purpose: To provide a comprehensive and interactive gallery of Advay Inabathini's photography work. This page serves as the primary showcase for freelance clients and is designed for deep engagement with the user's visual portfolio.

File Path: src/pages/photography/index.astro

[Section 2: Data Model]
Description: The content for this entire page will be driven by a single source of truth for all photos. This prevents data duplication and makes the portfolio easy to update.

File Location: src/data/photos.js

Data Structure: The file will export a single constant array named photos. Each object within this array must conform to the following Photo schema:

JavaScript

{
  id: Number,           // Unique numeric ID, e.g., 1
  title: String,        // Title of the photo/shoot, e.g., "Onam Celebrations"
  src: String,          // Filepath to the high-resolution image for the slideshow, e.g., "/images/photos/onam-celebrations.jpg"
  thumbnailSrc: String, // Filepath to the smaller, optimized image for the grid view
  alt: String,          // Descriptive alt text for accessibility
  genres: [String],     // An array of genre tags, e.g., ['portrait', 'event']
  isFeatured: Boolean,  // `true` if the photo should appear in the default "Featured" view
  exif: String          // Camera and lens info, e.g., "Nikon D90, 50mm f/1.8"
}
[Section 3: Page-Specific User Flows]
[Flow: FilterByGenre]

GIVEN the user is on the Photography page.

BY DEFAULT the [Component: PhotoGrid] displays only photos where isFeatured is true. The "Featured" filter button is in an active state.

WHEN the user clicks a genre filter button (e.g., "Portraits").

THEN the [Component: PhotoGrid] must dynamically update (without a page reload) to display only photos where the photo.genres array includes('portrait').

AND the "Portraits" filter button is marked as active, and all other filters are inactive.

AND if the user clicks the currently active filter button again, the filter resets to the default "Featured" view.

[Flow: ViewPhotoInSlideshow]

GIVEN a user is viewing the [Component: PhotoGrid].

WHEN the user clicks on any photo thumbnail.

THEN the [Component: Slideshow] appears as a full-screen modal with a semi-transparent black background.

AND the slideshow displays the high-resolution src image, its title, and exif data.

AND "Next" and "Previous" navigation controls are visible.

[Flow: CloseSlideshow]

GIVEN the [Component: Slideshow] is open.

WHEN the user clicks anywhere on the semi-transparent background (i.e., not the photo or the navigation controls).

OR WHEN the user presses the Escape key.

THEN the [Component: Slideshow] is hidden, and the user is returned to the [Component: PhotoGrid] view.

[Section 4: Component Requirements & Specifications]
[Component: PhotographyHeader]
Description: A simple header block introducing the photography section.

Content: Will contain a title ("Photography Portfolio"), a short descriptive paragraph, and a self-portrait image as per the Figma design.

Technical Implementation Notes:

Component Name: PhotographyHeader.astro

Location: src/components/

[Component: GenreFilters]
Description: An interactive set of buttons for filtering the photo gallery.

Content: Buttons must be dynamically generated. The list of genres should be derived automatically from the src/data/photos.js file to ensure all genres are represented. A "Featured" button must always be present as the first option.

Behavior: This component is responsible for handling the client-side logic for [Flow: FilterByGenre].

Technical Implementation Notes:

Component Name: GenreFilters.astro

Location: src/components/

This component MUST be an Astro Island (client:load) as its functionality is entirely dependent on client-side JavaScript to handle clicks and manipulate the gallery without reloading the page.

[Component: PhotoGrid]
Description: The main grid that displays photo thumbnails.

Content: It will receive a list of Photo objects as a prop and render them in a masonry-style grid.

Behavior: Each thumbnail is a button that, when clicked, triggers the [Flow: ViewPhotoInSlideshow].

Technical Implementation Notes:

Component Name: PhotoGrid.astro

Location: src/components/

Must use the Astro <Image /> component for all thumbnails, using the thumbnailSrc from the data object.

This component will be re-rendered by client-side JavaScript managed by [Component: GenreFilters].

[Component: Slideshow]
Description: A full-screen, modal-style image viewer (lightbox).

Content: Displays a single, high-resolution photo, its title, and EXIF data. Includes "Next" and "Previous" buttons.

Behavior: It is hidden by default. JavaScript will control its visibility, content, and handle the CloseSlideshow and navigation flows.

Technical Implementation Notes:

Component Name: Slideshow.astro

Location: src/components/

This component MUST also be an Astro Island (client:load) because it is fully interactive and managed by client-side JavaScript.

The state (which photo is currently visible, which filter is active) will need to be managed by a simple client-side script that controls both the GenreFilters and the Slideshow.