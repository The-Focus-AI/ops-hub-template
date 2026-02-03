# Acme Corp - Client Overview

**Status**: Phase 1 - Core Platform Development
**Health**: Excellent
**Last Updated**: 2026-01-15

---

## Contact

| Name | Role | Email | Notes |
|------|------|-------|-------|
| Jane Smith | CTO | jane@acmecorp.com | Primary point of contact |
| Bob Johnson | PM | bob@acmecorp.com | Day-to-day coordination |

---

## Overview

Acme Corp is building an analytics dashboard for their manufacturing operations. We're developing a real-time monitoring system that integrates with their existing ERP (SAP) and IoT sensor network. The goal is to reduce downtime by 30% through predictive maintenance alerts.

---

## Scope & Phases

| Phase | Description | Amount | Status |
|-------|-------------|--------|--------|
| Phase 0 | Assessment & Architecture | $5,000 | Complete |
| Phase 1 | Core Platform (Dashboard + API) | $15,000 | Active |
| Phase 2 | Predictive Analytics | $12,000 | Planned |
| Phase 3 | Mobile App | $8,000 | Future |

---

## Repositories

| Repo | Description |
|------|-------------|
| `acme-dashboard` | Next.js dashboard frontend |
| `acme-api` | FastAPI backend + data pipeline |

---

## Revenue

| Invoice | Amount | Status | Date |
|---------|--------|--------|------|
| #1 - Phase 0 Assessment | $5,000 | PAID | 2025-12-15 |
| #2 - Phase 1 Core (50%) | $7,500 | PAID | 2026-01-10 |
| #3 - Phase 1 Core (50%) | $7,500 | OUTSTANDING | 2026-01-30 |

---

## Technical Notes

- **Stack**: Next.js 15, FastAPI, PostgreSQL (Supabase), deployed on Vercel + Fly.io
- **Integrations**: SAP S/4HANA REST API, MQTT for IoT sensors
- **Auth**: Clerk with SSO for their corporate accounts
- **Key decision**: Chose Supabase Realtime over custom WebSocket for live sensor data

---

## Meeting Notes

See `meetings/` directory for transcripts.

Recent meetings:
- 2026-01-13: Kickoff Phase 1 - agreed on 4-week timeline, Jane reviewing wireframes
- 2026-01-08: Phase 0 review - architecture approved, SAP access granted
