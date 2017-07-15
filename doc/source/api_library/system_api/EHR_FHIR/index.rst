EHR FHIR System API
!!!!!!!!!!!!!!!!!!!

FHIR System API's will be used to fetch Patient related information from FHIR Database System, we are using Postgre to integrate with Mulesoft. 

As part of first release we have developed following API's and are enabled to perform GET based on provided ID

Patient API:

Patient API is available on below provided URL, we need to perform HTTP GET by providing PatientID.
EC2 Instance URL: http://ec2-34-208-134-225.us-west-2.compute.amazonaws.com:8081/api/Patient/{PatientID}   
{PatientID}=Patient-1125

Please refer below figure to check Json response structure for Patient details.


Condition API:

Similar to Patient API we have enabled Condition API as well to perform GET operation on exposed REST API by providing CondtionID.

EC2 Instance URL: http://ec2-34-208-134-225.us-west-2.compute.amazonaws.com:8081/api/Condition/{ConditionID}   
eg:{ConditionID}=Condition-10018

Refer above figure to invoke API and get standard json structure for response.

.. image:: /_static/Patient-Condition-test.GIF

Appointment API:

EC2 Instance URL: http://ec2-34-208-134-225.us-west-2.compute.amazonaws.com:8081/api/Appointment/{AppointmentID}   

eg:{AppointmentID} = 2019724

Please refer below figure to get json response

.. image:: /_static/Appointment-test.GIF



