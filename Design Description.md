# Requirements and Design Description

1.	When the app is started, the user is presented with the main menu, which allows the user to 
(1) enter or edit current job details, (2) enter job offers, (3) adjust the comparison settings, 
or (4) compare job offers (disabled if no job offers were entered yet ). 

- To realize this requirement, I added class 'System' and its three operations 'createMyCurrentJob()', 'createMyJobOffer()', and 'compareJobOffers()' to my class diagram. 

- I added another class 'Jobs', which consists of current job and job offers. I added an attribute 'isCurrentJob: boolean' to distinguish current job and job offers.

- Use relationship 'Association' between class 'System' and 'Jobs'.


2.	When choosing to enter current job details, a user will:

a.	Be shown a user interface to enter (if it is the first time) or edit all of the details of their current job, which consist of:

- Add 'enterJob()' and 'editJob()' to class 'Jobs' as operations.

i.	Title

- Add 'title: String' to class 'Jobs' as an attribute.

ii.	Company

- Add 'company: String' to class 'Jobs' as an attribute.

iii.	Location (entered as city and state)

- Add 'city: String' and 'state:String' to class 'Jobs' as an attribute.

iv.	Cost of living in the location (expressed as an index)

- Add 'costLiving: int' to class 'Jobs' as an attribute.

v.	Possibility to work remotely (expressed as the number of days a week one could work remotely, between 1 and 5)

- Add 'remoteWorkDay: int' to class 'Jobs' as an attribute.

vi.	Yearly salary

- Add 'yearlySalary: int' to class 'Jobs' as an attribute.

vii.	Yearly bonus

- Add 'yearlyBonus: int' to class 'Jobs' as an attribute.

viii.	Retirement benefits (as percentage matched)

- Add 'retireBenefit: double' to class 'Jobs' as an attribute.

ix.	Leave time (vacation days and holiday and/or sick leave, as a single overall number of days)

- Add 'leaveTime: int' to class 'Jobs' as an attribute.

b.	Be able to either save the job details or cancel and exit without saving, returning in both cases to the main menu.

- Add 'saveJob()' and 'cancelJob()' to class 'Jobs' as operations.


3.	When choosing to enter job offers, a user will:

a.	Be shown a user interface to enter all of the details of the offer, which are the same ones listed above for the current job.

- Since the attributes of job offers are the same as current job, I put them all in class 'Jobs'. I added attribute 'jobID:int' to class 'Jobs' to identity each job.

b.	Be able to either save the job offer details or cancel.

- Already added 'saveJob()' and 'cancelJob()'.

c.	Be able to (1) enter another offer, (2) return to the main menu, or (3) compare the offer with the current job details (if present).

- Add operation 'returnMainMenu()' and 'compareCurrent()' to class 'Jobs'.


4.	When adjusting the comparison settings, the user can assign integer weights to:

- Add class 'JobComparison'. Use relationship 'Association' between class 'System' and 'JobComparison'.

a.	Possibility to work remotely

- Add 'remoteWeight: int' to class 'JobComparison' as an attribute.

b.	Yearly salary

- Add 'salaryWeight: int' to class 'JobComparison' as an attribute.

c.	Yearly bonus

- Add 'bonusWeight: int' to class 'JobComparison' as an attribute.

d.	Retirement benefits

- Add 'retireWeight: int' to class 'JobComparison' as an attribute.

e.	Leave time

- Add 'leaveTimeWeight: int' to class 'JobComparison' as an attribute.

If no weights are assigned, all factors are considered equal.

- Set default value of above attributes to 1.

5.	When choosing to compare job offers, a user will:

a.	Be shown a list of job offers, displayed as Title and Company, ranked from best to worst (see below for details), and including the current job (if present), clearly indicated.

- Add opreation 'getList()' to class 'JobComparison'.

b.	Select two jobs to compare and trigger the comparison.

- Add opreation 'selectJobs()' to class 'JobComparison'.

c.	Be shown a table comparing the two jobs, displaying, for each job:

- Add opreation 'showTable()' to class 'JobComparison'.

i.	Title

ii.	Company

iii.	Location

iv.	Yearly salary adjusted for cost of living

v.	Yearly bonus adjusted for cost of living

vi.	Retirement benefits (as percentage matched)

vii.	Leave time

- Use relationship 'Association' between class 'Jobs' and 'JobComparison'.

d.	Be offered to perform another comparison or go back to the main menu.

- Add operation 'returnMainMenu()' to class 'JobComparison'.


6.	When ranking jobs, a job¡¯s score is computed as the weighted sum of:

AYS + AYB + (RBP * AYS) + (LT * AYS / 260) - ((260 - 52 * RWT) * (AYS / 260) / 8)

- Add class 'JobScore'. Add operation 'rankJob():int' to class 'JobScore'.

where:
AYS = yearly salary adjusted for cost of living

- Add 'AYS: int' to class 'JobScore' as an attribute.

AYB = yearly bonus adjusted for cost of living

- Add 'AYB: int' to class 'JobScore' as an attribute.

RBP = retirement benefits percentage

- Add 'RBP: double' to class 'JobScore' as an attribute.

LT = leave time

- Add 'LT: int' to class 'JobScore' as an attribute.

RWT = remote work days per week

- Add 'RWT: int' to class 'JobScore' as an attribute.

The rationale for the RWT subformula is:

a.	value of an employee hour = (AYS / 260) / 8

b.	commute hours per year (assuming a 1-hour/day commute) =
1 * (260 - 52 * RWT)

c.	therefore commute-time cost = (260 - 52 * RWT) * (AYS / 260) / 8

For example, if the weights are 2 for the yearly salary, 2 for the retirement benefits, and 1 for all other factors, the score would be computed as:

2/7 * AYS + 1/7 * AYB + 2/7 * (RBP * AYS) + 1/7 * (LT * AYS / 260) - 1/7 * ((260 - 52 * RWT) * (AYS / 260) / 8)

- Add operation 'getScore():int' to class 'JobScore'.

- Use relationship 'Association' between class 'Jobs' and 'JobScore'.

- Use relationship 'Dependency' between class 'JobScore' and 'JobComparison' ('JobComparison' uses 'JobScore').


7.	The user interface must be intuitive and responsive.


8.	For simplicity, you may assume there is a single system running the app (no communication or saving between devices is necessary)

- Since it is a single system app, I didn't create a 'User' class.
