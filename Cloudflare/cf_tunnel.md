

# Cloudflare Tunne Guide

## Create a Zero Trust organization

1. Sign up for a [Cloudflare account](https://dash.cloudflare.com/sign-up).

2. Add your domain by updating name servers on your domain registrar 

3. On your Account Home in the [Cloudflare dashboard](https://dash.cloudflare.com/), select the **Zero Trust** icon.
   ![https://i.imgur.com/0tVoYKP.png](https://i.imgur.com/0tVoYKP.png)

4. On the onboarding screen, choose a team name. The team name is a unique identifier for your Zero Trust organization. Users will enter this team name when they enroll their device.

5. Complete your onboarding by selecting a subscription plan and entering your payment details. If you chose the **Zero Trust Free plan**, this step is still needed but you will not be charged.


Now navigate to Access > Tunnels

![](https://i.imgur.com/LlG3vnA.png)



## Step 01

- Create a tunnel

- Name the Tunnel

- [Download](https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-windows-amd64.msi)

![](https://i.imgur.com/3410KLI.gif)

## Step 02

To connect your tunnel to Cloudflare, copy-paste one of the following commands into a terminal window.

**Store your token carefully.** This command includes a sensitive token that allows the connector to run. Anyone with access to this token will be able to run the tunnel.

1. Run the connector installer.

2. Open Command Prompt as Administrator.

3. Run the following command:

```
cloudflared.exe service install secrettoken
```

![](https://i.imgur.com/spJoUF0.png)

![](https://i.imgur.com/Aa7caBe.png)

Now move to next page

## Step 03

I have a service name Filebrowser running on my host at port number `2001`
which I would like to point to `browse.cyberally.in` let's see how to do just that.

![](https://i.imgur.com/npBZAWt.gif)

Add another one ?
well this is how you do it.

![](https://i.imgur.com/oG2mZLj.gif)

Removing Public Hosts from Tunnel
![](https://i.imgur.com/WB5V7IN.png)



> Note: When creating a public host a CNAME is also created in your DNS records you need to delete that record too



![](https://i.imgur.com/oAExo61.png)



So that's how you setup Cloudflare tunnel to remote access your internal services.
