FROM  mcr.microsoft.com/devcontainers/base:jammy

RUN apt-get update \
    && apt-get install --no-install-recommends -y rsyslog systemd systemd-cron \
    # Fix a bug with common-debian script
    && rm -f /usr/local/bin/systemctl \
    #  Clean up
    && apt-get clean && rm -rf /var/lib/apt/lists/*
    #  Install Cloudflare Warp from Repo
    #  GPG Key
    && curl -fsSL https://pkg.cloudflareclient.com/pubkey.gpg | sudo gpg --yes --dearmor --output /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
    # Add this repo to your apt repositories
    echo "deb [signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://pkg.cloudflareclient.com/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/cloudflare-client.list
    # Install
    sudo apt-get update && sudo apt-get install cloudflare-warp

CMD ["/lib/systemd/systemd", "--system", "--unit=basic.target"]
