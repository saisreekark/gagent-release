# gagent (3.2.0)

A terminal coding agent running Gemini and Claude models on Google Vertex AI,
with a native Rust fullscreen TUI and native Rust Vertex transport.
No source code or npm package installation is required — clone and run directly
on `linux-x64` with Node 22+.

Access is restricted to whitelisted `@google.com` LDAP accounts verified via
Google Application Default Credentials (ADC).

## Prerequisites

- **Platform:** `linux-x64` (native Rust TUI and Vertex provider are embedded inside `gagent.mjs` and cached in `~/.gagent/cache/release/` on first run)
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

## Troubleshooting

- **Blocked with "credentials don't identify a verified user account" (or a `*.gserviceaccount.com` address):**
  On a fresh Cloud Workstation without user ADC, authentication falls back to the workstation's metadata service account; this also happens if ADC was created with custom `--scopes` that omitted `userinfo.email`. Run a plain `gcloud auth application-default login` (no custom `--scopes`) and re-check with `node gagent-release/gagent.mjs doctor`.
- **Blocked with `<email> is not on the allowlist`:**
  Confirm you signed into ADC with your whitelisted `@google.com` account (`gcloud auth application-default login`). If your ADC email uses a different domain or alias, ask the release maintainer to include that full email in the next release and `git pull`.
- **Blocked with `couldn't verify your Google LDAP account` (network, proxy, or transient `429`/`5xx`):**
  Retry if transient. If your workstation requires `HTTPS_PROXY`, run with `NODE_USE_ENV_PROXY=1` (for example `NODE_USE_ENV_PROXY=1 node gagent-release/gagent.mjs`). Ensure outbound HTTPS to `oauth2.googleapis.com` and `aiplatform.googleapis.com` is permitted.
- **Blocked with `Google rejected the signed-in ADC credentials`:**
  Your ADC token is expired or revoked. Run `gcloud auth application-default login` and restart `gagent`.
- **`No Google Cloud project id could be resolved` or `404` on the first prompt:**
  Set your project with `gcloud config set project YOUR_PROJECT_ID` (or `export GOOGLE_CLOUD_PROJECT=YOUR_PROJECT_ID`), and ensure `aiplatform.googleapis.com` and **Gemini 4 Neon** in **Vertex AI → Model Garden** are enabled for that project.

## Third-party licences

See [`THIRD-PARTY-NOTICES.txt`](THIRD-PARTY-NOTICES.txt).
