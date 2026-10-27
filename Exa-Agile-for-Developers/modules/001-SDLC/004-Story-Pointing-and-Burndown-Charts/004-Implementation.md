
## Estimating with Story Points

### How are story points calculated? 

Story points are essentially determined by comparing a project's features to those of a prior, comparable project. With this kind of approach, the team can comprehend the complexity of a given feature. They can also use it to assign a number that represents a specific feature effort.

**What happens if this is the team's first time estimating effort?**

A team must choose a baseline tale in such a situation. It doesn't have to be the tiniest one; just something that all the team members can relate to. After establishing the baseline tale, the group can start estimating story points by contrasting them with the baseline.

Let’s illustrate this approach using Circles as a simple example.

![Story Point Illistration](images/SP_and_BDC.png)

Circle A is clearly the smallest one. B is about double the size of A. Whereas C is roughly four, maybe five times bigger than A, and two times bigger than B. Here, we do not have precise absolute values to assign to each circle. Please note that exact absolute values were not provided, but the sizes were determined relative to Circle A as the baseline.

The following video can provide you with additional insight into agile story points:

[Agile Story Points](https://www.youtube.com/watch?v=5wc8fQn1Y_g)

### Story Points Sizing:

With an agile methodology, teams work with user stories rather than circles. Teams are able to assess the relative size of each user narrative and give them story points by comparing them with one another. Naturally, this approach works with requirements expressed in any other format as well as with user stories.

You may now be asking how the relativity ratio between individual user tales should be scaled. Naturally, there must be a greater disparity between them the larger the user story. If not, it would be challenging to distinguish between objects and estimate how much larger they actually are. Let's use circles once more to demonstrate this idea.  

![Story Point Illistration 2](images/SP_and_BDC2.png)

A and B, as well as B and D, differ significantly from one another. However, if you compare D and E, the differences between them are so slight that it is impossible to determine how much they differ. This is the reason why several Agile relative estimating methods represent narrative point values using various scales, or sizes:


* **Fibonacci sequence**: (0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89,...), where each number equals the sum of the two numbers before it.
    * **Benefits**:
        * **Non-Linear Scale**: The gaps between consecutive numbers in the Fibonacci sequence increase as the numbers grow. This non-linear scale reflects the uncertainty and variability inherent in estimating the effort or complexity of tasks.
        * **Reflects Relative Sizing**: It emphasizes the relative sizing of tasks rather than an absolute scale, making it suitable for expressing the inherent uncertainty in estimating work.



* **Linear sequence** in which the same amount is added or subtracted to go from one term to the next (e.g., 1, 2, 3, 4, 5; or 3, 6, 9, 12, 15, 18,...
    * **Benefits**:
        * **Simplicity**: Linear sequences provide a straightforward and simple scale. The effort or complexity increases uniformly with each increment.
        * **Ease of Understanding**: It can be easier for some teams, especially those new to agile practices, to work with a linear scale because of its simplicity.

## Considerations for Choosing Between Fibonacci Sequence vs Linear Sequence:

1. **Uncertainty and Non-Linearity**:
    * **Fibonacci**: Recognizes that as tasks become larger, there's often an increasing level of uncertainty and non-linearity in effort.
    * **Linear**: Assumes a more straightforward and linear relationship between the size of a task and the effort required.
2. **Ease of Use**:
    * **Fibonacci**: Some teams find the Fibonacci sequence more intuitive for capturing the relative complexity of tasks, especially when the differences between task sizes are not consistent.
    * **Linear**: Offers simplicity and ease of use, particularly when team members prefer a straightforward progression.
3. **Psychological Factors**:
    * **Fibonacci**: Can sometimes encourage teams to think in terms of general categories rather than precise values, fostering a more flexible mindset.
    * **Linear**: May make it easier for teams to make precise estimates, but could potentially lead to overemphasis on exact values.

Ultimately, the choice between the Fibonacci sequence and a linear sequence depends on the team's preferences, the nature of their work, and their comfort with the chosen scale. Many teams find success with either approach, and some even use hybrid scales that combine elements of both sequences. The key is to establish a scale that works well for the team and facilitates effective estimation and planning.


### How to Use a Burndown Chart in Agile & Scrum:

To plan and carry out projects, agile project management uses agile sprints. These are brief work periods known as sprints, during which a team works to achieve predetermined objectives that were first discussed and decided upon at the sprint planning meeting. Agile project managers find that burndown charts are quite useful since they help them stay on top of remaining work, assess performance against predetermined standards, and rapidly identify any delays. The following are instances of how an agile or scrum project can be managed with the aid of a burndown chart.

* Create a work management baseline to compare planned vs. actual work
* Complete a gap analysis based on discrepancies
* Get information for future sprint planning meetings
* Reallocate resources and manage tasks to complete sprints on time

### How to Create a Burndown Chart?

Summing the Sprint Backlog estimations for each day of the Sprint will allow you to see how much work is left, as seen in this graph. The total quantity of work left in the Sprint Backlog is the amount of work that is still unfinished for each Sprint. Using the daily totals you keep track of, make a graph that illustrates the amount of work left over over time.

### Burndown Chart Example:

* Duration: 5 days
* Sprint Backlog: 8 tasks
* Velocity: 80 available hours



**Step 1** – Create Estimate Effort

Suppose your ideal baseline for using the available hours over the sprint.  So in the simplest for this is the available hours divided by number of days.  In this example, 80 hours over 5 days equating to 16 hours a day. In order to create the project burn-down chart, the data needs to be captured as a daily running total starting with 80 hours than 64 hours left 1 (80 – 16) at end of day, 48 hours left at end of day 2, etc.

### Burndown- Estimate effort:  

| Day	| Effort Remaining|
|-------|-----------------|
|  0	|  80             |
|  1	|  64             |
|  2	|  48             |
|  3	|  32             |
|  4	|  16             |
|  5	|  0              |

**Step 2** – Track Daily Process

The daily progress is then captured in the table against each task.  It is important to remember that the value captured for each day is the estimated effort to complete the task, not the actual effort.  

|Task	  | Hours |Day - 1|Day - 2 |Day - 3	|Day - 4|Day - 5|Total|
|---------|-------|-------|--------|--------|-------|-------|-----|
|Task - 1 |	10	  |  3	  |  2	   | 0	    | 1	    | 4	    | 10  |
|Task - 2 |	10	  |  3	  |  2	   | 0	    | 1	    | 4	    | 10  |
|Task - 3 |	10	  |  3	  |  2	   | 0	    | 1	    | 4	    | 10  |
|Task - 4 |	10	  |  3	  |  2	   | 0	    | 1	    | 4	    | 10  |
|Task - 5 |	10	  |  3	  |  2	   | 0	    | 1	    | 4	    | 10  |
|Task - 6 |	10	  |  3	  |  2	   | 0	    | 1	    | 4	    | 10  |
|Task - 7 |	10	  |  3	  |  2	   | 0	    | 1	    | 4	    | 10  |
|Task - 8 |	10	  |  3	  |  2	   | 0	    | 1	    | 4	    | 10  |

**Step 3** – Compute the Actual Effort

The total remaining effort needs to be captured at the end of each day.  This is the total (sum) of all of the estimated time remaining at the end of each day.  

|Days|	Actual Effort |	Effort Remaining|
|----|----------------|-----------------|
|0	 |80	          |80               |
|1	 |56	          |64               |
|2	 |40	          |48               |
|3 	 |40	          |32               |
|4	 |32	          |16               |
|5	 |0	              |0                |

**Step 4** – Obtain the Final Dataset

When the data is available, the project burn-down chart can be created.  This is relatively simple using the line chart option available within Excel.  

|Days|	Actual Effort |	Effort Remaining|
|----|----------------|-----------------|
|0	 |80	          |80               |
|1	 |56	          |64               |
|2	 |40	          |48               |
|3 	 |40	          |32               |
|4	 |32	          |16               |
|5	 |0	              |0                |

Highlight the summary table that contains the daily total for baseline effort and estimated effort.  You should also capture the heading of time period (Day 0, Day 1, etc).

**Step 5** – Plot the Burndown using the Dataset

It is very simple to create a project burn-down chart as following, as long as you know what data you are tracking.

### Burndown chart example:
![Burndown Chart Example](images/SP_and_BDC3.png)