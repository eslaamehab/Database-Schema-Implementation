Schema 1
Data Inserted:
15 Departments inserted CS1-CS15
For Each department :
There are 15 Courses CSEN1-CSEN15
400 Students
And 10 Instructors












Query 1
Without Index



Flags:
	set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan: 
	 Tables section and takes undergo Nested Loop Inner Join
	 Output is then Materialized and Fully Merge Joined with table student.
	 Sequential scan on tables student, section and takes.

Avg Planning time= 1.340+1.010+0.806/3=1.052ms
Avg Execution time= 7.023+5.040+4.712/3=5.591ms





B+ Tree Index





Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=false;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;

Execution Plan: 
	Index is created on tables takes and section on column section_id
	The indices are Merge inner Joined together
	This output is materialized and Merge fully joined with table student.
	Index scan using takesindex and sectionindex
	Sequential scan on table student
	
Avg Planning time= (0.991+ 1.336 +1.344)/3= 1.224ms
Avg Execution time= (3.372 +4.151 +5.467)/3= 4.330ms

Bitmap Index




Flags:
	set enable_indexscan=true; 
	set enable_indexonlyscan=true; 
	set enable_bitmapscan=true; 
	set enable_hashjoin=false; 
	set enable_sort=false; 
	set enable_nestloop=true; 
	set enable_material=true; 
	set enable_hashagg=false; 
	set enable_seqscan=true;

Execution Plan:
	The index on table takes is used then the result is Nested loop inner joined 	with table section.
	This output is then materialized and merge fully joined with table student.
	


Avg Planning time= (0.178+0.175+0.172)/3=0.175 ms
Avg Execution time= (0.038+0.038+0.037)/3=0.038 ms








Hash Index






Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=true;
	set enable_sort=true;
	set enable_nestloop=false;
	set enable_material=false;
	set enable_hashagg=false;
	set enable_seqscan=true;

Execution Plan:
	Table section is hashed then Hash inner joined with table takes
	This output is then materialized and merge fully joined with table student.

Avg Planning time= (0.316+0.240+0.221)/3=0.259ms
Avg Execution time= (0.111+0.054+0.043)/3=0.069ms





Final Conclusion For Query1:
As we can see from the results the Bitmap index achieved the fastest execution and planning time.
Followed by the bitmap, the hash is the second fastest then the B+ Tree index and finally the query without indexing.

Bitmap indexing first does a normal sequential scan on table student and then on table section.
Followed by bitmap heap scan on table takes and bitmap index on takesindex.
































Schema 2
Data Inserted:
5000 employees, 30 departments, 20 department locations, and 600 projects















Query 2
Without Index














Flags:
	set enable_indexscan=false;
	set enable_indexonlyscan=false;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=true;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;



Avg Planning time= (0.209+0.358+0.310)/3=0.292ms
Avg Execution time= (1.166 +1.166+1.268)/3=1.200ms




























B+ Tree Index

Index created on employee on column last name


Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=true;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;

Avg Planning time= 0.356 +0.352+0.342/3=0.350 ms
Avg Execution time= 0.138+0.138+0.137/3=0.138 ms




Bitmap Index
		

Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=true;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;




Avg Planning time= (0.479+0.449+0.352)/3 = 0.426ms
Avg Execution time= (1.410+1.263+1.389)/3 = 1.354ms




Hash Index




	Index created on employee on column last name

Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=true;
	set enable_sort=false;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=true;
	set enable_seqscan=true;



Avg Planning time= (0.426+0.367+0.331)/3= 0.374ms
Avg Execution time= (0.141+0.153+0.115)/3=0.136ms























--Final Conclusion For Query2:










































Query 3
Without Index




Flags:
	set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

-----Execution Plan:
	--check 
	 Sequential scan on table employee and rows are filtered
	 Sequential scan on employee

Avg Planning time= 0.104 +0.137+0.110/3=0.117 ms
Avg Execution time= 49.680+51.637+56.478/3=52.598 ms




B+ Tree Index



