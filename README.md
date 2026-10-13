# Raj Kumar Shoe Repairing backend

## Configuration profiles

Shared application, JWT, email, and notification settings belong in
`src/main/resources/application.properties`. The default `local` profile uses
`application-local.properties` for the local Oracle database and local
frontend/CORS addresses. Render activates the `uat` profile, whose
`application-uat.properties` configures PostgreSQL/Neon and the deployed
frontend/CORS addresses. The unused `prod` profile is retained separately.

Configuration is read from these Spring property files; there is no `.env`
import. Keep profile-specific values in the appropriate profile and keep
shared values in `application.properties`. These files currently contain
plaintext credentials in the working tree: do not stage, commit, publish, or
share them. Replace any credential that has already been committed or exposed.

The SMTP integration needs valid SMTP credentials and sender/inbox addresses
before email can be sent. WhatsApp/Twilio integrations likewise require valid
provider credentials. No SFTP mail integration is implemented; email is sent
using SMTP. An existing owner account keeps its current password, so changing
the configured seed password does not reset that account.

## Deploy the backend to Render

Create a Render Web Service for this repository using its Docker runtime. The
Dockerfile activates the `uat` Spring profile and the service listens on port
8080. Update the UAT profile values for the Neon PostgreSQL database and
deployed frontend before deploying.

## Deploy the frontend to Render

Create a Render Static Site for the frontend repository. Set the root directory
to `frontend`, use `npm ci && npm run build` as the build command, and set
`dist` as the publish directory. Set `VITE_API` to the backend's public URL
ending in `/api` and redeploy after changing it.

## Run locally

Start Oracle locally, then run the backend from this directory with
`mvn spring-boot:run`; the default Spring profile is `local`. In the frontend
repository, run `npm run dev` from its `frontend` directory. The frontend
defaults to `http://localhost:8080/api` for the backend API.
