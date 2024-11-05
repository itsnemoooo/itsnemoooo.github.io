Like every sequential decision making problem we have goals.

Problem: Small D2C businesses have failed to adapt to pricing at scale. This wastes inventory, money, and time.

Solution: We learn a policy that determines the value of being in state S and taking action A.

The highest level goal is to sell more product on the ecommerce website by changing prices based on the environment.

Each product gets its own agent. The agent has continuous action space of pricing. Full control from low to high.

| State Variable       | Description                       |
|----------------------|-----------------------------------|
| date                 | Date of the observation           |
| current price        | Current price of the product      |
| clicks               | Number of clicks                  |
| # of competitors     | Number of competitors             |
| competitor prices    | Prices of competitors             |
| media campaign (y/n) | Whether there is a media campaign |
| decline (y/n)        | Whether there is a decline        |
| product category     | Category of the product (tree)    |
| collection name      | Name of the collection            |
| type                 | Type of the product               |
| color                | Color of the product              |
| material             | Material of the product           |

Like any good engineering challenge, it starts with data analysis.
