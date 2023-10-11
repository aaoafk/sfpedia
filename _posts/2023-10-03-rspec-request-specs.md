---
title:      "Rspec request specs"
date:       2023-10-03T14:32:01-04:00
tags:       ["rspec"]
identifier: "20231003T143201"
---

Request specs provide a thin wrapper around Rails' integration
tests. It drives behavior through the full stack.

Rquest specs are marked by `type: :request` or if set have set
`config.infer_spec_type_from_file_location!` by placing them in
`spec/requests`

With request specs we can:

1. Specify a single request.
2. Specifly multiple requests across multiple controllers.
3. Specify multiple requests across multiple sessions.

We need to check the rails documentation on integration tests for more information.
