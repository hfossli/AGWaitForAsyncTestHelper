#WaitForAsyncTestHelper

C Macro to wait for any async test and get an STFail in your test if it exceeds time limit.

###Current functions
     
    WAIT_WHILE(whileTrue, limitInSeconds)
    WAIT_WHILE_WITH_DESC(whileTrue, seconds, description, ...)
    WAIT_WHILE_EQUALS(value1, value2, limitInSeconds)
    WAIT_WHILE_EQUALS_WITH_DESC(value1, value2, limitInSeconds, description, ...)
    WAIT_WHILE_EQUALS_WITH_ACCURACY(value1, value2, accuracy, limitInSeconds)
    WAIT_WHILE_EQUALS_WITH_ACCURACY_WITH_DESC(value1, value2, accuracy, limitInSeconds, description, ...)
    WAIT_WHILE_NOT_EQUALS(value, equalTo, limitInSeconds)
    WAIT_WHILE_NOT_EQUALS_WITH_DESC(value1, value2, limitInSeconds, description, ...)
    AG_STALL_RUNLOPP_WHILE(whileTrue, limitInSeconds)

Examples
------

Most basic

    __block BOOL jobDone = NO;
    
    [CEO asyncFireAllEmployes:^{
        jobDone = YES; 
    }];
    
    WAIT_WHILE(!jobDone, 0.2); // stalls runloop until jobDone is true

`WAIT_WHILE`will stall current runloop for givven timeperiod. It is possible to do job on the main thread and so on.. Like in this silly example


    __block BOOL jobDone = NO;
    
    [CEO asyncFireAllEmployes:^{

        dispatch_async(dispatch_get_main_queue(), ^{
            
            int value = 2 + 2;
            [you tellWife2Plus2Is:4];
            
            [CEO tellJanitorToStopBuggingYouAsync:^{
                jobDone = YES;
            }];
        });
    }];
    
    WAIT_WHILE(!jobDone, 0.2); 


Cocoa pods
-------
    
It is added to the Cocoa Pods public repository as `WaitForAsyncTestHelper`.

[![Agens | Digital craftsmanship](http://static.agens.no/images/agens_logo_w_slogan_avenir_small.png)](http://agens.no/)
