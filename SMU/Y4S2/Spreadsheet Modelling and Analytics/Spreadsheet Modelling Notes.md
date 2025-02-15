#### Fill Function (same as copy & paste formulas)
- Done by dragging selected cells with formulas over new cells, which will be automatically filled with same formulas, with the required changes
- By either dragging horizontally or vertically, column letters / row numbers will be updated accordingly
#### Auto-Fill Function (no formulas involved)
- Done by selecting **at least 2 adjacent cells** and dragging over new cells, which will be filled with values by extrapolation automatically
- Basic principle is fitting points with straight line using least-squared method. New cell values are predicted using extrapolation
#### Absolute, Mixed & Relative Referencing
- Relative: without locking row/column
- Mixed: lock either row/column (e.g. $C5 / C$5)
- Absolute: lock both row/column (e.g. $C$5)
### TREND() Function
`trend(known_y, known_x, new_x, [const])`
- tries to predict a new_y using linear relationship between known_y and known_x and using a corresponding new_x
- if const=TRUE or omitted, b is computed. Else if cons=FALSE, b=0
	![|400](images/Pasted%20image%2020240219140906.png)
### Overview of Modelling
**Stages**
1. Model building
	- Formulate the relationships (Influence diagram)
	- Frame what you understand (Black box view)
	- Construct the model (Spreadsheet model)
1. Analysing the Model
#### Influence Diagram
- Draw a picture (**influence diagram**) to better understand the situation
- Identify the **decision variables**, the **parameters**, or **uncontrollable inputs**, and the **outputs**
- Define the **logic** necessary to **transform the inputs into the outputs**
- Determine the **formulas** relating the inputs to the intermediate calculations and outputs
##### Steps in building an influence diagram
- Start with the performance measure 
- Decompose the performance measure into 2 or more intermediate variables that combine mathematically to define the performance measure
- Further decompose each intermediate variables into more intermediate variables until the the input decision variable is define

Example - to determine profit by setting price
- Start with "Profit" and define intermediate variables until the "Price" is defined. Intermediate variables will include demand, revenue, cost, etc. 

![](images/Pasted%20image%2020240219150026.png)
#### Blackbox Model
- Draw the **black box model** to determine where the inputs, intermediate calculations, and outputs will go
- **Highlight** the **key inputs** and **outputs** to make the model easier to use for what-if-analysis
![](images/Pasted%20image%2020240219145839.png)
#### Construct the Model
- Create the **spreadsheet model** and test it using **trial values**
- Verify the results by hand, if possible
### Goal Seek
- Used when you know the desired result of a single formula, but not the input value the formula needs to determine the result
### Solver
- It is a program that searches for the optimal solution of a problem involving several variables
- Solver adjusts the values in the decision variable cells to satisfy the limits on the constraint cells and produces the result you want for the objective cell
### Trade-off Analysis
- Used when a *decision variable* value (e.g. price) is changed, to examine how *performance measure* (e.g. profit) "tradeoff" against each other
- Can also use Solver or Goal Seek
### Sensitivity Analysis
- Used when *uncontrollable parameter values* (e.g. slope of price-demand curves) are changed to examine how "sensitive" *performance measures* (e.g. profit) are to the parameter changes
- **Data Table**
	- 2 uncontrollable parameters - demand curve slope and number of cartridges per printer sold
	- Results of total profit are tabulated in the table
- **Conclusion**: Profit change is more sensitive to demand slope change at higher number of cartridges per printer sold. Model is more robust at lower number of cartridges per printer sold
### Data Tables
- A data table is a range of cells that shows how changing the values of input variables in your formulas affects the results of the formulas
- Data tables calculates multiple results in one operation without the need to bother with relative & absolute referencing
- It allows you to view and compare the results of all the different variations together on your worksheet
#### One-Variable Data Table
![](images/Pasted%20image%2020240219155615.png)
#### Two-Variable Data Table
![](images/Pasted%20image%2020240219155652.png)
## LOOKUP Functions
### lookup()
`lookup(lookup_value, lookup_vector, [result_vector])`
- returns the corresponding *result_value* in the *result_vector* where value in the *lookup_vector* is the largest value but smaller than or equal to the *lookup_value*
	![](images/Pasted%20image%2020240219160658.png)