BTree Index Created on table employee column dno

Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=false;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=false;
Execution Plan: 
	Sequential scan performed on employee at first
	Index scan performed on empindex(index created on the table employee)
	
	
Avg Planning time= (0.099+ 0.131 +0.102)/3= 0.110ms
Avg Execution time= (35.633 +39.531 +34.889)/3= 36.684ms









Bitmap Index




Bitmap Index Created on table employee column dno

Flags:
	set enable_indexscan=true; 
	set enable_indexonlyscan=true; 
	set enable_bitmapscan=true; 
	set enable_hashjoin=false; 
	set enable_sort=false; 
	set enable_nestloop=true; 
	set enable_material=true; 
	set enable_hashagg=false; 	
	set enable_seqscan=true;


Execution Plan: 
----check
	Sequential scan performed on employee at first
	Bitmap heap scan performed on employee
	Bitmap index scan on empindex (index created on table employees)
	
	
Avg Planning time= (0.192+ 0.116 +0.113)/3= 0.140ms
Avg Execution time= (36.513 +34.041 +35.544)/3= 35.366ms

Hash Index



Hash Index Created on table employee column dno

Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=true;
	set enable_sort=true;
	set enable_nestloop=false;
	set enable_material=false;
	set enable_hashagg=true;
	set enable_seqscan=false;
Execution Plan
	 Sequential scan on table employee 
	 Sequential scan performed on employee at first
	Index scan performed on empindex(index created on the table employee)


Avg Planning time= 0.113 +0.123+0.093/3=0.109 ms
Avg Execution time= 4.375+5.644+5.492/3=5.169 ms




--Final Conclusion For Query3:


Hash index proved to be the fastest with all the other options very close to each other especially in execution time.






































Query 4
Without Index



Flags:
	set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan: 
		Sequential scan on table employee then sequential scan on table dependent

Avg Planning time= 0.379+ 0.316 +0.089/3=0.261ms
Avg Execution time 2246.465+2315.891+2137.236/3=2233.197ms










B+ Tree Index


Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=false;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;

Execution Plan: 
	Sequential scan on table employee then sequential scan on table dependent
	
Avg Planning time= (0.108+ 0.140 +0.114)/3= 0.120ms
Avg Execution time= (2137.632 +2213.803 +2120.319)/3=2159.251 ms
















Bitmap Index


    Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=false;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;

Execution Plan: 
		Sequential scan on table employee then sequential scan on table dependent
	
Avg Planning time= (0.340 +0.164 +0.093)/3=0.199 ms
Avg Execution time= (2366.489+ 2259.932+2363.423)/3=2329.948 ms












Hash Index


Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=true;
	set enable_sort=true;
	set enable_nestloop=false;
	set enable_material=false;
	set enable_hashagg=false;
	set enable_seqscan=true;

Execution Plan:
		Sequential scan on table employee then sequential scan on table dependent
Avg Planning time= (0.739 +0.986+ 0.144)/3=0.623ms
Avg Execution time= (2486.985+2371.393+2598.566)/3=2485.648ms









Final Conclusion For Query4:
As we can see from the results that no index was formed on any of the queries due to the 'not' operation that cannot be indexed and in the following to shots when the not was removed the indexing was working properly




































Query 5

Without Index



Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=true;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;
Execution Plan: 
 Table employee is sorted and Merge Semi Joined with table dependent sorted.
Avg Planning time= 0.326+0.288+0.246/3=0.28ms
Avg Execution time= 7.543+7.502+7.141/3=7.39ms














B+ Tree Index



Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=false;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;
Execution Plan:
Table employee is index scanned then Merge Semi joined with table dependent index only scanned
Avg Planning time= (0.217+0.263+0.219)/3=0.233ms
Avg Execution time= (6.298+5.475+5.741)/3=5.83ms


















Bitmap Index



Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=true;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=true;
set enable_seqscan=true;
Execution Plan:
	The Bitmap index on table dependent is used then the output is Bitmap Heap scanned.The result is Nested loop Semi joined with table employee.
