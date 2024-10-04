---
title: Tugo
publishDate: 2021-10-01 00:00:00
img: https://storage.googleapis.com/jennyencho-website/landing-img/tugo-landing.png
img_alt: tugo-landing
description: |
  Transforming music discovery by connecting you to the beats of those around you.
tags:
  - UI/UX Design
  - Engineering
---

## Context

> Transforming music discovery by connecting you to the beats of those around you.

### Background

Have you ever walked through a beach or park and wondered what people are listening to in their earbuds? Tugo is a mobile application designed to answer that curiosity by making music-sharing with others more transparent and social.

### Team

This project began in October 2021 as part of UCLA DevX's 2021 Fall Project Cycle. Originially named Retune, I joined the team as a founding UI/UX designer and developer. I collaborated with 1 fellow designer Emily, 3 frontend developers (Angelina, Leslie, Liah), 2 backend developers (Nathan, Sanya), and product manager (Jake).

Ultimately, as Retune came to an end, I decided to continue working on this project, renaming it Tugo. I formed a new team of two alongside fellow developer and colleague Nastazia Coronado.

### Problem

Retune was inspired by a common user curiosity: "What songs are the people around me listening to?" My team and I saw the opportunity to transform this question into a unique music discovery experience for the UCLA community, where students can easily view the songs other students are currently listening to. However, the team wanted to go beyond a simple music feed.

### Observation

#### Connecting with people in a large space is hard.

Students want to socialize with other students before honing in for the academic year. However, connecting with new people in a large space, like UCLA, can be quite intimidating.

#### People like to be in-the-know.

Inspired by a popular tiktok trend, where influencers ask nearby strollers in an area what song they were listening to, I wondered if people around me were also naturally curious about other peoples' whereabouts.

### Proposal

Based on these observations, my team and I envisioned Retune as a music exploration and discovery platform that would enable students to connect and foster new musical connections with the people around them. This app would allow users to see what others around them are listening to and explore a diverse mix of songs from those nearby. With this concept in mind, I initiated the research process.

## Research

### Competitive Analysis

First, I conducted an analysis on four existing music platforms — Spotify, Apple Music, SoundCloud, and YouTube Music. This revealed a gap: none of these platforms offered an easy way to share music with people nearby.

### Contextual Inquiry

My next priority was to gather some thoughts about our concept from the students around me. I reached out to the UCLA community first to understand students' music-listening preferences. Additionally, I reached out to students outside of UCLA, as well as non-students, to hear as many diverse perspectives possible.

### Affinity Mapping

Given the responses of +200 interviewees, I used an affinity map to identify common themes and tackle actionable insights. This approach revealed several distinct categories of feedback.

### Key Insights

#### People worry about use of personal information when signing up for new social platforms.

Although many people were fond of the idea, they were also concerned with how their personal information would be used and displayed with Tugo.

#### People have an innate curiosity about others around them.

People are curious about what the people around them are doing, including what songs they are listening to.

#### People want to explore new music genres.

People are open to exploring new music genres regardless of their preferences, but do not know where to look.

### Key Solutions

#### Discover new songs privately or publicly.

Users will have public and private viewing options to make the music discovery experience accessible for all users with varying preferences.

#### Access songs that other Tugo users nearby are listening to.

Users can see what songs other Tugo users are listening to, as well as their recent music activity if they want to share it.

#### Allow users to listen to songs for a few seconds.

Users can only listen to up to 30 seconds of a song to maximize the music discovery experience as much as possible for people on the move.

## Design Process

### Low-Fi Wireframes

To jumpstart the design process, I created low-fidelity wireframes to provide the engineering team with a basic framework while the design team synthesized user insights and refined the visual elements.

### Style Guide

Creating a style guide was a challenging but essential step before diving into high-fidelity designs. I identified many inconsistencies in key design components from Retune. I developed a UI style guide to ensure that components were styled consistently throughout the app. Inspired by the blue summer skies of Los Angeles, this style guide was intended to reflect that aesthetic.

