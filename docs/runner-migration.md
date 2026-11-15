# Local Linux runner migration

## Scope and acceptance

Run every existing Linux x64 workflow job on this computer using
`[self-hosted, Linux, X64, the-bugger-public]`. Preserve events, release conditions,
permissions, deployment environments, artifacts and application checks.
Public jobs run in a dedicated QEMU VM with its own Docker daemon. Each runner accepts one job and the VM disk is discarded before the next registration. Never grant these repositories access to the desktop user runners.

## Phases

1. Provision and verify runner connectivity and required tools.
2. Change routing and run the existing checks on a pull request.
3. Integrate only after review and successful checks. Production publication
   retains its existing triggers; do not create a release to test routing.

## Verification

Validate workflow syntax and execute the existing workflow checks. Confirm
GitHub reports the expected local runner. A skipped deploy does not validate
production credentials or publishing.

## Rollback

Revert the workflow routing commit to restore GitHub-hosted Ubuntu runners.
Do not change published artifacts or application data.
