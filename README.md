# Bmvp

## set up Github actions

create .github/workflows/fly.yml

it references secrets.FLY_API_TOKEN

Get that by running `fly auth token`.

go to the github settings for the project, Secrets and Variables, Actions.  Then create a new Repository Secret.  Name it FLY_API_TOKEN and the value is the generated auth token.


## Set up domain
  - using homelessjedakan.com for now
  - set up DNS:  
    - `fly ips list`
    - A record, host: @, ip4
    - AAAA record, host: @, ip6
  - set up ssl and www:
    - `fly certs create homelessjedakan.com`
    - `fly certs create www.homelessjedakan.com`
      - check if they're ready via 
        - `fly certs show homelessjedakan.com`
        - `fly certs show www.homelessjedakan.com`
    - add CNAME record, www, homelessjedakan.com 
    - add `check_origin: ["https://#{host}", "https://www.#{host}"],` to runtime.exs
  - set up the app PHX_HOST env var
    - fly secrets set PHX_HOST=homelessjedakan.com


