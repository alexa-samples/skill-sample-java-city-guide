# Build an Alexa City Guide Skill in ASK Java SDK
<img src="https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/quiz-game/header._TTH_.png" />

[![Voice User Interface](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/navigation/1-locked._TTH_.png)](./1-voice-user-interface.md)[![Lambda Function](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/navigation/2-on._TTH_.png)](./2-lambda-function.md)[![Connect VUI to Code](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/navigation/3-off._TTH_.png)](./3-connect-vui-to-code.md)[![Testing](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/navigation/4-off._TTH_.png)](./4-testing.md)[![Customization](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/navigation/5-off._TTH_.png)](./5-customization.md)[![Publication](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/navigation/6-off._TTH_.png)](./6-publication.md)

## Setting Up A Lambda Function Using Amazon Web Services

In the [first step of this guide](1-voice-user-interface.md), we built the Voice User Interface (VUI) for our Alexa skill.  On this page, we will be creating a Lambda function using [Amazon Web Services](http://aws.amazon.com).  You can [read more about what a Lambda function is](http://aws.amazon.com/lambda), but for the purposes of this guide, what you need to know is that Lambda is where our code lives.  When a user asks Alexa to use our skill, it is our Lambda function that interprets the appropriate interaction, and provides the conversation back to the user.

1.  **Go to http://aws.amazon.com and sign in to the console.** If you don't already have an account, you will need to create one.  [Check out this quick walk-through for setting up a new AWS account](https://github.com/alexa/alexa-cookbook/blob/master/aws/set-up-aws.md).

    [![Sign In](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/2-1-sign-in-to-the-console._TTH_.png)](https://console.aws.amazon.com/console/home)

2.  **Choose "Services" at the top of the screen, and type "Lambda" in the search box.**  You can also find it in the list of services.  It is in the "Compute" section.

    [![Lambda](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/2-2-services-lambda._TTH_.png)](https://console.aws.amazon.com/lambda/home)

3.  **Check your AWS region.** Lambda only works with the Alexa Skills Kit in four regions: US East (N. Virginia), EU (Ireland), US West (Oregon) and Asia Pacific (Tokyo).  Make sure you choose the region closest to your customers.

    ![Lambda Regions](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/2-3-check-region._TTH_.png)

4.  **Click the "Create a Lambda function" button.** It should be near the top of your screen.

    ![Create Function](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/2-4-create-a-lambda-function._TTH_.png)

5.  **Click on "Author from scratch".**  We will configure our Lambda function next.
    1. These values will only ever be visible to you, but make sure that you name your function something meaningful. "sampleJavaCityGuide" is sufficient if you don't have another idea for a name.

    2. From the "Runtime" dropdown select Java 8.

    3. **Set up your Lambda function role.**  If you haven't done this before, we have a [detailed walk-through for setting up your first role for Lambda](https://github.com/alexa/alexa-cookbook/blob/master/guides/aws-security-and-setup/lambda-role.md).  If you have done this before, you only need to select the **Existing role**.

    4. Click **Create function**.

6.  **Configure your trigger.** There are many different AWS services that can trigger a Lambda function, but for the purposes of this guide, we need to select "Alexa Skills Kit." from the left hand side.

    Once you have selected Alexa Skills Kit, scroll down and find the Skill ID verification section.  Although you will want to paste your skill's ID in the Skill ID field, however for this tutorial, click Disable.  Click the **Add** button in the lower right.  Click the orange **Save** button in the top right corner.

7.  **Finish configuring your function**. Click on your function's name (you'll find it in the middle) and scroll to ``Function code``. You have an option of either uploading your code as a zip file, as a JAR file and from an Amazon S3 bucket.

    To build the JAR file and properly upload this code to Lambda, you'll need to perform the following:

    1. This skill uses the [ASK SDK for Java](https://github.com/alexa/alexa-skills-kit-sdk-for-java) for development. To build the sample, open a terminal and go to the directory containing pom.xml, and run `mvn org.apache.maven.plugins:maven-assembly-plugin:2.6:assembly -DdescriptorId=jar-with-dependencies package`. This will generate a JAR file named "CityGuide-1.0-jar-with-dependencies.jar" in the target directory.
    2. On the AWS Lambda console, change the **code entry type** drop-down to **Upload a .zip file or .jar file**, upload the generated JAR file in AWS lambda console and enter `com.amazon.ask.cityguide.CityGuideStreamHandler` (fully qualified name of the stream handler) in the `Handler` text box. and click on **Save**.

    *(Optional)* Follow the ASK Java SDK [Getting Started](https://alexa-skills-kit-sdk-for-java.readthedocs.io/en/latest/Setting-Up-The-ASK-SDK.html#) documentation, to check alternative ways of installing the sdk and deploying to AWS Lambda console.

8. (Optional) Click the **Configure test events** dropdown menu on the top of the page.

    1. Select 'Alexa Start Session' from the 'Event Template' dropdown.
    2. Type `LaunchRequest` into the 'Event Name' field.
    3. Click the orange 'Create' button at the bottom of the page
    4. Click the **Test** button at the top of the page.
    5. You should see a light green box with the message: *Execution result: succeeded* at the top of the page.

9. **As a final step, copy the ARN value from the top right corner of the screen.** You will need this value in the next section of this guide.

[![Next Step](https://m.media-amazon.com/images/G/01/mobile-apps/dex/alexa/alexa-skills-kit/tutorials/general/buttons/button_next_connect_vui_to_code._TTH_.png)](3-connect-vui-to-code.md)
