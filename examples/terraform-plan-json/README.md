# Terraform directory

This example shows how to run Infracost actions with a Terraform plan JSON file. Installing Terraform is not needed since the Infracost CLI can use the plan JSON directly.

[//]: <> (BEGIN EXAMPLE)
```yml
name: Terraform plan JSON
on: [pull_request]

jobs:
  terraform-plan-json:
    name: Terraform plan JSON
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      
      - name: Setup Infracost
        uses: infracost/actions/setup@v1
        with:
          api_key: ${{ secrets.INFRACOST_API_KEY }}
          
      - name: Run Infracost
        run: infracost breakdown --path=examples/terraform-plan-json/code/plan.json --format=json --out-file=/tmp/infracost_breakdown.json
        
      - name: Post the comment
        uses: infracost/actions/comment@v1
        with:
          breakdown_json: /tmp/infracost_breakdown.json
```
[//]: <> (END EXAMPLE)