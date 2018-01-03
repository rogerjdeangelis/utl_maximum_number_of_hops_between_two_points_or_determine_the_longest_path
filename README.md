# utl_maximum_number_of_hops_between_two_points_or_determine_the_longest_path
Maximum number of hops between two points or dtermine the longest path.                                                                                                                                                                                                          Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics                   artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP                natural language processing machine learning igraph.   
    Maximum number of hops between two points or determine the longest path;                                                            
                                                                                                                                        
    github                                                                                                                              
    https://tinyurl.com/y8caexm5                                                                                                        
    https://github.com/rogerjdeangelis/utl_maximum_number_of_hops_between_two_points_or_determine_the_longest_path                      
                                                                                                                                        
    see                                                                                                                                 
    https://stackoverflow.com/questions/48011045/maximum-number-of-hops-between-two-points                                              
                                                                                                                                        
    Cpak profile                                                                                                                        
    https://stackoverflow.com/users/7958356/cpak                                                                                        
                                                                                                                                        
    Determine the longest route from 3 to 17.                                                                                           
                                                                                                                                        
    INPUT                                                                                                                               
    =====                                                                                                                               
                                                                                                                                        
    WORK.HAVE total obs=14                                                                                                              
                                                                                                                                        
     FROM    TO                                                                                                                         
                                                                                                                                        
       3      5  Start at 3                                                                                                             
       3     17                                                                                                                         
       4      7                                                                                                                         
       5     12                                                                                                                         
       5     13                                                                                                                         
       5     17                                                                                                                         
       8     13                                                                                                                         
       8     17                                                                                                                         
      13     17  End at 17                                                                                                              
                                                                                                                                        
                                                                                                                                        
    RULES pick the longest from all the routes                                                                                           
                                                                                                                                        
     Here are all the routes                                                                                                            
                                                                                                                                        
      3 - 17                                                                                                                            
      3 - 5 - 17                                                                                                                        
      3 - 5 - 13 - 17  * find this one  (3 hops)                                                                                        
                                                                                                                                        
    PROCESS (working code)                                                                                                              
    =======================                                                                                                             
                                                                                                                                        
       G <- graph_from_data_frame(have);         * create graph object;                                                                 
       start <- 3;                               * starting locations                                                                   
       lst<-all_simple_paths(G, start);          * get all possible starting from 3 to last stop 13                                     
       len<-lengths(all_simple_paths(G, start)); * vector of hops                                                                       
       imx<-which(len==max(len));                * index for longest path;                                                              
       want<-as.data.frame(capture.output(lst[[imx]])[2]); * logets path to dataframe;                                                  
                                                                                                                                        
    OUTPUT;                                                                                                                             
    ======                                                                                                                              
                                                                                                                                        
      WORK.WANT total obs=1                                                                                                             
                                                                                                                                        
      START   LONGEST_PATH                                                                                                              
                                                                                                                                        
        3     [1] 5  13 17                                                                                                              
                                                                                                                                        
                                                                                                                                        
    *                _              _       _                                                                                           
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _                                                                                    
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |                                                                                   
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |                                                                                   
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|                                                                                   
                                                                                                                                        
    ;                                                                                                                                   
                                                                                                                                        
    options validvarname=upcase;                                                                                                        
    libname sd1 "d:/sd1";                                                                                                               
    data sd1.have;                                                                                                                      
    input From  To;                                                                                                                     
    cards4;                                                                                                                             
    3  5                                                                                                                                
    3  17                                                                                                                               
    4  7                                                                                                                                
    5  12                                                                                                                               
    5  13                                                                                                                               
    5  17                                                                                                                               
    8  13                                                                                                                               
    8  17                                                                                                                               
    13 17                                                                                                                               
    ;;;;                                                                                                                                
    run;quit;                                                                                                                           
                                                                                                                                        
    *          _       _   _                                                                                                            
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                                 
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                               
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                               
                                                                                                                                        
    ;                                                                                                                                   
                                                                                                                                        
    %utl_submit_wps64('                                                                                                                 
    libname sd1 "d:/sd1";                                                                                                               
    options set=R_HOME "C:/Program Files/R/R-3.3.1";                                                                                    
    libname wrk "%sysfunc(pathname(work))";                                                                                             
    proc r;                                                                                                                             
    submit;                                                                                                                             
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);                                                                     
    library(haven);                                                                                                                     
    library(igraph);                                                                                                                    
    have<-read_sas("d:/sd1/have.sas7bdat");                                                                                             
    G <- graph_from_data_frame(have);                                                                                                   
    start <- 3;                                                                                                                         
    lst<-all_simple_paths(G, start);                                                                                                    
    len<-lengths(all_simple_paths(G, start));                                                                                           
    imx<-which(len==max(len));                                                                                                          
    want<-as.data.frame(capture.output(lst[[imx]])[2]);                                                                                 
    colnames(want)=c("LONGEST_PATH");                                                                                                   
    want$START<-"3";                                                                                                                    
    want;                                                                                                                               
    endsubmit;                                                                                                                          
    import r=want  data=wrk.want;                                                                                                       
    run;quit;                                                                                                                           
    ');                                                                                                                                 
                                                                                                                                        
                               
