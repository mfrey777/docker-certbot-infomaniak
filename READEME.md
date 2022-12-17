# Build image
docker build -t [docker username]/certbot-infomaniak:latest .

# Push image to docker hub
docker push [docker username]/certbot-infomaniak:latest

# Create certificate command (docker)
# generate domain token in infomaniak dashboard
# add  --dry-run when testing to avoid rate limit
sudo docker run -e INFOMANIAK_API_TOKEN='ABCDEF' -it --rm --name certbot -v "/etc/letsencrypt:/etc/letsencrypt" -v "/var/lib/letsencrypt:/var/lib/letsencrypt" [docker username]/certbot-infomaniak certonly --authenticator dns-infomaniak  --server https://acme-v02.api.letsencrypt.org/directory --agree-tos -m [email address] -d [domain]

# give access to /etc/password
sudo chmod 0755 /etc/letsencrypt/{live,archive}

# doc example
export INFOMANIAK_API_TOKEN=UF6cYyU54MrmSJ8oUO_GvzrJr-tV0r08vWusz8MqwbchrHK_tg8o6LsgUTxWF4b3_a8_og3Y0VxCmpQS
certbot certonly \
  --authenticator dns-infomaniak \
  --server https://acme-v02.api.letsencrypt.org/directory \
  --agree-tos \
  --rsa-key-size 4096 \
  -d 'death.star'






