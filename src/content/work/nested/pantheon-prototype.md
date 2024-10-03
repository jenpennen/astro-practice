---
title: Pantheon Prototype
publishDate: 2011-03-04 00:00:00
img: https://storage.googleapis.com/jennyencho-website/landing-img/pantheon-prototype.png
img_alt: pantheon-prototype
description: |
  Securing and scaling identity management with Keycloak and Kubernetes.
tags:
  - Design
  - Engineering
---

## Context

### Background

At Develop For Good (DFG), the need for robust, scalable, and secure identity management solutions became paramount as more and more nonprofit clients and students were seeking DFG for technical opportunities and services. Unlike most non-profit organizations, DFG focuses on new technology that allows for novel ways to serve their clients and student volunteers. With this comes with a demand to upgrade their internal infrastructure as well.

### Purpose

This demo illustrates how modern identity and access management solutions can be seamlessly integrated with many services used by DFG. Specifically, it showcases:

- The integration capabilities of Keycloak with other applications using the OpenID Connect protocol.
- The advantages of using Kubernetes for managing and scaling application infrastructure.

## Demo

### Keycloak

Keycloak is an open-source identity and access management platform developed by Red Hat. It provides robust security features that seamlessly integrates authentication and authorization mechanisms into applications and services. Used widely by many companies, such as Bosch and Deloitte, some key features of Keycloak include single sign-on (SSO), user federation, centralized management, and the admin console. All of these features will be essential for DFG's infrastructure as it scales.
![keycloak]

### Penpot

Penpot, developed by Kaleidos Open Source, is an open-source design and prototyping tool, similar to Figma. Unlike other design tools, Penpot is web-based and platform-independent, and thus can be used on any operating system. Penpot is an excellent design tool for designers, making it a great example of an application that can be integrated with Keycloak in the future.

### Key Takeaways

#### Identity Management

Keycloak manages user identities, roles, and permissions, ensuring secure access to applications.

#### Scalability

The scalability and flexibility of using Kubernetes to deploy and manage applications makes it possible to horizontally scale and seamlessly adapt to changing organizational needs.

#### Future-Proofing Infrastructure

This setup can be future-proofed, making it easier for DFG to adapt and scale their infrastructure in response to envolving demands.

## Impact

I was excited to learn that this demo was well-received during Mary’s meetings with funders and technology pioneers such as Kevin Gibbs. In August 2023, I, along with fellow DFG engineer Anish Sinha, proposed new tech initiatives for Develop For Good directly to founder Mary Zhu. Since then, Anish and I have joined Develop For Good as staff software engineers, focusing on internal cloud and AI technologies. Most recently, we developed a unified data management tool called Pantheon, designed to streamline key lifecycle tasks at DFG, and published a paper with Okta during the process.
