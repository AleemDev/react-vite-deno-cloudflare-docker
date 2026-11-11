# react-vite-deno-cloudflare-docker
A production-ready boilerplate for a front-end microservice built with React, Vite, and Deno, fully containerized with Docker and pre-configured for edge deployment on Cloudflare Pages using the Wrangler CLI.

## Project Overview

This repository provides a standalone, reusable starter kit for building a Single Page Application (SPA) deployed to Cloudflare Pages. It utilizes Deno as the native TypeScript runtime and package manager in place of Node.js, while keeping local development entirely isolated within Docker. The boilerplate includes local edge emulation to accurately simulate Cloudflare's production routing before deployment.
Tech Stack

* Framework: React initialized via Vite.

* Runtime & Package Manager: Deno (utilizing native npm: specifier compatibility).

* Edge Emulator: Cloudflare Wrangler CLI.

* Containerization: Docker & Docker Compose (using the denoland/deno image).

* Deployment Target: Cloudflare Pages.

## Core Architecture & Configuration

* Dual-Port Docker Environment: The docker-compose.yml mounts the local directory as a volume (.:/app) and maps two distinct ports: one for Vite's rapid Hot Module Replacement (HMR) during code development, and another for Cloudflare's Wrangler emulator.

* Local Edge Emulation: The project defines a pages:dev script in package.json that dynamically executes deno run -A npm:wrangler pages dev dist. This simulates Cloudflare's edge network locally, allowing you to test routing, redirects, and compiled static assets exactly as they will behave in production.

* Permission & Cache Management: The Docker configuration maps to the local host user ("${UID:-1000}:${GID:-1000}") and forces the Deno cache into a local .deno_cache/ directory. This prevents root ownership lockouts on Linux/WSL host machines and ensures fast container restarts.