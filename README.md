Here's a polished version of the project description for your GitHub repository:

---

# Automate AWS EC2 with Python

This project shows how to use Python to automate the management of Amazon Web Services EC2 instances. The solution requires creating a Lambda function to check the status of EC2 instances on a regular basis and restart any that have been stopped. This system helps to keep instances available without requiring manual intervention.

## Project Overview
### Architecture

1. **AWS Lambda Function**: 
     Create a Lambda function to automate tasks.
     The function interacts with AWS EC2 services through the 'boto3' library.
     It examines the status of all EC2 instances and restarts those that are determined to be stopped.

2. **AWS EventBridge**:
    Every hour, an EventBridge rule triggers the Lambda function.
   The rule schedules Lambda execution using a cron expression.

### Services Used

AWS Lambda: Checks and starts EC2 instances using Python code.
Lambda function is scheduled to run periodically using AWS EventBridge (formerly CloudWatch Events).
The Boto3 SDK for Python allows users to interact with AWS services.


## Implementation

1. Create a Lambda function using Python 3.10 runtime.
    Set up the function to utilize 'boto3' to handle EC2 instances.
   To interact with EC2, add necessary permissions to the Lambda execution role.

2. **EventBridge Rule**:
   Set a scheduled rule to trigger the Lambda function every hour.
   To define the schedule, use a cron expression (for example, '0 0 * *? *' every hour).

### Code Example

Here's a simplified example of the Python code used in the Lambda function:

```python
import boto3

def lambda_handler(event, context):
    
    # Create EC2 Client
    ec2 = boto3.resource('ec2')
    
    for instance in ec2.instances.all():
        state = instance.state['Name']
        if state == 'stopped':
            try:
                instance.start()
            except:
                print('Something went wrong')
```

Define the Lambda Function:

Create a new Lambda function to host the Python script.
Configure the execution role to have full access to EC2.
To set up EventBridge:

Make a new rule in EventBridge with a cron expression to run the Lambda function every hour.


## Conclusion
A practical solution is provided for managing EC2 instances and ensuring they are running correctly. Python is used to demonstrate how AWS Lambda and EventBridge are integrated for automation.
