
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
  
  To Setup Connection and use partytown, Use follwing code. (code should be pasted to theme.liquid)
  
  ### 1 : Setting up partytown 
  
  ```
  <script>
          partytown = {
            resolveUrl(url, location) {

      url.searchParams.append('shop', 'yourShopifyURL');
      // url.searchParams.append('shop', 'partytownlib.myshopify.com');
      const proxyUrl = new URL('yourWebServiceURL/reverse-proxy');
      // const proxyUrl = new URL('https://partytownlib.onrender.com/reverse-proxy');
      proxyUrl.searchParams.append('url', url.href);
      url.searchParams.append('shop', 'yourShopifyURL');
      // url.searchParams.append('shop', 'partytownlib.myshopify.com');

            },
            forward: ["dataLayer.push"],
            lib:'/a/proxy/',
            logCalls: true,
            logGetters: true,
            logSetters: true,
            logImageRequests: true,
            logMainAccess: true,
            logSendBeaconRequests: true,
            logStackTraces: false,
            logScriptExecution: true
          };
    </script>
  ```
  ### 2. Checking if server is online
  
  ```
   <script>
      var uri = '/a/proxy/paratytown.js'
      var xhr = new XMLHttpRequest();
      xhr.open("GET",uri,false);
      xhr.send(null);
      if(xhr.status == 200) {
          //is online
          //if its, online, we are including party town script to DOM
        var script = document.createElement('script');
        script.src = '/a/proxy/partytown.js';
        document.head.appendChild(script);
        console.log("Server is online");

      }
      else {
          //is offline
          console.log("Server is offline, loading GTM on main Thread");
          //The Server is offline, Call all scripts to run on mainthread.
      }
    </script>
  ```
  
  ### 3.1. Running Small Scripts with PartyTown ( GTM )
  
  ```
   <script type="text/partytown" crossorigin="anonymous">
            console.log("Loading GTM with party town");
            //paste your GTM Code here. PartyTown Will handle Everything Else
    </script>
  ```
  
  ### 3.2. Running Third Party Scripts ( Jquery )
  
  ```
  <script type="text/partytown">
                    console.log("trying to load jquery");
                    var script = document.createElement('script');
          script.onload
          
          
          //upload your Scripts to "Assets" section of your theme.Else You'll face CORS issue. Alternatively, you can upload files to webservice
          //to "proxy/YourClientName/", But i recommend the former approach.
          
          
              script.src = 'https://cdn.shopify.com/s/files/1/0715/0600/2240/t/2/assets/jquery.js';

              document.head.appendChild(script);
      script.onload = function () {
                if (window.jQuery) {
                // jQuery is loaded
                console.log("jQuery Installation Verified");
            } else {
                // jQuery is not loaded
                alert("Doesn't Work");
            }
      };
    </script>
  ```
