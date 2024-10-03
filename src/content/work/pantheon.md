---
title: Pantheon
publishDate: 2024-06-02 00:00:00
img: https://storage.googleapis.com/jennyencho-website/landing-img/pantheon-landing.png
img_alt: Iridescent ripples of a bright blue and pink liquid
description: |
  Powering nonprofit volunteer management with seamless tech integration.
tags:
  - Design
  - Engineering
---

## Context

> Powering nonprofit volunteer management with seamless tech integration.

### Background

<a href="https://www.developforgood.org/">Develop For Good (DFG)</a> is a 501(c)(3) nonprofit organization that empowers underserved and underrepresented college students by providing opportunities to work on real-world technical projects for nonprofits. Founded in March 2020 by Stanford students Mary Zhu and Amay Aggarwal, DFG was established to support nonprofits struggling with digital access during the COVID-19 pandemic, and to provide opportunities for students to engage in meaningful tech-focused volunteer work.

### Observation

#### Develop For Good operates in four-month project cycles twice a year.

Volunteers are placed in teams focusing on technical projects in web/mobile development, data engineering, and UI/UX design, with each team consisting of at least 8 volunteers.

#### An increasing number of students and nonprofits are turning to DFG for technical opportunities and services.

An increasing number of students and nonprofits are seeking technical opportunities and services from DFG. Despite this rising demand, DFG can currently support around 35 nonprofit clients per cycle.

### Problem

#### Develop For Good needs a dedicated cloud environment.

Develop For Good currently operates without a dedicated cloud environment for its services, resulting in user fragmentation. This limitation makes it difficult to securely manage and store data specific to both volunteers and nonprofit clients, highlighting the need for a more robust, centralized system.

#### DFG's onboarding/offboarding processes limits scalability.

The onboarding and offboarding processes at Develop For Good is labor-intensive, with Program Director Amanda Lo manually managing over 400 volunteers and clients each project cycle on DFG's social platforms. This time-consuming task limits DFG's ability to scale efficiently with its current infrastructure.

> With the scale of our programs surpassing the manual capacity of our staff, how might we manage program lifecycle tasks seamlessly and securely?

### Goals

#### Automate the onboarding/offboarding process for all project cycles.

Instead of manually inviting every new volunteer onto DFG's platforms, we can invite volunteers in bulk.

#### Determine what services the management team needs to handle lifecycle tasks.

The management team also relies on other lifecycle tasks to ensure that each cycle operates seamlessly. Understanding what services are needed to interact with both volunteers and clients were crucial.

## Research

### Existing Solutions

Nonprofits have already been using a variety of platforms for volunteer management, with popular solutions including VolunteerHub, Bloomerang, and Point. However, none of these out-of-the-box products had the specific app integrations and project management features we need for our unique program, as they integrated poorly with our existing and working infrastructure.

### DFG's Approach

Pantheon is a tool we conceptualized a year ago and initiated in January of 2024. Our vision was clear.

#### Unified Management Platform

Build a unified management platform for DFG capable of handling all client lifecycle tasks seamlessly.

- We noted this
- And also this other point

#### Central Data Hub

Establish a central hub for hosting and bridging data between disparate apps and services, from user management to custom AI models.

As a starting tool, our top priority, as of now, is functionality.

### Okta Single Sign-On (SSO)

Enter Okta. Our partnership with Okta for Good was instrumental in facilitating access to a potent tool: Okta Workforce Federation. This workflow was straightforward. Upon a volunteer’s acceptance to a project cycle, they are added to an Airtable sheet. Afterwards, a lambda is triggered to create all volunteers in our Okta tenant’s universal directory.

However, this plan fell short when we discovered that Single Sign-On (SSO) integration was an enterprise feature in platforms like Slack, Figma, and Notion. Despite our paid business and pro plans, we lack the resources for enterprise-level subscriptions, rendering our Okta-based solutions unviable. We were back at square one.

### Square One: Google For Nonprofits

Currently, the only volunteers issued Develop for Good handles (@developforgood.org) are product leads and management team members.

However, the Google for Nonprofits plan allows up to 2,000 users. Although it can’t scale forever, we are hardly using a fifth of its total capacity. When we eventually reach this threshold, we could potentially pay for SSO capabilities for the essential services we rely on. Until then, we decided to build Pantheon around Google Workspace. This concept is simple: accept students, upload their information to Workspace (and issue them @developforgood.org emails), monitor the email allocations, and delete them at the end of each cycle to free up space in Workspace.

This streamlined approach not only manages user accounts and their life cycles, but also ensures controlled access to services since every service we rely on has complimentary SSO for Google. With this plan in motion, we started building.

## Tech Process

### Airtable

Our foundation was Airtable. To facilitate executive access and data management, we needed a solution to bridge Airtable and Google Workspace seamlessly. Although no first-party integration met our requirements, this wasn’t a setback, as we were prepared to build everything from scratch.

