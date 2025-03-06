---
draft: false
date:
  created: 2024-12-01
categories:
  - Containerization
  - Security
authors:
  - nhamchanvi
---

# Docker Security: Keepin' Your Containers Safe (and Cozy)

So, you've got these awesome Docker containers running your apps, right? But here's the thing: just like your house needs locks and alarms, your containers need some security love too. Don't worry, it's not rocket science. Let's break it down, nice and easy.

[![Image]](./docker-security-keepin-your-containers-safe-and-cozy.md)

[Image]: ../../assets/docker-security.jpg

<!-- more -->

## 1. Updates, Updates, Updates!

Think of Docker updates like those software updates on your phone. They often have those pesky security patches that keep the bad guys out. So, keep your Docker engine and all its buddies up-to-date, okay?

```bash title="Update that Docker engine!"
sudo apt-get update && sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## 2. Slim Down Those Images

Imagine your container is like a backpack. You don't want to carry a bunch of junk you don't need, right? Same goes for Docker images. Use those "minimal" ones like alpine or distroless. They're like those lightweight backpacks – just the essentials, no extra baggage.

```bash title="Dockerfile"
FROM alpine:latest
# Your app's instructions go here
```

## 3. Don't Give 'Em the Keys to the Kingdom

Running containers as "root" is like giving everyone the keys to your house. Not a good idea, huh? Create a special user for your app, kinda like giving your friend a key to just their room.

```bash title="Dockerfile"
# Create a user, just for your app
RUN adduser -D myuser
USER myuser
# Your app's instructions go here
```

## 4. Set Some Limits

Imagine your app is like a kid in a candy store. You gotta set some limits, right? Same with Docker. Set those CPU and memory limits so your app doesn't gobble up all the resources.

```bash
docker run --cpus="1" --memory="512m" my-image
```

## 5. Secret Stash for Sensitive Stuff

Don't leave your passwords and secret codes lying around, right? Same goes for your Docker images. Use those "Docker Secrets" – it's like a super safe vault for your sensitive stuff.

```bash title="Create a secret, shhh..."
echo "mysecret" | docker secret create my_secret -
```

```bash title="Use the secret in your Docker Compose file"
services:
  my-service:
    secrets:
      - my_secret
secrets:
  my_secret:
    external: true
```

## 6. Scan for Those Sneaky Vulnerabilities

Think of vulnerability scanners like those security guards at the mall. They're always on the lookout for trouble. Use tools like Trivy, Clair, or Snyk to scan your images for those sneaky vulnerabilities.

```bash title="Trivy to the rescue!"
trivy image my-image
```

## 7. Network Lockdown

Your Docker network is like the neighborhood your container lives in. You want some fences and security cameras, right? Use Docker's network features to keep things separated and secure.

- Custom Networks: Like having your own little gated community.
- Firewall Rules: Think of these as your security guards, controlling who comes and goes.
- Don't Open Too Many Doors: Only expose the ports your app really needs, like locking up those extra doors in your house.

```bash title="Dockerfile"
EXPOSE 8080
```

## 8. Read-Only, Please!

Imagine your app's files are like those precious family photos. You don't want anyone messing with them, right? Mount your app's filesystem as "read-only" to keep those files safe and sound.

```bash
docker run --read-only my-image
```

## 9. Content Trust: Verify, Then Trust

Think of "Content Trust" as verifying someone's ID before letting them in. Enable Docker Content Trust to make sure those images you're pulling are the real deal.

```bash
export DOCKER_CONTENT_TRUST=1
docker pull my-trusted-image
```

## 10. Keep an Eye on Things

Just like you check your house for anything suspicious, you gotta keep an eye on your Docker containers. Use those logging and monitoring tools to spot any weird activity.

# Wrapping It Up

Securing your Docker containers is like building a fortress around your apps. It's all about layers of protection, you know? Keep things updated, use those minimal images, and don't forget to scan for those sneaky vulnerabilities. And hey, if you ever need a hand, you know where to find me 😉.
