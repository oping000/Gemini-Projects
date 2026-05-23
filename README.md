Automating this workflow is a fantastic way to clear out inbox clutter. Because Google Apps Script doesn't have a built-in "summarize" function, we will use a free Google Gemini API key to handle the AI summarizing portion, while Apps Script handles the scanning and file saving.
Here is the step-by-step setup followed by the complete code script.
The Setup Steps
To prevent the script from constantly scanning your entire inbox, we will look for a specific Gmail label (e.g., ToSummarize).
1.Get a Free Gemini API Key:Requires 2 minutes.
Go to Google AI Studio, log in with your Google account, and click Create API Key. Copy this key; you will paste it into your script shortly.
2.Set Up Your Gmail and Drive Folders:In Gmail and Google Drive.
	• In Gmail: Create a new label called ToSummarize. Apply this label to any email containing an attachment you want to test.
	• In Google Drive: Create a new folder where you want your summaries stored. Open the folder and copy its ID from the URL bar (the long string of letters and numbers at the end of the web link).
3.Create the Apps Script Project:Via Google Drive.
Go to Google Apps Script and click New Project. Delete any code in the editor window and replace it entirely with the script provided below.
4.Configure Your Script Settings:Inside the script editor.
At the top of the script, paste your Gemini API Key and your Google Drive Folder ID into the designated placeholder quotes (YOUR_GEMINI_API_KEY and YOUR_DRIVE_FOLDER_ID). Click the disk icon to save.
5.Run and Authorize:First-time run execution.
Select the scanAndSummarizeEmails function from the top toolbar dropdown and click Run. Google will prompt you to grant access permissions (Gmail, Drive, and External Connections). Click Advanced -> Go to Untitled Project (unsafe) to authorize it.
The Google Apps Script
This script looks for unread emails tagged with ToSummarize, extracts text files (like .txt or .csv) or PDF contents, passes that data to the Gemini API, generates a summary document in Google Drive, and marks the email as read so it isn't processed twice.
--------------------------------------------This is Where the Automation Project Starts-----------------------------------
Step 1
To start, you don't need to open your email or Drive just yet. We need to go to Google AI Studio to get your free Gemini API key. This key is the "password" that allows your script to talk to the AI.
Here is exactly what to do first:
	1. Open your web browser and go to aistudio.google.com.
	2. Log in using the same Google account (Gmail) where you want this automation to run.
	3. Look near the top-left corner of the screen and click the button that says Create API Key (or Get API key).
	4. Click Create API key again in the pop-up, select a project (or let it create a default one), and copy the long string of letters and numbers it gives you.

API Key
AIzaSyAtrTGSf6PI24M01A2GnEueEyWPp2gguj4

STEP 2
Now we need to set up Gmail and Google Drive so the script knows exactly where to look for your emails and where to save your summaries.

"
You are completely right, and that is actually a much smarter way to handle it! Skipping the label means you don’t have to manually organize anything—the script can just run in the background, look for your specific criteria, and handle it completely hands-free.
To make this work, we just need to decide on that "trigger" criteria.
What specific rule should the script look for? For example, you could choose:
	• A specific phrase in the Subject Line (e.g., Subject: "Weekly Report" or contains "Invoice").
	• A specific Sender (e.g., From: "boss@company.com").
	• Or simply any unread email that has a PDF or Text attachment.
Tell me what specific rule or keywords you want to use, and I will adjust our plan so you don't need to create any labels at all. What type of email should it look for?"

Perfect! Targeting unread emails with the subject "Resume" that contain a .docx file makes your rule completely precise.
We can craft the search query to look exactly for that. In Gmail, the term has:attachment ensures an attachment is present, and we'll use your subject filter.

(see C:\Users\oping\OneDrive\Desktop\Gen AI-Gemini folder for Javascript)


Next Steps for Step 3
	1. Head over to script.google.com.
	2. Select New Project in the upper left.
	3. Paste this script into the blank canvas.
	4. Input your GEMINI_API_KEY and DRIVE_FOLDER_ID on lines 5 and 6.
	https://script.google.com/home/projects/1VMHoc_f8GsQUW0XiYHuxpty95m6LMG3r-vO9NwPZ_X32YDsvY-hQJYXY/edit
	1VMHoc_f8GsQUW0XiYHuxpty95m6LMG3r-vO9NwPZ_X32YDsvY-hQJYXY
	
	Remember to Create a New Folder on Google Drive and Copy + Paste after/folders into Line 6.*
	https://drive.google.com/drive/folders/18010lgzrftkFIpecdjb2FIR6Pl7jUQTd
	
	
STEP 4
Now that your code is securely saved, we just need to activate the Drive API Service so your script can read those .docx and PDF files without crashing.
Here is how to do that:
	• Look at the far-left sidebar of your Apps Script page.
	• Find the section labeled Services and click the + (plus sign) right next to it.
	• A menu will pop up. Scroll down until you see Drive API and click on it.
	• Leave the version identifier as default (v3) and click the blue Add button in the bottom right of that window.
Let me know once you see "Drive" listed under your Services section, and we will finally trigger our first test run!










Now that your script is saved and the Drive API Service is added, we are officially ready for Step 5: Run and Authorize.
Because this is a brand-new script that wants to access your personal Gmail, read attachments, write files to your Google Drive, and talk to an external API (Gemini), Google has a very strict, one-time security handshake you have to complete.
Here is how to run it for the first time:
1. Trigger the Run
	• At the top toolbar of your Apps Script editor, look at the dropdown menu next to the "Debug" button. Ensure it says automatedEmailSummarizer.
	• Click the Run button (the triangle play icon).
2. Bypass the Google Security Warning
A popup window will appear saying "Authorization Required."
	• Click Review Permissions.
	• Select your Google Account.
	• You will likely see a scary-looking screen that says "Google hasn’t verified this app". This is completely normal because you wrote this code yourself rather than downloading a commercial app.
	• Click the small Advanced link near the bottom.
	• Click the link that says Go to Untitled Project (unsafe) (or whatever you named your project).
3. Allow Access
	• A list of permissions will appear showing that the script wants to view your emails, manage your Drive files, and connect to an external service. Scroll to the bottom and click Allow.
What to check next
Once you click Allow, look at the bottom of your screen at the Execution Log.
	• If you don't have an unread email with the subject "Resume" in your inbox right now, it will say: No unread emails found matching query...
	• To give it a real test run, send yourself a quick test email with the subject line Resume and attach any .docx file, leave it unread, and hit Run one more time!
Let me know what your Execution Log says after the run!


CTRL-S to save


The script successfully connected to your Gmail, found the unread "ODell Resume" email, cleanly extracted the text from the .docx file, and sent it off to the Gemini API.


Step 6 Automate
How to automate it completely:
	1. On the left-hand sidebar of your Apps Script page, click the Alarm Clock icon (Triggers).
	2. Click the blue + Add Trigger button in the bottom right corner.
	3. Configure the settings like this:
		○ Choose which function to run: automatedEmailSummarizer
		○ Select event source: Time-driven
		○ Select type of time based trigger: Hour timer (or Day timer depending on how often you want it to scan).
		○ Select hour interval: Every hour
	4. Click Save.
And that is it! You can close the tab and let it run on autopilot. Go check your Resume Summaries folder in Google Drive to see how the formatting looks on those three generated files!

1.


