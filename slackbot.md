# Intro to Slack Bot Development
This workshop will cover how to get up and running with your own bot on Slack using stdlib and node.js.

## Join Slack
You will need to be a part of a Slack workspace to create your bot. For the purpose of this workshop, please join **csclub-sandbox**.slack.com using your SSU email address.

## Join stdlib
This is a platform that will enable rapid API development, without the need for much boilerplate code. (https://stdlib.com/)

## Create your app
Visit **api.slack.com/apps** and click “Create an App”. Give it a name and select **csclub-sandbox** as the slack workspace. Once you create the app, on the sidebar select “bot users” and “add bot user”. Fill out the required fields and add the bot to the workspace. 

## Set up for development
Create a local directory on your computer to store your code in (hint: mkdir)

Enter the directory, and run `npm install lib.cli -g`

Next, run `lib init` and sign in to your stdlib account

Run  `lib create -s @slack/app`  to create a slack app using the template

## Test your setup
Change into the directory of your project:  `cd <username>/slack-app`

Test your project:  `lib .commands.hello test general “welcome"`

Finally, run `lib up dev` to deploy the app on stdlib

## Set up your first command
On the slack API site, click on ‘Slash Commands’ and then ‘Create New Command,’ 
and fill out the following fields. Since commands are not namespaced, make sure your ‘slash command’ 
is unique to the workspace. 
- Command: /hello&lt;username>
- Request URL: https://<username>.lib.id/<appname>@dev/commands/:bg
- Add a short description
- Rename <username>/<appname>/functions/commands/hello.js to the name of your command.

Click on OAuth & Permissions, and choose ‘Add New Redirect URL’
Fill in the following: https://<username>.lib.id/<appname>@dev/auth/
Click ‘Save URLS’

Click on ‘Event Subscriptions’ on the side, and enable the switch in the top right. Request URL: https://<username>.lib.id/<appname>@dev/events/:bg
Scroll down, and under ‘Subscribe to Workspace Events,’ select ‘message.channels’

## Authorize stdlib
We’re almost there! Next, return to stdlib (https://dashboard.stdlib.com/dashboard/) and click on Library Tokens. 

Retrieve your main token, and paste it into the “dev” section of env.json in your project, as the STDLIB_TOKEN. 

Add you app’s name to SLACK_APP_NAME.

Return to the Slack API, click on ‘Basic Information,’ and scroll down to ‘App Credentials’ and copy the appropriate values from this screen into SLACK_CLIENT_ID, SLACK_CLIENT_SECRET, and SLACK_VERFICIATION_TOKEN in env.json. Add the value https://<username>.lib.id/<appname>@dev/auth/ to the field SLACK_REDIRECT.

Deploy your changes by running `lib up dev` again

Visit https://<username>.lib.id/<appname>@dev/ click on ‘Add to Slack’, and authorize your application.

## Modify the Code
Now the fun part! Your function logic is located in functions/commands/hello.js, functions/events/message/__main__.js, and functions/events/message/channel_join.js. 

Whenever making a change, run `lib up dev` afterward to deploy the changes!

### Alternatively, you can edit your application directly at code.xyz once it has been deployed once.

<hr>

# Brief Javascript Reference
Many of you have a strong grasp of Python and C/C++, so here's a few important points about Javascript:

## Functions
*Functions are not typed and can either return values, or not*

```javascript
function funcName(arg1, arg2) {
	<…function body>
}
```

## Variables
*const and let are used to define variables*
```javascript
const varName = ‘hello world’;
let varName2;
```

## Strings
*Strings can be defined in multiple ways:*

String literal: `'hello, world'` OR `"hello, world"`

Template literal:
```javascript
const message = `hello, ${user.name}`;
```

## Logic
*Javascript has typed and untyped equality operators. Using the typed versions is the recommended way of executing comparisons:*

<table>
<tr>
<td>
Equal
</td>
<td>
===
</td>
<td>
Not equal
</td>
<td>
!==
</td>
</tr>
<tr>
<td>
Less than
</td>
<td>
&lt;
</td>
<td>
Less than or equal to
</td>
<td>
&lt;=
</td>
</tr>
<tr>
<td>
Greater than
</td>
<td>
>
</td>
<td>
Greater than or equal to
</td>
<td>
>=
</td>
</tr>
<tr>
<td>
And
</td>
<td>
&&
</td>
<td>
Or
</td>
<td>
| |
</td>
</tr>
</table>

```javascript
if (club.name === ‘Computer Science’) {
	console.log(‘🎉’);
}  
```

## Objects
*Objects can be created using JSON-like formatting to store data:*

```javascript
const student = {
	name: {
		first: ‘Joe’,
		last: ‘Smith’,
	},
	majors: [‘Computer Science’, ‘Math’],
	gpa: 4.0,
	email: ‘smithj@school.edu’,
};

student.name.first = ‘Joseph’;
student.majors[1] = ‘Biology’;
console.log(student.gpa);
```

**For more information, check out Mozilla’s fantastic MDN docs at https://developer.mozilla.org/en-US/docs/Web/JavaScript**
