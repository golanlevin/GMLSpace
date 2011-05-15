http://localhost:9292/test1.html 
rackup


Server: 
	Java: Compute 36 (28) metrics for each GML from today's Tgzball
	Java: Compute that day's Master SVD matrix (*), 28 columns x 3 rows.
	Java: Update the SVD analysis file (5000 rows with name,x,y,z)
		Max: will fetch tarballs, going into the past until we hit 5000 or bottom out. 
		
	Script: shell script which does the above, 
		Each day, we compute the 5000-analysis-file and the day's 28x3 matrix. 
		
	Don't forget: 
		- An ant project
		- 36 numbers need to be pre-processed according to getFieldSpecificPreprocessedValue();
		- Fixes according to computeBoundsAndStatsForAllDatumFields(); constrainAnalysisOutliers();
	
Client:
	Requests from the server, the SVD analysis file 5000*(row: filename + x,y,z)  ~500k
	Requests from the server, the Master SVD matrix (28x3)
	
	The Client issues two possible situations to the server: 
		I choose one of the 5000, compute the 30 most cosine similar of the 5000, ask for those 30. Get back JSON Marks. 
		I draw a mark, I computer 36(28) metrics, massage them, project into the SVD space (using the master SVD matrix*), then, 
			compute the 30 most cosine similar of the 5000, ask for those 30. Get back JSON Marks. 
	
Notes: 
	The 30 JSON tags are fetched from their database. 
	Since each request has overhead, can we ask for a method analogous to "recent_marks", which returns a JSON bundle of a specific 30. 
