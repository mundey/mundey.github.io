---
published: true
layout: post
title: Traefik Reverse Proxy
categories: Reverse Proxy
tags: devops reverse-proxy
author: Jags
---

## Using Traefik as reverse proxy
Traefik works out of the box with sensible defaults but to tame this program is not easy task until concepts are well understood. I'll write this post assuming you are coming from other established reverse proxies such as nginx. We will make it work with similar analogy but traefik has more capabilities which could be for another post. For now, all we want to do is relay number of services from backend.

On high level, we need to connect 
EntryPoints -> Providers -> Routers -> [Rules(Virtual Host), TLS] -> Services

Let's get to work

Assumptions and targets:
  - traefik version: 2.x
  - yml format used instead of toml for readibility
  - couple of services running behind proxy for exposure
  - tls ending is done on Traefik

Directory structure used:
  - /opt/traefik
    - bin: traefik (binary file)
    - etc: traefik.yml
      - conf.d: (vh1.yml, vh2.yml ..., tls.yml)
    - tls (optional): (domain.crt, domain.key)
    - log (log configuration)

Traefik has two configs: static and dynamic
static config, defined in traefik.yml and has following sections:
  [important]
  - entrypoint: defines on which ip and port to listen to incoming connections
  - providers: provider type which further defines dynamic config location. For our use case, we are going to use file type which defines location of dynamic configuration (conf.d in our case).
  [useful]
  - global: for checking new versions or send out usage stats
  - log: where to send program logs, when traefik loads, this log shows different 
  - accessLog: access log details
  - api: ui of traefik to see the configuration visually.

dynamic config, for each site we can define separate config and also define tls.
virtualhost has following config:
  - http: handler used for web protocol. tcp is used for other types such as db/mail or raw network service.
    - routers:
      - define which entry point the rule is for. if not specified, the router would listen to all entry points.
      - tls: blank section just says this is tls ending router. if you intend to define both http and https, define two routers
      - rule: virtualhost name rule. there are many other rules which could be of interest. Another interesting thing to note, you can define same virtualhost names (one.example.com, one.example.com) and it would not complain. Because it's a dynamic config. It's just that it would not resolve to expected values. e.g. we can define same virtual hosts but on different ports and it would work.
      - service: which service is used for connecting to this router
    - services:
      - loadBalancer:
        - servers:
          - url: "http://<backend-server-ip>:<port>/"
tls config
  - tls:
    - certiifcates:
      - certFile: location of cert file
        keyFile: location of key file

if tls is not found, traefik would generate it's own cert and use it for TLS.

That's all. This minimal config can be used to replace nginx with traefik. There are more config options available as well.
Todo:
- different tls for different virtual-hosts
- redirect from http to https when hitting http
