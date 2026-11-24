# Ojanaa: invoices, receipts and commerce foundations

**Status:** private implementation; merchant rollout and current end-to-end production readiness are unverified.

[Project documentation](https://github.com/iamnortey/ojanaa-docs) · [Portfolio](../README.md)

## The problem

Small sellers need clear records of what was ordered, what they have confirmed and what the customer should receive. Ojanaa explores these needs through a commerce workflow designed around invoices and receipts.

## What exists

The implementation includes invoice and **seller-confirmed receipt** workflows. Development records also describe inventory, reporting and customer-management database foundations. These foundations are not presented as complete customer-facing features.

The core approach separates a seller’s confirmation from an independent payment-provider verification. That distinction matters: a status in a seller workflow is not, by itself, proof that money has settled.

Earlier architecture and demo records describe broader WhatsApp, payment and POS ambitions. Those records should be read as design/development context, not certification of a live payment service. This summary supersedes earlier broad production claims and unverified scale metrics.

## Why it is relevant to US retailers

The transferable work is organizing products, invoices, status changes and reporting so a small team can understand them. I would begin with the owner’s existing process and tools before choosing which parts to automate.

A separate [proposed Clover/POS inventory pilot](../proposals/clover-inventory-pilot.md) applies that experience to a read-only stock-review workflow. Ojanaa itself is not a deployed Clover integration.

**My role:** product direction, implementation, data-model and workflow decisions, review and documentation, using AI coding tools as development partners.
