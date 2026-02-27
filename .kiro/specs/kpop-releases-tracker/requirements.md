# Requirements Document

## Introduction

The K-pop Releases Tracker is a browser-based tool that fetches and displays K-pop music releases from the r/kpop subreddit. The tool provides an interactive interface for users to view categorized releases within specified time ranges without requiring command-line interaction or API authentication.

## Glossary

- **Tracker**: The K-pop Releases Tracker system
- **Release_Post**: A Reddit post from r/kpop that announces a K-pop music release
- **Time_Range**: A period specification for filtering posts (24 hours, 7 days, 30 days, or custom dates)
- **Release_Type**: A category of K-pop release (Teaser, Music Video, Album, or Song)
- **Flair_Tag**: A Reddit post flair marker ([Teaser], [MV], [Album], or [Audio])
- **Results_Display**: The organized presentation of filtered Release_Posts in the browser
- **Reddit_JSON_API**: Reddit's public JSON endpoint for accessing subreddit data
- **Custom_Date_Range**: A user-specified start and end date for filtering posts

## Requirements

### Requirement 1: Browser-Based Interface

**User Story:** As a K-pop fan, I want to access the tracker through a single HTML file, so that I can use it without installing software or running command-line tools.

#### Acceptance Criteria

1. THE Tracker SHALL be implemented as a single HTML file containing all necessary HTML, CSS, and JavaScript code
2. WHEN a user opens the HTML file in a web browser, THE Tracker SHALL display the interactive interface without requiring additional file downloads
3. THE Tracker SHALL render all content within the same browser window without opening new tabs or windows

### Requirement 2: Time Range Selection

**User Story:** As a user, I want to select different time ranges for viewing releases, so that I can see recent releases or releases from the past week.

#### Acceptance Criteria

1. THE Tracker SHALL default to displaying Release_Posts from the last 24 hours when first opened
2. THE Tracker SHALL automatically fetch and display results for the 24-hour Time_Range without requiring user interaction
3. THE Tracker SHALL provide buttons for selecting predefined Time_Ranges of 24 hours and 7 days
4. WHEN a user clicks a time range button, THE Tracker SHALL filter Release_Posts to show only those within the selected Time_Range

### Requirement 3: Reddit Data Fetching

**User Story:** As a user, I want the tracker to automatically fetch posts from r/kpop, so that I can see current release information without manual data entry.

#### Acceptance Criteria

1. THE Tracker SHALL fetch posts from the Reddit_JSON_API endpoint for r/kpop subreddit
2. THE Tracker SHALL retrieve posts without requiring Reddit API authentication credentials
3. WHEN the Reddit_JSON_API returns data, THE Tracker SHALL parse the JSON response to extract Release_Posts
4. IF the Reddit_JSON_API request fails, THEN THE Tracker SHALL display an error message indicating the fetch operation failed

### Requirement 4: Release Categorization

**User Story:** As a user, I want releases organized by type, so that I can quickly find teasers, music videos, albums, or songs.

#### Acceptance Criteria

1. THE Tracker SHALL categorize Release_Posts into four Release_Types: Teaser, Music Video, Album, and Song
2. WHEN a Release_Post contains the Flair_Tag "[Teaser]", THE Tracker SHALL categorize it as Teaser
3. WHEN a Release_Post contains the Flair_Tag "[MV]", THE Tracker SHALL categorize it as Music Video
4. WHEN a Release_Post contains the Flair_Tag "[Album]", THE Tracker SHALL categorize it as Album
5. WHEN a Release_Post contains the Flair_Tag "[Audio]", THE Tracker SHALL categorize it as Song
6. THE Tracker SHALL display categorized Release_Posts in separate sections within the Results_Display
7. THE Tracker SHALL sort posts within each category by newest first
8. WHEN in "Teasers" mode, THE Tracker SHALL display only the Teaser section
9. WHEN in "New Releases" mode, THE Tracker SHALL display only Music Video, Album, and Song sections

### Requirement 5: Results Display

**User Story:** As a user, I want to see organized release information with clickable links, so that I can easily access the original Reddit posts.

#### Acceptance Criteria

1. THE Tracker SHALL display each Release_Post with its thumbnail, title, posting date, timestamp in local time, and Release_Type
2. THE Tracker SHALL display thumbnails on the left side of each post
3. THE Tracker SHALL always display a thumbnail - either the post's image or a fire emoji (🔥) placeholder
4. THE Tracker SHALL render each Release_Post title as a clickable hyperlink to the original Reddit post
5. THE Tracker SHALL organize the Results_Display with clear visual separation between Release_Types
6. WHEN no Release_Posts match the selected Time_Range, THE Tracker SHALL display a message indicating no releases were found
7. THE Tracker SHALL display timestamps in the user's local timezone with 12-hour format

### Requirement 6: CORS Handling

**User Story:** As a user, I want the tracker to work when opened as a local file or deployed to GitHub Pages, so that I can access it from anywhere.

#### Acceptance Criteria

1. THE Tracker SHALL handle Cross-Origin Resource Sharing (CORS) restrictions when accessing the Reddit_JSON_API from any domain
2. THE Tracker SHALL use a CORS proxy service (corsproxy.io) to bypass browser CORS restrictions
3. THE Tracker SHALL work correctly when deployed to GitHub Pages or similar static hosting services
4. THE Tracker SHALL work correctly when opened as a local file in modern browsers

### Requirement 7: Data Limitations

**User Story:** As a user, I want to understand the limitations of the tracker, so that I have appropriate expectations about available data.

#### Acceptance Criteria

1. THE Tracker SHALL fetch up to 100 most recent posts from the Reddit_JSON_API
2. WHEN the selected Time_Range extends beyond the available posts, THE Tracker SHALL display only the Release_Posts available within the 100-post limit
3. THE Tracker SHALL display a notice informing users that results are limited to approximately the 100 most recent posts from r/kpop

### Requirement 8: Minimal Dependencies

**User Story:** As a user, I want the tracker to work without installing additional libraries or frameworks, so that I can use it immediately.

#### Acceptance Criteria

1. THE Tracker SHALL implement all functionality using standard HTML, CSS, and JavaScript without requiring external library downloads
2. THE Tracker SHALL not require Node.js, Python, or other runtime installations to function
3. WHERE external resources are needed, THE Tracker SHALL load them from public CDNs accessible via the internet

### Requirement 9: Interactive Operation

**User Story:** As a user, I want all interactions to happen through the browser interface, so that I never need to use the command line.

#### Acceptance Criteria

1. THE Tracker SHALL provide all functionality through clickable buttons, input fields, and interactive elements
2. THE Tracker SHALL not require users to execute command-line commands for any operation
3. WHEN a user performs an action, THE Tracker SHALL provide immediate visual feedback within the browser interface
