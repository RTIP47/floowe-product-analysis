🇵🇱 Polish version → [Zobacz wersję polską](../pl/04-features.md)

---

# Feature Proposals – Floowe

This document proposes three new features for the Floowe platform based on the previous product analysis, user flows, and event storming results.

The ideation phase was supported by Claude AI and refined to align with the current product architecture.

---

# Feature 1 – Content Performance Dashboard

Domain: Distribution  
Type: Analytics

## User Story

As a marketing manager using Floowe  
I want to see engagement metrics for every published article and social post  
So that I can understand which content drives the most traffic and leads.

## Acceptance Criteria

- Dashboard displays article metrics such as page views, average time on page, and search impressions.
- Social metrics (likes, shares, clicks, reach) are aggregated across Facebook, LinkedIn and X.
- System ranks top-performing articles by engagement score.
- Metrics refresh automatically every 24 hours.
- Each metric links to the original analytics source.

## Business Case

Floowe currently focuses on generating and publishing content but lacks visibility into performance.  
Providing analytics closes the feedback loop and helps users improve their content strategy, increasing perceived product value.

## Technical Overview

Components:
- Analytics dashboard UI
- Backend metrics aggregation service
- Metrics storage layer

Integrations:
- Google Search Console API
- Facebook Graph API
- LinkedIn Marketing API
- X API

Possible Tech Stack:
- React dashboard
- Node.js aggregation service
- PostgreSQL for metrics storage
- Redis caching layer

## Risks and Challenges

- API rate limits across analytics platforms.
- Inaccurate attribution without UTM tracking.
- Maintenance overhead of multiple analytics integrations.

---

# Feature 2 – Content Calendar & Scheduling

Domain: Publishing  
Type: Core workflow

## User Story

As a small business owner using Floowe  
I want to schedule articles and social posts for future publication  
So that I can maintain a consistent publishing schedule without manual intervention.

## Acceptance Criteria

- Users can schedule a specific publication date and time.
- A calendar view displays drafts, scheduled posts and published content.
- Scheduled posts can be rescheduled or cancelled.
- Users receive notifications before a scheduled post goes live.
- Failed scheduled posts are retried automatically.

## Business Case

Consistent publishing is essential for SEO growth and audience engagement.  
A scheduling system transforms Floowe from a content generator into a full content operations platform.

## Technical Overview

Components:
- Scheduling module
- Calendar interface
- Background job queue

Integrations:
- Social media APIs
- CMS publishing API
- Email notification service

Possible Tech Stack:
- React + FullCalendar
- Node.js scheduling service
- Redis + BullMQ job queue
- PostgreSQL scheduled jobs table

## Risks and Challenges

- OAuth token expiration for scheduled posts.
- Timezone management for global users.
- Reliability of background job queues.

---

# Feature 3 – Brand Voice & Tone Profiles

Domain: Content Generation  
Type: AI personalization

## User Story

As a marketing agency managing multiple clients  
I want to define brand voice profiles for each client  
So that generated content matches each brand’s tone and style automatically.

## Acceptance Criteria

- Users can create multiple brand voice profiles.
- Profiles include tone, writing style, audience description, and phrase rules.
- A profile can be selected during article generation.
- AI generation respects configured tone and style constraints.
- Users can define a default brand voice profile.

## Business Case

Generic AI-generated content often requires heavy editing.  
Brand voice profiles ensure that generated content matches the intended brand identity, reducing editing time and increasing user satisfaction.

## Technical Overview

Components:
- Brand voice profile management UI
- AI prompt configuration layer
- Profile storage database

Integrations:
- LLM API for content generation

Possible Tech Stack:
- React settings interface
- Node.js prompt builder
- PostgreSQL profile storage

## Risks and Challenges

- LLM models may not fully respect style constraints.
- Increased UI complexity for smaller users.
- Voice consistency may vary after model updates.

---

# Summary

| Feature | Domain | Type | Impact |
|-------|-------|-------|-------|
| Content Performance Dashboard | Distribution | Analytics | Enables data-driven content strategy |
| Content Calendar & Scheduling | Publishing | Core workflow | Improves publishing consistency |
| Brand Voice & Tone Profiles | Content Generation | AI personalization | Improves content quality and brand consistency |
