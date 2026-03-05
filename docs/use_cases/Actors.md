# User
A User is a person that uses the system without being logged in as Admin. The User does not need to login at all. As a consequence, it cannot access functionalities such as change the data storage method or see the execution logs. The User can access UC01 through UC09, as well as UC00 to initiate an Admin session when needed. 
# Admin
An Admin is a generalization of the User. To be elevated to Admin, a User must execute UC00 with the correct credentials. Besides all the functionalities the User can access (UC01–UC09), the Admin can also change the data storage method (UC10) and view the execution logs (UC11).
