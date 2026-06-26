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
