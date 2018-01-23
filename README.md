# Lockstep Playbook
- [Lockstep Playbook](#lockstep-playbook)
  - [PR etiquette](#pr-etiquette)
    - [Contributors](#contributors)
    - [Reviewers](#reviewers)
  - [Performance](#performance)
    - [Check list](#check-list)
    - [Test page performance](#test-page-performance)
    - [Libraries](#libraries)
  - [Security](#security)
    - [Development machines](#development-machines)
    - [Source Control](#source-control)
    - [Rails](#rails)
    - [Servers](#servers)
    - [Additional Resources](#additional-resources)

## PR etiquette

### Contributors

* Open Pull Requests as soon as possible to give interested people a chance to get involved.
See: [How we use Pull Requests to build GitHub](https://github.com/blog/1124-how-we-use-pull-requests-to-build-github')
* While PRs can be work in progress, they generally should adhere to minimum coding standards, so please include JSLint, ESLint, RuboCop etc. in your editor config.
See: [Rubocop Editor Integration](https://rubocop.readthedocs.io/en/latest/integration_with_other_tools/)
* Before you request a review on a PR, please ensure the following:
  * the code has no obvious errors or bugs
  * the branch has been rebased against the most current version of its merge target and conflicts have been resolved
  * you tested the code both with automated tests and manually
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

### Additional Resources

* [OWASP Ruby on Rails Cheatsheet](https://www.owasp.org/index.php/Ruby_on_Rails_Cheatsheet)
* [Rails Security Checklist](https://github.com/eliotsykes/rails-security-checklist): Community-driven Rails Security Checklist
* [Zen Rails Security Checklist](https://github.com/brunofacca/zen-rails-security-checklist): An alternatice checklist of security precautions for Ruby on Rails applications
* [Rails security guide](http://guides.rubyonrails.org/security.html), great resource!
* [OWASP Top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)

[⬆](#lockstep-playbook)