### VLOOKUP()
`VLOOKUP(lookup_value, table_array, col_index_num, [range_lookup])`
- searches for a value in the **leftmost column** of a table, and then returns a value in the same row from the column as indicated by *col_index_num*
	 ![](images/Pasted%20image%2020240219160846.png)
- If *range_lookup* is TRUE or omitted, `vlookup` returns an **approximate value**, that is the largest value that is less than or equal to the *lookup_value*
- If *range_lookup* is FALSE, `vlookup` returns an **exact match value** when one is found, else returns \#NA
### XLOOKUP()
`XLOOKUP(lookup_value, return_array, [if_not_found], [match_mode], [search_mode])`
- *[if_not_found]* is a text response if an exact match is not found. If *[if_not_found]* is missing, \#NA is returned if an exact match is not found
- *[match_mode]*
	- 0=exact match(default). If not round, return text response or \#NA
	- -1=exact match. If not found, return next smaller item
	- 1=exact match. If not found, return next larger item
	- 2=wildcard match (can use *, ? and ~)
		> ? - any single character
		> * - any number of characters
		> ~ - escape character for ?, *, ~
- *[search_mode]*
	- 1=start from first item(default)
	- -1=start from last item
	- 2=binary search (*lookup_array* must be in ascending order)
	- -2=binary search (*lookup_array* must be in descending order)
### MATCH()
`MATCH(lookup_value, lookup_array, [match_type]`
- Returns a relative position of an item in an array that matches a specified value in a specified order
- Use `MATCH` instead of `LOOKUP` when you need the **position of an item in a range instead of the item itself**
- *[match_type]*
	- 1: returns the relative position of the largest value that is less than or equal to *lookup_value* (default)
	- 0: returns the relative position of the first value that is exactly equal to the *lookup_value*
	- -1: returns the relative position of the smallest value that is greater than or equal to the *lookup_value*
	> Note: *match_type 1 and -1 are approximate matches*
### INDEX() - single row or column
`INDEX(array, row_num, [column_num])`
- If array contains only one row or column, the corresponding, row_num or column_num argument is optional
	![](images/Pasted%20image%2020240219164109.png)
### INDEX() & MATCH()
- allows us to identify values using dynamically changing *row_num* and *column_num* where the *row_num* and *column_num* values are results from using `MATCH` 
### Linear Programming (LP)
- is the problem of minimising (or maximising) a linear cost function subject to linear equality and inequality constraints
- 3 components of the LP model
	![](images/Pasted%20image%2020240219164547.png)
#### Optimisation Results
- 4 possible results for optimisation of LP
	- There exists a **unique optimal solution** and this solution must be at a corner point
	- There exists **multiple optimal solutions**. Objective function line lies exactly on a constraint
	- The **optimal cost is $-\infty$ (or $+\infty$)** for minimisation / maximisation. Feasible region is unbounded
	- There are **feasible solutions**, as there is no feasible region
		![](images/Pasted%20image%2020240219165239.png)
#### Setting Up Objective Function
- Each optimisation problem needs to fulfil an objective, usually to minimise or maximise an objective function value
- You will need to set up a cell to contain the objective function value
- The **objective function value** is a computation of the value which you want to minimise or maximise
#### Setting Up Constraints
- Composed of =, <=, >=
- Constraints can also be used to set the type for decision variables to be integer or binary
- Solver allows you to specify constraints requiring decision variables to assume only integer values in the final solution
### SUMIF()
`SUMIF(range, criteria, sum_range)`
- Returns the sum result of all cells meeting the selection criteria
### CONCATENATE() or &
- We can concatenate text together using `Concatenate() or &`
### SUMIFS()
`SUMIFS(sum_range, criteria_range1, criteria1, [criteria_range2, criteria2], ...)`
- Returns the sum result which satisfies all criteria
### Time Value of Money
![](images/Pasted%20image%2020240219171105.png)
![](images/Pasted%20image%2020240219171120.png)
#### PMT()
`PMT(rate, nper, pv, [fv], [type]`
- Returns the periodic payment amount
- Type: sets the periodic payment type
	- 0 = payment due end of period (default)
	- 1 = payment due beginning of period
