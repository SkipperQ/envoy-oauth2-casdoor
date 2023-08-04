# envoy-casdoor-oauth2

An example of using Casdoor with Envoy proxy for user auth utilizing Envoy's [oauth2 filter](https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/oauth2_filter)

## Prerequisites
A running Casdoor server. See the Casdoor documentation for [Server Installation](https://casdoor.org/docs/basic/server-installation) and [Try with Docker](https://casdoor.org/docs/basic/try-with-docker).

## Configuring Casdoor
1. Add **Application** "Envoy". In the **Redirect URLs** field, type the URL of the Envoy instance including the port number, and ending in **/oauth2/callback** (in this sample, http://%REQ(:authority)%/oauth2/callback ), record the values in the Client ID and Client Secret, 
2. Add **Roles** "envoy-casdoor-role". 
3. Add **Users** "user1". Select **Envoy** in Signup application. In the **Managed accounts** field, select **Envoy** in Application and fill in the username and password. Go back to the **Roles** page and click Edit on the nginx-casdoor-role row. In the opened page, in the **Sub users** field, select the username you just created(here it is built-in/user1)

## Configure Envoy
1. modify token_endpoint, authorization_endpoint and client_id in **envoy.yaml**
2. modify inline_string in **token-secret.yaml** to the Client Secret of Envoy from casdoor
3. modify inline_bytes in hmac-secret with a unique, long, and secure phrase.

## How to Run
1. Start containers via `docker-compose up`
2. Go to http://localhost:10000 where Envoy listens. You should see immediate redirect to casdoor for user auth.
