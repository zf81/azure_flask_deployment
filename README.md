# azure_flask_deployment

Here is a step-by-step guide of how I set up a Flask application and deployed it using Azure.

Azure Deployment URL: [fizzah-504-flaskappnew.azurewebsites.net](https://fizzah-504-flaskappnew.azurewebsites.net/)

## How to set up your Flask application:

**1.** I created a new repository on Github called ```azure_flask_deployment``` and made sure the option "**Add a README.md file**" was checked on. I then opened up Google Shell environement and in the terminal I cloned this repository using the command ```git clone```. 

**2.** In the Google Shell start page, I clicked **"Open Folder..."** and this displayed my cloned repo. 

**3.** Created a new file and named it ```requirements.txt```. In the ```requirements.txt``` file, I typed in the following relevant requirements ```pandas``` ```flask```  and ```faker```, each on a separate line. 

**4.** Created a new folder called **data** and uploaded my dataset. 

**5.** I then created a new file and called it ```app.py```. It contained the following code: 

```
from flask import Flask, render_template
import pandas as pd

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('base.html')

@app.route('/about')
def aboutpage():
    return render_template('about.html')

df = pd.read_csv('https://raw.githubusercontent.com/zf81/azure_flask_deployment/main/data/FastFoodNutrition.csv')
@app.route('/data')
def data(data=df):
    data = data.head(15)
    return render_template('data.html', data=data)

if __name__ == '__main__':
    app.run(
        debug=True,
        port=8080
    )
```


**6.** Created a new folder called **templates** and within that folder I created the following three files: ```about.html```, ```base.html```, and ```data.html```.

**7.** The code found in the ```about.html```, ```base.html```, and ```data.html``` files were taken from Professor Hants Williams ```WK2``` ```flaskapp_0``` file. I edited the code to include the content from my dataset about fast food nutrition. 

**8.** To push my changes to Github, I entered the following commands in the Shell terminal: ```git add .```, ```git commit -m'<message>'```, and ```git push```. 


# Deploying the Application on Azure
**1.** In the Shell environment terminal at the bottom of the page, we need to install [AZURE CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt) using the following command ```curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash```. 

**2.** To ensure that it has properly installed, type in the command ```az```. 

**3.** Type the command ```az login --use-device-code```. Wait for a link and a code to appear in the terminal. Copy the code and click on the link to log in to your Azure account. This will help connect your Google Shell with your Azure account. Make sure that after entering the code and validating your account, you wait for a couple of seconds before navigating back to the Shell terminal.

**4.** Log in to your [Azure account](https://azure.microsoft.com/en-us/). Navigate to **Resource Group** and create a new Resource Group with a unique name. Then press **Review and Create**.

**5.** Back to the Google Shell. To ensure the correct Azure subscription has been enabled, type the command ```az account list --output table```. You need to check that you have the correct subscription. For my class, the subscription is **Azure for Students**. If the correct subscription is not listed, type in ```az account set --subscription <paste the correct SubscriptionId here>```.

**6.** In the terminal, type ```az webapp up --name <app-name> --runtime PYTHON:3.9 --sku B1```. Replace the ```<app-name>``` with your app name and click enter. 

**7.** The terminal will show that the webapp does not exist and will take a couple of minutes to create it for you. 

**8.** When the service completes the deployment, you can navigate to **App Services** on the Azure website to deploy your web app. Click on your web app so that you can look at the overview of the app. You can find the link to your application next to **Default domain**. Click on the link which will redirect you to your web application!

Note: An error that I made was that after creating my web app in the terminal, I kept refreshing **App Services** to see if my application was ready. I refreshed numerous times and could not find my web app. I decided to look at the code the next day and it turns out that in the App Services section, there is a little tab at the top which says **Subscription Equals**. I clicked on it and saw a dropdown menu with the options SBU DoIT AVD, SBU DoIT DevTest, and Azure for Students. Of course, the first two options were checked the whole time and the Azure for Students option was unchecked. Therefore, the App Services tab was not showing me my web app. When I clicked on Azure for Students, I found multiple web apps from the previous day which I had created thinking my app was not saving. I immediately stopped the web apps from running and deleted the extra apps I had created. 




