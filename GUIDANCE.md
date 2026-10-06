# Mailpit on Wodby

What Wodby sets up for this Mailpit service. Mailpit is a mail catcher for development and testing: it accepts mail over SMTP and shows it in a web interface. It does not deliver mail to the recipients.

## How applications reach it

- SMTP: host is the name of this app service inside the environment, port `1025`. No TLS, no username and no password; no token is generated.
- The service carries the `smtpd` label, so it satisfies the mail link of application services. A linked PHP service, for example, receives the host and port as `MSMTP_HOST` and `MSMTP_PORT` and PHP's `mail()` then ends up here; other runtimes receive variables named by their own service, such as `SMTP_HOST` and `SMTP_PORT`. Read those variables; do not hardcode the host.
- An application that requires SMTP authentication or TLS for its mail transport fails against this service: configure the transport without them.

## Web interface and API

Port `8025` serves the web interface and Mailpit's REST API (`/api/v1/...`). Messages are read, searched and deleted there.

## What to expect

- Every message sent to it is captured, whatever the recipient address. Nothing leaves the environment, so mail from an environment that uses Mailpit never reaches real mailboxes. For real delivery the environment needs a relay service such as OpenSMTPD instead.
- Mailpit keeps a limited number of messages and deletes the oldest ones first.
- The manifest sets no Mailpit options. Options are environment variables on this service in Mailpit's `MP_*` form.

## Data

The optional `data` volume is mounted at `/data`. Mailpit stores messages in a temporary file that is removed on exit unless its database option points at a file, so captured mail survives a restart only when `MP_DATABASE` is set to a path under `/data` and the volume exists. The manifest declares no backups, imports or actions.

## Check the result

- Send a test message from the application, then open the web interface, or request `GET http://<app service name>:8025/api/v1/messages` from a service in the environment.