Avg Planning time= (0.259+0.194+0.188)/3=0.213ms
Avg Execution time= (20.658+18.828+17.781)/3=19.089ms
















Hash Index



Flags:
set enable_indexscan=true;
set enable_indexonlyscan=true;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=true;
set enable_seqscan=true;
Execution Plan:
Table employee is index scanned then Merge Semi joined with table dependent index only scanned
Avg Planning time= (0.406+0.176+0.216)/3=0.266ms
Avg Execution time= (3.907+4.102+3.840)/3=3.949ms


















Final Conclusion For Query 5:
As we can see from the results the Hash index achieved the fastest execution time.Followed by the B+ Tree index, then without indexing and finally the query with Bitmap index. 
Hash indexing first does a hash table dependent then and then hash semi join with table employee.




































Query 6
Without Index




Execution Plan:
Table department is  sorted then Merge inner joined with table employee sorted .
The output is  Merge inner joined with table employee sorted then aggregated

Avg Planning time= (0.222+0.228+0.189)/3=0.213ms
Avg Execution time= (5.160+5.459+5.914)/3=5.511ms






































B+ Tree Index


Execution Plan:
Table employee is  sorted then nested inner joined with table department index only scanned .The output Merge inner joined with table employee sorted then aggregated
Avg Planning time= (0.187+0.216+0.183)/3=0.195ms
Avg Execution time= (5.868+6.455+5.423)/3=5.915ms

Bitmap Index








Execution Plan:
Table employee is  sorted then nested inner joined with table department index only scanned .The output Merge inner joined with table employee Bitmap index scanned then Bitmap heap scanned and sorted .This output is Merge inner joined

Avg Planning time= (0.180+0.213+0.185)/3=0.192ms
Avg Execution time= (5.213+5.822+5.589)/3=5.41ms 





































Hash Index



Execution Plan:
Table employee is  sorted then nested inner joined with table department index only scanned .The output Merge inner joined with table employee sorted then aggregated
Avg Planning time= (0.210+0.175+0.201)/3=0.197ms
Avg Execution time= (5.552+4.929+4.539)/3=5.01ms

Final Conclusion For Query 6:
As we can see from the results the Hash index achieved the fastest execution time.Followed by the Bitmap index, then without indexing and finally the query with Btree index. 
hash indexing index scan department then nest inner join with table employee sorted
then Merge inner joined the output











Schema 3
Data Inserted:

9000 sailors, 3000 boats, and 15000 reserves
For each boat there are 3 sailors and for each boat there are 5 reserves.

















Query 7
Without Index


Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=true;
set enable_nestloop=false;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan:
Merge join of tables sailors and reserves on sid
Sorting
Seq scan on table reserves then filter and remove rows

Planning time: (0.182+0.208+0.165)/3 = 0.185
Execution time: (5.066+4.990+5.250)/3 = 5.102
B+ Tree Index



Flags:
set enable_indexscan=true;
set enable_indexonlyscan=true;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan:
Seq scan on table reserves 
Then B+ Tree index scan on table sailors column ssid


Planning time: (0.230+0.228+0.195)/3 = 0.2176
Execution time: (1.534+1.121+1.261)/3 = 1.305












Bitmap Index



Flags:
set enable_indexscan=false;
set enable_indexonlyscan=true;
set enable_bitmapscan=true;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan:
Seq scan on table reserves
Bitmap heap scan on table sailors
Bitmap index scan on table sailors by primary key


Planning time: (0.199+0.185+0.191)/3 = 0.191
Execution time: (1.199+1.099+1.812)/3 = 1.37







Hash Index




Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=true;
set enable_sort=false;
set enable_nestloop=false;
set enable_material=false;
set enable_hashagg=true;
set enable_seqscan=true;

Execution Plan:
Hash join on tables sailors and reserves on sid
Seq scan on table sailors
Hashing
Seq scan on table reserves


Planning time: (0.317+0.188+0.191)/3 = 0.232
Execution time: (2.978+2.672+2.794)/3 = 2.814










