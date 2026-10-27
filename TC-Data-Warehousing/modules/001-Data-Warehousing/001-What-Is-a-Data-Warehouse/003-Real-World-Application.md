## A Retail Example

Consider a national retail chain with hundreds of stores plus an online storefront. Store transactions live in one system, online orders in another, and customer loyalty data in a third. None of these systems alone can answer a question like "which product categories grew fastest among loyalty members over the past two years, broken down by region."

A data warehouse solves this by regularly pulling data from all three systems, standardizing it, for example making sure a product ID means the same thing everywhere, and storing it in a structure built for exactly this kind of cross system, historical analysis. Business analysts then query the warehouse directly, without needing to understand or access the three original operational systems at all.