# K-pop Releases Tracker - Planning Document

## Project Overview
A simple, single-file HTML application that fetches and displays K-pop music releases from r/kpop subreddit with an interactive UI.

## Requirements

### Functional Requirements
1. Fetch posts from r/kpop subreddit
2. Filter posts by time range (24h, 7 days, 30 days, custom)
3. Categorize releases by type (Music Videos, Albums, Songs)
4. Display results in an organized, readable format
5. No installation or command-line usage required

### Technical Requirements
- Single HTML file with embedded CSS and JavaScript
- No external dependencies or frameworks
- Works offline after initial load (except for data fetching)
- Compatible with modern browsers (Chrome, Firefox, Safari, Edge)

## Technical Approach

### Data Source
- **Reddit JSON API**: `https://www.reddit.com/r/kpop.json`
- Public endpoint, no authentication required
- Returns up to 100 most recent posts
- Can paginate using `after` parameter if needed

### Post Filtering Strategy
1. **By Flair**: Look for common flairs
   - `[MV]` - Music Videos
   - `[Album]` - Album releases
   - `[Song]` - Single songs
   - `[Audio]` - Audio releases
   - `[Release]` - General releases

2. **By Keywords** (fallback if no flair):
   - Music Video: "MV", "M/V", "Music Video"
   - Album: "Album", "EP", "Mini Album", "Full Album"
   - Song: "Song", "Single", "Digital Single"

3. **By Date**: Filter based on post creation timestamp

### UI Components

#### 1. Header Section
- Title: "K-pop Releases Tracker"
- Subtitle: "Latest releases from r/kpop"

#### 2. Controls Section
- Quick select buttons:
  - "Last 24 Hours"
  - "Last 7 Days"
  - "Last 30 Days"
- Custom date range:
  - Start date picker
  - End date picker
  - "Search" button
- "Refresh" button to reload data

#### 3. Results Section
- Loading indicator while fetching
- Error message display if fetch fails
- Categorized lists:
  - **Music Videos** section
  - **Albums** section
  - **Songs** section
  - **Other Releases** section (catch-all)
- Each item displays:
  - Title (linked to Reddit post)
  - Artist name (extracted from title)
  - Post date/time
  - Thumbnail (if available)
  - Link to external content (if available)

#### 4. Stats Section
- Total releases found
- Breakdown by category

## Data Structure

### Reddit JSON Response
```javascript
{
  data: {
    children: [
      {
        data: {
          title: string,
          url: string,
          permalink: string,
          created_utc: number,
          link_flair_text: string,
          thumbnail: string,
          author: string
        }
      }
    ]
  }
}
```

### Processed Release Object
```javascript
{
  title: string,
  artist: string,
  type: 'mv' | 'album' | 'song' | 'other',
  redditUrl: string,
  externalUrl: string,
  date: Date,
  thumbnail: string,
  flair: string
}
```

## Implementation Plan

### Phase 1: HTML Structure
- Create basic HTML layout
- Add semantic structure for all sections
- Include meta tags for proper rendering

### Phase 2: CSS Styling
- Modern, clean design
- Responsive layout (mobile-friendly)
- Color scheme: K-pop themed (vibrant but readable)
- Loading states and animations
- Category badges/tags

### Phase 3: JavaScript Functionality
- Fetch data from Reddit JSON API
- Parse and filter posts
- Extract artist names from titles
- Categorize by type
- Handle date filtering
- Render results dynamically
- Error handling and user feedback

### Phase 4: Testing & Refinement
- Test with different time ranges
- Verify categorization accuracy
- Check browser compatibility
- Handle edge cases (no results, API errors, etc.)

## Challenges & Solutions

### Challenge 1: CORS Restrictions
**Problem**: Browser may block cross-origin requests to Reddit
**Solution**: Reddit's JSON API supports CORS, but if issues arise, user can use browser extension or open file with `--allow-file-access-from-files` flag

### Challenge 2: Limited Data History
**Problem**: JSON API only returns ~100 recent posts
**Solution**: 
- Implement pagination to fetch more posts if needed
- Set realistic expectations (30-day view may be incomplete)
- Add note in UI about limitations

### Challenge 3: Inconsistent Post Formatting
**Problem**: Post titles vary in format, making artist extraction difficult
**Solution**:
- Use regex patterns to extract artist names
- Handle common formats: "Artist - Song Title [MV]"
- Fallback to full title if extraction fails

### Challenge 4: Categorization Accuracy
**Problem**: Some posts may not have clear flairs or keywords
**Solution**:
- Priority: flair > keywords > "Other" category
- Allow multiple keywords per category
- Manual review of "Other" category for improvements

## File Structure
```
kpop-releases.html (single file containing):
├── HTML structure
├── <style> CSS
└── <script> JavaScript
```

## Future Enhancements (Optional)
- Save favorite releases to localStorage
- Export results as CSV/JSON
- Filter by specific artists
- Sort options (date, alphabetical, etc.)
- Dark mode toggle
- Share results via URL parameters
- Integration with music streaming services

## Success Criteria
- ✅ Opens and runs in browser without installation
- ✅ Fetches real data from r/kpop
- ✅ Correctly filters by time range
- ✅ Categorizes releases accurately (>80% accuracy)
- ✅ Clean, intuitive UI
- ✅ Handles errors gracefully
- ✅ Responsive design works on mobile

## Timeline Estimate
- Planning: Complete
- Implementation: ~2-3 hours
- Testing: ~30 minutes
- Total: ~3 hours

## Next Steps
1. Review and approve this plan
2. Create `kpop-releases.html` file
3. Implement HTML structure
4. Add CSS styling
5. Implement JavaScript functionality
6. Test and refine
7. Document usage instructions