--Final Conclusion For Query7:


B+ Index was the fastest here while hash and bitmap indices were almost the some and the slowest was the approach without any index.


















Query 8
Without Index




Flags:
	set enable_indexscan=false;
	set enable_indexonlyscan=false;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;

Execution Plan:
Nested loop on tables sailors and reserves
Seq scan on table sailors then nestled loop on tables sailors and boats
Seq scan on table reserves and the output is materialized
Seq scan on table boat

Avg Planning time= 1.144 +0.584 +0.921/3= 0.883 ms
Avg Execution time= 7964.176+8741.229+8157.918/3= 8287 ms

B+ Tree Index
Created BTree index on table sailors on column sid




Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;

Execution Plan:
Nested loop on tables sailors and reserves
Index scan on sailors using sailorsindex
Index scan on table boat using primary key


Avg Planning time= 0.688 +0.375 +0.351/3= 0.471 ms
Avg Execution time= 33.10+36.83+35.0/3= 34.97 ms

Bitmap Index
	Created Bitmap index on table sailors on column sid




Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=true;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan:
Seq scan on table sailors
Bitmap heap scan on table reserves
Bitmap index scan on table reserves on primary key
Bitmap index on table boat on primary key

Avg Planning time= 0.368 + 0.353 +0.296 /3= 0.339 ms
Avg Execution time= 179.653 + 122.835 + 127.806 /3= 143.43 ms



Hash Index
	Created Hash index on table sailors on column sid
	
	


Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=true;
	set enable_sort=false;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=true;
	set enable_seqscan=true;






Execution Plan:
Hash join on tables sailors and reserves
Hashing the output
Hash join on tables reserves and boats
Seq scan on table reserves then hashing the output and then seq scan on table boats on color


Avg Planning time= 0.489 + 0.691 +0.266 /3= 0.482 ms
Avg Execution time= 7.984 + 9.225 + 8.153 /3= 8.454 ms






















--Final Conclusion For Query8:
Hash index was the fastest for this query
Then the b+ index in 2nd place then the bitmap index and lastly the no-index approach


























Query 9
Without Index

Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=true;
set enable_nestloop=false;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan: 
    the boat and reserves tables undergo nested loop inner join then the result is materialized, then the result undergoes nested loop inner join with the sailors table, the result is now materialized and undergoes nested loop semi join with the sailors table. The result is now materialized and undergoes nested loop inner join with the nested loop inner join result of the boat and reserves table.
Avg Planning time= 1.403+1.606+1.182/3=1.397ms
Avg Execution time 23200.781+22966.424+24133.821/3=23433.675ms



































B+ Tree Index
    
    Flags:
set enable_indexscan=true;
set enable_indexonlyscan=true;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;
Execution Plan: 
Sailors index and reserves undergo merge inner join , the result undergoes nested loop inner join with boat, then the result undergoes merge semi join with sailors. The result now undergoes merge inner join with the reserves and then undergoes nested loop inner join with the boat. The reserves , boat, sailors undergo index scan.

Avg Planning time= 2.141+1.669+2.426/3=2.078ms
Avg Execution time 68.521+63.474+68.347/3=66.78ms




Bitmap Index
        

 Flags:
set enable_indexscan=true; 
	set enable_indexonlyscan=true; 
	set enable_bitmapscan=true; 
	set enable_hashjoin=false; 
	set enable_sort=false; 
	set enable_nestloop=true; 
	set enable_material=true; 
	set enable_hashagg=false; 
	set enable_seqscan=true;
Execution Plan:	
    Index scan on table boat . Index scan on table reserves. Index scan on table sailors. They undergo a nested loop inner join . Sequential scan on table boat. They undergo a nested loop inner join. A sequential scan on table on table boat b. It undergoes a nested loop inner join as well with the previous result.



Avg Planning time= 1.850+1.345+1.514/3=1.569ms
Avg Execution time 62.908+66.653+67.476/3=65.679ms



