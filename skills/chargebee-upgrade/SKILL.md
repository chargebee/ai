---
name: chargebee-upgrade
description: Migration guide for upgrading Chargebee SDKs to the latest version. Use when (1) migrating or upgrading a Chargebee SDK to a newer major version, (2) modernizing legacy Chargebee SDK usage patterns, (3) updating Chargebee SDK dependencies. Activates when deprecated or legacy Chargebee SDK patterns are detected in any supported language.
---

# Chargebee SDK Upgrade

This skill helps you migrate Chargebee SDK code to the latest version. It detects legacy patterns, suggests migration, and applies transformation rules.

IMPORTANT: Do not auto-apply changes. Always suggest migration first and let the user decide.

## Supported Migrations

| Language | From | To | Min. Runtime | Guide |
|----------|------|----|-------------|-------|
| Java | V3 (3.x.x) | V4 (4.x.x) | Java 11+ | `references/java/v3-to-v4.md` |

## Detection

Scan the codebase for legacy SDK patterns. When detected, inform the user that a migration guide is available.

### Java V3

Look for any of:
- Imports from `com.chargebee.models.*` or `com.chargebee.Environment`
- `Environment.configure(...)` calls
- Static resource method chains ending in `.request()` (e.g., `Customer.create().firstName("x").request()`)
- `Result` or `ListResult` types from `com.chargebee`
- Dependency `com.chargebee:chargebee-java` with version `3.x.x` in pom.xml or build.gradle

When detected, read **references/java/v3-to-v4.md** for the complete migration rules (17 transformation rules), code examples, and verification checklist. Apply the rules precisely, preserving all business logic, comments, and code structure.

## Workflow

1. Detect legacy SDK patterns in the project
2. Inform the user and suggest migration
3. On approval, read the relevant migration guide
4. Apply transformations file-by-file, explaining each change
5. Flag manual review items (e.g., where to create/inject the client instance)
6. Run through the post-migration checklist

## References

- **references/java/v3-to-v4.md** - Complete Java SDK V3 to V4 migration guide with 17 transformation rules, import mappings, code examples, and verification checklist
