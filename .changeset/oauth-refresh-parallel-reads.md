---
"@better-auth/oauth-provider": patch
---

The `refresh_token` grant now answers faster on databases with high per-query latency. It looks up the refresh token while it authenticates the client, and resolves the resource policy while it reads the user. Error responses are unchanged: a client error is still returned before a refresh token error, and a missing user before a resource error.

Add `onRefreshTokenReuse` to handle a reused refresh token yourself. It runs when a rotated or revoked refresh token is presented outside `refreshTokenReuseInterval`, just before the token's family is invalidated. Return `true` to skip family invalidation, for example after revoking only the session the reused token belonged to. The grant still answers `invalid_grant`.
