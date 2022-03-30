#functions

    function clean($number){
        //Clean of Any White Spaces and Dash
        $number_clean = preg_replace('/[- )(]/', '',trim($number));
    		
        //Clean of ZERO Before Adding Country Code
    	$clean = preg_replace('/9509/', '959',$number_clean);
    	$number_null_zero = preg_replace('/^\+?9509\d{7,9}$/',$clean,$number_clean);
    	
    	//If Double Country Code Is Found Then Replace
    	$country_code = "+959" . preg_replace('/^\+?95959/', '',$number_null_zero);
    	$number_clean = preg_replace('/^\+?95950?9\d{7,9}$/',$country_code, $number_null_zero);
        $add_country_code = preg_replace('/^\+?959|09/', '959',$number_clean); 
        
    	return $add_country_code;
    }
	
	function is_valid($number){
		return preg_match('/^(09|\+?950?9|\+?95950?9)\d{7,9}$/',clean($number)) ? true : false;
	}
    
    function network($number){
    	//Clean & Add Country Code To Number 
        $number = clean($number); 
        
    	//MPT
    	if(preg_match('/^(09|\+?959)(2[0-4]\d{5}|5[0-6]\d{5}|8[13-7]\d{5}|4[1379]\d{6}|73\d{6}|91\d{6}|25\d{7}|26[0-5]\d{6}|40[0-4]\d{6}|42\d{7}|44[0-589]\d{6}|45\d{7}|87\d{7}|89[6789]\d{6})$/',$number))
    	return 'MPT'; 
        
        //Ooredoo 
     	if(preg_match('/^(09|\+?959)9\d{8}$/',$number))
     		return 'OOREDOO'; 

        //Mytel
     	if(preg_match('/^(09|\+?959)6\d{8}$/',$number))
     		return 'MYTEL'; 
            
        //Telenor
     	if(preg_match('/^(09|\+?959)7\d{8}$/',$number))
     		return 'TELENOR'; 
    }






# How To Use

> 1. Put the functions in your functions page(includes/functions.php)  
> 2. Include the function file in the page which you want to verfi numbers   

> let's say user input number of "091823457432";  
> $clean = clean('091823457432');  
> $is_valid = is_valid($clean);  

> //if number is valid then check network type
> if($is_valid)  
>	$network = network($clean); 
> else  
>	echo 'Number Not Valid'; 
