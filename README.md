# ClioSort MCP

Move hardcoded app content into editable collections. Use ClioSort to find data like course catalogs or pricing tables in a GitHub repo, then serve it to your app through a REST API. Once your app reads from ClioSort, content edits can go live without a code change or redeploy.

[Open ClioSort](https://cliosort.com) · [Integration guide](INTEGRATION.md) · [MCP client config](mcp.json)

## Quickstart

1. **Scan a repo.** In [ClioSort Projects](https://cliosort.com/projects), connect a GitHub repository and run a scan. ClioSort has read-only access to the repo.
2. **Connect your agent.** Add `https://cliosort.com/api/mcp` as a remote server in a client that supports MCP over HTTP with OAuth. Sign in to ClioSort and approve access when prompted.
3. **Review what ClioSort found.** Copy the project ID from your ClioSort project URL and try this prompt in your agent.

   > Use ClioSort MCP to read the scan results for project `<PROJECT_ID>`. Show me one candidate worth moving into a collection, where it is defined, and which files use it.

### JSON configuration

If your client uses an `mcpServers` JSON config, merge in this entry. In a client with a remote server URL field, paste the URL directly.

```json
{
  "mcpServers": {
    "cliosort": {
      "url": "https://cliosort.com/api/mcp"
    }
  }
}
```

Once you’ve picked a candidate, follow the [integration guide](INTEGRATION.md) to import it, fetch a record, and replace the hardcoded data in your app.
