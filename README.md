# utl-minimum-value-in-a-row-excluding-zero-r
Minimum value in a row excluding zero
    Minimum value in a row excluding zero                                                                                           
                                                                                                                                    
    A row with all 0s should have a missing value for the mininum                                                                   
                                                                                                                                    
    github                                                                                                                          
    https://tinyurl.com/y6ebxwlk                                                                                                    
    https://github.com/rogerjdeangelis/utl-minimum-value-in-a-row-excluding-zero-r                                                  
                                                                                                                                    
    SAS Forum                                                                                                                       
    https://tinyurl.com/yytcfylp                                                                                                    
    https://communities.sas.com/t5/SAS-Programming/Need-help-Use-an-array-to-find-the-minimum-value-excluding-0/m-p/691519          
                                                                                                                                    
    /*                                                                                                                              
     _                   _                                                                                                          
    (_)_ __  _ __  _   _| |_                                                                                                        
    | | `_ \| `_ \| | | | __|                                                                                                       
    | | | | | |_) | |_| | |_                                                                                                        
    |_|_| |_| .__/ \__,_|\__|                                                                                                       
            |_|                                                                                                                     
    */                                                                                                                              
                                                                                                                                    
    options validvarname=upcase;                                                                                                    
    libname sd1 "d:/sd1";                                                                                                           
    data sd1.have;                                                                                                                  
      input x1 x2 x3 x4 x5 x6;                                                                                                      
    cards4;                                                                                                                         
    0 0 0 0 0 0                                                                                                                     
    0 0 0 0 0 0                                                                                                                     
    0 1 2 4 6 7                                                                                                                     
    0 0 2 1 4 1                                                                                                                     
    ;;;;                                                                                                                            
    run;quit;                                                                                                                       
                                                                                                                                    
     SD1.HAVE total obs=4                                                                                                           
                                                                                                                                    
     X1    X2    X3    X4    X5    X6                                                                                               
                                                                                                                                    
      0     0     0     0     0     0                                                                                               
      0     0     0     0     0     0                                                                                               
      0     1     2     4     6     7                                                                                               
      0     0     2     1     4     1                                                                                               
                                                                                                                                    
    /*           _               _                                                                                                  
      ___  _   _| |_ _ __  _   _| |_                                                                                                
     / _ \| | | | __| `_ \| | | | __|                                                                                               
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                               
                    |_|                                                                                                             
    */                                                                                                                              
                                                                                                                                    
                                                                                                                                    
    WORK.WANT total obs=4                                                                                                           
                                                                                                                                    
     MIN    X1    X2    X3    X4    X5    X6                                                                                        
                                                                                                                                    
      .      0     0     0     0     0     0                                                                                        
      .      0     0     0     0     0     0                                                                                        
      1      0     1     2     4     6     7                                                                                        
      1      0     0     2     1     4     1                                                                                        
                                                                                                                                    
    /*                                                                                                                              
     _ __  _ __ ___   ___ ___  ___ ___                                                                                              
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|                                                                                             
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                             
    | .__/|_|  \___/ \___\___||___/___/                                                                                             
    |_|                                                                                                                             
    */                                                                                                                              
                                                                                                                                    
    %utl_submit_r64('                                                                                                               
    library(haven);                                                                                                                 
    library(SASxport);                                                                                                              
    have<-read_sas("d:/sd1/have.sas7bdat");                                                                                         
    want<-as.data.frame(apply(have,1,function(x) min(x[x>0])));                                                                     
    want[want==Inf] <- NA;                                                                                                          
    colnames(want)<-"MIN";                                                                                                          
    want;                                                                                                                           
    write.xport(want,file="d:/xpt/want.xpt");                                                                                       
    ');                                                                                                                             
                                                                                                                                    
    libname xpt xport "d:/xpt/want.xpt";                                                                                            
    data want;                                                                                                                      
      merge xpt.want sd1.have ;                                                                                                     
    run;quit;                                                                                                                       
    libname xpt clear;                                                                                                              
                                                                                                                                    
