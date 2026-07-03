# Operator Guide

## First Deployment

1. Define consent, role and safeguarding rules.
2. Register synthetic people, caregivers and services.
3. Run check-in workflows in assisted mode.
4. Review escalation behavior with staff.
5. Publish a redacted workload and outcome report.

## Minimum Production Controls

- consent record
- role-based access
- safeguarding escalation path
- caregiver workload audit
- data-retention policy

## Day in the Life: working a case through the loop

This walks one real case through the intake → propose → approve → execute →
audit loop this blueprint runs on (README Core Contract). The occupation is
community care coordination (ISIC 8810) — the case below is a concrete
aging-in-place check-in, not an abstract "task."

1. **Intake.** Case 014 enters the queue: Mr. Sato, 78, aging-in-place,
   flagged for a wellness check-in after his caregiver co-op reported a
   missed medication pickup. The case is only a case because a consented
   care-plan record already exists for him — no consent, no case (Trust
   Controls: "consent and purpose limitation").
2. **Propose.** The Care Support Advisor proposes the concrete support task:
   send the check-in robot (or a caregiver) to Mr. Sato's home to confirm
   medication adherence, check on him, and log the visit — plus, this round,
   route his open co-op report through as a safeguarding signal rather than
   folding it quietly into the routine visit.
3. **Approve — the Safeguarding Governor sign-off.** Before the robot or
   caregiver may act, the task goes through the Safeguarding Governor's
   decision rule (see [business-model.md](business-model.md#safeguarding-governor-decision-rule)):
   is there a consent record on file, is this a `:high`/`:safety-critical`
   in-home action, and — critically — does the missed-medication report look
   like a safeguarding signal that must escalate rather than close quietly?
   The governor either clears the visit as a routine task, or holds it and
   escalates to a human reviewer. The advisor cannot decide this for itself.
4. **Execute.** Once cleared, the visit happens: the robot or caregiver
   performs the check-in, confirms medication, and the visit is logged to
   the support ledger; the caregiver queue advances to the next case.
5. **Audit.** The visit and any escalation are written to the auditable
   workload/visit record (Trust Controls: "caregiver workload and visit
   records are auditable"). At period end this feeds the redacted workload
   and outcome report (Offer: "outcome and workload reporting").

**The safeguarding-alert case.** Not every case is routine. If the check-in
turns up something sharper than a missed refill — e.g. signs of neglect or a
risk to Mr. Sato's safety — that case is a safeguarding alert: it still goes
through the exact same office sign-off (no shortcut, no standing exemption),
but it counts at higher weight in workload/outcome accounting because it
represents materially higher risk and reviewer effort than a routine visit.

**The violation case — what "skipping the sign-off" actually means.** If an
operator or the advisor closes a case (marks the visit complete, discharges
the case, or reports the safeguarding signal as resolved) without the
governor's sign-off, that is exactly the invariant this business exists to
prevent: an unreviewed eligibility/discharge decision, or a hidden
safeguarding signal (Trust Controls). It is a certification failure, not a
process shortcut — see Certification below.

### Feel the loop hands-on: the playable prototype

`network-isekai` ships a playable prototype of this exact loop at
`/itonami/care-coordination` (`gftdcojp/network-isekai`,
`public/games/itonami/care-coordination/`): you move a coordinator around a
depot of 8 case sites plus one rarer safeguarding-alert case. You must brief
at the "office" first — that's the safeguarding-governor sign-off, the same
`equipped` gate described above — before you're allowed to close a case;
close a case unequipped and it's scored as unsafeguarded (you lose a life).
The safeguarding-alert case is worth 3x a routine case but requires the
identical sign-off — mirroring the higher-weight-but-same-gate treatment
above. It's a fast way for a trainee operator to internalize "the sign-off
comes before the close, every time, no exceptions" before touching a real
caseload.

## Certification

Certified operators must prove safeguarding escalation, consent handling and
human review for eligibility, risk and service discontinuation decisions.
