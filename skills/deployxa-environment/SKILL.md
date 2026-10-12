---
name: deployxa-environment
description: Manage Deployxa project environment variables and domain configurations safely without leaking sensitive secrets.
---

# Deployxa Environment & Configuration Skill

This skill guides ZCode agents through managing environment variables, custom domains, and DNS guidance via Deployxa MCP tools.

## When to use this skill
- When inspecting or setting project environment variables.
- When configuring custom domains and DNS records.
- When checking project readiness or scaling configurations.

## Workflow

### 1. Environment Variable Management
- **List Variables**: Call `deployxa_list_environment` with `projectId`.
  - Notice: Deployxa returns variable keys while securely redacting sensitive secret values.
- **Set Variable**: Call `deployxa_set_environment` with `projectId`, `key`, `value`, and optional `branch`.
  - Secret values passed in tool arguments are safely masked in output logs.
- **Delete Variable**: Call `deployxa_delete_environment` with `environmentId` and `confirmed: true` (deletion is a dangerous action requiring confirmation).

### 2. Custom Domains & DNS
- **List Domains**: Call `deployxa_list_domains` with `projectId`.
- **Add Domain**: Call `deployxa_add_domain` with `projectId` and `domain`.
- **DNS Guidance**: Call `deployxa_get_dns_guidance` with `projectId` and `domain` to output recommended A, CNAME, or TXT DNS records for the user.
- **Verify Domain**: Call `deployxa_verify_domain` once DNS propagation starts.
- **Delete Domain**: Call `deployxa_delete_domain` with `projectId`, `domain`, and `confirmed: true`.

### 3. Domain Search & Purchasing
- **Check Availability & Pricing**: Call `deployxa_check_domain_availability` with `domain` to see if a domain is available and retrieve registration/renewal prices.
- **Get Suggestions**: Call `deployxa_suggest_domains` with `keyword` to discover alternative available domains.
- **Purchase Domain**: Call `deployxa_purchase_domain` with `projectId`, `domain`, optional `durationYears`, and `confirmed: true`.
  - *Important*: Purchasing a domain deducts topped-up organization credits. Always inform the user of the price and get their confirmation before setting `confirmed: true`.
- **List Domain Orders**: Call `deployxa_list_domain_orders` to view registration and transfer order statuses.
- **Renew Domain**: Call `deployxa_renew_domain` with `domain` and `confirmed: true`.
