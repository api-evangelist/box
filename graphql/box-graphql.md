# Box GraphQL Schema

## Overview

This directory contains a conceptual GraphQL schema for the Box cloud content management platform. Box exposes a REST API (v2) at `https://api.box.com/2.0`. The schema in `box-schema.graphql` translates that REST surface into a typed GraphQL layer covering the full breadth of Box platform capabilities.

## Provider

- **Name:** Box
- **Developer Portal:** https://developer.box.com/
- **API Reference:** https://developer.box.com/reference/
- **GitHub:** https://github.com/box
- **Base URL:** `https://api.box.com/2.0`
- **Auth Base URL:** `https://account.box.com/api/oauth2`

## Schema Source

**Source:** Conceptual — derived from the Box REST API v2 reference documentation and OpenAPI specifications contained in this repository.

## Type Summary

The schema defines **75 named types** organized across the following domains:

| Domain | Types |
|---|---|
| Core Content | File, FileVersion, FileRequest, FileLock, Folder, FolderLock, FolderItemsPage, LockedOperations, WebLink, PathCollection |
| Watermarks | Watermark, WatermarkDetails, WatermarkInfo |
| Collaboration | Collaboration, CollaborationAllowlistEntry, CollaborationAllowlistExemptTarget, AcceptanceRequirementsStatus, TermsOfServiceAcceptanceStatus, StrongPasswordStatus, TwoFactorAuthStatus |
| Permissions | Permission, SharedLinkPermissions, SharedLinkPermissionsInput, GroupPermissions |
| Shared Links | SharedLink, SharedLinkSettings |
| Users & Identity | User, UserProfile, EmailAlias, Avatar, AvatarUrls, TrackingCode, Enterprise, Invite |
| Groups | Group, GroupMembership |
| Metadata | Metadata, MetadataParent, MetadataTemplate, MetadataField, MetadataFieldOption, MetadataQuery, MetadataQueryOrderBy, MetadataCascadePolicy, FileMetadataUpdate |
| Comments & Tasks | Comment, Task, TaskAssignment, TaskAssignmentPage |
| Events | Event, EventSource, EventStream |
| Collections | Collection, CollectionItem |
| Search | Search, SearchResult, DateRange, SizeRange, MetadataFilter |
| Classification | Classification |
| Legal Hold | LegalHoldPolicy, LegalHoldAssignment, LegalHoldAssignmentCounts, LegalHold |
| Retention Policy | RetentionPolicy, RetentionAssignmentCounts, RetentionPolicyAssignment |
| Sign Requests | SignRequest, SignRequestSigner, SignerDecision, SignInput, SignPrefillTag, SignFiles, SignFile, Template, TemplateSigner, ReadySignLink, CustomBranding |
| Auth / Tokens | OAuth2Token, AccessToken, FileScope, RefreshToken, Session, DevicePin |
| Terms of Service | TermsOfService, Term, TermsOfServiceAcceptance |
| Storage Policies | StoragePolicy, StoragePolicyAssignment |
| Webhooks | Webhook, Trigger |
| SKU / Capabilities | SKU |
| Shield / Info Barriers | InformationBarrier, InformationBarrierSegment, InformationBarrierSegmentMember, InformationBarrierSegmentRestriction, InformationBarrierReport, InformationBarrierReportDetails |
| Root Operations | Query, Mutation |
| Enums | AccessLevel, CollaborationRole, CollaborationStatus, TaskAction, TaskResolution, TaskAssignmentStatus, RetentionPolicyType, RetentionPolicyDispositionAction, SignRequestStatus, SignRequestSignerRole, WebhookTrigger, UserStatus, GroupRole, MetadataFieldType, EventType, TermsOfServiceType, TermsOfServiceStatus, LegalHoldPolicyStatus |
| Scalars | DateTime, JSON, Upload |
| Input Types | SharedLinkSettingsInput, FileMetadataUpdateInput, MetadataFieldInput, MetadataFieldOptionInput, TrackingCodeInput, SignRequestSignerInput, SignFileInput, SignPrefillTagInput, MetadataFilterInput, SearchOptions |

## Key Query Operations

- `file(id)`, `folder(id)`, `webLink(id)` — fetch individual content items
- `folderItems(id, limit, offset)` — paginated folder contents
- `search(query, options)` — full-text and metadata search
- `events(streamType, streamPosition)` — real-time and enterprise event streams
- `currentUser` — authenticated user details
- `signRequests` / `signRequest(id)` — Box Sign e-signature workflows
- `retentionPolicies`, `legalHoldPolicies` — governance and compliance
- `metadataTemplates(scope)` — enterprise metadata schemas
- `informationBarriers` — Box Shield configuration

## Key Mutation Operations

- `createFolder`, `copyFile`, `updateFile`, `deleteFile` — content management
- `createCollaboration`, `updateCollaboration` — sharing and access control
- `createSignRequest`, `cancelSignRequest` — e-signature workflows
- `createRetentionPolicy`, `createLegalHoldPolicy` — compliance automation
- `createWebhook`, `updateWebhook` — event notifications
- `createMetadataTemplate`, `createFileMetadata` — structured metadata

## Authentication

Box supports three OAuth 2.0 grant types:

1. **Authorization Code (OAuth 2.0)** — User-authenticated apps via `https://account.box.com/api/oauth2/authorize`
2. **JWT App Auth** — Server-to-server with RSA key pairs; no user interaction required
3. **Client Credentials Grant (CCG)** — Machine-to-machine using client ID and secret

Access tokens are short-lived (60 minutes). Refresh tokens are valid for 60 days (single use).

## Rate Limits

- Per-user: 1,000 requests/minute
- 100 concurrent upload sessions
- API call quotas vary by plan (50K/mo Business, 100K/mo Enterprise, 200K/mo Enterprise Advanced)

## Notable Platform Features

- **Box Sign** — Native e-signature with signer roles, prefill tags, and redirect flows
- **Box Skills** — AI-powered metadata extraction cards on uploaded files
- **Box Shield** — Information barriers for regulated industries (financial services, legal)
- **Box Relay** — Workflow automation triggered by content events
- **Box AI** — Content Q&A and generation (Enterprise plans)
- **Metadata Templates** — Strongly typed custom attributes on files and folders with cascade policies
- **Webhooks v2** — 30+ trigger types for content and collaboration events
- **Retention & Legal Hold** — Governance controls for regulatory compliance

## Files

| File | Description |
|---|---|
| `box-schema.graphql` | Conceptual GraphQL schema with 75+ named types, enums, scalars, queries, and mutations |
| `box-graphql.md` | This documentation file |
