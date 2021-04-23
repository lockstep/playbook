# Verumex Playbook

* [Lockstep Playbook](#lockstep-playbook)
  * [Product Management](#product-management)
    * [General Principles](#general-principles)
    * [Ticket Tracking Workflow](#ticket-tracking-workflow)
    * [GitHub Workflow](#github-workflow)
  * [PR etiquette](#pr-etiquette)
    * [Contributors](#contributors)
    * [Reviewers](#reviewers)
  * [Performance](#performance)
    * [Check list](#check-list)
    * [Test page performance](#test-page-performance)
    * [Libraries](#libraries)
  * [Security](#security)
    * [Development machines](#development-machines)
    * [Source Control](#source-control)
    * [Rails](#rails)
    * [Servers](#servers)
    * [S3](#s3)
    * [Additional Resources](#additional-resources)

## Product Management

### General Principles

* **Over-communicate**: It should be impossible for team leads or clients to be unsure about what you are working on, challenges you are facing, questions you have, assumptions you've made, etc. We employ Loud Productivity<sup>TM</sup> to ensure clients and team members can "hear" how projects are going without having to look closely or investigate to understand what is happening.
* **Disambiguate Responsibility**: It should be obvious at every step in the life cycle of a ticket or GitHub PR who is immediately responsible for its completion. See the workflows below regarding ticket assignments and related expectations.
* **Anticipate Challenges**: It is incumbent upon the developer in charge of a ticket to _understand the business requirements and implementation plan thoroughly ahead of the implementation_ and to identify/raise concerns or questions before any code is written. We are frequently 12 time zones away from each other, so frequent back-and-forths about minor issues/concerns throughout the implementation of any given feature require 24-hour cycles and is _devastating_ to timelines and productivity. Ask blocking questions as early as possible to minimize their quantity and their impact on the timeline of the feature. If possible, propose solutions or seek clarification internally before engaging remote stakeholders directly for input.

### Ticket Tracking Workflow

* Use a ticket-tracking software (GitHub issues/projects, JIRA or a similar PM software) to track discrete business requirements and the process from discovery through completion.
* Use columns that capture the following intents (at minimum):
  1.  TODO: Tickets that are unassigned but ready for immediate development. These should be estimated (via story points or comparable measure) prior to or soon after being added to the TODO column. Estimate and/or self-assign an unassigned TODO ticket as soon as you are ready to begin development on that ticket.
  2.  IN PROGRESS: This column indicates that **development is active**. Make sure that whatever you are currently working on is in this column and assigned to you. There should never be multiple in-progress tickets assigned to you unless they are in fact both in active development (and potentially should have been one ticket). If something needs clarification or review it _should not be in this column_. If your ticket becomes blocked during implementation, move it to TODO (or another preceding column) and assign it to the blocker, with a comment on the ticket articulating what is needed. It may also be appropriate to put it in the IN REVIEW column if the block depends on a review, to indicate that the ticket is mostly done (or at least work has been started) but input is needed either on the implementation or UX before continuing.
  3.  IN REVIEW: If a PR is open and a review has been requested (see the [GitHub Workflow](#github-workflow) below), the corresponding ticket should be in this column. Similarly, this column may be used for tickets in a QA process (if a separate QA column is not present). Tickets under refactoring or revision based on feedback should move back to IN PROGRESS.
  4.  DONE: Tickets should move to a column indicating completion OR be removed from the view/board after the Review/QA process is completed in order to reduce clutter and facilitate the tracking of total completion time.
* You are responsible for **managing your own tickets**. This is the primary means of communicating progress with your team—if you don't have an IN PROGRESS ticket we will safely assume you've just moved something into IN REVIEW and assigned it appropriately or are reviewing other tickets assigned to you.
* If you are working on a feature or request that is not explicitly part of your IN PROGRESS ticket or is not even captured in a ticket, **stop**. This frequently manifests as an "urgent" request or "quick fix", and it is tempting to switch off of your current ticket to tackle the "time-sensitive" issue. **DO NOT DO THIS LIGHTLY.** Coordinate with the team lead or make the stakeholder aware of the deviation/interruption and _relocate or create tickets as needed_ to reflect the new work.
* Tickets should include references/links to their corresponding GitHub PRs or branches, and vice-versa. It is important for review purposes to navigate between the ticket and its implementation quickly and efficiently.
* If a ticket seems larger than is appropriate, engage the Reporter for clarification or with a recommendation to decompose the ticket into smaller tasks. If a ticket is still large but won't be decomposed into smaller tickets, address the feature with a series of sensible and self-contained pull requests.
* Engage the Reporter as early as possible if the scope changes on a ticket so a new ticket can be created or relevant parties can be informed about the corresponding timeline/expectation change.
* Do not assume there is nothing to do. Sometimes team leads, product managers or stakeholders fall behind in creating or prioritizing tickets. The first place to look for tickets is the TODO column, the second is the top of the backlog (to work ahead on estimation/clarification), and if neither has tickets that need review please communicate with the team lead.
* Establish velocity in order to determine a reasonable and sustainable pace. The purpose of estimation is to establish expectations both for delivery timeline and developer productivity. The latter is important if we are to align incentives—ideally extra hours worked or efficiency gains are recognized and rewarded instead of simply leading to higher expectations and a less sustainable workload. No one likes a moving goalpost.

### GitHub Workflow

* Assign Pull Requests to whomever is immediately responsible for the completion of the ticket. If you are still working on the code, you should be the assignee. If you need a review from someone to move forward, **reassign the PR to that reviewer**.
* Assigned reviewers should review the PR in a timely fashion (within 48 hours) or explicitly indicate/notify that they will be delayed to allow for expeditious re-assignment elsewhere. The reviewer must **merge or reassign appropriately** after reviewing.
* A Pull Request should always be assigned to exactly one person.
* Assign a "Reviewer" (the GitHub Reviewer feature) only as a way to request **optional** reviews from that reviewer. Mandatory/blocking reviews are managed via the Assignee feature (as outlined above), so the "Reviewer" function should be used only as an indication to optional reviewers that you are ready for (and want) feedback as time allows.
* Multiple "Reviewers" are acceptable but review requests should be used conscientiously, sensibly and sparingly. Do not "shotgun" your review requests.
* **All reviewers** must "Accept Changes" prior to the PR being merged. Thus if an optional reviewer requests changes they become a mandatory/assigned reviewer at some point prior to the merge.
* If you assign someone to your PR you will also have moved the ticket to IN REVIEW in the ticket tracking software. _You may remain the assignee on the ticket_. We don't want to inundate assigned reviewers with notifications and constantly update assignments across multiple systems as PRs go through a review process. But **if a blocking review is taking more than 48 hours** to complete, assigning the PR reviewer in the ticket tracker in addition to GitHub is a polite and appropriate way to spur them on and to indicate who is responsible for moving the ticket forward.
* DONE tickets are much more valuable than IN PROGRESS tickets, both from an immediate functional perspective and given the maintenance overhead of stale branches/merge conflicts. Unless context switching will cause inefficiency, you should prioritize working on tickets that need revisions after a review or reviewing PRs assigned to you rather than beginning or continuing work on a more recent ticket.

## PR etiquette

### Contributors

* Open Pull Requests as soon as possible to give interested people a chance to get involved.
  See: [How we use Pull Requests to build GitHub](https://github.com/blog/1124-how-we-use-pull-requests-to-build-github')
* While PRs can be work in progress, they generally should adhere to minimum coding standards, so please include JSLint, ESLint, RuboCop etc. in your editor config.
  See: [Rubocop Editor Integration](https://rubocop.readthedocs.io/en/latest/integration_with_other_tools/)
* Branch naming and commit message conventions:
  * Your branch name should include the ticket id and (optionally) relevant keywords, e.g. `1147-fix-provision-parser`
  * Write clear and crisp commit messages. Commit message bodies should include the ticket id using "Contributes to" or "Closes" keywords, e.g. `Contributes to #1147`. We're generally following Tim Pope's recommendations [here](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).
* Before you request a review on a PR, please ensure the following:
  * The code has no obvious errors or bugs
  * The branch has been rebased against the most current version of its merge target and conflicts have been resolved
  * You tested the code both with automated tests and manually
* Assign **one** person to your PR when you are ready for a formal review. You may add one or more "reviewers" for in-progress feedback but those reviewers are considered optional, the _assignee_ is the person formally responsible for the progress of the PR. Refrain from requesting code reviews outside of the assignee and reviewer mechanisms in Github, it just causes redundant spam, though polite follow-ups in Github, chat or email are acceptable if the reviewer is taking too long to respond.
* After you merge a PR, please delete the corresponding branch to keep GitHub clean.

### Reviewers

* Keep in mind that unless a Pull Request has been assigned to you or your review was requested, it is considered to be work in progress.
* All feedback should be polite, helpful, constructive, and professional.
* The provided feedback should mostly focus on logic, business requirements etc.
* Please refrain from starting arguments about coding style, unless there are credible performance/security implications. It's ok to leave style suggestions, but PRs should not be rejected because of this (this does NOT apply to obvious formatting issues that should have been caught by a lint tool).
* See: [Crafting Better Code Reviews](https://slimwiki.com/lockstep-labs/crafting-better-code-reviews)

[⬆](#lockstep-playbook)

## Performance

### Check list

* Image optimization (e.g. [ImageOptim](https://imageoptim.com/mac), see [Essential Image Optimization](https://images.guide) ebook)
* Use CDN if possible (e.g. S3 + [CloudFront](https://aws.amazon.com/cloudfront/), works well with [asset_sync](https://github.com/AssetSync/asset_sync))
* Gzip (e.g. [heroku-deflater](https://github.com/romanbsd/heroku-deflater))
* Cache-Control headers ([time-based](https://devcenter.heroku.com/articles/http-caching-ruby-rails#time-based-cache-headers), [conditional GET](https://devcenter.heroku.com/articles/http-caching-ruby-rails#conditional-cache-headers))
* [Fragment caching](http://guides.rubyonrails.org/caching_with_rails.html#fragment-caching) (+ [Russian doll caching](http://guides.rubyonrails.org/caching_with_rails.html#russian-doll-caching) were applicable)
* Consider using the [loadCSS](https://github.com/filamentgroup/loadCSS) polyfill in combination with [critical](https://github.com/addyosmani/critical)/[penthouse](https://github.com/pocketjoso/penthouse) or similar tools to avoid blocking CSS loads

### Test page performance

* [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/) (by Google)
* [WebpageTest](WebpageTest) (ugly, but probably the most comprehensive tool)

### Libraries

* [Oj](https://github.com/ohler55/oj): A fast JSON parser and Object marshaller as a Ruby gem. Drop-in replacement for the bundled JSON gem when used in compat mode.
* [bootsnap](https://github.com/Shopify/bootsnap): By Shopify. Plugs into a number of Ruby and (optionally) ActiveSupport and YAML methods to optimize and cache expensive computations (included by default in Rails 5.2+).
* [rack-mini-profiler](https://github.com/MiniProfiler/rack-mini-profiler): Profiler for your development and production Ruby rack apps (included in our Rails template)
* [bullet](https://github.com/flyerhzm/bullet): helps to kill N+1 queries and unused eager loading (included in our Rails template)

[⬆](#lockstep-playbook)

## Security

### Development machines

* Consider [turning on FileVault](https://support.apple.com/en-us/HT204837) if you store client data on your machine and take your laptop out of the office.
* Enable 2FA for all services that support it ([Google](https://support.google.com/a/answer/175197#setup), etc.)
* Use unique, strong passwords for all logins. Use a password manager like [1Password](https://1password.com/), [LastPass](https://www.lastpass.com/) or [KeePass](http://keepass.info/).
* Lock your computer whenever you're away from it.

### Source Control

* Enable two-factor authentication ([Github](https://help.github.com/articles/providing-your-2fa-authentication-code/), [BitBucket](https://confluence.atlassian.com/bitbucket/repository-privacy-permissions-and-more-221449716.html))!
* Never check secrets (API keys etc.) into source control.
* If secrets did get checked in, consider them compromised, even when dealing with a private repository. Immediately revoke them and generate new keys.
* Be restrictive with permissions ([GitHub](https://help.github.com/enterprise/2.9/user/articles/repository-permission-levels-for-an-organization), [BitBucket](https://confluence.atlassian.com/bitbucket/repository-privacy-permissions-and-more-221449716.html))

### Rails

* Use [bundler-audit](https://github.com/rubysec/bundler-audit) in every project (included in our Rails template)
* Ensure extra good spec coverage around features related to payments and privacy.
* If your app processes payments and may get audited, consider disabling the TRACE HTTP method to prevent XST attacks (a custom Rack middleware is included in our Rails template and can be turned on via an env variable).
* Consider using [rack-attack](https://github.com/kickstarter/rack-attack) in production.

### Servers

* Enable 2FA ([Heroku](https://devcenter.heroku.com/articles/two-factor-authentication), [AWS](https://aws.amazon.com/iam/details/mfa/))
* Use SSL for serving your content. [QualSys SSL Lab](https://www.ssllabs.com/ssltest/analyze.html) is an excellent tool for verifying your setup
* Consider the use of different [HTTP headers for added security](https://www.smashingmagazine.com/2017/04/secure-web-app-http-headers/). Use [securityheaders.io](https://securityheaders.io/) for suggestions and further information.
* [Hardenize](https://www.hardenize.com) gives a nice security overview, good to check occasionally.

### S3

Given that we frequently store assets on S3, the minimum security configuration
should be one IAM User and one Bucket per environment (development, staging,
production). Each of these IAM Users (typically machine/ssl-only users, without
dashboard access) should have a custom Policy specific to the target
environment. For example the `development-machine` User might have a policy
as follows:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket"],
      "Resource": ["arn:aws:s3:::myapp-development"]
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:PutObject",
        "s3:GetObject",
        "s3:DeleteObject",
        "s3:PutObjectAcl"
      ],
      "Resource": ["arn:aws:s3:::myapp-development/*"]
    }
  ]
}
```

NOTE: You should never grant a machine (or dashboard) user full S3 access. Only
a client representative or a team lead should have unrestricted access to AWS
resources.

[⬆](#lockstep*playbook)

### Additional Resources

* [OWASP Ruby on Rails Cheatsheet](https://www.owasp.org/index.php/Ruby_on_Rails_Cheatsheet)
* [Rails Security Checklist](https://github.com/eliotsykes/rails-security-checklist): Community-driven Rails Security Checklist
* [Zen Rails Security Checklist](https://github.com/brunofacca/zen-rails-security-checklist): An alternatice checklist of security precautions for Ruby on Rails applications
* [Rails security guide](http://guides.rubyonrails.org/security.html), great resource!
* [OWASP Top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)

[⬆](#lockstep-playbook)