Hash Index

Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=true;
	set enable_sort=true;
	set enable_nestloop=false;
	set enable_material=false;
	set enable_hashagg=true;
	set enable_seqscan=true;

Execution Plan:
    Sailors table is hashed and undergoes hash inner join with reserves table, the result undergoes hash inner join with the hashed result of boat. The result is hashed. The table sailors undergoes hashing then hash inner join with the table reserves. Then they undergo hash semi join with the previous result.
	
Avg Planning time= (2.445+1.613+1.973)/3=2.01ms
Avg Execution time= (27.669+31.037+28.565)/3=29.09ms



































Final Conclusion For Query9:
As we can see from the results the hash index achieved the fastest execution and planning time.
Followed by the bitmap, the hash and then the B+ Tree index and finally the query without indexing.
















Schema 4
Data Inserted:

12000 actors
 2000 directors
1000 movies  and for each movie  there are 12 actors and 2 directors 
10 genres and for each genre there are 100 movies 
1000 rating for each movie there is a rating a reviewer









Query 10
Without Index

Flags:
	set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan: 
Nested loop inner join on tables movie and movie_cast. The result is then materialized to and undergoes a nested loop semi join with table actor.
Sequential scan on tables movie, movie_cast and actor.

Avg Planning time= 0.311+0.421+0.434/3=0.388ms
Avg Execution time= 19.418+14.236+18.973/3=17.54ms





B+ Tree Index

    Flags:
	set enable_indexscan=true;
set enable_indexonlyscan=true;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;
Execution Plan:
Sequential scan on table movie then it is materialized then it undergoes a nested loop inner join with movie_cast. The result undergoes merge semi join with actor table.Actor table and movie_cast undergo index scan.

Avg Planning time= 0.340+0.342+0.383/3=0.355ms
Avg Execution time= 4.691+4.407+4.501/3=4.533ms









Bitmap Index

      Flags:
	set enable_indexscan=true; 
	set enable_indexonlyscan=true; 
	set enable_bitmapscan=true; 
	set enable_hashjoin=false; 
	set enable_sort=false; 
	set enable_nestloop=true; 
	set enable_material=true; 
	set enable_hashagg=false; 
	set enable_seqscan=true;


Execution Plan:
Movie table is materialized undergoes nested loop inner join with movie cast table undergoes merge semi join with actor table. Sequential scan over movie.Index scan over actor table and movie_cast table.
Avg Planning time= 0.565+0.392+0.324/3=0.427ms
Avg Execution time= 4.679+4.617+4.606/3=4.634ms












Hash Index

         
      Flags:
	set enable_indexscan=true; 
	set enable_indexonlyscan=true; 
	set enable_bitmapscan=true; 
	set enable_hashjoin=false; 
	set enable_sort=false; 
	set enable_nestloop=true; 
	set enable_material=true; 
	set enable_hashagg=false; 
	set enable_seqscan=true;


Execution Plan:
Movie table is hashed and undergoes a hash inner join with table movie cast. The result is hashed and undergoes a hash semi join with table actor.
Sequential scan on movie , movie_cast , and actor.

Avg Planning time= 0.397+0.360+0.416/3=0.391ms
Avg Execution time= 3.323+3.410+3.505/3=3.412ms







Final Conclusion For Query10:
As we can see from the results the hash index achieved the fastest execution and planning time.
Followed by the B+ tree index,  then the bitmap  index and finally the query without indexing.




































Query 11
Without Index








Flags:
	set enable_indexscan=false;
	set enable_indexonlyscan=false;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=true;
	set enable_nestloop=false;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;

Execution Plan:
	
Avg Planning time= (0.703+0.619+0.579)/3=0.636 ms
Avg Execution time= (52.223+46.029 +42.423)/3=46.892 ms





























B+ Tree Index
Indices on tables actor movie_cast and director







Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=true;
	set enable_nestloop=false;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;







Execution Plan:
	




Avg Planning time= (0.707+0.773+0.776)/3=0.752 ms
Avg Execution time= (41.662+44.268 +48.475)/3=44.801 ms










































