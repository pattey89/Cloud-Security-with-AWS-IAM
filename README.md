<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Cloud Security with AWS IAM

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-iam)

**Author:** PATRICK ADDAI  
**Email:** patrickaddai1689@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-security-iam_1c864649)

---

## Introducing Today's Project!

In this project, I will demonstrate how to use AWS IAM to control access and permission settings in our AWS account. I'm doing this project to learn about cloud security from the absolute foundations - every company thinks about access permissions, and there are even entire jobs called 'IAM Engineers' focused on the skills I am abou to build today.

### Tools and concepts

Services I used were Amazon EC2 and AWS IAM. Key concepts I learnt include IAM users, policies, user groups and account alias. We also learn how to use Policy Stimulator and how JSON policies work. How to launc an instances, how to tag an instances, how to log in as another user.

### Project reflection

This project took me approximately1.5 hours including project demo time. The most challenging part was understanding the IAM policysince it was written in JSON and it contained multiple statements.  It was most rewarding to see permission denied when our intern tried delete our production instance 'My IAM access managenment is working'

---

## Tags

Tags are like labels you can attach to AWS resources for organization.

This tagging helps us with identifying all resources with the same tag at once (they are useful filters when you're searching for something), cost allocation, and applying policies based on environment types. You'll see the last point about policies in action soon!

The tag I’ve used on my EC2 instances is called tag called "Env" with a value of "production" or "development" to label the instances used in production vs development environments. 

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-security-iam_2e0e5a5d)

---

## IAM Policies

IAM Policies are rule for who can do what with your AWS resources. It's all about giving permissions to IAM users, groups, or roles, saying what they can or can't do on certain resources, and when those rules kick in.




### The policy I set up

For this project, I’ve set up a policy using JSON. In this project, we will use the JSON method.


I’ve created a policy that the policy holder (i.e. the intent to have permission to do anything they want to any instance tagged with "development". They can also see information for any instance, they are denied access to deleting or creating access.

### When creating a JSON policy, you have to define its Effect, Action and Resource.

The Effect, Action, and Resource attributes of a JSON policy can have two values - either Allow or Deny - to indicate whether the policy allows or denies a certain action. Deny has priority. Looking at the first statement, "Effect": "Allow" means this statement is trying to allow for an action.

In this case, "Action": "ec2:*" means all actions that you could possibly take on EC2 instances are allowed. Woohoo!

---

## My JSON Policy

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-security-iam_1c864649)

---

## Account Alias

An account alias is a friendly name for your AWS account that you can use instead of your account ID (which is usually a bunch of digits) to sign in to the AWS Management Console.

Creating an account alias took me 30 seconds -It's  a simple configuration in the IAM dashboard. Now, my new AWS console sign-in URL uses alias instead of my account ID.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-security-iam_0eb4439b)

---

## IAM Users and User Groups

### Users

IAM users are people or entities that have access/can log in to my account.

### User Groups

An IAM user group is a collection/folder of IAM users. It allows you to manage permissions for all the users in your group at the same time by attaching policies to the group rather than individual users.

I attached the policy I created to this user group, which means any user created inside this group will automatically get the permission attached to my NextWorkDevEnvironmentPolicy IAM Policy.

---

## Logging in as an IAM User

The first way is is to send Email sign-in instructions to the user and the second way is to Download the csv files with the sign in details inside.

Once I logged in as my IAM user, I noticed that user is already denied items to items or panels on the main AWS console dashboard. This was because we only set up permissions to  my development EC2 instance so my intern wouldn't have access to anything else and even see anything else.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-security-iam_6f2ab446)

---

## Testing IAM Policies

I tested my JSON IAM policy by attempting to stop both the development and the production instances.

### Stopping the production instance

When I tried to stop the production instance I met with an error. This was because my production instance is tagged with the 'production' label which is outside of the scope of our permission policy - interns are only allow
to do things to the development instances.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-security-iam_0e7a9d6a)

---

## Testing IAM Policies

### Stopping the development instance

Next, when I tried to stop the development instance, I succesfully saw the instance state change to Stopping and the Stopped.  This was because our permission policy allows the intern (i.e. the network-dev-group) to stop instances.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-security-iam_1811801c)

---

## The IAM Policy Simulator

The IAM Policy Simulator is a tool use to stimulator policies and test permissions settings by defining a specific user/group/role and the action I want to test for   It's useful for saving time when testing permission settings! No more logging into another user or acvtually stopping resources.

### How I used the simulator

I set up a simulation forwhether my dev user group has permission to Stop Instances or Delete Tags. The results were denied for both. I had to adjust scope of the EC2 instances to ones that are tagged with 'development'. Once we apply that tag permission was allowed.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-security-iam_069d8a621)

---

---
