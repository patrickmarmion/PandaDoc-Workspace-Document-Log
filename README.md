# Workspace Document Log

This repo exports information from every document in a PandaDoc workspace to a Google Sheet.

## Prerequisites:

### Setting up OAuth 2.0 using Google:

Go to the [Google Cloud Platform Console](https://console.cloud.google.com/) From the projects list, select a project or create a new one.

If this is your first time or a new project, you will need to go to *Enable APIs and Services* on the left side menu:

- Add APIs and Services

- Search for Google Sheets and enable the Google Sheets API. 

Then click *OAuth consent Screen* on the left side menu:
- The project can be External 
- Assign a Name, e.g. Migration, your email as the support email and developer contact email at the bottom of the screen. 
- Add the following scope from the Google Sheets API: “../auth/spreadsheet” then click Save and Continue
- Add your email as a test user, click Save and Continue and then Back to Dashboard

Open *Credentials* from the console left side menu:

- Click *New Credentials*, then select OAuth client ID.
- Select Web Application and give the App a name.
- Add an authorised redirect URI as: 'http://localhost' and create the Credentials.
- After being redirected, download the JSON file of your OAuth client. 

### NPM Modules

- Install [Node](https://nodejs.org/en/) or make sure that you're running v16+
- Make a directory where you will store the files and navigate to this directory on your terminal. 
- Install the following NPM Modules:

  * [Dotenv](https://www.npmjs.com/package/dotenv)
  * [Google APIs](https://www.npmjs.com/package/googleapis)
  * [Axios](https://www.npmjs.com/package/axios)
  * [readline-promise](https://www.npmjs.com/package/readline-promise)

### Fork & Clone this Repo

[Bring the code](https://docs.github.com/en/get-started/quickstart/fork-a-repo) into the directory that you created earlier


### Add Files

To the root directory you will need to add a .env File. You can copy and paste the contents of the .envSample file and fill in the PandaDoc Access token.

In the Credentials Folder you will need to add 3 files: ‘credentials.json’, ‘refresh.json’, ‘token.json’. Both the refresh.json & the token.json files can be left empty. However, in your credentials.json file you will need to copy and paste the contents of the Google OAuth Client file which you downloaded earlier. There is a credentialsSample.json file so you can check that it is correct, obviously yours will have data. 

## Run the Script

In your terminal make sure you are in the correct Directory and run:
```bash
node index.js
```

You will be asked to authorise the app by visiting a URL, copy and paste this into your browser and allow the Google Permissions. This will redirect you to a blank page, however in the URL there will be a Code which you can copy and then paste back into your terminal. 

If this is successful, the application will write your credentials into your token.json and refresh.json files.

It will then prompt you for the Customer’s Name (this will act as the name of the Google Sheet), once you have filled this in it will create the File and start reading through every document in the workspace and populating the Sheet with the relevant information. You can go to your Google Sheets, open the newly created file and see this in action. Your terminal will also log out the row which it has got to. 

You can now chill while this runs, I have found it runs at roughly 1 row per 2-3 seconds. 

## End of the Script

At the End of the Script, the file will be automatically organised:
- Adding headers
- Filtering only Editor 2 Documents 
- Creating a Sheet for Errors
- Creating a Sheet for any Document which has a linked opportunity or deal

It is this final sheet which the customer would be responsible to provide the corresponding New IDs (if you are doing a Migration). 