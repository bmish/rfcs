- Repo: eslint/eslint
- Start Date: 2021-06-03
- RFC PR: (leave this empty, to be filled in later)
- Authors: [bmish](https://github.com/bmish)

# List Disable Directives

## Summary

<!-- One-paragraph explanation of the feature. -->

Add a new [CLI option](https://eslint.org/docs/user-guide/command-line-interface#options) `--list-disable-directives` that shows the complete list of inline-disabled rules by count (descending order).

```plaintext
yarn eslint --list-disable-directives .

[normal eslint output (showing any violations) goes here]

Rule                   | Count | Relative
:----------------------|------:|--------:
no-console             |   125 |    40.1%
no-unused-vars         |   104 |    33.3%
radix                  |    43 |    18.8%
node/no-missing-import |    22 |     7.1%
import/order           |    15 |     4.8%
prettier/prettier      |     2 |     0.6%
no-undef               |     1 |     0.3%
```

This matches the output format of the [TIMING](https://eslint.org/docs/1.0.0/developer-guide/working-with-rules#per-rule-performance) environment variable which can be used to see summary statistics about rule performance.

## Motivation

<!-- Why are we doing this? What use cases does it support? What is the expected
outcome? -->

In a large codebase, there can easily be hundreds or even thousands of places where inline disable directive comments (like `// eslint-disable-line no-console`) have been used.

There is not currently a convenient method to find out what rules developers are disabling like this other than manually searching the codebase or writing a custom regexp parsing script. In fact, I put together a [custom script](https://github.com/ember-template-lint/ember-template-lint/blob/master/docs/count-lint-violations.sh) for exactly this purpose, but it's a bit buggy/limited and not easily available across different projects.

Gaining an understanding / summary statistics of what rules are being most frequently disabled by contributors can be useful for a variety of reasons:

- determining what kinds of tech debt exist in a codebase
- determining what rules may be buggy and in need of improvements
- determining what issues developers need more education about

## Detailed Design

<!--
   This is the bulk of the RFC.

   Explain the design with enough detail that someone familiar with ESLint
   can implement it by reading this document. Please get into specifics
   of your approach, corner cases, and examples of how the change will be
   used. Be sure to define any new terms in this section.
-->

## Documentation

<!--
    How will this RFC be documented? Does it need a formal announcement
    on the ESLint blog to explain the motivation?
-->

This new option will be documented on the [CLI options](https://eslint.org/docs/user-guide/command-line-interface#options) page. A formal announcement isn't needed.

## Drawbacks

<!--
    Why should we *not* do this? Consider why adding this into ESLint
    might not benefit the project or the community. Attempt to think
    about any opposing viewpoints that reviewers might bring up.

    Any change has potential downsides, including increased maintenance
    burden, incompatibility with other tools, breaking existing user
    experience, etc. Try to identify as many potential problems with
    implementing this RFC as possible.
-->

-- There may be a slight increase in maintenance burden to ESLint core developers who touch/change (i.e. add new features to) the disable directive implementation.

## Backwards Compatibility Analysis

<!--
    How does this change affect existing ESLint users? Will any behavior
    change for them? If so, how are you going to minimize the disruption
    to existing users?
-->

As this is a new option, there are no backwards compatibility concerns. This new option will not have any impact on users unless they choose to use it.

## Alternatives

<!--
    What other designs did you consider? Why did you decide against those?

    This section should also include prior art, such as whether similar
    projects have already implemented a similar feature.
-->

- A different name could be chosen for the CLI option
  - So far, `--list-disable-directives` is the most clear and concise name I have come up with
- This functionality could be enabled by an environment variable (i.e. `LIST_DISABLE_DIRECTIVES=true`) instead of a CLI option
  - But we already have related CLI options `--no-inline-config` and `--report-unused-disable-directives`
  - I'm not sure why [TIMING](https://eslint.org/docs/1.0.0/developer-guide/working-with-rules#per-rule-performance) was created as an environment variable instead of a CLI option

## Open Questions

<!--
    This section is optional, but is suggested for a first draft.

    What parts of this proposal are you unclear about? What do you
    need to know before you can finalize this RFC?

    List the questions that you'd like reviewers to focus on. When
    you've received the answers and updated the design to reflect them,
    you can remove this section.
-->

## Help Needed

<!--
    This section is optional.

    Are you able to implement this RFC on your own? If not, what kind
    of help would you need from the team?
-->

## Frequently Asked Questions

<!--
    This section is optional but suggested.

    Try to anticipate points of clarification that might be needed by
    the people reviewing this RFC. Include those questions and answers
    in this section.
-->

## Related Discussions

<!--
    This section is optional but suggested.

    If there is an issue, pull request, or other URL that provides useful
    context for this proposal, please include those links here.
-->
