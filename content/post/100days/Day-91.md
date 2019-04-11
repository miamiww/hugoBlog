+++
title = "Shodan Stories Day 91: Collecting Workforce Biometrics in Mumbai, GPS Tagging My Employee Assets to Ensure Payroll Compliance, and Using Watermarked Stock Footage in Your Deployed Product Means Never Having To Say You're Sorry"
date = 2019-04-10T22:51:25-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I just went looking for AWS servers.

## AWS EC2 Instance on 35.154.190.199

The first one I found, in India, seemed pretty interesting. It had ssh running on port 22 and on 80 a webserver that just hosted a login.
![](/images/100Days/Day91/firstlook.png)
But this login page had a 15 second video loop with a giant watermark saying POND 5 on it. Turns out that [POND 5](https://www.pond5.com/) is a stock image/footage company and the fact that this video still has a giant watermark means that it certainly was not paid for. Whoops! Hopefully this page isn't released into production, but it probably is.

Now it looks like the login is for a service, [EmployRoll](http://www.employroll.com/), which is created by the company Thumbmatic Solutions, which provides biometric tracking and ID services for employers wanting to better track and control their employees. Fun! You can tell they are fun because of the great little illustrations on their website.
![](/images/100Days/Day91/biometrics.png)
They have several different human resources management products. One of their products is GPS tracking employees via their smartphones in order to geofence their access to different systems. I don't really understand all of what they have on offer though. Read this one and see if you can figure it out.

>Innovatively self-designed & developed biometric devices. GPRS based biometric device ensures real-time attendance data transfer. Designed especially for our cloud based application to control proxy attendance and human intervention.

Yeah... I'll have to sleep on that one. See you tomorrow.
