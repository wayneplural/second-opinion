# Second Opinion 🩺 (AI Code Review)

A github action which reviews your code


### Example Usage

```yaml
name: Second Opinion - AI Code Review
run-name: Second Opinion - Diagnosing code 🩺
on: 
  pull_request:
    types: [opened, synchronize]

jobs:
  second-opinion:
    permissions:
      pull-requests: write
      contents: read
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
        with:
          fetch-depth: 2

      - name: Generate A Second Opinion
        uses: wayneplural/second-opinion@v1
        with:
          azure-openai-api-endpoint: "https://openaiplural.openai.azure.com/"
          azure-openai-api-key: ${{ secrets.AZURE_OPENAI_API_KEY }}
          api-version: "2024-05-01-preview"
      
```