### Usability Testing

Starting with the old Retune designs, I created a working prototype and recruited 20 participants to test it. I decided to use Figma's prototype feature due to the cost of our other option, Maze. While Figma had some limitations compared to Maze, I recieved valuable feedback on our current designs.

### Feedback

#### Remove the close friends and public viewing maps.

While participants appreciated the public and private viewing options with the close friends and public maps, I identified a significant UX flaw: these options should apply to the user, not the map. A striking 60% of the participants chose the close friends map over the public map, and nearly half expressed no preference. There was essentially no difference between the two maps.

Instead of two maps, I introduced a feature in the user's profile settings that allows users to selectively share personal information with the public.

#### Scrap the followers feature.

Many participants noted that the follow button felt out of place, making the app feel more like a social network than a music discovery platform. Moreover, the profile view of other Tugo users, along with their profile handles, made it difficult to access the play button and gave the cluttered appearance.

#### Share less on the music tab.

One key feature my Retune team developed was the user music tab, which displays a user’s current song, favorite albums, and artists. However, only 20% of participants fully explored it, and 80% found it too cluttered, hindering their discovery experience. To address this, I streamlined the music tab to focus on song shuffling and added a profile view for detailed music activity.

This led me to conclude that it is better to keep all users' information hidden during the song shuffling process to preserve the focus on music exploration and discovery as much as possible.

### Flow Chart

Given our feedback, I revised Tugo's flow chart and took into consideration new features to replace old and obsolete ones. This process further helped to breakdown the essential features and steps of building Tugo, allowing my team and I to set milestones seamlessly.

## Final Work

### Onboarding

Users are initially greeted with a log in/sign up portal where they can customize their profile from start to finish. Users must enable location permissions, unless Tugo cannot work.

### Song Shuffle

When a user clicks on a vinyl icon on the map, another user's current song appears on the song tab, which can be expanded to show other recently played songs. Users can also shuffle through nearby songs via the shuffle icon, enabling music discovery while maintaining privacy.

### Playlist Creation

If users like what they find, they can add the song to a playlist! Simply press the plus icon on the music tab and follow the playlist creation process.

### Profile Visibility

The close friends and public maps are a thing of the past! Now, all users are placed on a public map, but they can choose what to share with other Tugo users – such as profile photo, name, playlists, and song history. In return, everyone must share their currently playing song with the public.

## Impact

### Outcome

Since its inception, Tugo has reached the hearts and earbuds of the UCLA community. From usability testing from the design team to the marketing team that helped bring Tugo widespread to the UCLA campus, Tugo has helped 200+ students discover and engage with new music from artists they did not know. Tugo aims to contribute to a broader movement of supporting and promoting diverse music genres and enriching users' listening experiences.

Tugo has undergone many changes since its inception both in design and technical toolkit. As Retune came to a close, I was determined to revamp this project from scratch. As of May 2024, our top priority is to build Tugo with new designs in consideration.

### Reflections

#### Stay proactive with the latest technology.

This project truly emphasized the importance of staying current in design and tech. Redesigning features was challenging, but my background in software development and design helped me quickly adapt, revealing the growing connection between the two fields. On the design side, I mastered Figma’s new prototyping and dev tools. On the tech side, I discovered frameworks and libraries that can enhance Tugo’s codebase. Tugo is headed in an exciting direction, and I’m eager to continue working on it and see where it leads!

#### It's okay to steer projects in a different direction.

My time at Retune was invaluable. Diving into UI/UX design and frontend development with a project serving the UCLA community was a rewarding experience, but I often felt frustrated by the communication gap between the designers and engineers. Since Retune was an engineering-heavy project, I found myself redesigning many features and UIs to match the engineering team's capabilities, even when they weren't the best design choices.

Revamping this project as Tugo with a team I built—just as my product manager did with Retune—has been an exciting new path. With this shift, I’m giving design a voice in all engineering decisions while giving myself and my project partner Azia the space to explore new technologies that enhance our engineering capabilities.
