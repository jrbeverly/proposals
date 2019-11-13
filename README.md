# Proposals

Experimenting with the underlying infrastructure for a GitHub based proposals mechanisms that deploys to a web resource (website/subpage/etc)

## Motivations

- Automation to ensure contribution guidelines are both accessible and followed (e.g. first contribution bot, linting)
- Contribution previews, either by links to markdown rendering or branch previews
- Support for supplemental resources (e.g. `assets/list-of-items.csv`)
- Methods to organize the proposals better (date? slugs? IDs?)
- Simple layout in code (minimal overhead), with tooling to move assets into the correct locations
- When working with code, the proposals have some organization mechanism
- Minimal barriers when trying to write a proposal

## Notes

Using date-based directory organization helps for filtering based on the latest proposals. If you are looking for the proposals in the most recent year, its fairly easy to complete that query (`ls designs/2019/`). I find that this falls apart when navigating the history for proposals related to a project. I could enforce directory naming standards, but I feel that makes the repository difficult to approach. If I want all the proposals related to a certain project, I'd need to use tools like `jq` or `grep`.

A model that involves namespaces paired with status directories (`archived`/etc) would help resolve these issues. My concern with this though is the solution becomes over-engineered and closely connected to the concept of directories. I think the 'Namespaces and Status' example really shows how it can become difficult to work with when sticking with tree structure for organization.

Since each proposal is a self-contained package with metadata, the proposals can be moved freely about the file system. From this, I'd say that the best solution is to just use namespace slugs for directory names. Each proposal will have metadata in the form of the `DESIGN` schema, so the post-processing stage can organize it by that.

This repository does a [simple](docs/proposal.png) [example](docs/search.png) using `mkdocs` to create a website hosting the proposals. The proposals are put in hardcoded locations to avoid the need for a post-processing step.

### Namespaces and Status

```markdown
> designs/
    > project1/
        > sub1/
            > remove-items-from/
                > README.md
                > assets/
                    > diagram.png
            > establish-baseline/
                > README.md
                > supplementary/
                    > NOTES.md
        > sub2/
            > remove-items-from/
                > README.md
    > project2/
        > sandbox-components-by/
            > README.md
        > replace-grpc-with/
            > README.md
> archived/
    > 2019
        > project1/
            > establish-project1-for/
                > README.md
    > 2018
        > project2/
            > establish-project2-for/
                > README.md
```

### Directory scoping

```markdown
> xyz/
    > README.md
    > DESIGN
    > assets/
        > diagram.png
        > architecture.svg
    > supplmentary/
        > NOTES.md
        > ESTIMATES.md
```
