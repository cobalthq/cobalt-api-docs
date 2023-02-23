# API Documentation Style Guide

At Cobalt, we follow the writing guidelines outlined in the [Google developer documentation style guide](https://developers.google.com/style), with the following exceptions:

- We use title case in [document titles and headings](https://developers.google.com/style/capitalization#capitalization-in-titles-and-headings). To check your title, use [this title capitalization tool](https://capitalizemytitle.com/style/Chicago/).
- Security-specific terms such as _blacklist_ or _whitelist_ are acceptable.

Refer to the following guidelines:

- **Methods**. To learn how to describe API methods, see [Methods](https://developers.google.com/style/api-reference-comments#methods) in [API reference code comments](https://developers.google.com/style/api-reference-comments).
- **Placeholders**. To learn more about formatting placeholders, see [Format placeholders](https://developers.google.com/style/placeholders).

## Other Resources

Here are some more useful resources:

- Cobalt UI Text Style Guide in an internal Confluence space. Pay attention to the following sections:
  - General Writing Guidelines and Principles
  - Language, Grammar, and Formatting
  - Word List
- [Dictionary by Merriam-Webster](https://www.merriam-webster.com/), if you need to check spelling.

## English Grammar Linter (Vale)

In this repository, we've set up Vale to check content against the specified rules. For more information, see [GrammarLinter.md](./GrammarLinter.md).

## Hugo Shortcodes

With [Hugo shortcodes](https://gohugo.io/content-management/shortcodes/), you can reuse chunks of content across multiple files and maintain a single source of truth in the API documentation.

Use shortcodes for:

- Placeholders, such as `YOUR-PERSONAL-API-TOKEN`
- Descriptions of HTTP status codes
- Parameter definitions, such as `id`, `asset_type`, or `methodology`
- Other content that you want to use in multiple locations

To add a shortcode:

1. Create a new file in [layouts](./layouts)/shortcodes.
    - Use a meaningful filename, such as `204-response.md`.
1. Add content to the file that you created.
1. In the target file where you want to pull the content of the shortcode file, call the shortcode using this command `{{% shortcodename %}}`.
    - For HTML files, use `<>` instead of `%%` as the delimiter.

Hugo automatically pulls content from the shortcode file to the specified location in the target file.
