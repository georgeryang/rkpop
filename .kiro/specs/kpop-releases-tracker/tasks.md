# Implementation Plan: K-pop Releases Tracker

## Overview

This plan implements a minimal single-file HTML application that fetches and displays K-pop releases from r/kpop. Maximum simplicity: no testing frameworks, no complex error handling, just core functionality. All code embedded in one file (kpop-releases.html).

## Tasks

- [x] 1. Create HTML structure with embedded CSS
  - Create kpop-releases.html with basic HTML5 structure
  - Add header with title
  - Add time range buttons (24h and 7d only)
  - Add results container with sections for Music Videos, Albums, and Songs
  - Add simple loading message div
  - Add embedded CSS with basic responsive styling (one breakpoint at 768px)
  - Style buttons to be touch-friendly (min 44px height) with rounded corners
  - Keep styling minimal and clean
  - _Requirements: 1.1, 1.2, 2.3, 9.1_

- [x] 2. Implement core JavaScript functionality
  - [x] 2.1 Create fetchRedditPosts() function
    - Use fetch() to call https://www.reddit.com/r/kpop.json
    - Parse JSON and extract posts from data.children array
    - Return array with title, url, created_utc, link_flair_text fields
    - Basic try-catch with simple "Failed to load" message on error
    - _Requirements: 3.1, 3.2, 3.3_
  
  - [x] 2.2 Create filterPostsByDateRange() function
    - Filter posts by created_utc timestamp within date range
    - Simple comparison, no edge case handling needed
    - _Requirements: 2.5, 2.6_
  
  - [x] 2.3 Create categorizePost() function
    - Check link_flair_text for [MV], [Album], [Song] (case-insensitive)
    - Return 'mv', 'album', 'song', or skip if no match
    - No keyword fallback needed (keep it simple)
    - _Requirements: 4.1, 4.2, 4.3, 4.4_
  
  - [x] 2.4 Create renderResults() function
    - Clear previous results
    - Create sections for each category
    - Render posts as simple list with title links and dates
    - Use toLocaleDateString() for date formatting
    - Show "No releases found" if empty
    - _Requirements: 5.1, 5.2, 5.3, 5.4_

- [x] 3. Implement UI controller and initialization
  - [x] 3.1 Create main loadReleases() function
    - Accept start and end date parameters
    - Show loading message
    - Call fetchRedditPosts(), filter, categorize, and render
    - Hide loading message when done
    - _Requirements: 1.3, 9.3_
  
  - [x] 3.2 Create initializeApp() function
    - Set up on DOMContentLoaded
    - Automatically load last 24 hours on page load
    - Attach click handlers to time range buttons (calculate 24h and 7d from now)
    - _Requirements: 2.1, 2.2, 2.3, 9.1_

- [x] 4. Manual testing and refinement
  - Open file in Safari on Mac and verify it works
  - Test on iPhone/iPad via iCloud Drive
  - Verify time range buttons work
  - Verify custom date range works
  - Check that posts are categorized correctly
  - Make any quick fixes needed
  - _Requirements: 1.2, 6.1_

## Notes

- No automated testing - just manual verification
- No complex error handling - simple "Failed to load" messages
- No keyword fallback for categorization - flair only
- Minimal CSS - just enough to be usable and responsive
- All code in single kpop-releases.html file
- Total implementation time: ~1-2 hours
