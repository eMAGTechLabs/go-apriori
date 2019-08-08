# Go-Apriori
Go-Apriori is a simple go implementation of the Apriori algorithm for finding frequent sets and association rules 

## Short Apriori Algorithm description 
Apriori is a classic algorithm for learning association rules. Apriori is designed to operate on databases / data sets 
containing transactions (for example, collections of items bought by customers)

The algorithm extracts useful information from large amounts of data. For example, the information that a customer who 
purchases 'butter' also tends to buy 'jam' at the same time is acquired from the association rule below:
- Support: The percentage of task-relevant data transactions for which the pattern is true. 
```
Support (Butter->Jam) = ( No of transactions containing both 'butter' and 'jam' ) / ( Total no of transactions )
```
- Confidence: The measure of certainty or trustworthiness associated with each discovered pattern.
```
Confidence (Butter->Jam) = ( No of transactions containing both 'butter' and 'jam' ) / ( No of transactions containing 'butter' )
```
- Lift: This measure of how likely item 'jam' is purchased when item 'butter' is purchased, while controlling for how 
popular item 'butter' is
```.
Lift (Butter->Jam) =  ( No of transactions containing both 'butter' and 'jam' ) / ( No of transactions containing 'butter' ) * ( No of transactions containing 'jam' )
```

The algorithm aims to find the rules which satisfy both a minimum support threshold and a minimum confidence threshold.
- Item: article in the basket.
- Itemset: a group of items purchased together in a single transaction.

### How it works
- Find all frequent itemsets:
    - Get frequent items:
        - Items whose occurrence is greater than or equal to the minimum support threshold.
    - Get frequent itemsets:
        - Generate candidates from frequent items.
        - Prune the results to find the frequent itemsets.
- Generate association rules from frequent itemsets:
    - Rules which satisfy the minimum support, minimum confidence and minimum lift thresholds.

## Usage

### How to get
```
go get github.com/eMAGTechLabs/go-apriori
```

### Options
```go
type Options struct {
    minSupport    float64 // The minimum support of relations (float).
    minConfidence float64 // The minimum confidence of relations (float).
    minLift       float64 // The minimum lift of relations (float).
    maxLength     int     // The maximum length of the relation (integer).
}
```
**Note:** If maxLength is set to 0, no max length will be taken into consideration

### How to use
```go
import "github.com/eMAGTechLabs/go-apriori"

transactions := [][]string{
    {"beer", "nuts", "cheese"},
    {"beer", "nuts", "jam"},
    {"beer", "butter"},
    {"nuts", "cheese"},
    {"beer", "nuts", "cheese", "jam"},
    {"butter"},
    {"beer", "nuts", "jam", "butter"},
    {"jam"},
}
apriori := NewApriori(transactions)
results := apriori.Calculate(NewOptions(0.1, 0.5, 0.0, 0))
```

### Sample Output
```
[
...
    {
        supportRecord: {items: [beer cheese jam nuts] support:0.125 } 
        orderedStatistic: [
            { base: [beer cheese jam] add: [nuts] confidence: 1 lift: 1.6 }
            { base: [beer cheese nuts] add: [jam] confidence: 0.5 lift: 1 }
            { base: [cheese jam nuts] add: [beer] confidence: 1 lift: 1.6 }
        ]
    }
...
]
```

## Inspiration
- [Association Rules and the Apriori Algorithm](https://www.kdnuggets.com/2016/04/association-rules-apriori-algorithm-tutorial.html)
- [Apyori](https://github.com/ymoch/apyori) - Apriori python implementation
- [Apriori-Algorithm](https://github.com/Omar-Salem/Apriori-Algorithm) - Apriori C# implementation

## Contributing
Thanks for your interest in contributing! There are many ways to contribute to this project. Get started [here](CONTRIBUTING.md).

#### Tags

\#apriori-algorithm \#go 