Title: Using SSH to tunnel traffic
Date: Tue Dec 19 23:13:01 EST 2017
Modified: Sat Dec 23 12:20:16 EST 2017 
Category: misc
Tags: Networking,linux,ssh
Slug: my-first-post
Authors: Amey Joshi
Summary: ssh tunnel

This post assumes you have some knowledge of linux command like SSH and networking. 
I plan to write windows version of this in sometime. The difference would be running ssh command on PUTTY instead of terminal. I think everything else should stay same
**Problem**
I want to securely browse net at public wifi.

I want to view websites that filter content based on geographic location of the user. For example , when I am in Boston I can not see content on hotstar.com website. or when I am in Pune,India I can not see contents on US websites that filter based on user location (Hulu / Netflix)

**Solution**
Use ssh port forwarding using remote host in geographical location you want. I am usingfree tier Amazon ec2 instance for this. I
keep 2 amazon free tier instances, one in US region and one in India (Mumbai) region.

*Once you get IP of your Amazon ec2 instance run this command to run socks proxy on
localhost with traffic tunneled to your remote host. I use identity file that I newly created with my ec2 host for ssh. You can either use this method or public key for ssh.
I name this .pem file from AWS as aws-ec2-us.pem and aws-ec2-india.pem

```
$ chmod 400 aws-ec2-us.pm
$ ssh -ND 1081 ubuntu@<remote IP> -p 22 -4 -i aws-ec2-us.pem
```
* Next step is make your browser to use http proxy that we setup above
Go to Chrome->settings->open http proxy->set socks proxy
use localhost:1081 as we used above
* Once you setup browser to use proxy, check your IP, it should show up as your AWS ec2 public IP. 

The continuation of this post would be how to use this technique for applications that do not support SOCKS proxy. Looking around the web the solution looks like SOCKS programs like Dante / Socksify
