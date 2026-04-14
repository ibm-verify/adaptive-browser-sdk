# Security Policy

## Vulnerability Status

### ✅ Fixed Vulnerabilities

#### 1. bn.js Infinite Loop (GHSA-378v-28hj-76wf) - FIXED
**Severity**: Moderate
**Status**: ✅ Resolved
**Fix**: Added npm overrides to ensure bn.js >= 4.12.3 or >= 5.2.3

#### 2. yargs-parser Prototype Pollution (GHSA-p9pc-299p-vxgp) - FIXED
**Severity**: Moderate
**Status**: ✅ Resolved
**Fix**: Updated babel-minify to 0.6.0-alpha.9 which uses secure yargs-parser version

#### 3. brace-expansion Process Hang (GHSA-f886-m6hf-6m8v) - FIXED
**Severity**: Moderate
**Status**: ✅ Resolved (in demo directory)
**Fix**: Updated @ibm-verify/adaptive-browser to 1.7.0 and added overrides

### ⚠️ Known Vulnerabilities (Awaiting Upstream Fix)

#### Elliptic Cryptographic Primitive Issue (GHSA-848j-6mx2-7j84)

**Status**: Awaiting upstream fix
**Severity**: Low
**Published**: January 8, 2026
**Affected Package**: `elliptic@6.6.1` (transitive dependency via `browserify`)

##### Description
The elliptic package uses a cryptographic primitive with a risky implementation. This is a transitive dependency introduced through:
- `browserify@17.0.1` → `crypto-browserify` → `elliptic@6.6.1`

##### Current Mitigation
- ✅ Updated `browserify` to the latest version (17.0.1)
- ✅ Added npm overrides configuration in `package.json` to automatically use newer versions when available
- ✅ Monitoring the elliptic repository for security patches

##### Next Steps
As of April 2026, there is no patched version of elliptic available in the npm registry. The latest version is 6.6.1, which contains the vulnerability. Once a patched version (6.6.2 or later) is released, run:

```bash
npm install
```

The overrides configuration will automatically use the newer, patched version.

##### Risk Assessment
This is classified as a **LOW severity** vulnerability. The risk is minimal for this SDK as:
1. The SDK is used in browser environments
2. The cryptographic functions are used by browserify's build-time bundling process
3. No direct cryptographic operations are exposed to end users

## Package Overrides Configuration

The following npm overrides are configured in `package.json` to ensure secure versions:

```json
"overrides": {
  "elliptic": ">=6.6.1",
  "bn.js": "^4.12.3 || ^5.2.3",
  "yargs-parser": ">=13.1.2"
}
```

## Reporting Security Issues

If you discover a security vulnerability in this project, please report it to verify@au1.ibm.com.