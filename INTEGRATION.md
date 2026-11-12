# Use ClioSort data in your app

Start with a [scanned project and a connected MCP client](README.md#quickstart). This walkthrough moves a hardcoded course catalog into ClioSort, then reads it from your app.

## 1. Import one collection

Ask your agent to run `get_scan_results` for your project ID. Pick the course catalog candidate and ask the agent to import it with `import_scan_candidate` and the slug `courses`. Use your own slug for other content, and use that same slug in the request below. Check the imported records under **Collections** in ClioSort before changing your app.

## 2. Fetch the collection

Create an API key in [ClioSort account settings](https://cliosort.com/account), grant it access to your project, and store it as `CLIOSORT_API_KEY` in your server environment. Your MCP client signs in via OAuth. Your app uses this API key for REST reads, which require an active ClioSort plan.

From a Bash-compatible shell with that variable set, replace `YOUR_PROJECT_ID` and run:

```bash
curl --fail-with-body https://cliosort.com/functions/fetchProjectData \
  -H "Authorization: Bearer ${CLIOSORT_API_KEY}" \
  -H "Content-Type: application/json" \
  --data '{"project_id":"YOUR_PROJECT_ID","collection":"courses"}'
```

Look for `"ok": true` and your records in `collections[0].items`. If the request returns `403`, check that the key can read the project, the project’s data API is enabled, and the account has an active plan. A `404` usually means the collection slug differs from the one in ClioSort.

## 3. Replace the hardcoded data

Use the same request in a server-side route or loader and pass the returned records to your existing component. If your app runs entirely in the browser, add a serverless function to make the request so the API key stays server-side.

Cache successful reads for about 60 seconds. Keep the last successful result available if a refresh fails. To verify the integration, change one course title in ClioSort and reload the page after the cache expires.

See the [REST API reference](https://cliosort.com/docs#rest) for the response format and error codes.
