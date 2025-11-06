# Copo

[Copo.st](https://copo.st)  
[Alvin5, Inc](https://alvin5.com)

- contact@alvin5.com
- bora@alvin5.com

# Features

- Multi-platform > Web, mobile web, native (iOS, Android), TV or embed in your existing apps and websites. Web-embeddable.
- Video/Photo/GenAI posts (Vertical/Horizontal)
- Short-form (and long form) video platform
- GenAI Enabled Social Platform
  - Direct Integration with OpenAI
  - AI Video/Image creation with Sora2(Sora-like social genai app platform). Create, share, comment, remix...
  - Fal/Replicate integration\*
- User profiles
  - Pinned posts, links, profile customization, custom feeds(e.g. playlist, series)
- Follow Users/Feeds...
- Channels
- Bookmarks
- Reposts
- Feeds (Users can create public feeds/series)
- Hashtags, mentions, links
- DMs
- Search
- User notification/activity feed
- Comments
- Action buttons for posts
- Custom feeds (Public/Private, single/multi user, shareable, instant/shareable/embeddable feeds)
- Location features: Nearby feeds, map\*
- Locked posts (Video plays blurred, users pay to unlock post)
- Locked feeds
  - Users pay to unlock feeds(e.g. series, short-drama)
  - First x episodes could be set free to watch
- In App Payment Architecture
  - User credit/star balance
  - AppStore/GooglePlay In-app-purchase, web-based payments\*
  - Subscriptions\*
- Monetization options\*
  - Ads
  - Boost posts
  - Paid Channels, Pay to post to channel
  - Locked/Paid Posts/Feeds
  - Pay to message
  - Gifts
  - Custom monetization models
  - Connect your Stripe
- Native push notifications platform
  - Direct connection to Apple/Google
  - Rich-notifications with images
- Native Login system
  - Direct native login architecture, no third-party/in-app-browser based login
  - Use your own login system
- Share
  - Native share architecture
  - Open-graph enabled. Content (posts, videos, profile, feeds) shared appears natively in third-party apps(Messages, Whatsapp, X, Telegram...)
  - URL Shortener with referral analytics and tracking functionality, built for supporting user-share revenue sharing models and other growth tactics.
- Report/Block User/Post/Comment
- Embeddable Architecture
  - Embed apps/feeds/profiles/posts in your website or mobile app
  - Control embedded web-app from your web-app/mobile-app via API
- Direct Integration with Meta Marketing Platform
  - Web/Mobile conversion tracking
  - Automated ad creation with Meta Marketing API

# Technical Infra

## Frontend

TODO

## Backend

Multi-tenant backend to support multiple social networks/apps using a single unified backend infra which offers SOTA cost-effective architecture for serving and operating.

The backend is in-house built custom Graph architecture that builds on previous and new SOTA architectures referencing [Facebook TAO](https://research.facebook.com/publications/tao-facebooks-distributed-data-store-for-the-social-graph/), [Tiktok's ByteGraph](https://vldb.org/pvldb/vol15/p3306-li.pdf) and many other engineering practices from Meta, Pinterest, Instagram, Uber, LinkedIn..

The core graph architecture is basically supported by only two 'logical' tables -objects and edges - which supports the generic social network concepts and provides super efficient way create new app patterns simply by creating new object types and edges. This architecture provides efficient serving/operational architecture and offers a fundamental data graph architecture for AI models for both semantic operations, building custom models and Graph Rag like operations.

Objects ids are 64bit int, with custom format similar to [IG](https://www.youtube.com/watch?v=bLyv8zKa5DU) and Snowflake systems.

Objects and other data architectures stored as [protobuf](https://protobuf.dev/).

Graph data is served with a Meta TAO like architecture with caching(Redis) in front (with point and range capabilities) and persistent storage(KV store e.g RocksDB+). We have explored and need to further explore the possibility of a single storage product(Redis, RocksDB, new Postgres features) for both cache and persistent storage -to support a new architecture that supports our efficiency, modularity and scalability requirements.

### Video Backend Infra

Custom Node based ffmpeg task executor that supports custom video encoder for short-form video or other usage patterns.

We use advanced video encoding architectures that generates fragmented MP4(ISOBMFF) video variants with fragments and other settings specifically tuned for our client-side custom MSE video player.

Videos/photos are uploaded directly to CDN/SD3 directly from clients - enabling fast and efficient upload experience. We also support chunked upload for larger files. Currently our architecture supports uploading large files(2GB+) and multiple files at once.

We have experience on various server side video processing/rendering workflows like headless Chrome/Canvas based processing. We also have previous code architecture for executing on-server Cuda based AI models on video/images. We are following recent Webcodecs and agentic video developments.
