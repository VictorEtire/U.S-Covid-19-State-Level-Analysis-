Select *
from vaccinations_us;

Select 
state, date, 
total_vaccinations, 
total_distributed, 
people_vaccinated, 
daily_vaccinations
from vaccinations_us
order by 1, 2;

-- Looking at Total_distributed vs People_vaccinated

Select 
state, date, 
total_distributed, 
daily_vaccinations, 
people_vaccinated,(people_vaccinated/total_distributed)*100 
as successful_vaccinated_percentage
from vaccinations_us
order by 1, 2;

-- Looking at Total_distributed vs Daily_vaccination
Select 
state, date, 
total_distributed,
people_vaccinated,  
daily_vaccinations,(daily_vaccinations/total_distributed)*100
as successful_daily_vaccinated_percentage
from vaccinations_us
order by 1, 2;

-- Total vaccinations by state (Top 20)
Select state,
MAX(total_vaccinations) AS total_vaccinations
FROM vaccinations_us
GROUP BY state
ORDER BY total_vaccinations DESC
LIMIT 20;

-- Top 20 states with the most distributed vaccines 
Select state,
MAX(total_distributed) AS total_distributed
FROM vaccinations_us
GROUP BY state
ORDER BY total_distributed DESC
LIMIT 20;

-- Latest Vaccination Numbers (National Overview for 3 States)
Select 
	date AS snapshot_date,
    total_vaccinations,
    people_vaccinated,
    people_fully_vaccinated,
    total_boosters
    FROM vaccinations_us
    WHERE state = 'Alabama'
    ORDER BY date DESC
    LIMIT 1;

Select 
	date AS snapshot_date,
    total_vaccinations,
    people_vaccinated,
    people_fully_vaccinated,
    total_boosters
    FROM vaccinations_us
    WHERE state = 'California'
    ORDER BY date DESC
    LIMIT 1;
    
Select 
	date AS snapshot_date,
    total_vaccinations,
    people_vaccinated,
    people_fully_vaccinated,
    total_boosters
    FROM vaccinations_us
    WHERE state = 'Pennsylvania'
    ORDER BY date DESC
    LIMIT 1;
  
  -- Vaccine Distribution Efficiency and Utilization Rate
    
Select 
state,
MAX(total_distributed) AS
total_distributed,
MAX(total_vaccinations) AS 
total_vaccinations,
ROUND((MAX(total_vaccinations)/MAX(total_distributed))*100,2)
AS calculated_utilization_rate,
ROUND(MAX(share_doses_used)
*100,2)AS
max_recorded_share_pct
FROM vaccinations_us
WHERE state NOT IN ('United
States', 'Dept of Defense', 'Bureau
of Prisons', 'Veterans Health',
'Indian Health Svc', 'Long Term Care')
GROUP BY state
HAVING total_distributed > 0
ORDER BY
calculated_utilization_rate DESC;


-- Average Daily Vaccinations By States
Select state,
AVG(daily_vaccinations) AS avg_daily_vaccinations
FROM vaccinations_us
GROUP BY state
ORDER BY avg_daily_vaccinations DESC;


-- Monthly Data of Daily Vaccinations in General and 3 Highlighted States

Select
    DATE_FORMAT(`date`, '%Y-%m') AS 'year_month',
    SUM(daily_vaccinations) AS total_vaccinations_per_month,
    ROUND(AVG(daily_vaccinations), 0) AS avg_daily_vaccinations
FROM vaccinations_us
WHERE state NOT IN (
    'United States',
    'Dept of Defense',
    'Bureau of Prisons',
    'Veterans Health',
    'Indian Health Svc',
    'Long Term Care'
)
GROUP BY DATE_FORMAT(`date`, '%Y-%m')
ORDER BY 'year_month';


-- In Colorado
Select
    DATE_FORMAT(`date`, '%Y-%m') AS 'year_month',
    SUM(daily_vaccinations) AS total_vaccinations_per_month,
    ROUND(AVG(daily_vaccinations), 0) AS avg_daily_vaccinations
FROM vaccinations_us
WHERE state = 'Colorado'
GROUP BY DATE_FORMAT(`date`, '%Y-%m')
ORDER BY 'year_month';

-- In Florida

Select
    DATE_FORMAT(`date`, '%Y-%m') AS 'year_month',
    SUM(daily_vaccinations) AS total_vaccinations_per_month,
    ROUND(AVG(daily_vaccinations), 0) AS avg_daily_vaccinations
FROM vaccinations_us
WHERE state = 'Florida'
GROUP BY DATE_FORMAT(`date`, '%Y-%m')
ORDER BY 'year_month';

-- In Idaho

Select
    DATE_FORMAT(`date`, '%Y-%m') AS 'year_month',
    SUM(daily_vaccinations) AS total_vaccinations_per_month,
    ROUND(AVG(daily_vaccinations), 0) AS avg_daily_vaccinations
FROM vaccinations_us
WHERE state = 'Idaho'
GROUP BY DATE_FORMAT(`date`, '%Y-%m')
ORDER BY 'year_month';

