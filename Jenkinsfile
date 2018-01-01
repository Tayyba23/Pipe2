node {
    // Clean workspace before doing anything
    try {
	   stage ('Clone') {
            checkout scm      
			bat "bteq <clearTables.txt>  table_clear_Log.txt"
             }
        stage ('Loading Customer SI Data') {
	   try {        
				
			bat "load_customer_SI.bat"
			def logCust = readFile "${env.WORKSPACE}/load_customer_SI_error.txt"
			echo logCust
			if (logCust.contains('0')) {
			
					echo " No Error log generated for script Load Customer"
					}
			else
					throw err				
			}
		catch(err){
			echo "Error log generated for load_data_customer Script, Marking build as unstable"
			currentBuild.result = "UNSTABLE"
					   }
        
        }
 
      					   
      } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
