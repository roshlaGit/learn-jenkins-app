FROM mcr.microsoft.com/playwright:v1.39.0-jammy
RUN npm install -g netlify-cli serve
RUN apt update && apt install jq -y

FROM mcr.microsoft.com/playwright:v1.39.0-jammy

# Install global tools: netlify-cli, serve, and jq
RUN npm install -g netlify-cli serve \
    && apt update \
    && apt install -y jq

# Ensure necessary ports are open (if serving locally)
EXPOSE 5000

