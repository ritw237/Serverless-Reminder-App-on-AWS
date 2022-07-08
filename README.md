# Serverless-Reminder-App-on-AWS
Serverless Reminder App on AWS using S3, API Gateway, Lambda, Step Functions, SNS and SES

## Step 1: Configuring SES and SNS
The application will use SES (Simple Email service) to send reminder emails and SNS (Simple Notification Service) to send notification messages. 
Since SES starts off in sandbox mode, that means you can only add verified email addresses to send emails to.

To keep things simple, the application needs one application sender email address (from which the application will send email) and one application customer email address (for the test customer). 

However in production, it can be configured that email notfications can be sent to any number of customers.

### Step 1.1: Setting up application sender email 

Start off in `SES console` 

![image](https://user-images.githubusercontent.com/58885463/177976361-db5e1377-aa00-411c-a273-829b440dafbc.png)

Go to `Verified Identities` under configuration tab and then click on `Create Identity`

<img width="960" alt="image" src="https://user-images.githubusercontent.com/58885463/177977527-fa2db93e-3298-434b-adb8-d908cb5bb634.png">

Click on `Email address` button. Add an email address. Notice the email address I have used. It's a neat little trick Gmail has (read that in Norman Osborn's voice pls), you can add additional emails like this ( ex: you had abc@gmail.com, so you can use abc+newEMAIL@gmail.com).
The email I have used for the application to send emails from is : ` ritwik.srv237+reminder_app@gmail.com ` 

![image](https://user-images.githubusercontent.com/58885463/177980106-8e87ec0d-652e-4a99-857d-800fc375a9e0.png)

Don't add Tags (as they are optional)
Click on `Create Identity` below
Notice that the screen which is now opened, there is an "Unverified" in red highlighted text below Identity Status. 

You need to go to your Gmail, there would be an email from AWS to verify your newly created identity (in this case, `ritwik.srv237+reminder_app@gmail.com`). Click on that URL to see a Congratulations page open.

Congratulations! The new email identiy is verified now (highlighted in green text). Refresh the browser to see the updated status.

![image](https://user-images.githubusercontent.com/58885463/177981418-3f8f695c-98e8-4088-bab5-96a6cd9d632f.png)




### Step 1.2: Setting up application customer email

The test customer email (which the reminder app will deliver these emails to) I have used is: `ritwik.srv237+production@gmail.com`

Adding another email identity in `SES` console follows the same process as described in Step 1.1

If you now go to `Verified identities` tab you will see both the emails

![image](https://user-images.githubusercontent.com/58885463/177982672-841500d1-0968-4d62-b261-a8d5a1260a6a.png)

### Step 1.3: Setting up SMS number in SNS Console

Start off in `SNS` console and click on `Text Messaging (SMS)` under Mobile section in left panel.

![image](https://user-images.githubusercontent.com/58885463/177984668-9e970c0f-d3bd-4002-81e1-ca84662e41d9.png)

Scroll down to see account information, SNS is also in sandbox mode. So you need a verified mobile number (Sandbox destination phone no.) to take SNS out of sandbox

Click on `Add phone number` in `Sandbox destination phone numbers` section.

On the next screen add phone number and verification message language. Click `Add Phone Number`. Type your verification code sent to you phone and click verify button.

<img width="538" alt="image" src="https://user-images.githubusercontent.com/58885463/177986076-dd849818-42c7-400b-9b3a-f5b380372499.png">

Now we can use this number to send SMS messages to.





