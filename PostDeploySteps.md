#After deploying Ops Man on the jumpbox or on the opsmgr box
# Create bosh client - https://docs.pivotal.io/pivotalcf/2-2/customizing/opsmanager-create-bosh-client.html
uaac target https://192.168.101.10:8443 --ca-cert /var/tempest/workspaces/default/root_ca_certificate

# Create new user - https://opsman.pas.pcf-labs.com/infrastructure/director/credentials
# This will prompt of admin user and password which are also found in the credentials page
uaac token owner get login -s UAA-LOGIN-CLIENT-PASSWORD

# Now that you have a token Create a new UAA Client with bosh.admin privileges
uaac client add ci --authorized_grant_types client_credentials \
--authorities bosh.admin --secret PCF4tw

export BOSH_CLIENT=ci
export BOSH_CLIENT_SECRET=PCF4tw

bosh alias-env pcf-demo -e 192.168.101.10 --ca-cert /var/tempest/workspaces/default/root_ca_certificate
