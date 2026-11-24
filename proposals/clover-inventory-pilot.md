# Proposed pilot: useful inventory answers for a local retailer

**Status:** proposed pilot. Clover authorization and adapter scaffolding exists in earlier Ninolex work; the inventory adapter uses placeholders. A working ChatGPT/Codex inventory connection and merchant deployment are not claimed.

## Start with the owner’s question

For an independent Greater Boston retailer, I would first identify one recurring stock question: which items need review, which records look inconsistent, or what should be checked before reordering?

We would use an owner-approved product/stock export and agree the rules together. The first result would be a simple report whose calculations can be checked against the source. ChatGPT could help explain and explore that report; Codex could help me build and test the tool.

## First community day

1. Watch how the owner checks stock today and record the task’s starting time and common errors.
2. Choose one question and prepare a permitted sample without customer or payment data.
3. Build the smallest useful report, retaining item identifiers and the source date.
4. Check calculations and exceptions against the original records.
5. Have the owner repeat the workflow and leave written instructions and a follow-up check.

Stock-on-hand data alone cannot establish sales velocity or an appropriate reorder quantity. Those questions would require additional data and owner-approved assumptions.

## If the first version is useful

Evaluate a merchant-authorized, read-only Clover connection. Clover distinguishes read permissions from write permissions, so the initial scope would retrieve approved inventory information without changing stock, prices, orders or payments. See [Clover’s permission model](https://docs.clover.com/dev/docs/permissions).

The build would need to handle access expiry, incomplete data and refresh failures. Any later write capability would be a separate, explicitly reviewed scope.

## What success would mean

The owner can repeat the task, explain the report and trace its answers to source records. We would compare completion time and errors before and after the pilot. Savings, sales increases and inventory improvements are outcomes to measure, not promises made in advance.

[Portfolio](../README.md)
