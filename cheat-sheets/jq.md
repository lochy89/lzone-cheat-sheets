Example-wise the jq manpage is not really helpful. Let's document some
simple examples here...

### Output Formatting

If you do only care about output formatting (pretty print) run

    cat my.json | jq

Note: for redirection you need to pass a filter too to avoid a syntax error:

    cat my.json | jq . >output.json

### Simple Extraction

Consider this example document

    {
        "timestamp": 1234567890,
        "report": "Age Report",
        "results": [
            { "name": "John", "age": 43, "city": "TownA" },
            { "name": "Joe",  "age": 10, "city": "TownB" }
        ]
    }

To extract top level attributes "timestamp" and "report"

    jq '.[] | {timestamp,report}'

To extract name and age of each "results" item

    jq '.results[] | {name, age}'

Filter this by attribute

    jq '.results[] | select(.name == "John") | {age}'      # Get age for 'John'
    jq '.results[] | select(.name | contains("Jo"))'       # Get complete records for all names with 'Jo'
