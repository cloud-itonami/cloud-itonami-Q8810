# cloud-itonami-8810

Open Business Blueprint for **ISIC Rev.5 8810**: social work activities
without accommodation for older persons and persons with disabilities.

This repository designs a forkable OSS business for community care
coordination, check-ins, benefits navigation, caregiver scheduling and
non-residential support operations.

## Core Contract

```text
person-centered plan + consent + service directory + visit/check-in records
        |
        v
Care Support Advisor -> Safeguarding Governor -> task, hold, or escalate
        |
        v
support ledger + caregiver queue
```

The advisor can coordinate support tasks, but cannot hide safeguarding signals,
override consent, or make eligibility/discharge decisions without review.

## Runbook

- Start with consented care plans and synthetic cases.
- Add check-in and task queues.
- Add caregiver and service matching.
- Add safeguarding escalation and audit reports.

See [`docs/business-model.md`](docs/business-model.md) and
[`docs/operator-guide.md`](docs/operator-guide.md).

## License

Code and implementation templates are AGPL-3.0-or-later.
