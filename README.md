1. << To create DataBase >>

CREATE DATABASE CENSUS_2011  ;

2. << To select DataBase >>

USE CENSUS_2011 ;

3. << Now Import data from our computer System , the data is recorded as csv file >>

For importing the data , I clicked on my Database CENSUS_2011 and there is a option to import data
 and then I browse it from my computer resources


4. << After importing the two data csv file , I renamed the data set as data1 and data2 respectively >>

	ALTER TABLE data3
	RENAME TO data1 ;
    
    
5 << To Show Data in the TABLE >> 

    SELECT *FROM  data1 
    SELECT *FROM data2 ;

6 << To Count no. of rows in both of the dataset >>

    Select count(*) from data1 
	Select count(*) from data2
    
				
				
7 << To Show the data of "BIHAR" AND "UTTAR PRADESH" >>

     Select *from data1 WHERE  state in ('BIHAR' , 'UTTAR PRADESH')
             
             
8 << COUNT No. of rows in both of the state "BIHAR" AND "UTTAR PRADESH" >>
     
     
     select count(*) from data1 where state in('BIHAR','UTTAR PRADESH')    
      
                
                
9 << To Show the Name_of_all_Districts and  population of ALL Districts of "BIHAR" and "UTTAR PRADESH" >>

	select  District , Population from data2 where state in("BIHAR" , "UTTAR PRADESH");


10 << Sum of Total population of INDIA >>
   
      Select sum(Population) as population  from  data2;
    
              
      
11 << Average growth % by state  >>
       
	Select state ,round(Avg(growth)*100) as Avg_Growth_percentage from data1 group by state ;
         
                
12 << Avg Sex_Ratio  >>  
	
    select state , round(avg(sex_ratio),0) as Avg_Sex_Ratio from data1
	group by state  order by Avg_Sex_Ratio desc;   
    
13 << Avg Literacy_Rate >>
                
	select state , round(avg(literacy),0) as Avg_Literacy_Rate  from data1
	group by state having round(avg(literacy),0) > 90 order by Avg_Literacy_Rate desc;   
    
                
14 << Top 3 State Showing Heighest Growth_rate >>

    select state , round(avg(growth)*100,0) as Avg_Growth_Rate  from data1
    group by state  order by Avg_Growth_Rate desc limit 3 ;   
    
	
15 << Bottom 3 state showing Lowest Sex_Ratio >> 
      
	select State , round(avg(sex_ratio),0) as avg_sex_ratio from data1
	group by state order by avg_sex_ratio desc limit  3 ;     
       
       
16 << Top 3 state showing highest Literacy_Rate in different table >> 

DROP TABLE IF EXISTS top_state;
create table top_state(state varchar(40) not null,
tops_state float )

  insert into top_state  select State , round(avg(literacy),0) as avg_literacy_rate from data1
  group by state order by avg_literacy_rate desc limit 3 ;
       
       
     select *from top_state 
     
     
17 << Bottom 3 State showing low Literacy_Rate in different table >>      
     
   DROP TABLE IF EXISTS bottom_state; 
    create table bottom_state(state varchar(40) not null,
    bottom_state float );

    insert into bottom_state  select State , round(avg(literacy),0) as avg_literacy_rate from data1
	group by state order by avg_literacy_rate asc limit 3 ;
       
       select *from bottom_state
       
       
18 << Joining of 2 tables by  UNION command to show Highest and Lowest Literacy_rate >>   
       
        
    Select * from   (select *from top_state order by tops_state desc limit 3 )a
       
	union
      
	Select * from  (select *from bottom_state order by bottom_state asc limit 3)b
        

19 << State name starting with letter "A"  >>        
  
    select distinct state from data1  where state like "A%" ;
    
20 << Joining Both Table >> 

  select  data1.district , data1.state , data1.sex_ratio, data2.population  from data1
  inner join data2
  on data1.district = data2.district;
  
 

