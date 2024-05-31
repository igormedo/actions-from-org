# GitHub Actions with Org-level actions

You're using GitHub Enterprise and you're restricted to use only corporate-enabled actions. On top of it those actions are outdates as well.  
But you want your actions, right? No matter what.

## Solution

We'll an Org level actions repositoru as git submodule and refer them as local actions.

## Usage

Add your org level actions as submodule:

``` shell
git submodule add -- https://github.com/igormedo/org-level-actions.git .github/org-level-actions
```

Recommended: use specific tags to maintan stability of your actions

``` shell
git submodule set-branch --branch v1 -- .github/org-level-actions
```

In your workflow, upon checkout don't forget to clone submodules:

``` yaml
...
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          submodules: recursive
...
```

Then use these local actions in your steps as follows:

``` yaml
...
uses: ./.github/org-level-actions/actions/github-script
...
uses: ./.github/org-level-actions/terraform/setup-terraform
...
uses: ./.github/org-level-actions/reviewdog/action-tflint
```

## Example

Here's an example of a workflow that uses these actions to perform a simple Terraform syntax check and linting:

[.github/workflows/lint.yml](.github/workflows/lint.yml)
