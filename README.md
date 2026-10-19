# Artifact Freshness Guard

SHA-256 fingerprints that invalidate proof when artifacts change.

Standalone ES module. No npm install required. Works in **Node.js 20+** and modern browsers (serve over HTTP for browser demos).

## Install / import

Copy the files into your project, or clone this repository:

```js
import { fingerprint,checkFreshness } from './artifact-freshness-guard.js';
const evidence={artifactId:'invoice.json',fingerprint:await fingerprint('{"total":42}')};
const artifacts={'invoice.json':'{"total":99}'};
console.log(await checkFreshness(evidence,artifacts)); // fresh: false
```

## Use cases

### 1. Catch edits made after verification

- **Scenario:** A previously verified invoice is changed before delivery.
- **Outcome:** Compare its current SHA-256 hash to recorded evidence and invalidate the old result.

### 2. Guard a release handoff

- **Scenario:** A build is tested before being copied to another environment.
- **Outcome:** Check exact artifact identity before reusing its test evidence.

## Exports

- `fingerprint`
- `checkFreshness`
- `createArtifactFreshnessGuard`

## Notes

- Keep API keys and secrets out of this module and out of browser storage.
- Treat verification callbacks, ledger writers, and permission checks as trusted application code.
- This library is intentional local reliability plumbing, not a claim of cryptographic attestation unless stated in the source comments.

## License

MIT
