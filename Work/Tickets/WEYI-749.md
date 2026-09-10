---
created: 2026-08-17
summary: Add ability to switch between two endpoints (current voyce-gateway and cloudbreak-gateways)
source: https://cloudbreak.atlassian.net/browse/WEYI-749
---
# Description
Enhance the integration to support routing requests to either the existing Voyce Gateway endpoint or the new Cloudbreak Gateway endpoint. The endpoint should be configurable, allowing deployments to switch between gateways without requiring code changes.

# Background
The current implementation is tightly coupled to the existing Voyce Gateway endpoint. As Cloudbreak Gateway is introduced, the integration should support both endpoints to facilitate migration, testing, and future deployments.

The selected gateway should be determined through configuration, allowing environments to switch between the two implementations as needed.

# Requirements
#### 1. Configurable Gateway Endpoint
Add a configuration setting that determines which gateway endpoint will be used for all outsource API requests.
Supported options:
- Voyce Gateway (current implementation)
- Cloudbreak Gateway
#### 2. Routing Logic
Based on the configured endpoint:
- Route all supported outsource API requests to the selected gateway.
- Ensure the request and response handling remains consistent regardless of the selected endpoint.
#### 3. Backward Compatibility
- The existing Voyce Gateway should remain the default configuration.
- Existing deployments should continue to function without any configuration changes.

# Acceptance Criteria
- A configuration option is available to select the target gateway.
- The integration supports both the Voyce Gateway and Cloudbreak Gateway endpoints.
- Switching between gateways requires only a configuration change and does not require code modifications.
- Existing functionality remains unchanged when the Voyce Gateway is selected.
- The solution supports future migration from Voyce Gateway to Cloudbreak Gateway with minimal operational effort.

# Notes
- This change is intended to provide deployment flexibility during the migration period and should be extensible to support additional gateway implementations in the future if needed.

# Todo
- [ ] 