---
Task ID: 1
Agent: Main Agent
Task: Fix related videos below comments + channel page videos not showing

Work Log:
- Analyzed VideoPlayer.tsx (1513 lines) - RelatedVideosSection, CommentsSection, VideoInfo components
- Analyzed ChannelPage.tsx (586 lines) - channel data fetching, infinite query for more videos
- Analyzed youtube-api.ts - getVideoDetails, getChannelData functions
- Identified 3 bugs:
  1. Related videos scraping from YouTube watch page may fail due to HTML structure changes → no videos shown
  2. Channel videos scraping may fail → no videos on channel page
  3. ChannelPage infinite query had first page bug (pageParam=undefined causing immediate throw)
- Applied fixes:
  1. youtube-api.ts: Added search-based fallback for related videos when scraping returns < 8 videos
  2. youtube-api.ts: Increased related videos limit from 20 to 40
  3. youtube-api.ts: Fixed handle channelId extraction to include @ prefix from oEmbed
  4. youtube-api.ts: Added search-based fallback for channel videos when all extraction methods fail
  5. ChannelPage.tsx: Fixed infinite query to use continuationToken state as fallback for first page pageParam
  6. VideoPlayer.tsx: Increased RelatedVideosSection limit from 20 to 40

Stage Summary:
- 3 files modified: src/lib/youtube-api.ts, src/components/youtube/ChannelPage.tsx, src/components/youtube/VideoPlayer.tsx
- Pushed to both source repo (am6125241-cloud/V.I.P-Tube) and deploy repo (am6125241-cloud/viptube-deploy)
- Vercel auto-deploy will trigger from deploy repo push
