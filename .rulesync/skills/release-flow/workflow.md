# Release flow

Establish this repository's release policy from its working instructions, contribution
guidance and configured checks before preparing delivery. Follow its branch, commit,
review and deployment conventions; when a policy is missing, state the uncertainty
before taking an action that depends on it.

Keep commits limited to the intended change. Validate the affected behavior and
report what was verified. Describe the resulting behavior and relevant limitations
in the pull request using the repository's template.

Link work to its ticket without closing unfinished scope. A merge completes a ticket
only when every agreed requirement is delivered; otherwise link it as partial work.

Before an authorized merge, verify the current head's required checks and reviews,
resolve actual conflicts, and use the repository's configured merge method. Treat
merge, deployment and production promotion as distinct states; report only the
state supported by evidence. Production actions require the authorization specified
by the repository and the developer.
