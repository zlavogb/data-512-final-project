# Project: University of Washington, DATA 512 Autumn 2019, Final Project
# Title: An analysis of Higher Education Public Employee Earnings Data

## Author: Bianca Zlavog
## License: This work is available under an MIT license, included in the repository. All input data is published by the US government, and is therefore in the public domain.
## Course website: https://wiki.communitydata.science/Human_Centered_Data_Science_(Fall_2019)/Assignments#A7:_Final_project_report

 
## Project summary 
I studied how the pay of public employees varies across different positions, institutions, states, and time, among public higher education institutions in Washington and California. After cleaning the input data, I classified employees by job title into different job types, and compared the median earnings of different types of jobs across different institutions and states, accounting for relative price levels. I also investigated the types of positions which are most highly paid. The highest-paid employees included athletic coaches and professors, though at the median, executives and professors earned the most. While students made up a substantial proportion of California employees, they earned a very small proportion of salaries. I found that California median earnings exceed Washington median earnings across almost all job types, even when adjusting for relative costs of living across the two states. While this data is valuable in beginning to analyze these trends, I identify a need for greater transparency, especially around length of employment, hours worked, funding sources, and particular job functions.

 
## Input data

- [Washington state employee earnings, 2014-2018](http://fiscal.wa.gov/Salaries.aspx). 
This dataset is available for download in XLSX format from the Washington states fiscal information site, produced by the Legislative Evaluation and Accountability Program Committee in collaboration with the Office of Financial Management. The dataset contains information on all Washington state employees, the agency they work for, their job titles, and earnings information from 2014 to 2018 expressed in nominal dollars. This data is publicly available information pursuant to [RCW 42.56.210](https://app.leg.wa.gov/RCW/default.aspx?cite=42.56.210). Employee names have been removed from the hosted data in this repository.

- [Washington state employee earnings, 2010-2013](https://data.wa.gov/Labor/Annual-Salary-2010-thru-2013/y3ds-rkew). 
Similar to the more recent dataset, this separate dataset contains data for 2010-2013. Employee names have been removed from the hosted data in this repository.

<details>
  <summary>Data Fields</summary>
	
| Variable      | Description |
| -----------   | ----------- |
| Agy           | Employer agency code |
| AgyTitle      | Employer agency name |
| Name          | Employee name, removed from hosted dataset |
| JobTitle      | Employee job title |
| Sal2010       | Salary in 2010 |
| Sal2011       | Salary in 2011 |
| Sal2012       | Salary in 2012 |
| Sal2013       | Salary in 2013 |
| Sal2014       | Salary in 2014 |
| Sal2015       | Salary in 2015 |
| Sal2016       | Salary in 2016 |
| Sal2017       | Salary in 2017 |
| Sal2018       | Salary in 2018 |
 
</details>


- [California state employee earnings data, 2010-2018](https://publicpay.ca.gov/Reports/RawExport.aspx).
This data is available for download in zipped CSV format from the California State Controller's Office, with a file for each agency and year. California Sate University data is available from 2010-2018, University of California data is available from 2013-2018, and college data is available from 2011-2018. These datasets contain the employing agency of all California state public employees, job titles, and salary information expressed in nominal dollars, as well as value of benefits earned, from 2010 to 2018. A number of other fields are available which are not used in this analysis. 
This data is published by the US government, and is publicly available information pursuant to [California Government Code section 12463](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=GOV&sectionNum=12463).

<details>
  <summary>Data Fields</summary>
	
| Variable      | Description |
| -----------   | ----------- |
| Year           | Calendar year of reported data |
| EmployerType      | Employer agency type |
| EmployerName          | Employer agency name |
| DepartmentOrSubdivision      | Employer department name  |
| Position       |  Employee job title |
| ElectedOfficial       |  Whether the employee was elected to their position |
| Judicial       | Whether the employee belongs to a judicial position |
| OtherPositions       | Any other job titles the employee held with the respective agency during the calendar year |
| MinPositionSalary       | Minimum annual salary for the position |
| MaxPositionSalary | Maximum annual salary for the position |
| ReportedBaseWage | Base salary, only applicable for data before 2011 |
| RegularPay | Base salary earned in the calendar year |
| OvertimePay | Overtime salary earned in the calendar year |
| LumpSumPay | One-time salary payments earned in the calendar year |
| OtherPay | Other salary earned in the calendar year |
| TotalWages | Total salary earned in the calendar year |
| DefinedBenefitPlanContribution | Employer contribution to benefit plan |
| EmployeesRetirementCostCovered | Employee contribution to benefit plan |
| DeferredCompensationPlan | Employer contribution to retirement plan |
| HealthDentalVision | Employer contribution to health plan |
| TotalRetirementAndHealthContribution | Total employer contribution to benefit plans |
| PensionFormula | Pension formula determining employee retirement benefits |
| EmployerURL | Web address of employer agency |
| EmployerPopulation | Population of employer agency |
| LastUpdatedDate | Date the employer's data was last updated |
| EmployerCounty | County that an employer is based in |
| SpecialDistrictActivities |  special district information |
| IncludesUnfundedLiability |  whether employer agency includes payments toward the unfunded liability of the employer sponsored retirement plan |
| SpecialDistrictType | special district information |

</details>

- [Bureau of Economic Analysis Regional Price Parities by State and Metro Area, 2010-2017](https://www.bea.gov/data/prices-inflation/regional-price-parities-state-and-metro-area). This dataset evaluates price levels between different states, which will allow us to compare employee earnings accounting for differences in costs of living.

Date all data was accessed: November 10, 2019

## Data considerations
- If someone began their employment partway through the calendar year, only the total amount earned over the period they worked is reported, rather than total annual salary. This will skew the data toward lower salaries and it will be unlikely that these observations can be filtered out without additional information on date range worked or hours worked.
- Some employees in the dataset (such as sports coaches or research faculty) [are not paid directly by tax funds](http://fiscal.wa.gov/SalaryDataFAQ.pdf), but rather by funding raised by their department or research grants. In addition, some employee salaries in the academic sector may be funded by grants rather than taxes. This makes it harder to identify which employees' salaries are directly funded by taxpayers.
- In the Washington state data, student employees are subject to stricter privacy laws around salary information, so job groups such as teaching assistants [are not available in the data](http://fiscal.wa.gov/SalaryPersonnelIncluded.pdf).
- Unionized employees likely earn higher salaries than non-unionized employees, but employee union status is not available in this database, so it will be harder to parse out pay differences due to union status.
- There is no information available on part time or full time employee status, which is likely another driver of pay differences.
- Employee turnover introduces noise in the salary data, as different employees may not earn the same wages in the same position due to a number of factors such as experience level, educational level, and salary bargaining. However, if we assume this noise is uniform in the data, it should not impact the validity of these analyses.
- There are hundreds of thousands of unique job titles in the data, which will make it difficult to effectively classify all employees into a few defined job types.


## Output data

- One file contating all Washington and California higher education employees earnings data, saved as `edu_salaries.csv`.
Fields included: 
`year`: Calendar year of data
`employer`: Name of employer institution
`title`: Employee job title
`salary`: Total earnings in the given calendar year
`state`: State of employer institution

- One file containing regional price parity factors for the two states, saved as `state_ppp.csv`.
Fields included: 
`state`: State of employer institution
`year`: Calendar year of data
`adj`: State price parity adjustment factor

## Software used

- MacOS Mojave 10.14.6

- ipython 7.2.0

- RStudio 1.1.383

- R 3.5.2