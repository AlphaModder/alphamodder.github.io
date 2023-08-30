+++
title = "space-email-api"
date = 2017-05-13
in_search_index = false

[taxonomies]
project-tags = ["libraries", "tools", "async"]

[extra]
thumbnail = "./space_email.png"
clickthrough = "https://github.com/AlphaModder/space_email_api"
+++

{% project_header2(adjust=-4) %}
- {{badge(path="https://img.shields.io/badge/status-actively maintained-brightgreen")}} {{badge(path="https://img.shields.io/crates/v/space-email-api.svg")}}
- [on GitHub](https://github.com/AlphaModder/space_email_api)
{% end %}

`space-email-api` is a Rust client for the website [Space Email](https://space.galaxybuster.net), "an indirect communication platform that allows for a unique exchange of conversation over space and time." It is implemented with the `reqwest` library, and is fully compatible with Rust's new `async-await` features. [`space_email_scraper`](https://github.com/AlphaModder/space_email_scraper) is a tool of mine built with `space-email-api`.