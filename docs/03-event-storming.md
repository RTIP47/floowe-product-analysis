# Event Storming – Floowe

This document presents an Event Storming analysis of the Floowe product, identifying the key domain events, commands, actors and external systems involved in the content creation and distribution workflow.

The analysis was initially supported by Claude AI and refined based on previously identified user flows.

---

# Actors

- User
- AI Content Engine (system actor)

---

# Commands

- Register Account
- Save Brand Profile
- Link Social Channels
- Generate Article
- Edit Article
- Attach Image
- Approve Article
- Publish Article
- Distribute Content

---

# Domain Events

## Onboarding Domain
- Account Created
- Brand Profile Saved
- Channels Linked

## Content Generation Domain
- Article Generation Requested
- Draft Article Created

## Editing Domain
- Article Edited
- Image Attached
- Article Approved

## Publishing Domain
- Article Published
- Social Posts Generated

## Distribution Domain
- Social Post Published
- Content Distributed
- SEO Loop Started

---

# External Systems

- AI Content Engine
- Website CMS
- Facebook API
- LinkedIn API
- X (Twitter) API
- Search Engines

---

# Domain Boundaries

## 1. Onboarding
User creates an account, defines brand context and connects social channels.

Key dependency: Channels must be linked before publishing can occur.

## 2. Content Generation
The AI system generates an SEO-optimized draft based on the user command.

The event **Draft Article Created** triggers the rest of the workflow.

## 3. Editing
The user refines the content and attaches images.  
The event **Article Approved** acts as a gate before publishing.

## 4. Publishing
Publishing triggers two processes:

- publishing to CMS
- generation of social posts

These actions may run asynchronously.

## 5. Distribution
Content is distributed across multiple social platforms through API integrations.

Terminal events include **Content Distributed** and **SEO Loop Started**, representing the business outcome of the system.

---

# Event Storming Diagram

![Event Storming](event-storming-floowe.svg)

---

# Open Questions / Hotspots

During event storming analysis, several system design questions were identified:

- What happens if a social media API call fails during distribution?
- Should publishing retries be implemented automatically?
- Is article approval an explicit user action or implicit after editing?
- Should generated social posts be editable before distribution?

These areas represent potential risks and design considerations for future development.
