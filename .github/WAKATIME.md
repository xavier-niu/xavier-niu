# WakaTime README updates

[WakaTime requires OAuth tokens to read coding activity](https://wakatime.com/developers/#authentication).
API keys are write-only and are intended for editor plugins that send activity.

To configure or rotate the workflow's credential:

1. Sign in to [WakaTime's personal OAuth token page](https://wakatime.com/oauth)
   and generate an access token. A personal token does not require registering an
   OAuth application. If scopes can be selected, `read_stats.languages` is enough
   for the language stats displayed by this workflow.
2. Save the token as the repository Actions secret `WAKATIME_OAUTH_TOKEN` in
   [GitHub's secret settings](https://github.com/xavier-niu/xavier-niu/settings/secrets/actions).
   Store only the token value, without a `Bearer ` prefix. Alternatively, run
   `gh secret set WAKATIME_OAUTH_TOKEN --repo xavier-niu/xavier-niu` and enter the
   token at the prompt.
3. Once the updated workflow is on `master`, manually run **Waka Readme** from
   GitHub Actions to verify the README updates. Scheduled runs continue hourly.

The `athul/waka-readme` action accepts OAuth tokens through its existing
`WAKATIME_API_KEY` input. The workflow maps `WAKATIME_OAUTH_TOKEN` to that input;
the old `WAKATIME_API_KEY` repository secret is no longer used. The workflow's
GitHub token has `contents: write` permission so the action can update `README.md`.