Bitmap Index
	Indices on tables actor movie_cast and director









Flags:
	set enable_indexscan=false;
	set enable_indexonlyscan=false;
	set enable_bitmapscan=true;
	set enable_hashjoin=false;
	set enable_sort=true;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=false;

Execution Plan:
	
Avg Planning time= (0.728+0.741+0.793)/3=0.821 ms
Avg Execution time= (44.476+47.429 +42.719)/3=44.875 ms























Hash Index

	Indices on tables actor movie_cast and director













Flags:
	set enable_indexscan=false;
	set enable_indexonlyscan=false;
	set enable_bitmapscan=false;
	set enable_hashjoin=true;
	set enable_sort=true;
	set enable_nestloop=false;
	set enable_material=true;
	set enable_hashagg=true;
	set enable_seqscan=true;

Execution Plan:
	
Avg Planning time= (0.767+0.791+0.703)/3=0.753 ms
Avg Execution time= (7.658+8.486 +8.498)/3=8.214 ms




























Final Conclusion For Query11:

In this query, the hash index is the fastest while all the other indices including the no index approach are very similar.






































Query 12
Without Index


Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=true;
set enable_nestloop=true;
set enable_material=false;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan:
Join on director and movie_direction
Sorted
Seq scan on director and sorted using quick sort
Join on movie_direction and movie case then sorted
Seq scan on movie_direction and sorted
Seq scan on movie_case 
Seq scan on movie

Planning time: (1.346+0.450+0.416)/3 = 0.737
Execution time: (9.553+9.826+8.424)/3 = 9.276







B+ Tree Index




Flags:
set enable_indexscan=true;
set enable_indexonlyscan=true;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan:
Join on tables director and movie_direction
Index scan on director
Index scan on movie_direction then output is materialized
Seq scan on movie
Index scan on movie_cast


Planning time: (0.675+0.464+0.427)/3 = 0.522
Execution time: (4.259+3.911+4.032)/3 = 4.067











Bitmap Index



Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=true;
set enable_sort=false;
set enable_nestloop=false;
set enable_material=false;
set enable_hashagg=true;
set enable_seqscan=true;

Execution Plan:
Join on tables director and movie_direction
Seq scan on director and the output is hashed 
Seq scan on movie_cast and output is hashed
Hash join then seq scan on movie

Planning time: (0.509+0.676+0.440)/3 = 0.541
Execution time: (0.365+0.363+0.206)/3 = 0.311






Hash Index



Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=true;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan:
Join on tables director and movie_direction
Seq scan on director and the output is materialized 
Seq scan on movie_cast and output is materialized
Seq scan movie
Bitmap heap scan on movie_cast
Bitmap index scan on movcast


Planning time: (0.400+0.399+0.435)/3 = 0.411
Execution time: (3.817+4.261+4.199)/3 = 4.092


Final Conclusion For Query12:
Bitmap index was the fastest while hash and B+ were very similar and the no index approach was the slowest

















Schema 5
Data Inserted:
5000 Soccer countries
195 countries each with two soccer cities
1950 cities one venue each with capacity 10k
10 positions, 10,000 players will play in each
500 teams each of 20 people and 1 coach
500 team coaches
Each match has a penalty so 5000 shootouts
10 Stages each 500 matches
500 referees each will be assigned to a game and each has an assistant
Playerinandout only works for the first 500 matches
Germany1 vs germany2 is added manually. (match no 5000)





Query 13
Without Index




Flags:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=true;
set enable_nestloop=false;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan:
Join tables soccer_country and match_details on id
Seq scan on soccer_country
Seq scan on match_details
	
Avg Planning time= (0.566+0.302+0.235)/3=0.367 ms
Avg Execution time= (6.959+5.945 +3.410)/3=5.438 ms









B+ Tree Index
Index created on tables soccer_country and match_details


Flags:
set enable_indexscan=true;
set enable_indexonlyscan=true;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=true;
set enable_nestloop=false;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;



