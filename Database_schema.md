# DebateX — Database Schema

## Overview

DebateX is a real-time debate platform built with Node.js, Express and Socket.IO. This document outlines the proposed PostgreSQL schema for persistent user accounts, debate sessions, arguments and results.

## Tables

### 1. users

Stores registered user accounts.

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| username | VARCHAR(50) | Unique username |
| password_hash | TEXT | Securely hashed password |
| created_at | TIMESTAMPTZ | Account creation time |

### 2. debates

Stores debate session information.

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| room_code | VARCHAR(8) | Unique room identifier |
| topic | TEXT | Debate topic |
| status | VARCHAR(20) | Current debate status |
| created_by | UUID | References users.id |
| created_at | TIMESTAMPTZ | Creation timestamp |
| finished_at | TIMESTAMPTZ | Completion timestamp |

### 3. arguments

Stores messages submitted during debates.

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| debate_id | UUID | References debates.id |
| user_id | UUID | References users.id |
| content | TEXT | Argument content |
| created_at | TIMESTAMPTZ | Submission timestamp |

### 4. debate_results

Stores final debate evaluations.

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| debate_id | UUID | References debates.id |
| winner_id | UUID | References users.id; nullable |
| verdict | TEXT | Final evaluation |
| created_at | TIMESTAMPTZ | Evaluation timestamp |

## Planned implementation

- Integrate PostgreSQL using the Node.js `pg` package.
- Replace in-memory user storage with database queries.
- Persist debate sessions and argument history.
- Save final verdicts and retrieve past debates.
- Keep database credentials in environment variables.

**Status:** Proposed schema; implementation and migration pending.
