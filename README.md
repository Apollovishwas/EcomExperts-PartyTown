
## EcomExperts - Partytown 


Fork this Repo to continue.

### Step 1 : Hosting Custom App on Render.com

1. Go to Render.com, Signup for new account, Create a new Webservice. While creating a new webservice, connect github repo to the webservice. Deploy it.
2. After Deployment, Go to "Environment" Section and add Environment Variables.
#### HOST : yourwebservice.onRender.com (For Eg -> https://partytownlib.onrender.com)
#### SHOPIFY_API_KEY : You can get this when you create app on shopify. ("App overview" Section)
#### SHOPIFY_API_SECRET : You can get this when you create app on shopify. ("App overview" Section)

Save and manually deploy it again.

### Step 2 : Creating new app on shopify

1.In the dashboard, click "Apps -> Create App -> Create App Manually"
2. After you create app, go to "App Setup", Scroll to "App URL" and setup the following.

#### App URL : YourWebService/shopify (For Eg https://partytownlib.onrender.com/shopify)
#### Preferences URL : 
#### Allowed Redirections URL(S) : YourWebService/shopify/callback (For Eg https://partytownlib.onrender.com/shopify/callback)

3. In the Same section, Scroll Down to, "App proxy" and setup following things, 

#### Subpath Prefix : a
#### Subpath : proxy
#### Proxy URL : YourWebService/proxy (For Eg https://partytownlib.onrender.com/proxy)


### 3. Installing Custom app on Shopify stores.
  1.To install it on dev store, Use this URL : "your Webservice URL"/shopify?shop="your store URL without https" 
for Eg( https://partytownlib.onrender.com/shopify?shop=ecomexperts.io/)

  2. To install it on production Server : Choose "Distribution" on App management on Dashboard. Choose 'Install to specific Store'. Copy paste the link.
  
### 4. Accessing PartyTown in Store Theme : 

  Once the app is installed and the webservice is live, partytown.js can be accessed "/a/proxy/partytown.js"
  
  To Setup Connection and use partytown, see BoilerPlate.html for instructions. (code in the file should be pasted to theme.liquid)
