# Requirements and Design Description

1.	When the app is started, the user is presented with the main menu, which allows the user to 
(1) enter or edit current job details, (2) enter job offers, (3) adjust the comparison settings, 
or (4) compare job offers (disabled if no job offers were entered yet ). 

- To realize this requirement, I added class 'CurrentJob', 'JobOffers', and 'JobComparison' to my class diagram. 

2.	When choosing to enter current job details, a user will:

a.	Be shown a user interface to enter (if it is the first time) or edit all of the details of their current job, which consist of:

i.	Title

- Add 'title: String' to class 'CurrentJob' as an attribute.

ii.	Company

- Add 'company: String' to class 'CurrentJob' as an attribute.

iii.	Location (entered as city and state)

- Add 'city: String' and 'state:String' to class 'CurrentJob' as an attribute.

iv.	Cost of living in the location (expressed as an index)

- Add 'costofLiving: int' to class 'CurrentJob' as an attribute.

v.	Possibility to work remotely (expressed as the number of days a week one could work remotely, between 1 and 5)

- Add 'remoteWorkDay: int' to class 'CurrentJob' as an attribute.

vi.	Yearly salary

- Add 'yearlySalary: int' to class 'CurrentJob' as an attribute.

vii.	Yearly bonus

- Add 'yearlyBonus: int' to class 'CurrentJob' as an attribute.

viii.	Retirement benefits (as percentage matched)

- Add 'retireBenefit: double' to class 'CurrentJob' as an attribute.

ix.	Leave time (vacation days and holiday and/or sick leave, as a single overall number of days)

- Add 'leaveTime: int' to class 'CurrentJob' as an attribute.

b.	Be able to either save the job details or cancel and exit without saving, returning in both cases to the main menu.
3.	When choosing to enter job offers, a user will:
a.	Be shown a user interface to enter all of the details of the offer, which are the same ones listed above for the current job.
b.	Be able to either save the job offer details or cancel.
c.	Be able to (1) enter another offer, (2) return to the main menu, or (3) compare the offer with the current job details (if present).
4.	When adjusting the comparison settings, the user can assign integer weights to:
a.	Possibility to work remotely
b.	Yearly salary
c.	Yearly bonus
d.	Retirement benefits
e.	Leave time
If no weights are assigned, all factors are considered equal.
5.	When choosing to compare job offers, a user will:
a.	Be shown a list of job offers, displayed as Title and Company, ranked from best to worst (see below for details), and including the current job (if present), clearly indicated.
b.	Select two jobs to compare and trigger the comparison.
c.	Be shown a table comparing the two jobs, displaying, for each job:
i.	Title
ii.	Company
iii.	Location
iv.	Yearly salary adjusted for cost of living
v.	Yearly bonus adjusted for cost of living
vi.	Retirement benefits (as percentage matched)
vii.	Leave time
d.	Be offered to perform another comparison or go back to the main menu.
6.	When ranking jobs, a job¡¯s score is computed as the weighted sum of:

AYS + AYB + (RBP * AYS) + (LT * AYS / 260) - ((260 - 52 * RWT) * (AYS / 260) / 8)

where:
AYS = yearly salary adjusted for cost of living
AYB = yearly bonus adjusted for cost of living
RBP = retirement benefits percentage
LT = leave time
RWT = remote work days per week
The rationale for the RWT subformula is:
a.	value of an employee hour = (AYS / 260) / 8
b.	commute hours per year (assuming a 1-hour/day commute) =
1 * (260 - 52 * RWT)
c.	therefore commute-time cost = (260 - 52 * RWT) * (AYS / 260) / 8

For example, if the weights are 2 for the yearly salary, 2 for the retirement benefits, and 1 for all other factors, the score would be computed as:

2/7 * AYS + 1/7 * AYB + 2/7 * (RBP * AYS) + 1/7 * (LT * AYS / 260) - 1/7 * ((260 - 52 * RWT) * (AYS / 260) / 8)

7.	The user interface must be intuitive and responsive.
8.	For simplicity, you may assume there is a single system running the app (no communication or saving between devices is necessary)