Execution Plan:
Merge join soccer_country and match_details on id
Index scan using countryindex on soccer_country
Seq scan on match_details
	
Avg Planning time= (0.215+0.260+0.261)/3=0.245 ms
Avg Execution time= (2.237+4.174 +2.104)/3=2.838 ms












Bitmap Index



Flag:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=true;
set enable_hashjoin=false;
set enable_sort=true;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=false;

Execution Plan:
Seq scan on match_details
Bitmap heap scan on soccer_country
Bitmap index on countryindex on id
	
Avg Planning time= (0.193+0.315+0.271)/3=0.259 ms
Avg Execution time= (6.051 +6.696 +7.565)/3=6.770 ms









Hash Index



Flag:
set enable_indexscan=false;
set enable_indexonlyscan=false;
set enable_bitmapscan=true;
set enable_hashjoin=false;
set enable_sort=true;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=false;

Execution Plan:
	Merge join soccer_country and match_details on id
	Index scan on soccer_country
	Seq scan on match_details
Avg Planning time= (0.198+0.228+0.233)/3=0.220 ms
Avg Execution time= (1.872 +1.784 +1.936)/3=1.864 ms






Final Conclusion For Query13:



























Query 14  
	Without Index
 
                          Flags:
	set enable_indexscan=false;
	set enable_indexonlyscan=false;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=true;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;





Execution Plan:
Table  soccer_country is sequential scanned 2 times and aggregated with table match_details sorted.
Avg Planning time= (0.166+0.146+0.209)/3=0.173ms
Avg Execution time= (2.359+2.706+2.563)/3=2.54ms





















B+ Tree
 
 Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=true;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=false;
Execution Plan:
Table  soccer_country is index scanned 2 times and aggregated with table match_details index only scanned
Avg Planning time= (0.159+0.163+0.142)/3=0.154ms
Avg Execution time= (1.672+1.589+1.779)/3=1.68ms
 Bitmap Index

 Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=true;
	set enable_hashjoin=false;
	set enable_sort=true;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=false;


Execution Plan:
Table  soccer_country is index scanned 2 times and aggregated with table match_details index only scanned
Avg Planning time= (0.128+0.217+0.267)/3=0.204ms
Avg Execution time= (0.199+0.257+0.282)/3=0.246ms



















Hash Index
 
 Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=true;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=false;



Execution Plan:
Table  soccer_country is index scanned 2 times and aggregated with table match_details index only scanned
Avg Planning time= (0.147+0.171+0.112)/3=0.143ms
Avg Execution time= (2.051+1.654+1.373)/3=1.69ms
























Final Conclusion For Query 14:
As we can see from the results the Bitmap index achieved the fastest execution time.Followed by  Btree index, then Hash and finally the query without  index.  Bitmap indexing  is the fastest because it can scan unique values better than any other indices(team_id in table match_details)























Query 15
Without Index

      Flags:
	set enable_indexscan=false;
	set enable_indexonlyscan=false;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;

Execution Plan:
Match details is sorted then undergoes aggregation with tables soccer_country. The result is materialized then undergoes nested inner loop with match mast.
Match_mast , match_details, soccer_country undergo sequential scan.
Avg Planning time= 0.260+0.293+0.247/3=0.266ms
Avg Execution time= 19.116+17.244+20.340/3=18.9ms

       
B+ Tree Index


           Flags:
set enable_indexscan=true;
set enable_indexonlyscan=true;
set enable_bitmapscan=false;
set enable_hashjoin=false;
set enable_sort=false;
set enable_nestloop=true;
set enable_material=true;
set enable_hashagg=false;
set enable_seqscan=true;

Execution Plan:
The tables soccer_country and match details are aggregated, then they undergo nested loop inner join with the table match_mast. The table soccer_country undergo sequential scan however and index scan is performed on table match_details and match_mast.

Avg Planning time= 0.280+0.246+0.291/3=0.272ms
Avg Execution time= 3.157+3.865+2.884/3=3.302ms

