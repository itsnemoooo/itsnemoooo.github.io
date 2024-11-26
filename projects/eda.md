## Datasets Provided
1. Petrovich
2. Leroy

## Dataset Shape
combined: 44102983 x 16
Petrovich DataFrame shape: (2313025, 16)
Leroy DataFrame shape: (41789958, 16)

Petrovich only is 5% of Leroy

## Variable types:
match_type                categorical [0, 1, 2]: no match, 100% match, exclusive
category_1                categorical
category_2                categorical
category_3                categorical
category_4                categorical
category_5                categorical
sku                       unique ID
brand                     categorical
our_price                numerical
price                    numerical
price_before_discount    numerical
date                      date
city                      categorical
status                    categorical (y/n)
competitor                categorical (petrovich/leroy)

## Preprocessing
1. match type one hot encoding to create: No Match, 100% Match, Exclusive 
2. Category 2-5 Drop
3. Category 1: Building materials isolate
## MVP
We see category 1 named building materials hs 157k rows with 6k unique SKUs. This is a good place to start.
28k has our_price values