- Last 2 arguments in [] are optional when their values are = 0
**Example**
![](images/Pasted%20image%2020240219173041.png)
#### PV()
`PV(rate, nper, pmt, fv, [type]`
- Returns the present value of an investment based on periodic, constant payments of a single future value
- When pmt is entered, fv is optional; when pmt is omitted, then fv must be entered
- type needs to be defined when pmt is non-zero value
**Example**
- rate=8% p.a.; nper=10 months, pmt=-$1037.03 (per month)
- PV(8%/12, 10, -$1037.03) = $10000
- $10000 today is equivalent to a series of future monthly payments of $1037.03 for 10 months
#### FV()
`FV(rate, nper, pmt, pv, [type])`
- Returns the value of an investment based on periodic, constant payments, or a single investment today
- When pmt is entered, pv is optional; when pmt is omitted, then pv must be entered
- type needs to be defined when pmt is non-zero value
**Example**
![](images/Pasted%20image%2020240219173849.png)
#### RATE()
`RATE(nper, pmt, pv, fv, [type], [guess]`
- Returns the interest rate per period of an annuity
- RATE is calculated by iteration and can have zero or more solutions. If the successive results of RATE do not converge within 0.0000001 after 20 iterations, RATE returns \#NUM! error
- When pmt is ignored, then fv must be entered, else fv is optional
- type needs to be defined when pmt is non-zero value
- guess is the initial guess for rate. If omitted, **Excel will use 10% as initial guess**
#### NPER()
`NPER(rate, pmt, pv, [fv], [type]`
- Returns the number of periods for an investment based on periodic, constant payments and a constant interest rate
#### NPV()
`NPV(rate, value1, value2, ...)`
- Calculates the net present value of an investment by using a discount rate and a series of future payments (negative values) and income (positive values)
- Rate is the discount rate applied to future payments (-) or incomes (+) to compute present worth, and must be expressed in the same time period as the values
- Each value must be equally spaced in time
- **If your first investment occurs at the beginning of the first period, the first value must be added to the NPV result, and not included in the values arguments**

Different from the `PV()` function
- PV() allows cash flows to begin at the end of at the beginning of the period
- PV() cash flows must be constant throughout the investment
#### IRR()
`IRR(values, [guess])`
- Returns the internal rate of return for a series of cash flows represented by the numbers in values
- The internal rate of return is the interest rate received for an investment consisting of payments (negative values) and income (positive values) that occur at regular periods
- Cash flow values need not be the same but must be equally spaced in time and occur at the end of each period
- Values must contain at least one positive value (income) and one negative value (payment)
- IRR calculation is iterative until the result is accurate within 0.00001 percent. After 20 iterations, RATE returns \#NUM! error. Add a guess value to enhance search
- **IRR is related to NPV. IRR is the interest rate corresponding to a zero net present value**
### Circular Reference
- When a formula refers back to its own cell, either directly or indirectly
- Resolved by iteration, following the recalculation order
### Monte Carlo Simulation
- Refers to simulating scenarios repeatedly using random generation of input variables to the model
- Random generation of input variables can be obtained from known distribution if you know which distribution best describes the input variable
- We can analyse the results obtained from multiple scenarios to determine desired outputs
### Random Generators
`RAND()`
- Generates a random number between 0 and 1.0 (excluding 1)
- Probability Density Function (PDF) > Continuous Uniform Distribution
`RANDBETWEEN()`
- Returns a random integer number defined between bottom and top (inclusive)
- Probability Mass Function (PMF) > Discrete Uniform Distribution
### Data Simulation
1. Using Frequency Bins
	- Build a CRF table and use RAND() function to match CRF to get new X'
	- Different ways to build CRF table
		1. frequency count
		2. percentage of occurrence
2. Using Re-sampling
	1. Discrete data - use `SMALL(array, RANDBETWEEN(1, N))`
	2. Continuous data - use `PERCENTILE(array, RAND())`
3. Using Inverse Distribution
	1. Discrete distribution (Uniform, Poisson, Binomial)
	2. Continuous distribution (many)

