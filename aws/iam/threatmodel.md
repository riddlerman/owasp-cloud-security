# AWS Identity and Access Management (IAM) Threat Model

## See also

* https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started.html

# Assumptions

* A threat model exists for console and API access to service. This page does not include threat models of the TLS or authentication mechanism of the AWS API itself.

# Scope

This threat model is scoped to the IAM service itself, including for example roles and policies, but not to all the possible IAM actions of every single AWS service. The only IAM actions considered here are those of IAM itself (e.g. PassRole and AssumeRole).

# Notes

* No MFA?
* Policy VersionId defaults to 2008 - is that bad?
* Non-unique PolicyId?
* Deny overrides allow which overrides implicit deny
* What happens when you use principal in policy attached to a user or group? - Docs state "Do not use the Principal element in policies that you attach to IAM users or groups"
* Wildcard principal means everyone/anonymous. A poorly defined condition could expose the policy to any user/role in any account.
* Root is entire account - nice idea for a tool perhaps to look for uses of :root arns
* Principal for specific users and roles uses canonical ids to prevent removal + addition
* Assume role session id?
* "Warning - When you use NotPrincipal in the same policy statement as Effect Allow the permissions specified in the policy statement will be granted to all principals except the ones specified, including anonymous". For example, an administrative policy that includes NonPrincipal:NormalUsers, Effect:Allow, Actions:Dangerous stuff would actually expose those actions to anonymous users
* Apparently NonPrincipal + Effect:Deny is order dependant
* NotAction results in exposure to new actions

