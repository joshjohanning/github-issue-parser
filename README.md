# GitHub Issue Parser

Use this action to convert issues into a unified JSON structure. Read the [Codeless Contributions with GitHub Issue Forms](https://stefanbuck.com/blog/codeless-contributions-with-github-issue-forms) post on my blog.

## Setup

```yml
- uses: stefanbuck/github-issue-parser@v3
  id: issue-parser
  with:
    issue-body: ${{ github.event.issue.body }} # required
    template-path: .github/ISSUE_TEMPLATE/bug-report.yml # optional but recommended

- run: echo '${{ steps.issue-parser.outputs.jsonString }}' > bug-details.json
```

## Example

Given an issue form

```yml
body:
  - type: input
    id: favorite_dish
    attributes:
      label: What's your favorite dish?
    validations:
      required: true

  - type: checkboxes
    id: favorite_color
    attributes:
      label:  What's your preferred color?
      options:
        - label: Red
        - label: Green
        - label: Blue
```

And an issue body

```md
### What's your favorite dish?

Pizza

### What's your preferred color?

- [x] Red
- [ ] Green
- [x] Blue
```

The actions output will be

```json
{
  "favorite_dish": "Pizza",
  "favorite_color": ["Red", "Blue"]
}
```


Want to learn more about this concept? Check out the [Codeless Contributions with GitHub Issue Forms](https://stefanbuck.com/blog/codeless-contributions-with-github-issue-forms) post on my blog.


## Real-world examples

### Basic example

Ever wanted to order a pizza from a GitHub Issue? In this basic example, the order is processed and appended to the README using this Action.

[See workflow](https://github.com/stefanbuck/ristorante/blob/main/.github/workflows/order.yml)

### Awesome list

The [awesome-browser-extensions-for-github](https://github.com/stefanbuck/awesome-browser-extensions-for-github) repository is using this Action to make it super easy to submit a new extension just by filling a new GitHub Issue. The workflow runs and turns the issue into a code contribution once the label `merge` has been added.

[See workflow](https://github.com/stefanbuck/awesome-browser-extensions-for-github/blob/main/.github/workflows/handle-submission.yml)
