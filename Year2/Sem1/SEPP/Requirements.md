Functional Requirements

  

1.  User registration
    

1.1 - The system must provide means for a user to browse the portal without a user account, 

        being able to look at native tree species they can adopt, access the educational 

        resources and access publicly available posts in their community.

1.2 - The system must check if a user is signed in before they are able to adopt a tree, 

        interact with the community features, access environmental impact tracking, get tree 

        care and maintenance reminders and access the reward system.

1.3 - The system must transfer the user to a sign in/register sub system if they try to access 

        features that require an account. e.g. interact with community posts, adopt a tree.

1.4 - The system must provide means for the user to create accounts.

1.5 - The user profiles should include name, location, and adopted trees.

1.6 - The system should provide means for businesses to register separately, requiring 

        additional information such as their company number.

  

2.  Payment
    

2.1 - The system must be able to handle various payments as part of adopting a tree, 

        including not limited to, visa, mastercard, apple pay and google pay.

2.2 - The system should have a cart sub system that allows a user to adopt multiple   trees at 

        once as part of an order.

2.3 - The system must display a price breakdown of price, tax and cost to deliver and the 

        available payment methods.

2.4 - The system must redirect the user to their payment system of choice once they choose 

        to finalise an order.

2.5 - Once an order has been finalised, the system should send a confirmation email of the 

        order to the email of the user.

2.6 - Once these payment systems confirm a successful transaction the system must store  

        the information of the trees in the user account for Environmental impact tracking, tree 

        care and maintenance and the reward system.

  

3.  Environmental impact tracking
    

3.1 - Upon request from the user the system will take the information of adopted trees from 

        the user account (database) and calculate an estimate for carbon sequestration, oxygen 

        production and energy savings and display them to the user.

3.2 - The system may allow the user to filter this information such that they can see the 

        individual environmental impact of a tree, or group them based on the date they were 

        planted and species.

3.3 - The user may also be able to see the environmental impact of other adopters in the 

        area and the impact of businesses and organisations which sponsored tree planning 

        initiatives.

  
  
  
  

4. Credits
    

4.1 - The user should be able to access a credit store where they can use the credits they 

        have gained towards making purchases or donations.

4.2 - The user should be able to complete quizzes based on the provided educational 

        resources to gain additional credits.

  

5. Tree adoption
    

5.1 - The system must provide means for the user to browse and view available trees for 

        adoption.

5.2 - The system should provide details about each tree, including species, age, and 

        location.

5.3 - The system should make use of GPS location services or a provided location given by 

        the user to search for available trees in the area.

  

6. Notification System
    

6.1 - The system should give out notifications reminding users to take care of their trees.

6.2 - The system should give out notifications to keep companies informed about the status 

        of their registration, documents expiration and other relevant information.

  

7. Educational resources
    

7.1 - The system should provide relevant information on how to care for an adopted tree, 

        things such as watering frequency, diseases to look out for, fertilisation and other care 

        activities.

7.2 - The system, with the consent of the user, may also send push notifications to the user 

        when they need to complete these care activities.

7.3 - The system should provide the user with educational resources about various trees 

        upon request, including the environmental impact, estimated CO2 uptake over time.

  

8. Community features
    

8.1 - The system should provide a means for users to communicate with other tree adopters   

        through the app.

8.2 - The system should allow users to post pictures of their trees to track progress.

8.3 - The system could provide the user with a timeline of the growth of their tree based on 

         the pictures they upload over time. 

8.4 - The system should allow users to make posts that can be seen by everyone in their 

        area to share their progress, experiences and suggestions.

Non-Functional Requirements

  

1. Performance
    

1.1 - The system should load relevant parts at any given point within 15 seconds.

1.2 - The system should complete an adoption transaction within 30 seconds.

  

2. Space
    

2.1 - The system should have sufficient space to support a million users.

2.2 - The system should record and save all the user details of each signed up user like 

        name, username, email, DOB, payment details (opt-in).

2.3 - The system should save details of all orders/transactions made by a user.

2.4 - The system should save all details of all adopted trees

2.5 - The system should save all interactions between users.

  

3. Usability
    

3.1 - The system should have accessibility options to make use of the app easier for those      

        who need it

  

4. Reliability
    

4.1 - The system should achieve a mean time between failures of 500 hours

4.2 - The system should be available 99% of the time over a 6 month period

  

5. Security
    

5.1 - Personal data must be encrypted and stored in accordance to GDPR laws to prevent     

        access from unwanted parties Only the user should be able to see their personal 

        Information

  

6. Compatibility
    

6.1 - The system must be compatible with a wide range of web browsers, operating systems        

        and system architectures