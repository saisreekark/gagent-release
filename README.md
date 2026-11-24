# gagent (1.20.1)

A terminal coding agent running Gemini and Claude models on Google Vertex AI.
No source code or npm package installation is required — clone and run directly
with Node 22+.

Access is restricted to whitelisted `@google.com` LDAP accounts verified via
Google Application Default Credentials (ADC).

## Prerequisites

- **Node.js 22 or newer** (pre-installed on Cloud Workstations)
- **Google Cloud CLI (`gcloud`)**
- A **Google Cloud project** with the Vertex AI API enabled and **Gemini 4 Neon**
  (the default model) enabled in **Vertex AI → Model Garden**

## Setup

```bash
# 1. Clone (no npm install required)
git clone https://github.com/saisreekark/gagent-release.git

# 2. Authenticate ADC with your whitelisted @google.com account
gcloud auth application-default login

# 3. Select your GCP project
gcloud config set project YOUR_PROJECT_ID
# (or export GOOGLE_CLOUD_PROJECT=YOUR_PROJECT_ID)

# 4. Verify your account, ADC, and project setup
node gagent-release/gagent.mjs doctor
```

## Usage

Run directly from any workspace folder:

```bash
# Interactive TUI
node /path/to/gagent-release/gagent.mjs

# Or invoke directly
/path/to/gagent-release/gagent.mjs

# Headless one-shot prompt
node /path/to/gagent-release/gagent.mjs -p "summarize this repository"
```

## Updating

When a new release is published, pull the latest build:

```bash
git -C /path/to/gagent-release pull
```

## Third-party licences

See [`THIRD-PARTY-NOTICES.txt`](THIRD-PARTY-NOTICES.txt).
