START

CREATE queue_list as empty list

REPEAT
    DISPLAY Menu
        1. Add Customer
        2. Serve Customer
        3. View Queue
        4. Exit

    INPUT choice

    IF choice = 1 THEN
        INPUT customer_name
        ADD customer_name to queue_list
        DISPLAY "Customer added to queue"

    ELSE IF choice = 2 THEN
        IF queue_list is empty THEN
            DISPLAY "No customers in queue"
        ELSE
            REMOVE first customer from queue_list
            DISPLAY customer_name + " is now served"
        ENDIF

    ELSE IF choice = 3 THEN
        IF queue_list is empty THEN
            DISPLAY "Queue is empty"
        ELSE
            DISPLAY "Customers in Queue:"
            FOR each customer in queue_list
                DISPLAY customer
            ENDFOR
        ENDIF

    ELSE IF choice = 4 THEN
        DISPLAY "Exiting program"
        STOP

    ELSE
        DISPLAY "Invalid choice"
    ENDIF

UNTIL choice = 4

END