Bitmap Index
                                                      

      Flags:
	set enable_indexscan=true; 
	set enable_indexonlyscan=true; 
	set enable_bitmapscan=true; 
	set enable_hashjoin=false; 
	set enable_sort=false; 
	set enable_nestloop=true; 
	set enable_material=true; 
	set enable_hashagg=false; 
	set enable_seqscan=true;

                        Execution Plan:
The tables soccer_country and match details are aggregated, then they undergo nested loop inner join with the table match_mast. The table soccer_country undergo sequential scan however and index scan is performed on table match_details and match_mast.

Avg Planning time= 0.285+0.262+0.321/3=0.289ms
Avg Execution time= 3.621+3.996+3.887/3=3.834ms

































Hash Index


      Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=true;
	set enable_sort=true;
	set enable_nestloop=true;
	set enable_material=false;
	set enable_hashagg=false;
	set enable_seqscan=true;


Execution Plan:
Match details is sorted then undergoes aggregation with tables soccer_country. The result under goes hashing then undergoes hash inner join with match mast 
Match_mast , match_details, soccer_country undergo sequential scan.

Avg Planning time= 0.354+0.269+0.276/3=0.299ms
Avg Execution time= 3.658+3.326+3.274/3=3.419ms





























   Final Conclusion For Query15:
As we can see from the results the B+tree achieved the fastest execution and planning time.
Followed by the hash index,  then the bitmap  index and finally the query without indexing.































Query 16
Without Index
      

              Flags:
	set enable_indexscan=false;
	set enable_indexonlyscan=false;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;
Execution Plan:
Match_mast is aggregated and goal details is materialized to undergo a nested loop semi join with soccer_country.
Avg Planning time= 0.303+0.325+0.244/3=0.290ms
Avg Execution time= 6.115+6.597+6.031/3=6.247ms

     
B+ Tree Index
     

                   Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=false;
	set enable_sort=false;
	set enable_nestloop=true;
	set enable_material=true;
	set enable_hashagg=false;
	set enable_seqscan=true;
Execution Plan:
Goal details is materialized to enter a nested loop inner join with soccer_country and matchmast. Matchmast undergoes index only scan then is limited  then index scan. Soccer country undergoes sequential scan
Avg Planning time= 0.361+0.325+0.244/3=0.310ms
Avg Execution time= 2.534+2.568+2.406/3=2.502ms



Bitmap Index
    
       Flags:
	set enable_indexscan=true; 
	set enable_indexonlyscan=true; 
	set enable_bitmapscan=true; 
	set enable_hashjoin=false; 
	set enable_sort=false; 
	set enable_nestloop=true; 
	set enable_material=true; 
	set enable_hashagg=false; 
	set enable_seqscan=true;
        Execution Plan:
Goal details is materialized to enter a nested loop inner join with soccer_country and matchmast. Matchmast undergoes index only scan then is limited  then index scan. A bit map index is created on goal_details and on match_mast. Soccer country undergoes sequential scan
Avg Planning time= 0.355+0.325+0.345/3=0.341ms
Avg Execution time= 3.502+3.619+3.450/3=3.523ms




Hash Index
                            
     Flags:
	set enable_indexscan=true;
	set enable_indexonlyscan=true;
	set enable_bitmapscan=false;
	set enable_hashjoin=true;
	set enable_sort=true;
	set enable_nestloop=true;
	set enable_material=false;
	set enable_hashagg=false;
	set enable_seqscan=true;


Execution Plan:
Match_mast, soccer country and goal details is hashed to entered a nested loop inner join. Match mast is aggregated and undergoes a sequemtial scan.
Avg Planning time= 0.431+0.389+0.342/3=0.387ms
Avg Execution time= 2.525+2.534+3.938/3=2.999ms



   Final Conclusion For Query16:
As we can see from the results the B+tree achieved the fastest execution and planning time.
Followed by the hash index,  then the bitmap  index and finally the query without indexing.

























Query 17
Without Index


B+ Tree Index


Bitmap Index


Hash Index