![Pantheon Architecture](https://storage.googleapis.com/jennyencho-website/pantheon-img/pantheon-architecture.png)

We constructed an adapter mechanism which would recognize valid base structures in Airtable, and a frontend capable of creating and presenting read-only views from these bases. We then integrated various functionalities into different view types, each tailored to specific internal classifications. For instance, user views enable the export of users to Workspace. With this dashboard, crafted with TypeScript and React, our executives can log in, generate custom views pulling data from Airtable, and export users. We also utilized ShadCN/UI and TailwindCSS to craft an aesthetically pleasing UI that prioritizes user-friendliness, intuitiveness, and accessibility. Authentication was seamlessly managed through Auth0, an Okta product, bringing our project full circle.

### Backend

We used Rust for our backend. Our goal was to build a maintainable codebase which would compile to a small binary that could be easily deployed on a server or Kubernetes cluster, and horizontally scaled. Drawing from past experiences, we ruled out Go (over Rust) due to previous challenges. We used Axum as our backend web framework because it is lightweight and had excellent mechanisms for dependency injection. In selecting our database and cache solutions, we settled on PostgreSQL and Redis respectively as they are battle-tested technologies that were well-suited for our requirements. PostgreSQL is used to store views, keep track of exported users, and manage data regarding asynchronous jobs, such as export and import tasks. During development, we utilize Docker to spin up a database, while for production, we use an RDS t1.medium instance on AWS that fits our needs nicely.

### Challenges

#### Rate Limits

Airtable’s API imposes a maximum of 5 requests per second and returns only 100 records per request when fetching data. To circumvent these limitations without causing our API endpoint to block, we did three things. Firstly, we built a framework for asynchronous, cancellable tasks. Upon receiving a request, we return and initiate an asynchronous job. Job metadata is stored in PostgreSQL, and in the Pantheon UI, a window displays information about jobs associated with the view, categorized as complete, pending, error, or canceled.

This approach was powered by Tokio’s task functionality. Tokio is the asynchronous runtime we chose for our API and has the capability to run blocking tasks on a separate thread pool so as to not block the API. This solution ensures our API remains non-blocking while managing rate limits by launching tasks with artificial delays and retry mechanisms as needed.

Second, we lazily loaded the views. Rather than loading all the data at once, we waited until it was requested by a team member. Lastly, (and most importantly), we created a server-less function on AWS Lambda which is called by an Airtable automation we set up as a JavaScript script.

### Caching

Requests to Airtable often took considerable time (5 - 15 seconds), causing the UI to feel sluggish. Moreover, concerns about stale data persisted as new volunteers were added and accepted at DFG over time, which would invalidate the cache. To address this, we used our asynchronous job framework to schedule periodic data refreshes every few hours, with a manual refresh button in the UI for immediate updates.

This solution, although not perfect, allows our management team to ensure data accuracy by triggering a refetch when necessary, with a cooldown mechanism in place to prevent hitting rate limits. Thus far, this approach has proven effective, given our modest management team size and infrequent data synchronization issues.

## Final Work

### Dashboard View

DFG management members can create dashboard views extracted from DFG's Airtable bases. Each dashboard view contains information, specifically lists of volunteers, clients, and mentors, pertaining to a specific project cycle.

![Dashboard View](https://storage.googleapis.com/jennyencho-website/pantheon-img/pantheon-architecture.png)

Each dashboard view is tailored to specific internal classifications. With this dashboard below, crafted with TypeScript and React, our executives can log in, generate custom views pulling data from Airtable, and export users.

![Dashboard View](https://storage.googleapis.com/jennyencho-website/pantheon-img/pantheon-architecture.png)

### Job Management

DFG management members can export and import user data between Airtable and Pantheon seamlessly. They can also manage individual user information directly from the dashboard view, including adding and removing details. These dashboard displays these tasks in the UI, categorized by status: complete, pending, error, or canceled. This categorization helps streamlines updates and organization of DFG member data, ensuring accurate and efficient data management.

![Dashboard View](https://storage.googleapis.com/jennyencho-website/pantheon-img/pantheon-architecture.png)

### Airtable Automation

We created a server-less function on AWS Lambda which is called by an Airtable automation we set up as a Javascript script. Whenever a record is created, edited, or deleted, that lambda is triggered and notifies our system.

![Dashboard View](https://storage.googleapis.com/jennyencho-website/pantheon-img/pantheon-architecture.png)

## Impact

### Outcomes

As of now, we have a complete tool. We are currently running alpha tests on a student project team in our Summer 2024 cycle, and aim to roll the tool out for every team starting in our subsequent batch very soon.

### Next Steps

#### Design additional functionalities.

We're approaching Pantheon as a central platform to house custom AI models and features to further accelerate and personalize the end-to-end project development experience.

#### Streamline beneficiary intake.

We hope this key piece of software will help make it possible for DFG to scale our capacity indefinitely. As a tech nonprofit and startup that develops digital solutions for other nonprofits, we hope to continue contributing to the nonprofit sector with our learnings and insights.

### Reflections

#### Give back to your community.

One of the most rewarding aspects of my work with DFG was the enrichment I felt throughout the process. Contributing to an initiative that positively impacts hundreds of nonprofits and students has truly been a fulfilling experience. In many ways, creating Pantheon (and MelodyAI) was my way of giving back to an organization that has given me so much. At DFG, I've met some of the brightest and most ambitious people whose work ethic and life lessons inspire me to keep learning and pushing forward, even during the toughest challenges.

#### Be confident and run with it.

Pantheon highlighted the importance of confidence, especially when presenting new ideas. I stepped out of my comfort zone when Anish and I first pitched this project to Mary in August 2023. With Anish's support, I found the courage to propose and defend our ideas. What started as a work in progress has grown into something much bigger, ultimately turning into a project garnering $1M+ in funding from investors for DFG! This is a lesson I'll carry with me in my life and career.

A big thank you to the Okta for Good team for championing Develop for Good and for their continued support and advocacy of DFG's mission, programs, and technological innovations!
