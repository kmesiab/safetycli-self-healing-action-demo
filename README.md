# SafetyCLI Self-Healing Action Demo

Demo repository with intentional vulnerabilities to showcase SafetyCLI Self-Healing Action with Copilot integration.

## Overview

This repository demonstrates how the [SafetyCLI Self-Healing Action](https://github.com/kmesiab/safetycli-self-healing-action) automatically detects and helps fix security vulnerabilities in Python dependencies.

## How It Works

1. **Vulnerable Dependencies**: The `requirements.txt` file contains intentionally outdated Python packages with known security vulnerabilities (CVEs)
2. **Automated Scanning**: The GitHub Actions workflow (`.github/workflows/security.yml`) runs SafetyCLI to scan for vulnerabilities
3. **Issue Creation**: When vulnerabilities are detected, an issue is automatically created and assigned to GitHub Copilot
4. **Self-Healing**: Copilot analyzes the vulnerabilities and creates a pull request with updated, secure package versions

## Triggering the Demo

The security scan runs automatically:
- **Daily** at midnight (UTC)
- **On push** to the `main` branch when `requirements.txt` changes
- **Manually** via workflow dispatch in the Actions tab

To manually trigger the demo:
1. Go to the "Actions" tab
2. Select "Security Self-Healing" workflow
3. Click "Run workflow"

## Current Vulnerabilities

The `requirements.txt` contains the following vulnerable packages:
- `django==2.2.0` - Multiple SQL injection and DoS vulnerabilities
- `flask==0.12.0` - Cookie disclosure and DoS vulnerabilities
- `requests==2.6.0` - Credential protection issues
- `pillow==6.0.0` - Buffer overflow and DoS vulnerabilities
- `urllib3==1.24.0` - Decompression bomb and certificate validation issues
- `jinja2==2.10.0` - Security vulnerabilities
- `pyyaml==3.12` - **Critical** arbitrary code execution vulnerability (CVE-2017-18342)

## Expected Behavior

When the workflow runs:
1. SafetyCLI scans `requirements.txt` and detects 30+ vulnerabilities
2. An issue is created with details about the vulnerabilities
3. The issue is assigned to `@copilot` for automated remediation
4. Copilot analyzes the issue and creates a PR with updated package versions
5. The PR can be reviewed and merged to fix the vulnerabilities
