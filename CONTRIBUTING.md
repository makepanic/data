# Contributing

## Welcome!

We are so glad you are considering contributing to `ember-data`. Below you'll find sections
 detailing how to become involved to best ensure your contributions are successful!

### Reporting Bugs

Report issues you've discovered via the [issue tracker](https://github.com/emberjs/data/issues).
  We have provided an [issue template](./.github/ISSUE_TEMPLATE/bug.md) what will help guide you through the process.
  If you are unsure if something is a bug, the `#ember-data` channel on [Discord](https://discord.gg/zT3asNS) is
  a great place to ask for help!

### Discussion

Before embarking on a fix, a new feature, or a refactor it is usually best to discuss the
 intended work with other contributors. In addition to holding discussions on individual [issues](https://github.com/emberjs/data/issues)
 or [RFCs](https://github.com/emberjs/rfcs/labels/T-ember-data), you will find most contributors
 and [core team members](https://emberjs.com/team/) hangout in the `#dev-ember-data` channel on [Discord](https://discord.gg/zT3asNS)
 
### Weekly Meeting (video conference)

Members of the `ember-data` core team meet weekly to discuss pull-requests, issues, and road-map items. These
 meetings are open to all contributors and interested parties, but only team members may vote when a vote
 is necessary.
 
Currently meetings are Wednesdays at 2pm Pacific Time. A video conference link is posted in the
 `#dev-ember-data` channel on [Discord](https://discord.gg/zT3asNS) a few minutes prior to each meeting.

### Requesting Features or Deprecations

`ember-data` participates in the [RFC process (GitHub emberjs/rfcs)](https://github.com/emberjs/rfcs/).
  Most changes to the public API including new features, changes in behavior, or deprecations require
  community discussion and must go through this process.
  
  While there is no guarantee that an RFC will be accepted, successful RFCs typically follow a pattern
    of iteration while gathering requirements, addressing feedback, and consensus building. The best RFCs
    are narrowly scoped with clear understanding of alternatives, drawbacks, and their effect on the community.

    Here are a few suggestions of **steps to take before drafting your RFC** to best make your RFC successful.
    Often this process will complete quickly, but when it does not, don't despair! Often the best ideas
    take the longest to bake.

   1. Bring up your idea in the `#dev-ember-data` channel on [Discord](https://discord.gg/zT3asNS) or
     with individual [team members](https://emberjs.com/team/)
   2. Reflect on any concerns, alternatives, or questions that arise from these discussions.
   3. Continue to discuss the idea, giving time for everyone to digest and think about it.
   4. Attend the weekly team meeting to discuss your idea
   5. Open an [RFC issue](https://github.com/emberjs/rfcs/issues?q=is%3Aissue+is%3Aopen+label%3AT-ember-data)
      to broaden and record the discussion if the idea needs more time for discussion and iteration.
      - announce your issue in `#dev-ember-data` and anywhere else desired such as `#news-and-announcements` and `twitter`.
   6. [Draft an RFC](https://github.com/emberjs/rfcs#what-the-process-is) and share it with those you have
      been discussing the ideas with.
   7. Publish your RFC by opening a PR to [emberjs/rfcs/](https://github.com/emberjs/rfcs/)
      - announce your PR in `#dev-ember-data` and anywhere else desired such as `#news-and-announcements` and `twitter`.
   8. Attend weekly team meetings to discuss the RFC, continue iterating on the RFC, and to help shepherd it to completion.
   9. Build a proof-of-concept. Sometimes this is best if it occurs alongside drafting the RFC, as it often informs
      the RFC design, known drawbacks, and alternatives. Often it will become incorporated in the final implementation.
   10. If you are able, help land the work in a release! It is not required that you implement your own RFC but often
      this is the best way to ensure that accepted RFCs are implemented in a timely manner.

### Submitting Work



// TODO some more on guidelines, and tests, and whatnot

Some fixes might require new public API or changes to existing public APIs. If this is the case,
 it is even more important to discuss the issue's problem space and the proposed changes with
 [team members](https://emberjs.com/team/) before diving too deep into the implementation.


### Developing a Feature



## Developer Guide

## Using Feature Flags

Feature flags allow new features to be tested easily and strips them out of
production builds automatically.

1. Add your new feature flag to the [config/features.json](https://github.com/emberjs/data/blob/master/config/features.json) file.

  ```js
  {
    "ds-boolean-transform-allow-null": null,
    "ds-mynew-feature": null
  }
  ```

  Give it a default of `null` so it will not be used in production builds.

2. Import `isEnabled` from `ember-data/-private`, wrapping any new
  code with your feature:

  ```js
  import { isEnabled } from 'ember-data/-private';

  if (isEnabled('ds-mynew-feature')) {
    // ... any additional code
  } else {
    // ... any previous code that may have been overwritten
  }
  ```

3. Similarly, you will want to wrap any new or edited tests with the same
  feature flag.

  ```js
  import { isEnabled } from 'ember-data/-private';

  if (isEnabled('ds-mynew-feature')) {
    test('test for new feature', function(assert) {
      // ...
    })
  }
  ```

  This will allow the test suite to run as normal.

4. Running tests with all feature flags enabled is possible via
  `ember test --environment=test-optional-features` This is also possible while
  running tests in the browser via the `Enable Opt Feature` checkbox.

5. Add your feature to the [Features](https://github.com/emberjs/data/blob/master/FEATURES.md) file.
  Be sure to leave a description of the feature and possible example of how to
  use it (if necessary).

## Benchmarking

Ember Data is instrumented with [heimdalljs](https://github.com/heimdalljs/heimdalljs-lib)
 Top level scenarios for benchmarking are available via the `query` route in
 the dummy app, and desired scenarios to be run can be configured via `benchmarks/config.js`.

 The scenarios are configured to interop with [heimdall-query](https://github.com/heimdalljs/heimdall-query)
 for analysis. To run scenarios:

  1. Start the dummy app with instrumentation on: `ember s --instrument`

  2. Configure `benchmarks/config.js` with desired scenarios

  3. To run both the benchmarks and the analysis: `node ./benchmarks`

      a.) To just collect data (no analysis): `node ./benchmarks/bash-run.js`
      b.) To just run analysis (w/cached data): `node ./benchmarks/bash-analyze.js`
      c.) To cache a data set or use a cached data set, all commands accept `-c ./path/to/cache/dir`

  4. Do not commit cached data results, these should be git ignored already.

# Pull Requests

We love pull requests. Here's a quick guide:

1. Fork the repo.

2. Run the tests. We only take pull requests with passing tests, and it's great
to know that you have a clean slate, see notes on how to run unit tests [here](https://github.com/emberjs/data#how-to-run-unit-tests). (To see tests in the browser,
run `npm start` and open `http://localhost:4200/tests`.)

3. Add a test for your change. Only refactoring and documentation changes
require no new tests. If you are adding functionality or fixing a bug, we need
a test!

4. Make the test pass.

5. Commit your changes. Please use an appropriate commit prefix.
If your pull request fixes an issue specify it in the commit message. Some examples:

  ```
  [DOC beta] Update CONTRIBUTING.md for commit prefixes
  [FEATURE ds-pushpayload-return] Change `pushPayload` to return a value. #4110
  [BUGFIX beta] Allow optional spaces when parsing response headers
  ```

  For more information about commit prefixes see [Commit Tagging](#commit-tagging).

6. Push to your fork and submit a pull request. Please provide us with some
explanation of why you made the changes you made. For new features make sure to
explain a standard use case to us.

We try to be quick about responding to tickets but sometimes we get a bit
backlogged. If the response is slow, try to find someone on IRC (#emberjs) to
give the ticket a review.

Some things that will increase the chance that your pull request is accepted,
taken straight from the Ruby on Rails guide:

* Use Ember idioms and helpers
* Include tests that fail without your code, and pass with it
* Update the documentation, the surrounding one, examples elsewhere, guides,
  whatever is affected by your contribution

## Writing Tests

* We do write tests for our warns and assertion messages, using the `assert.expectAssertion()` and `assert.expectWarning()` helpers.
* Because Travis runs tests in the `production` environment, assertions and warnings are stripped out. To avoid tests on warning/assertion messages failing for your PR, use the `testInDebug` helper to skip them in production. See [this](https://github.com/emberjs/data/blob/b3eb9c098ef8c2cf9ff3378ed079769782c02bb5/tests/integration/adapter/queries-test.js#L32) example.

## Commit Tagging

All commits should be tagged. Tags are denoted by square brackets (`[]`) and come at the start of the commit message.

### Bug Fixes

In general bug fixes are pulled into the beta branch. As such, the prefix is: `[BUGFIX beta]`. If a bug fix is a serious regression that requires a new patch release, `[BUGFIX release]` can be used instead.

For bugs related to canary features, follow the prefixing rules for features.

The vast majority of bug fixes apply to the current stable or beta releases, so submit your PR against the `master` branch with one of the above mentioned BUGFIX tags.
(In the unusual case of a bug fix specifically for a past release, tag for that release `[BUGFIX release-1-13]` and submit the PR against the stable branch for that release: `stable-1-13`.)

### Cleanup

Cleanup commits are for removing deprecated functionality and should be tagged
as `[CLEANUP beta]`.

### Features

All additions and fixes for features in canary should be tagged as `[FEATURE name]` where name is the same as the flag for that feature.

### Documentation

Documentation commits are tagged as `[DOC channel]` where channel is `canary`,
`beta`, or `release`. If no release is provided `canary` is assumed. The channel should be the most stable release that this documentation change applies to.

### Security

Security commits will be tagged as `[SECURITY cve]`. Please do not submit security related PRs without coordinating with the security team. See the [Security Policy](https://emberjs.com/security/) for more information.

### Other

In general almost all commits should fall into one of these categories. In the cases where they don't please submit your PR untagged. An ember-data contributor will let you know if tagging is required.


NOTE:
* Partially copied from https://raw.github.com/thoughtbot/factory_girl_rails/master/CONTRIBUTING.md
* Commit tagging section taken from [ember.js](https://github.com/emberjs/ember.js/blob/5641c3089180bdd1d4fa54e9dd2d3ac285f088e4/CONTRIBUTING.md#commit-tagging)