![](images/Pasted%20image%2020240220082730.png)
![](images/Pasted%20image%2020240220132924.png)
#### Method 1: Frequency Bins
- compute the CRF of data X and build the CRF table
- Then, use `RAND()` to generate a random number between 0 and 10
- This number is compared with the CRF table using `LOOKUP()` and returns the simulated data X'
	![](images/Pasted%20image%2020240220133937.png)
#### Method 2a: Discrete Data Resampling
- We use `RANDBETWEEN(1, N)` to generate a random integer number from 1 to the number of raw data points N, say k. This number is used to return the $k^{th}$ value in the raw data collection as if the raw data is already **SORTED** in ascending order
> Note: While `RANDBETWEEN()` returns each number within 1 and N equally likely, the end result from the raw data will not be returned equally likely. It will depend on the frequency of the data
- The end result will still be reflective of the actual situation where higher frequency data will occur more likely than lower frequency data
#### Method 2b: Continuous Data Resampling
- `PERCENTILE` and `SMALL` will sort the raw data in ascending order (in memory)
- For a percentile value(k) provided by `RAND()`, it is rather unlikely that the `RAND()` value will coincide with the actual percentile values of the raw data. Thus, interpolation often occurs
	![|450](images/Pasted%20image%2020240220135514.png)
### Probability Functions
- Discrete Uniform Distribution -> probability mass function (pmf)
- Continuous Uniform Distribution -> probability density function (pdf)
- Cumulatively, both discrete and continuous functions will sum to 1.0 (which is the total probability) and known as cumulative distribution function (cdf)
#### Discrete
- Binomial `BINOMDIST(number_s, trials, probability_s, cumulative)`
- Poisson `POISSON(x, mean, cumulative)`
#### Continuous
- Exponential `EXPONDIST(x, 1/mean, cumulative)`
- Normal
	- `NORMSDIST(z)`
		- returns the cumulative probability for a given z for a standard normal distribution
	- `NORMDIST(x, mean, standard_dev, cumulative)`
		- returns the cumulative probability for a given x if cumulative is set to TRUE, and returns the probability density function for a given x if cumulative is set to FALSE 
- When we need to simulate more data points, we need to invert the functions
	- `NORMINV(RAND(), mean, stdev)`
	- `NORMSINV(RAND())`
#### Method 3A: Inverting Continuous Distribution
- Uniform: `X' = min + RAND()*(max-min)`
- Normal: `X'= NORMINV(RAND(), mean, SD)`
- Exponential:
	- `X' = (-Mean)*LN(RAND())`
	- `X' = (-Mean)*LN(1-RAND())`
#### Method 3b: Inverting Discrete Distribution
- Uniform: `X'=RANDBETWEEN(min, max)`
- Binomial:
	- `X' = CRITBINOM(n, p, RAND())`
	- `X' = BINOM.INV(n, p, RAND())`
- Poisson:
	- `X' = CRITBINOM(n, mean/n, RAND())`
	- `X' = BINOM.INV(n, mean/n, RAND())`
### Date and Time Management
Excel stores dates as sequential numbers that are called serial values
#### Date Functions
- `TODAY()` returns the current date
- `YEAR(serial_number)` returns the year corresponding to the serial number
	- WRONG: `YEAR(14-Jan-05)`
	- OK: `YEAR("14-Jan-05")`
- `MONTH(serial_number)` returns the month
- `DAY(serial_number)` returns the day corresponding to the serial number
	- `MONTH(39014)=10`, `DAY(39014)=24`; 39014 is 24th Oct 2006
- `DATE(year, month, day)` returns the serial number
- Subtraction
	- WRONG: 14-Jan-05 - 23-Sep-04
	- OK: "14-Jan-05" - "23-Sep-04"
#### Time Functions
- Time is stored as decimal fractions because it is considered as portion of a day. That is, they are digits to the right of a decimal point
- `NOW()` returns the current date and time
	- 38711.33333333 for 8:00AM on that day
- `HOUR(serial_number)`, `MINUTE(serial_number`, `SECOND(serial_number)`
- `TIME(hour, minute, second)` returns the serial number to the right of the decimal point in the format 0.XXXXX
