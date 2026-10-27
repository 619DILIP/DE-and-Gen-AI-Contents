
## Data Modeling

Data modeling is used in practice for evaluating the data objects and their relationships to other entities used to investigate the business' data requirements for processes.

For example, let's think about a driver's license. We can use data modeling to determine if we have enough available combinations for our unique identifiers. When generating ID identifiers, we need to make sure the data type and constraints we've established are enough to handle our needs, accounting for the growth of the population. Prior to implementation, we can establish the rules for our data, saving us time, money and headache in the future.

## Entity Relationship Diagram

Entity Relationship diagrams allows us to visualize the entities, their attributes and relationships to one another. This can be done via third party software such as Microsoft Visio or LucidChart, but inside of most database IDEs is some form of basic ERD generation tool. As you have seen previously, the image below is the example of an ERD generated through an IDE (DBeaver):

![](../../resources/schema_example.png)

We can see symbols at the end of relationship lines that link the entities. These symbols indicate how many instances of one entity are related to how many instances of another entity. In Crow's Foot notation, there are usually two symbols beside one another. For the first symbol, it can be a crows foot which indicates many instances, or it can be a single line which represents a single instance. For the second symbol, it can be either a single line to indiciate it is mandatory or a circle which represents that it is optional (there can be zero instances). Note that other notations use different symbols.

Using the above ERD for a commerce database, you can see how stores, customer, department and sales information is all intertwined. 