---
layout: post
title: Docker Self Signed Registry Pain
date: '2015-10-11T18:20:15+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/130981044784/docker-self-signed-registry-pain
---
I get it that docker makes money by selling its own registry services (and hey they created a cool thing and deserve some compensation), but do they have to make it so difficult to do a self signed registry?

Problem #0

I code on a macbook pro. So I’m having to use virtualbox as a proxy. That sucks but that’s life. The problem is that I use bonjour/zeroconf for name resolution. Guess what, the boot2docker image doesn’t have zeroconf installed. So it took me forever to figure out that while I can’t do this:

mtaylor@metis:~$ docker push fileserver.local:5000/ubuntu
The push refers to a repository [fileserver.local:5000/ubuntu] (len: 1)
unable to ping registry endpoint https://fileserver.local:5000/v0/
v2 ping attempt failed with error: Get https://fileserver.local:5000/v2/: dial tcp: lookup fileserver.local:     no such host
v1 ping attempt failed with error: Get https://fileserver.local:5000/v1/_ping: dial tcp: lookup fileserver.local: no such host


but I could do this:

mtaylor@metis:~$ curl -v -k https://fileserver.local:5000/v2/
*   Trying 192.168.1.2...
* Connected to fileserver.local (192.168.1.2) port 5000 (#0)
* TLS 1.2 connection using TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
* Server certificate: fileserver.local
> GET /v2/ HTTP/1.1
> Host: fileserver.local:5000
> User-Agent: curl/7.43.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Content-Length: 2
< Content-Type: application/json; charset=utf-8
< Docker-Distribution-Api-Version: registry/2.0
< Date: Sun, 11 Oct 2015 22:07:12 GMT
< 
* Connection #0 to host fileserver.local left intact
{}mtaylor@metis:~$


It wasn’t because I had the cert wrong and it was therefore refusing to connect to the host, it was because the daemon that lives in the boot2docker virtualbox virtual machine doesn’t have access to zeroconf name resolution.

Problem solved by adding an A record entry in the DNS zone file of my domain (annoying but eh, it works).

Problem #1

The real problem came when it was time to let docker know that it needed to pay attention to the CA I used to sign the registry cert (itself), or turn off checking CAs all together.

Nowhere in the !@#!%!#% documentation does it mention that when you’re using virtualbox to do your dockering that all the stuff it mentions in regard to editing files int /etc/default/docker or putting your ca.crt in /etc/docker/certs.d need to be done in the virtualbox virtual machine.

In retrospect this is now obvious, now that I know the ‘docker daemon’ lives inside the virtual machine, and that’s where all the magic happens. But being a docker newbie I naively assumed that I needed to be creating/editing those files outside of the virtual machine, since there are no other configuration tasks that require editing the configuration of the software running inside of the virtual machine.

Problem #1.5

As I became aware that I needed to modify the configuration files inside the virtual machine it then became a task of figuring out how to get root access inside of the virtualbox virtual machine docker uses (because that isn’t documented in the main docs at all).

The magic commands are simple in retrospect (but this needs to be in the main documentation):

docker-machine ssh name-of-your-vm
docker@name-of-your-vm:~$ sudo -s


Problem #2

It doesn’t work. It’s broken as of docker 1.8.2 :(

I’ve put my cert in the proper directory (inside the virtual machine) and still no joy.  Turns out there is an open bug where the docker daemon simply refuses to read the ca.crt file.

https://github.com/docker/docker/issues/9118

However, the work around of

DOCKER_OPTS="--insecure-registry fileserver.local:5000"


inside of /etc/defaults/docker does work.

It’s obviously not a perfect solution but it at least allows me to finally:

mtaylor@metis:~$ docker push fileserver.matthewjosephtaylor.com:5000/ubuntu
The push refers to a repository [fileserver.matthewjosephtaylor.com:5000/ubuntu] (len: 1)
cdd474520b8c: Image successfully pushed 
f03f3645bde1: Image successfully pushed 
9302827ed0a5: Image successfully pushed 
48731f0a6276: Image successfully pushed 
latest: digest: sha256:ce7e43866f0d66b4c9dbefca41966d60220ec4c681b2fc944dc1ca0d1d333ae1 size: 7729


and so the story has a semi-happy ending….
